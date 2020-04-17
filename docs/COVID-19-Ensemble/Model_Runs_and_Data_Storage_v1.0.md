---
layout: default
title: SEIR Model and Data Organization Application
parent: COVID-19 SEIR Ensemble with Behavioral Forcing
nav_order: 3
---

# Model Run and Data Storage Application Notebook

### Imports and carry-overs
The notebook begins with the library imports and a few settings. It then carries over a few of the functions and classes from the previous application - as this application is a modification of the original, larger application.


```python
import matplotlib.pyplot as plt
from matplotlib.animation import FuncAnimation
import math
import numpy as np
import random
import seaborn as sns
import pandas as pd
from scipy import stats
from scipy.stats import beta
import ipywidgets as widgets
from IPython.display import display
import pickle

sns.set()
plt.rcParams["figure.figsize"] = (20,10)

%matplotlib notebook

N = 10_000 # population size

def pert_dist(peak, low, high, sample_size=N, temp=4):
    
    pert = []
    pert_loc = low
    pert_scale = high - low
    
    con_1 = 1 + temp * (peak - low) / (high - low)
    con_0 = 1 + temp * (high - peak) / (high - low)
    
    pert = np.random.beta(con_1, con_0, sample_size)
    pert = pert_loc + pert_scale * pert
    return pert

def find_beta(exp_mu, exp_low, exp_high, exp_lda=4):
    mu_range = np.linspace(exp_low, exp_high, 40)
    low_range = np.linspace(0, exp_mu, 40)
    high_range = np.linspace(exp_mu, (exp_high * 2), 40)
    test_res, mu_res, low_res, high_res, mean_err_rec, exp_mu_rec = [], [], [], [], [], []
    
    for mu in mu_range:
        for low in low_range:
            for high in high_range:
                if low >= mu:
                    low = mu * .8
                if high <= mu:
                    high = mu * 1.2
                test_dist = pert_dist(mu, low, high, 1000, exp_lda)
                test_mean = np.mean(test_dist)
                test_low = np.percentile(test_dist, 10)
                test_high = np.percentile(test_dist, 90)
                mean_err = (test_mean - exp_mu)**2
                low_err = (test_low - exp_low)**2
                high_err = (test_high - exp_high)**2
                test_res.append(mean_err + np.sqrt(mean_err + low_err + high_err))
                mu_res.append(mu)
                low_res.append(low)
                high_res.append(high)
                mean_err_rec.append(np.sqrt(mean_err))
                exp_mu_rec.append(exp_mu)
                
    full_results = pd.DataFrame({
        'Test Results': pd.Series(test_res),
        'Mode Value': pd.Series(mu_res),
        'Low Value': pd.Series(low_res),
        'High Value': pd.Series(high_res),
        'mean_err': pd.Series(mean_err_rec),
        'expected mu': pd.Series(exp_mu_rec)
    })
    return full_results


class df_dist:
    
    def __init__(self, dist_mu, dist_low, 
                 dist_high, dist_size=10_000, 
                 dist_temp=4, name='Unknown'):
        
        self.mu = dist_mu
        self.low = dist_low
        self.high = dist_high
        self.temp = dist_temp
        self.dsize = dist_size
        self.name = name
        
        self.df = find_beta(self.mu, self.low, 
                            self.high, self.temp)
        self.df.sort_values(by=['Test Results'], 
                            inplace=True)
        self.new_mu, self.new_low, self.new_high = list(self.df.iloc[0, 1:4])
        self.pert = pert_dist(self.new_mu, self.new_low, 
                              self.new_high, self.dsize, self.temp)
        
    def checkParams(self):
        print(f'Pert vars: mu: {self.new_mu}, low: {self.new_low}, high: {self.new_high}')
        
        plt.hist(self.pert, 25)
        plt.show()
        
        print(f'Original inputs: Mean={self.mu}, Low={self.low}, High={self.high}')
        print(f'New outputs: Mean={np.mean(self.pert)}, Low={np.percentile(self.pert, 10)}, High={np.percentile(self.pert, 90)}')

    def getSample(self):
        return random.sample(list(self.pert), 1)[0]


def dangerPerception(dp_c, dp_q):
    if (dp_c/dp_q) <= 0.01:
        return .01
    elif (dp_c/dp_q) <= 0.99:
        return dp_c / dp_q
    else:
        return 0.99

def behaviorModifier(total_conf, conf_trigg):
    bm_dp = dangerPerception(total_conf, conf_trigg)
    beta_a = 10 - (10 * bm_dp)
    beta_b = 10 - beta_a/(total_conf+1)
    return np.random.beta(beta_a, beta_b)
```

### Loading in the previously generated distributions
Originally, we would be generating the following distributions using the classes and methods above, but to save time and computational resources we previously saved the generated classes for each and will now load them back into a modified version of the application.


```python
file_list = ['e2i_object', 'i2r_object', 'c2i_object',
             'h2i_object', 'freq_cont_object',
             'infreq_cont_object', 'cfr_object']

for filename in file_list:
    infile = open(filename, 'rb')
    if filename == 'e2i_object':
        e2i = pickle.load(infile)
    elif filename == 'i2r_object':
        i2r = pickle.load(infile)
    elif filename ==  'c2i_object':
        c2i = pickle.load(infile)
    elif filename == 'h2i_object':
        h2i = pickle.load(infile)
    elif filename == 'freq_cont_object':
        freq_cont = pickle.load(infile)
    elif filename == 'infreq_cont_object':
        infreq_cont = pickle.load(infile)
    elif filename == 'cfr_object':
        cfr = pickle.load(infile)
    infile.close()
```

## The ModelRun class
This is the main class of the application. The ModelRun class generates SEIR model run instances, each of which requires only an ID as input, though, the class can also accept different population sizes, durations, behavioral change triggers, and starting exposed and infectious population numbers. Additionally, the class has a simDay method that will simulate the next day in a model run, appending the results to the existing attributes of the instanced ModelRun class.


```python
class ModelRun:
    
    def __init__(self, id, population=10_000, duration=180, conf_trigger=50, exposed=1, infectious=0):
        self.id = id
        self.pop = population
        self.dur = duration
        self.conf_trigg = conf_trigger
        self.day = []
        self.beh_mod = []
        
        self.S, self.R, self.D = [population], [0], [0]
        self.NR, self.ND = [0], [0]
        self.E, self.I = [exposed], [infectious]
        self.NE, self.NI = [0], [0]
        self.E_C, self.I_C = [0], [0]
        self.IC, self.IH = [0], [0]
        self.NIC, self.NIH = [0], [0]
        
        self.inc_per = e2i.getSample()
        self.inf_per = i2r.getSample()
        self.c2i = c2i.getSample()
        self.h2i = h2i.getSample()
        self.freq_cont = freq_cont.getSample()
        self.infreq_cont = infreq_cont.getSample()
        self.cfr = cfr.getSample()
        
        self.lat_rate = 1/self.inc_per
        self.rec_rate = 1/self.inf_per

    def simDay(self, day):
        self.day.append(day)
        
        starting_sus = self.S[day]
        total_conf = self.IC[day]
        
        self.beh_mod.append(behaviorModifier(total_conf, self.conf_trigg))
        
        next_NE = ((self.beh_mod[day] * self.freq_cont * self.NI[day]) 
                   + (self.beh_mod[day] * self.infreq_cont * self.I[day])) 
        self.NE.append(next_NE) if next_NE < self.S[day] else self.NE.append(self.S[day])
                        
        next_NI = self.E[day] * self.lat_rate
        self.NI.append(next_NI) if next_NI > 0 else self.NI.append(0)
    
        self.I_C.append(self.I_C[day] + self.NI[day+1])           
        
        next_E = self.E[day] + self.NE[day+1] - self.NI[day+1]
        self.E.append(next_E) if next_E > 0 else self.E.append(0)
            
        self.E_C.append(self.E_C[day] + self.NE[day+1])
                   
        next_NIC = self.c2i * self.NI[day+1]
        self.NIC.append(next_NIC)
        self.IC.append(self.IC[day] + next_NIC)
                   
        next_NIH = self.h2i * self.NI[day+1]
        self.NIH.append(next_NIH)
        self.IH.append(self.IH[day] + next_NIH)
        
        next_NR = self.rec_rate * self.I[day]
        self.NR.append(next_NR)
        self.R.append(self.R[day] + next_NR)
                   
        next_ND = self.cfr * next_NIC
        self.ND.append(next_ND)
        self.D.append(self.D[day] + next_ND)
                   
        next_I = self.I[day] + self.NI[day+1] - next_NR - next_ND
        self.I.append(next_I) if next_I > 0 else self.I.append(0)

        next_S = self.pop - self.E[day+1] - self.I[day+1] - self.R[day+1] - self.D[day+1]
        self.S.append(next_S) if next_S > 0 else self.S.append(0)
            
```


```python
data_dict = {}
properties_dict = {'Model Sets': {}}

conf_trigger_list = [3, 5, 10, 15, 20, 35, 50, 75, 100]
            
for modifier in conf_trigger_list:
            
    model_dict = {}

    for i in range(1000):
        model_dict[f'model_{i}'] = ModelRun(i, conf_trigger=modifier)

        for day in range(model_dict[f'model_{i}'].dur):
            model_dict[f'model_{i}'].simDay(day)
    
    data_dict[f'conf_trigger_{modifier}'] = model_dict
    properties_dict['Model Sets'].update({f'Confirmed Infectious Behavior Max = {modifier}': {'id': f'conf_trigger_{modifier}'}})
```


```python
properties_dict.update({'Results': {'Susceptible (Running Total)': {'id': 'S'}, 
                                   'Exposed (Concurrent)': {'id': 'E'},
                                   'Infectious (Concurrent)': {'id': 'I'},
                                   'Recovered (Running Total)': {'id': 'R'},
                                   'Deaths (Current Total)': {'id': 'D'},
                                   'Recovered (New/Daily)': {'id': 'NR'},
                                   'Deaths (New/Daily)': {'id': 'ND'},
                                   'Exposed (New/Daily)': {'id': 'NE'},
                                   'Infectious (New/Daily)': {'id': 'NI'},
                                   'Confirmed Infectious (Cumulative)': {'id': 'IC'},
                                   'Confirmed Infectious(New/Daily)': {'id': 'NIC'},
                                   'Hospitalized Infectious (Cumulative)': {'id': 'IH'},
                                   'Hospitalized Infectious (New/Daily)': {'id': 'NIH'},
                                   'Exposed (Cumulative)': {'id': 'E_C'},
                                   'Infectious (Cumulative)': {'id': 'I_C'},
                                   'Behavioral Modifier (Daily)': {'id': 'beh_mod'},
                                    }
                      })
```


```python
filename = 'properties_dict'
outfile = open(filename, 'wb')
pickle.dump(properties_dict, outfile)
outfile.close()
```


```python
def getKeyWithID(in_dict, in_id, in_value):
    for key in in_dict:
        if properties_dict['results'][key] == {in_id: in_value}:
            return key
            
getKeyWithID(properties_dict['results'], 'id', 'I_C')
```




    'Infectious (Cumulative)'




```python
results_dict = {'S': {}, 
           'E': {},
           'I': {},
           'R': {},
           'D': {},
           'NR': {},
           'ND': {},
           'NE': {},
           'NI': {},
           'IC': {},
           'NIC': {},
           'IH': {},
           'NIH': {},
           'E_C': {},
           'I_C': {},
           'beh_mod': {}
            }

for conf_trigger_set in data_dict:
    for type_key in results_dict: 
        for x in range(len(data_dict[conf_trigger_set])-1):
            for property, value in vars(data_dict[conf_trigger_set][f'model_{x}']).items():
                if property == type_key:
                    temp_dict = {f'model_{x}': value}
                    try: results_dict[type_key][conf_trigger_set]
                    except KeyError: results_dict[type_key][conf_trigger_set] = None
                    if results_dict[type_key][conf_trigger_set] is None:
                        results_dict[type_key][conf_trigger_set] = temp_dict
                    else:
                        results_dict[type_key][conf_trigger_set].update(temp_dict)                     
```


```python
filename = 'results_dict'
outfile = open(filename, 'wb')
pickle.dump(results_dict, outfile)
outfile.close()
```


```python
stats_dict = {'S': {}, 
           'E': {},
           'I': {},
           'R': {},
           'D': {},
           'NR': {},
           'ND': {},
           'NE': {},
           'NI': {},
           'IC': {},
           'NIC': {},
           'IH': {},
           'NIH': {},
           'E_C': {},
           'I_C': {},
           'beh_mod': {}
            }

for result_type in results_dict:
    for conf_trig in results_dict[result_type]:
        temp_df = pd.DataFrame.from_dict(results_dict[result_type][conf_trig])
        temp_stats = temp_df.apply(pd.DataFrame.describe, percentiles=[.05, .1, .9, .95], axis=1)
        temp_stats.to_dict(orient='list')
        stats_dict[result_type][conf_trig] = temp_stats
```

    S
    conf_trigger_3
    Finished with S and conf_trigger_3
    conf_trigger_5
    Finished with S and conf_trigger_5
    conf_trigger_10
    Finished with S and conf_trigger_10
    conf_trigger_15
    Finished with S and conf_trigger_15
    conf_trigger_20
    Finished with S and conf_trigger_20
    conf_trigger_35
    Finished with S and conf_trigger_35
    conf_trigger_50
    Finished with S and conf_trigger_50
    conf_trigger_75
    Finished with S and conf_trigger_75
    conf_trigger_100
    Finished with S and conf_trigger_100
    E
    conf_trigger_3
    Finished with E and conf_trigger_3
    conf_trigger_5
    Finished with E and conf_trigger_5
    conf_trigger_10
    Finished with E and conf_trigger_10
    conf_trigger_15
    Finished with E and conf_trigger_15
    conf_trigger_20
    Finished with E and conf_trigger_20
    conf_trigger_35
    Finished with E and conf_trigger_35
    conf_trigger_50
    Finished with E and conf_trigger_50
    conf_trigger_75
    Finished with E and conf_trigger_75
    conf_trigger_100
    Finished with E and conf_trigger_100
    I
    conf_trigger_3
    Finished with I and conf_trigger_3
    conf_trigger_5
    Finished with I and conf_trigger_5
    conf_trigger_10
    Finished with I and conf_trigger_10
    conf_trigger_15
    Finished with I and conf_trigger_15
    conf_trigger_20
    Finished with I and conf_trigger_20
    conf_trigger_35
    Finished with I and conf_trigger_35
    conf_trigger_50
    Finished with I and conf_trigger_50
    conf_trigger_75
    Finished with I and conf_trigger_75
    conf_trigger_100
    Finished with I and conf_trigger_100
    R
    conf_trigger_3
    Finished with R and conf_trigger_3
    conf_trigger_5
    Finished with R and conf_trigger_5
    conf_trigger_10
    Finished with R and conf_trigger_10
    conf_trigger_15
    Finished with R and conf_trigger_15
    conf_trigger_20
    Finished with R and conf_trigger_20
    conf_trigger_35
    Finished with R and conf_trigger_35
    conf_trigger_50
    Finished with R and conf_trigger_50
    conf_trigger_75
    Finished with R and conf_trigger_75
    conf_trigger_100
    Finished with R and conf_trigger_100
    D
    conf_trigger_3
    Finished with D and conf_trigger_3
    conf_trigger_5
    Finished with D and conf_trigger_5
    conf_trigger_10
    Finished with D and conf_trigger_10
    conf_trigger_15
    Finished with D and conf_trigger_15
    conf_trigger_20
    Finished with D and conf_trigger_20
    conf_trigger_35
    Finished with D and conf_trigger_35
    conf_trigger_50
    Finished with D and conf_trigger_50
    conf_trigger_75
    Finished with D and conf_trigger_75
    conf_trigger_100
    Finished with D and conf_trigger_100
    NR
    conf_trigger_3
    Finished with NR and conf_trigger_3
    conf_trigger_5
    Finished with NR and conf_trigger_5
    conf_trigger_10
    Finished with NR and conf_trigger_10
    conf_trigger_15
    Finished with NR and conf_trigger_15
    conf_trigger_20
    Finished with NR and conf_trigger_20
    conf_trigger_35
    Finished with NR and conf_trigger_35
    conf_trigger_50
    Finished with NR and conf_trigger_50
    conf_trigger_75
    Finished with NR and conf_trigger_75
    conf_trigger_100
    Finished with NR and conf_trigger_100
    ND
    conf_trigger_3
    Finished with ND and conf_trigger_3
    conf_trigger_5
    Finished with ND and conf_trigger_5
    conf_trigger_10
    Finished with ND and conf_trigger_10
    conf_trigger_15
    Finished with ND and conf_trigger_15
    conf_trigger_20
    Finished with ND and conf_trigger_20
    conf_trigger_35
    Finished with ND and conf_trigger_35
    conf_trigger_50
    Finished with ND and conf_trigger_50
    conf_trigger_75
    Finished with ND and conf_trigger_75
    conf_trigger_100
    Finished with ND and conf_trigger_100
    NE
    conf_trigger_3
    Finished with NE and conf_trigger_3
    conf_trigger_5
    Finished with NE and conf_trigger_5
    conf_trigger_10
    Finished with NE and conf_trigger_10
    conf_trigger_15
    Finished with NE and conf_trigger_15
    conf_trigger_20
    Finished with NE and conf_trigger_20
    conf_trigger_35
    Finished with NE and conf_trigger_35
    conf_trigger_50
    Finished with NE and conf_trigger_50
    conf_trigger_75
    Finished with NE and conf_trigger_75
    conf_trigger_100
    Finished with NE and conf_trigger_100
    NI
    conf_trigger_3
    Finished with NI and conf_trigger_3
    conf_trigger_5
    Finished with NI and conf_trigger_5
    conf_trigger_10
    Finished with NI and conf_trigger_10
    conf_trigger_15
    Finished with NI and conf_trigger_15
    conf_trigger_20
    Finished with NI and conf_trigger_20
    conf_trigger_35
    Finished with NI and conf_trigger_35
    conf_trigger_50
    Finished with NI and conf_trigger_50
    conf_trigger_75
    Finished with NI and conf_trigger_75
    conf_trigger_100
    Finished with NI and conf_trigger_100
    IC
    conf_trigger_3
    Finished with IC and conf_trigger_3
    conf_trigger_5
    Finished with IC and conf_trigger_5
    conf_trigger_10
    Finished with IC and conf_trigger_10
    conf_trigger_15
    Finished with IC and conf_trigger_15
    conf_trigger_20
    Finished with IC and conf_trigger_20
    conf_trigger_35
    Finished with IC and conf_trigger_35
    conf_trigger_50
    Finished with IC and conf_trigger_50
    conf_trigger_75
    Finished with IC and conf_trigger_75
    conf_trigger_100
    Finished with IC and conf_trigger_100
    NIC
    conf_trigger_3
    Finished with NIC and conf_trigger_3
    conf_trigger_5
    Finished with NIC and conf_trigger_5
    conf_trigger_10
    Finished with NIC and conf_trigger_10
    conf_trigger_15
    Finished with NIC and conf_trigger_15
    conf_trigger_20
    Finished with NIC and conf_trigger_20
    conf_trigger_35
    Finished with NIC and conf_trigger_35
    conf_trigger_50
    Finished with NIC and conf_trigger_50
    conf_trigger_75
    Finished with NIC and conf_trigger_75
    conf_trigger_100
    Finished with NIC and conf_trigger_100
    IH
    conf_trigger_3
    Finished with IH and conf_trigger_3
    conf_trigger_5
    Finished with IH and conf_trigger_5
    conf_trigger_10
    Finished with IH and conf_trigger_10
    conf_trigger_15
    Finished with IH and conf_trigger_15
    conf_trigger_20
    Finished with IH and conf_trigger_20
    conf_trigger_35
    Finished with IH and conf_trigger_35
    conf_trigger_50
    Finished with IH and conf_trigger_50
    conf_trigger_75
    Finished with IH and conf_trigger_75
    conf_trigger_100
    Finished with IH and conf_trigger_100
    NIH
    conf_trigger_3
    Finished with NIH and conf_trigger_3
    conf_trigger_5
    Finished with NIH and conf_trigger_5
    conf_trigger_10
    Finished with NIH and conf_trigger_10
    conf_trigger_15
    Finished with NIH and conf_trigger_15
    conf_trigger_20
    Finished with NIH and conf_trigger_20
    conf_trigger_35
    Finished with NIH and conf_trigger_35
    conf_trigger_50
    Finished with NIH and conf_trigger_50
    conf_trigger_75
    Finished with NIH and conf_trigger_75
    conf_trigger_100
    Finished with NIH and conf_trigger_100
    E_C
    conf_trigger_3
    Finished with E_C and conf_trigger_3
    conf_trigger_5
    Finished with E_C and conf_trigger_5
    conf_trigger_10
    Finished with E_C and conf_trigger_10
    conf_trigger_15
    Finished with E_C and conf_trigger_15
    conf_trigger_20
    Finished with E_C and conf_trigger_20
    conf_trigger_35
    Finished with E_C and conf_trigger_35
    conf_trigger_50
    Finished with E_C and conf_trigger_50
    conf_trigger_75
    Finished with E_C and conf_trigger_75
    conf_trigger_100
    Finished with E_C and conf_trigger_100
    I_C
    conf_trigger_3
    Finished with I_C and conf_trigger_3
    conf_trigger_5
    Finished with I_C and conf_trigger_5
    conf_trigger_10
    Finished with I_C and conf_trigger_10
    conf_trigger_15
    Finished with I_C and conf_trigger_15
    conf_trigger_20
    Finished with I_C and conf_trigger_20
    conf_trigger_35
    Finished with I_C and conf_trigger_35
    conf_trigger_50
    Finished with I_C and conf_trigger_50
    conf_trigger_75
    Finished with I_C and conf_trigger_75
    conf_trigger_100
    Finished with I_C and conf_trigger_100
    beh_mod
    conf_trigger_3
    Finished with beh_mod and conf_trigger_3
    conf_trigger_5
    Finished with beh_mod and conf_trigger_5
    conf_trigger_10
    Finished with beh_mod and conf_trigger_10
    conf_trigger_15
    Finished with beh_mod and conf_trigger_15
    conf_trigger_20
    Finished with beh_mod and conf_trigger_20
    conf_trigger_35
    Finished with beh_mod and conf_trigger_35
    conf_trigger_50
    Finished with beh_mod and conf_trigger_50
    conf_trigger_75
    Finished with beh_mod and conf_trigger_75
    conf_trigger_100
    Finished with beh_mod and conf_trigger_100
    


```python
from sklearn.metrics import mean_squared_error

for cat in stats_dict:
    for conf_trig in stats_dict[cat]:
        check_rms = None
        for x in range(len(results_dict[cat][conf_trig])):
            test_model_col = results_dict[cat][conf_trig][f'model_{x}']
            test_mean_col = list(stats_dict[cat][conf_trig]['mean'])
            test_rms = np.sqrt(mean_squared_error(test_model_col, test_mean_col))
            if check_rms == None or test_rms < check_rms: 
                check_rms = test_rms
                check_col = test_model_col
                print(cat, conf_trig, test_rms)
        stats_dict[cat][conf_trig]['best_fit'] = check_col
```

    S conf_trigger_3 233.98858402639598
    S conf_trigger_3 98.58910167772851
    S conf_trigger_3 78.26844601399915
    S conf_trigger_3 33.853963519641994
    S conf_trigger_5 487.68460318901646
    S conf_trigger_5 250.84781227279956
    S conf_trigger_5 170.06649611932116
    S conf_trigger_5 141.14246697064848
    S conf_trigger_5 92.29831356698652
    S conf_trigger_5 90.35954824366897
    S conf_trigger_5 80.57706249680521
    S conf_trigger_5 67.09165749137556
    S conf_trigger_10 1685.8725650763877
    S conf_trigger_10 1446.6073516252065
    S conf_trigger_10 464.4688747921488
    S conf_trigger_10 409.7195993455905
    S conf_trigger_10 315.61292408170726
    S conf_trigger_10 275.3494793321354
    S conf_trigger_10 241.99254926564402
    S conf_trigger_10 224.137904678583
    S conf_trigger_10 149.46483745140202
    S conf_trigger_10 126.63313012344861
    S conf_trigger_10 104.96563358659324
    S conf_trigger_15 3285.694643251863
    S conf_trigger_15 1478.059271158057
    S conf_trigger_15 384.08489960167225
    S conf_trigger_15 303.09649397926
    S conf_trigger_15 243.59298125637005
    S conf_trigger_15 240.9815373326588
    S conf_trigger_15 231.22469659262157
    S conf_trigger_15 226.860838323902
    S conf_trigger_15 184.55702171238843
    S conf_trigger_15 145.4312169008641
    S conf_trigger_20 476.7604802037315
    S conf_trigger_20 456.39508045563394
    S conf_trigger_20 369.7840420488955
    S conf_trigger_20 248.05866190902145
    S conf_trigger_20 179.83715166271548
    S conf_trigger_35 1662.3789223074837
    S conf_trigger_35 1328.556668245344
    S conf_trigger_35 583.9305129566089
    S conf_trigger_35 516.7938158877207
    S conf_trigger_35 467.4178849016294
    S conf_trigger_35 461.6746404753518
    S conf_trigger_35 450.88117811712317
    S conf_trigger_35 433.63839319167033
    S conf_trigger_35 384.8957763336515
    S conf_trigger_35 357.6527688421403
    S conf_trigger_50 1815.2616096893066
    S conf_trigger_50 1291.1330052541057
    S conf_trigger_50 1260.7067103000372
    S conf_trigger_50 933.3313527895812
    S conf_trigger_50 736.3658045044483
    S conf_trigger_50 562.9960116486311
    S conf_trigger_50 472.50768295621964
    S conf_trigger_50 292.4654957083811
    S conf_trigger_75 780.1236740536596
    S conf_trigger_75 752.517648710352
    S conf_trigger_75 750.7066712424514
    S conf_trigger_75 722.418143970374
    S conf_trigger_75 697.7286236895127
    S conf_trigger_75 607.5563089014997
    S conf_trigger_75 485.94026233031497
    S conf_trigger_100 710.3983641090675
    S conf_trigger_100 617.4651914043174
    S conf_trigger_100 571.9349244127308
    E conf_trigger_3 43.36433824336901
    E conf_trigger_3 36.47329325455127
    E conf_trigger_3 35.421622761769704
    E conf_trigger_3 31.416305395651065
    E conf_trigger_3 28.841210976487414
    E conf_trigger_3 25.65255037401507
    E conf_trigger_3 24.51511907282383
    E conf_trigger_5 122.34525501159712
    E conf_trigger_5 44.230527510786466
    E conf_trigger_5 36.64852796019498
    E conf_trigger_5 32.41352298030378
    E conf_trigger_5 29.9373347266311
    E conf_trigger_10 302.05294111945886
    E conf_trigger_10 174.75229091445888
    E conf_trigger_10 148.51047984263013
    E conf_trigger_10 97.12813373677749
    E conf_trigger_10 93.60610396339834
    E conf_trigger_10 76.37198326500219
    E conf_trigger_10 75.2944562695216
    E conf_trigger_10 63.38921747512495
    E conf_trigger_10 58.44579971809163
    E conf_trigger_15 331.83927606189604
    E conf_trigger_15 195.2139302473399
    E conf_trigger_15 163.39904507959983
    E conf_trigger_15 138.4828260172277
    E conf_trigger_15 137.1370375131444
    E conf_trigger_15 111.8729471527027
    E conf_trigger_20 313.3016615175055
    E conf_trigger_20 262.78882936363266
    E conf_trigger_20 254.29229175980333
    E conf_trigger_20 250.24238728653157
    E conf_trigger_20 235.31887202056376
    E conf_trigger_20 227.43997243770787
    E conf_trigger_20 199.17118478844915
    E conf_trigger_20 178.63575097342417
    E conf_trigger_20 153.83062829587658
    E conf_trigger_20 116.32254793708599
    E conf_trigger_20 111.28175348051458
    E conf_trigger_35 372.04211273831123
    E conf_trigger_35 312.1955215312984
    E conf_trigger_35 303.74524545602117
    E conf_trigger_35 300.1649226182327
    E conf_trigger_35 294.2910160000131
    E conf_trigger_35 259.3724042205911
    E conf_trigger_35 239.17131167259265
    E conf_trigger_35 203.05522047604612
    E conf_trigger_35 185.265903751932
    E conf_trigger_50 757.8325254549086
    E conf_trigger_50 357.7979838533133
    E conf_trigger_50 292.27712635530503
    E conf_trigger_50 290.5102830840804
    E conf_trigger_50 287.3652745701547
    E conf_trigger_50 240.06165188224873
    E conf_trigger_75 607.3988835178446
    E conf_trigger_75 444.4960642700902
    E conf_trigger_75 442.77629855727156
    E conf_trigger_75 387.38992879242534
    E conf_trigger_75 381.28801389073095
    E conf_trigger_75 329.2821450195947
    E conf_trigger_75 328.42753458464506
    E conf_trigger_100 1080.1854357904385
    E conf_trigger_100 788.4261473741077
    E conf_trigger_100 677.9869240805491
    E conf_trigger_100 628.6498286481204
    E conf_trigger_100 457.4646668978453
    E conf_trigger_100 332.0595520083026
    I conf_trigger_3 69.8655579392113
    I conf_trigger_3 37.06357305845196
    I conf_trigger_3 24.63931704127982
    I conf_trigger_3 20.164115448752433
    I conf_trigger_3 15.440918713440816
    I conf_trigger_5 141.28744239767815
    I conf_trigger_5 46.16917426152974
    I conf_trigger_5 44.492242057210206
    I conf_trigger_5 44.34216566776377
    I conf_trigger_5 36.32733696598877
    I conf_trigger_5 32.15799792189883
    I conf_trigger_5 25.71273951302058
    I conf_trigger_10 245.4572942950338
    I conf_trigger_10 109.03908134070046
    I conf_trigger_10 78.26177594771495
    I conf_trigger_10 61.48128000670944
    I conf_trigger_10 52.7571468078002
    I conf_trigger_15 239.1382108639124
    I conf_trigger_15 223.29776606278296
    I conf_trigger_15 146.49393091586822
    I conf_trigger_15 135.38317005398002
    I conf_trigger_15 129.35612050657605
    I conf_trigger_15 129.09348489450727
    I conf_trigger_15 120.01668116349867
    I conf_trigger_15 118.79272980551465
    I conf_trigger_15 86.66024707946411
    I conf_trigger_15 69.54853404563144
    I conf_trigger_20 322.1249646317665
    I conf_trigger_20 238.73320684091166
    I conf_trigger_20 214.37613925916304
    I conf_trigger_20 152.2540072179432
    I conf_trigger_20 136.40726416646652
    I conf_trigger_20 128.62018183949576
    I conf_trigger_20 127.66776671122516
    I conf_trigger_20 121.3989200838494
    I conf_trigger_20 116.81877257808905
    I conf_trigger_20 109.55342980727892
    I conf_trigger_20 107.66878054409611
    I conf_trigger_35 332.3955828787058
    I conf_trigger_35 302.6562677751826
    I conf_trigger_35 290.40733823929907
    I conf_trigger_35 286.66767473785063
    I conf_trigger_35 222.4136999424575
    I conf_trigger_35 175.32300817697032
    I conf_trigger_35 157.7739149935733
    I conf_trigger_35 153.54636103364794
    I conf_trigger_50 832.9773352918218
    I conf_trigger_50 584.313556660981
    I conf_trigger_50 491.7137505276155
    I conf_trigger_50 385.31835450903753
    I conf_trigger_50 365.2852199728035
    I conf_trigger_50 285.440997088599
    I conf_trigger_50 260.52453902393364
    I conf_trigger_50 191.54670257173495
    I conf_trigger_50 183.44555193709837
    I conf_trigger_75 898.4659296762311
    I conf_trigger_75 604.1324044455893
    I conf_trigger_75 329.4822558834354
    I conf_trigger_75 253.95718314938486
    I conf_trigger_75 249.7621667901491
    I conf_trigger_75 243.32552981591869
    I conf_trigger_100 301.47585917041164
    I conf_trigger_100 297.0793813447139
    I conf_trigger_100 285.2840789331981
    I conf_trigger_100 265.9727176559035
    R conf_trigger_3 238.56142466943345
    R conf_trigger_3 52.66886391612724
    R conf_trigger_3 35.76996921545279
    R conf_trigger_3 27.61841193346614
    R conf_trigger_5 516.0528640991927
    R conf_trigger_5 221.74990497509881
    R conf_trigger_5 199.29861518186163
    R conf_trigger_5 183.44077152645863
    R conf_trigger_5 140.97090839773833
    R conf_trigger_5 63.81527910818406
    R conf_trigger_10 1630.179632749965
    R conf_trigger_10 1340.000583231961
    R conf_trigger_10 503.808597839933
    R conf_trigger_10 273.0068646006824
    R conf_trigger_10 214.01665322870468
    R conf_trigger_10 213.60685784064052
    R conf_trigger_10 197.8939751214252
    R conf_trigger_10 114.06244792746102
    R conf_trigger_10 50.34380703227497
    R conf_trigger_15 3085.1184805632765
    R conf_trigger_15 1322.555047176301
    R conf_trigger_15 483.47539366217967
    R conf_trigger_15 339.9741571958615
    R conf_trigger_15 237.42979506565013
    R conf_trigger_15 208.29882281062822
    R conf_trigger_15 154.79567893153137
    R conf_trigger_15 145.88705188805935
    R conf_trigger_15 86.90054575728921
    R conf_trigger_20 761.427206860138
    R conf_trigger_20 524.5304168532967
    R conf_trigger_20 487.45420336236475
    R conf_trigger_20 421.7056248931007
    R conf_trigger_20 403.4066575950594
    R conf_trigger_20 330.87637685062515
    R conf_trigger_20 260.48783262070594
    R conf_trigger_20 231.92933900055266
    R conf_trigger_20 204.26663920311324
    R conf_trigger_20 171.59415507020987
    R conf_trigger_35 1497.7172524441326
    R conf_trigger_35 1087.1845332650737
    R conf_trigger_35 687.8835386116234
    R conf_trigger_35 637.4656063520335
    R conf_trigger_35 507.46989645787346
    R conf_trigger_35 329.76696823894434
    R conf_trigger_35 160.63372590998335
    R conf_trigger_50 1821.650190801636
    R conf_trigger_50 1171.2036832093152
    R conf_trigger_50 1143.4153144886477
    R conf_trigger_50 1017.2251599337883
    R conf_trigger_50 742.8378483615157
    R conf_trigger_50 737.9597612586197
    R conf_trigger_50 580.4799267292517
    R conf_trigger_50 301.47252981683783
    R conf_trigger_50 143.54568162052323
    R conf_trigger_75 629.8358639151686
    R conf_trigger_75 616.3350628081371
    R conf_trigger_75 542.5297319740422
    R conf_trigger_75 494.08780076717517
    R conf_trigger_75 425.77778793758023
    R conf_trigger_75 422.6057017146084
    R conf_trigger_75 393.4726331418403
    R conf_trigger_75 335.0586961889599
    R conf_trigger_75 251.0842189975738
    R conf_trigger_100 489.98902039169667
    R conf_trigger_100 404.9277092319209
    R conf_trigger_100 295.8254669089954
    R conf_trigger_100 283.337769646016
    R conf_trigger_100 275.61478758275564
    R conf_trigger_100 273.4628556466357
    D conf_trigger_3 0.11086233525994516
    D conf_trigger_3 0.07821053996128313
    D conf_trigger_3 0.0722095674644871
    D conf_trigger_3 0.06466504166065162
    D conf_trigger_3 0.06100123332262515
    D conf_trigger_3 0.04212450360811619
    D conf_trigger_3 0.020217803405418115
    D conf_trigger_3 0.017903390234635476
    D conf_trigger_3 0.012654902396039221
    D conf_trigger_3 0.0058576200946689454
    D conf_trigger_3 0.00528848045937648
    D conf_trigger_3 0.0038203325309761147
    D conf_trigger_5 0.18406403837451554
    D conf_trigger_5 0.13311012561523697
    D conf_trigger_5 0.0370356933380992
    D conf_trigger_5 0.028290808017403204
    D conf_trigger_5 0.025702509808757955
    D conf_trigger_5 0.019138860557379376
    D conf_trigger_5 0.01912636500913503
    D conf_trigger_5 0.018795510125060567
    D conf_trigger_5 0.01719621891962345
    D conf_trigger_5 0.016161943005553354
    D conf_trigger_10 0.15704852133508448
    D conf_trigger_10 0.12570956494072572
    D conf_trigger_10 0.07438182532064452
    D conf_trigger_10 0.05618789008245328
    D conf_trigger_10 0.025172469019668887
    D conf_trigger_15 0.1883931564639546
    D conf_trigger_15 0.1620552795282772
    D conf_trigger_15 0.13759239885774965
    D conf_trigger_15 0.04403849294485106
    D conf_trigger_15 0.0411903535316724
    D conf_trigger_15 0.03890111747802893
    D conf_trigger_15 0.026079982997893176
    D conf_trigger_20 0.9063357723910769
    D conf_trigger_20 0.6963644953336668
    D conf_trigger_20 0.20823136011308924
    D conf_trigger_20 0.15711319826779618
    D conf_trigger_20 0.15191919856407496
    D conf_trigger_20 0.06520929582690628
    D conf_trigger_20 0.05720640231214281
    D conf_trigger_20 0.05310172263683337
    D conf_trigger_20 0.04381101800267042
    D conf_trigger_35 0.6950791130952275
    D conf_trigger_35 0.5761442852829853
    D conf_trigger_35 0.36407417367494543
    D conf_trigger_35 0.3618360684307808
    D conf_trigger_35 0.24841576118033024
    D conf_trigger_35 0.12299031602497947
    D conf_trigger_35 0.031843560621063756
    D conf_trigger_50 0.27518586999519623
    D conf_trigger_50 0.12373213703741363
    D conf_trigger_50 0.10018866480272241
    D conf_trigger_50 0.08376188394052686
    D conf_trigger_50 0.07859132508441025
    D conf_trigger_75 0.9122796627175188
    D conf_trigger_75 0.7442934913941264
    D conf_trigger_75 0.08921103814684568
    D conf_trigger_100 0.45408226453459866
    D conf_trigger_100 0.3405767012755436
    D conf_trigger_100 0.16612859711557204
    D conf_trigger_100 0.11703392769563489
    D conf_trigger_100 0.10147562408941975
    D conf_trigger_100 0.10094784641498888
    NR conf_trigger_3 4.095955675641138
    NR conf_trigger_3 3.7091777003699407
    NR conf_trigger_3 3.355565032162884
    NR conf_trigger_3 2.3584708938497134
    NR conf_trigger_3 1.1490151824837818
    NR conf_trigger_5 19.37183849298079
    NR conf_trigger_5 4.673302397234222
    NR conf_trigger_5 4.494180555111623
    NR conf_trigger_5 4.3746886511546235
    NR conf_trigger_5 4.149027519456035
    NR conf_trigger_5 2.422127844790344
    NR conf_trigger_10 34.38927641161696
    NR conf_trigger_10 15.553742427476136
    NR conf_trigger_10 14.045220320062471
    NR conf_trigger_10 7.355238918426005
    NR conf_trigger_10 6.856366757805694
    NR conf_trigger_15 38.2863735962735
    NR conf_trigger_15 26.884337638388434
    NR conf_trigger_15 19.54309318930676
    NR conf_trigger_15 9.087442230777265
    NR conf_trigger_15 6.464195644649644
    NR conf_trigger_20 68.08209484607053
    NR conf_trigger_20 58.56763740103684
    NR conf_trigger_20 55.41427954234977
    NR conf_trigger_20 45.399691716191015
    NR conf_trigger_20 25.713809819204016
    NR conf_trigger_20 17.18840648486179
    NR conf_trigger_20 16.16558481187333
    NR conf_trigger_20 14.492261329448521
    NR conf_trigger_20 13.33754969999742
    NR conf_trigger_20 12.390894556556017
    NR conf_trigger_35 50.4152105504649
    NR conf_trigger_35 45.31075556685147
    NR conf_trigger_35 38.50192453906107
    NR conf_trigger_35 30.416051767765005
    NR conf_trigger_35 28.98093446046623
    NR conf_trigger_35 25.97139537732937
    NR conf_trigger_35 23.328510030883663
    NR conf_trigger_35 20.52936793756706
    NR conf_trigger_35 15.686776293243904
    NR conf_trigger_35 14.708043561245757
    NR conf_trigger_50 109.21872429185663
    NR conf_trigger_50 78.75107958967114
    NR conf_trigger_50 71.68874845865557
    NR conf_trigger_50 65.38316114903623
    NR conf_trigger_50 50.813099556418614
    NR conf_trigger_50 38.86259188284146
    NR conf_trigger_50 36.490250833737676
    NR conf_trigger_50 30.51000080908876
    NR conf_trigger_50 29.838629899979864
    NR conf_trigger_50 26.548439444953363
    NR conf_trigger_50 21.94201284380037
    NR conf_trigger_50 19.138453638049707
    NR conf_trigger_50 18.79433350931602
    NR conf_trigger_50 15.91639371243051
    NR conf_trigger_75 55.28039939446543
    NR conf_trigger_75 52.20158639945184
    NR conf_trigger_75 51.54462595927899
    NR conf_trigger_75 44.854003445037435
    NR conf_trigger_75 36.490759916833824
    NR conf_trigger_75 33.86897779817413
    NR conf_trigger_75 31.421419197172764
    NR conf_trigger_75 23.77409101514688
    NR conf_trigger_75 22.246413810372424
    NR conf_trigger_75 19.14517446557894
    NR conf_trigger_75 17.47629484515545
    NR conf_trigger_100 51.76321687311578
    NR conf_trigger_100 48.237427900948056
    NR conf_trigger_100 41.74510674939506
    NR conf_trigger_100 32.55992032809908
    NR conf_trigger_100 27.418822435632844
    NR conf_trigger_100 20.624196650377428
    ND conf_trigger_3 0.0014531323715171512
    ND conf_trigger_3 0.0012196549591073074
    ND conf_trigger_3 0.001066358854648099
    ND conf_trigger_3 0.0010455196039713664
    ND conf_trigger_3 0.0007461766051887591
    ND conf_trigger_5 0.0024723423475352005
    ND conf_trigger_5 0.0016465926407863759
    ND conf_trigger_5 0.0016001977740622043
    ND conf_trigger_5 0.001585367359241491
    ND conf_trigger_5 0.0015488650951520633
    ND conf_trigger_5 0.0013360344424342625
    ND conf_trigger_10 0.007692080531245236
    ND conf_trigger_10 0.004468724014050391
    ND conf_trigger_10 0.0038763970198901674
    ND conf_trigger_10 0.003689130500301252
    ND conf_trigger_10 0.002951212264126534
    ND conf_trigger_10 0.0028939352754822575
    ND conf_trigger_10 0.002652090448695105
    ND conf_trigger_15 0.01616233103870884
    ND conf_trigger_15 0.005990723324683336
    ND conf_trigger_15 0.005127975531727324
    ND conf_trigger_15 0.005083004564662763
    ND conf_trigger_15 0.005054003534095113
    ND conf_trigger_15 0.004698700321059187
    ND conf_trigger_15 0.004471996636739292
    ND conf_trigger_15 0.004270808720496395
    ND conf_trigger_15 0.00408099698072416
    ND conf_trigger_15 0.003976446451491435
    ND conf_trigger_20 0.012145950493451563
    ND conf_trigger_20 0.008979641603294957
    ND conf_trigger_20 0.006480459265875515
    ND conf_trigger_20 0.006270064645987077
    ND conf_trigger_20 0.004937448432480333
    ND conf_trigger_20 0.004905361729270315
    ND conf_trigger_35 0.010633557407122709
    ND conf_trigger_35 0.009214956817862132
    ND conf_trigger_35 0.008395935121042539
    ND conf_trigger_35 0.007573513648494629
    ND conf_trigger_35 0.0066041423848884175
    ND conf_trigger_50 0.027023928105613305
    ND conf_trigger_50 0.01969622816129748
    ND conf_trigger_50 0.013483798023283667
    ND conf_trigger_50 0.012296552155700255
    ND conf_trigger_50 0.011609214468789302
    ND conf_trigger_50 0.011153765196757821
    ND conf_trigger_50 0.011044006874264448
    ND conf_trigger_50 0.010226103456944444
    ND conf_trigger_50 0.009608816591885295
    ND conf_trigger_50 0.008929219903939726
    ND conf_trigger_75 0.014422417164111233
    ND conf_trigger_75 0.01429460471993527
    ND conf_trigger_75 0.013143844472705436
    ND conf_trigger_75 0.012627844047757589
    ND conf_trigger_75 0.010947898827717333
    ND conf_trigger_75 0.010814382178465063
    ND conf_trigger_75 0.010027079266274415
    ND conf_trigger_100 0.0132493875254225
    ND conf_trigger_100 0.01240120483417288
    ND conf_trigger_100 0.012314993507296857
    ND conf_trigger_100 0.01104901002332195
    ND conf_trigger_100 0.010668541094112917
    ND conf_trigger_100 0.010572814674652023
    ND conf_trigger_100 0.010425323986161934
    NE conf_trigger_3 18.308223036904668
    NE conf_trigger_3 11.308352743233685
    NE conf_trigger_3 10.646793906841049
    NE conf_trigger_3 10.553617342003493
    NE conf_trigger_3 10.096938155636646
    NE conf_trigger_3 9.83957983781127
    NE conf_trigger_5 55.6423287099106
    NE conf_trigger_5 22.385977758605655
    NE conf_trigger_5 21.68541837219001
    NE conf_trigger_5 17.222275498984892
    NE conf_trigger_5 17.13952957826803
    NE conf_trigger_5 16.891400895082903
    NE conf_trigger_5 15.913357604106972
    NE conf_trigger_5 15.558236664858141
    NE conf_trigger_10 53.87993594542944
    NE conf_trigger_10 40.98644458823817
    NE conf_trigger_10 31.104642687354314
    NE conf_trigger_10 28.276773048611144
    NE conf_trigger_15 59.35272812769402
    NE conf_trigger_15 51.22758208365056
    NE conf_trigger_15 46.48751317162719
    NE conf_trigger_15 44.251992839436824
    NE conf_trigger_15 41.75140348738751
    NE conf_trigger_20 134.50483690536134
    NE conf_trigger_20 111.24994724637057
    NE conf_trigger_20 87.45257965038378
    NE conf_trigger_20 80.30357539302126
    NE conf_trigger_20 67.72403282693219
    NE conf_trigger_20 58.250406833927734
    NE conf_trigger_20 53.268214349172524
    NE conf_trigger_20 51.72372812784423
    NE conf_trigger_20 47.6486518042096
    NE conf_trigger_35 122.71148121628511
    NE conf_trigger_35 95.89991887353077
    NE conf_trigger_35 80.42193597432242
    NE conf_trigger_35 64.9969656332549
    NE conf_trigger_50 313.720238608202
    NE conf_trigger_50 182.82351367109362
    NE conf_trigger_50 160.29286538071375
    NE conf_trigger_50 113.11703396097803
    NE conf_trigger_50 108.63296219858019
    NE conf_trigger_50 101.36768555805205
    NE conf_trigger_50 89.37903859131586
    NE conf_trigger_50 83.10534812755249
    NE conf_trigger_75 254.98304088259619
    NE conf_trigger_75 197.59621017363332
    NE conf_trigger_75 137.762360048413
    NE conf_trigger_75 106.59031624518934
    NE conf_trigger_75 93.98361214698397
    NE conf_trigger_75 88.11112265823766
    NE conf_trigger_100 233.79181542573596
    NE conf_trigger_100 230.15572934477092
    NE conf_trigger_100 220.01261994089114
    NE conf_trigger_100 194.98483637749612
    NE conf_trigger_100 150.7584897924225
    NE conf_trigger_100 147.1779126713908
    NE conf_trigger_100 143.8755084672876
    NE conf_trigger_100 131.5319208597144
    NE conf_trigger_100 126.18018844433554
    NE conf_trigger_100 124.4933627475652
    NE conf_trigger_100 119.99395106612559
    NE conf_trigger_100 110.51628096148768
    NE conf_trigger_100 80.91725747777915
    NI conf_trigger_3 9.085602897482293
    NI conf_trigger_3 7.528221444016214
    NI conf_trigger_3 6.2445134847016455
    NI conf_trigger_3 5.543575142227087
    NI conf_trigger_3 4.787915794374333
    NI conf_trigger_3 4.506056972496982
    NI conf_trigger_5 39.14907269672305
    NI conf_trigger_5 8.092323320819249
    NI conf_trigger_5 8.079994138927644
    NI conf_trigger_10 41.34968899999259
    NI conf_trigger_10 26.1607384512692
    NI conf_trigger_10 22.816840157049967
    NI conf_trigger_10 22.411214539976758
    NI conf_trigger_10 22.339277423387596
    NI conf_trigger_10 21.699017576754105
    NI conf_trigger_10 21.540631483690547
    NI conf_trigger_10 20.38497089509296
    NI conf_trigger_10 19.700454585344676
    NI conf_trigger_10 18.644580470014205
    NI conf_trigger_10 15.689753741857759
    NI conf_trigger_15 47.41654487521428
    NI conf_trigger_15 39.227149539795874
    NI conf_trigger_15 28.714090979662508
    NI conf_trigger_15 27.979582411811304
    NI conf_trigger_15 26.22452161202817
    NI conf_trigger_15 22.708007781762873
    NI conf_trigger_15 22.03431880392036
    NI conf_trigger_15 21.666134191305684
    NI conf_trigger_20 98.60371621845235
    NI conf_trigger_20 94.90701543478639
    NI conf_trigger_20 70.99591592102568
    NI conf_trigger_20 69.38509336702076
    NI conf_trigger_20 58.62180979614013
    NI conf_trigger_20 48.77719181479055
    NI conf_trigger_20 46.457051877127164
    NI conf_trigger_20 37.404786877395814
    NI conf_trigger_20 25.988598415248052
    NI conf_trigger_20 25.59535754502297
    NI conf_trigger_35 86.03925918195152
    NI conf_trigger_35 83.56957740870747
    NI conf_trigger_35 82.70320639681337
    NI conf_trigger_35 50.560764535596064
    NI conf_trigger_35 42.27653617861982
    NI conf_trigger_35 38.23531307771972
    NI conf_trigger_50 216.46762601309342
    NI conf_trigger_50 128.20853438033492
    NI conf_trigger_50 111.25968436763515
    NI conf_trigger_50 83.19518327561062
    NI conf_trigger_50 78.61412039395734
    NI conf_trigger_50 61.9316712695464
    NI conf_trigger_50 57.330363459897995
    NI conf_trigger_50 45.46018710044534
    NI conf_trigger_75 118.554921881994
    NI conf_trigger_75 91.44370343861968
    NI conf_trigger_75 80.38369646440572
    NI conf_trigger_75 78.71546617513386
    NI conf_trigger_75 70.51700062618538
    NI conf_trigger_75 69.18158810321896
    NI conf_trigger_75 66.43083245697137
    NI conf_trigger_100 80.72841550535
    NI conf_trigger_100 77.50187620847916
    NI conf_trigger_100 77.36433142111716
    NI conf_trigger_100 74.83044273559524
    IC conf_trigger_3 0.9206940848767339
    IC conf_trigger_3 0.8659867775028853
    IC conf_trigger_3 0.6511316591425462
    IC conf_trigger_3 0.5431239000203468
    IC conf_trigger_3 0.5369822975946826
    IC conf_trigger_3 0.5158406573780896
    IC conf_trigger_3 0.4188354506329014
    IC conf_trigger_5 4.920073319061745
    IC conf_trigger_5 4.565948261834948
    IC conf_trigger_5 3.934060769368811
    IC conf_trigger_5 1.8557482794098037
    IC conf_trigger_5 1.5610127072563964
    IC conf_trigger_5 1.5100149297105456
    IC conf_trigger_5 0.8276492355799464
    IC conf_trigger_5 0.8162888354087902
    IC conf_trigger_10 18.513248398148583
    IC conf_trigger_10 5.669179111868673
    IC conf_trigger_10 5.514421065209118
    IC conf_trigger_10 4.990275176602865
    IC conf_trigger_10 3.1746974984433267
    IC conf_trigger_10 3.0561323294350333
    IC conf_trigger_10 2.2970194312354626
    IC conf_trigger_10 1.4704682066990102
    IC conf_trigger_15 16.96576295775872
    IC conf_trigger_15 16.03867084500175
    IC conf_trigger_15 11.756779216741165
    IC conf_trigger_15 7.240279033898861
    IC conf_trigger_15 2.9944252148615025
    IC conf_trigger_15 2.785592699526403
    IC conf_trigger_15 2.706936141438098
    IC conf_trigger_15 1.8757625515588952
    IC conf_trigger_15 1.506717439479091
    IC conf_trigger_20 24.59183264137965
    IC conf_trigger_20 14.037459195495828
    IC conf_trigger_20 9.794294931470306
    IC conf_trigger_20 8.560888576950372
    IC conf_trigger_20 6.247320515283095
    IC conf_trigger_20 4.297153873916118
    IC conf_trigger_20 3.5090783263635927
    IC conf_trigger_20 3.1527814013379123
    IC conf_trigger_20 2.4708474135626384
    IC conf_trigger_35 14.832321826757212
    IC conf_trigger_35 9.192054782249205
    IC conf_trigger_35 8.133222256129834
    IC conf_trigger_35 6.824375631767877
    IC conf_trigger_35 3.571056498976656
    IC conf_trigger_50 19.365875214438937
    IC conf_trigger_50 9.410880665909756
    IC conf_trigger_50 7.26919816384627
    IC conf_trigger_50 6.475850134224322
    IC conf_trigger_50 5.393455054289168
    IC conf_trigger_50 4.58989908176092
    IC conf_trigger_75 45.19559559412244
    IC conf_trigger_75 24.41666601094376
    IC conf_trigger_75 13.81208661386574
    IC conf_trigger_75 12.449292059105094
    IC conf_trigger_75 7.337621426530503
    IC conf_trigger_75 5.537628496009588
    IC conf_trigger_75 4.897373209482263
    IC conf_trigger_100 38.489530074351784
    IC conf_trigger_100 24.6137832167468
    IC conf_trigger_100 12.062047516965528
    IC conf_trigger_100 10.019376298748426
    IC conf_trigger_100 8.399666016084922
    IC conf_trigger_100 7.530271551911328
    IC conf_trigger_100 7.4566292529173825
    IC conf_trigger_100 6.807544361545326
    IC conf_trigger_100 6.373667683417573
    IC conf_trigger_100 6.269217643742159
    NIC conf_trigger_3 0.12176496102474503
    NIC conf_trigger_3 0.0821180789689982
    NIC conf_trigger_3 0.07094430712587252
    NIC conf_trigger_3 0.0697765703911676
    NIC conf_trigger_3 0.06695023486789048
    NIC conf_trigger_3 0.04972868540068113
    NIC conf_trigger_5 0.22359313937374695
    NIC conf_trigger_5 0.18460546712951229
    NIC conf_trigger_5 0.16548320998061988
    NIC conf_trigger_5 0.11196843082398698
    NIC conf_trigger_10 0.45641124697639923
    NIC conf_trigger_10 0.28686578315139855
    NIC conf_trigger_10 0.24735222022653308
    NIC conf_trigger_10 0.22411486312377762
    NIC conf_trigger_10 0.19101834517776645
    NIC conf_trigger_15 0.6019746333038205
    NIC conf_trigger_15 0.4204537856794833
    NIC conf_trigger_15 0.32696907420922683
    NIC conf_trigger_15 0.31654855864475984
    NIC conf_trigger_15 0.30296006432514555
    NIC conf_trigger_20 0.6104585883467182
    NIC conf_trigger_20 0.5797502475885549
    NIC conf_trigger_20 0.518067778147933
    NIC conf_trigger_20 0.4384487048532972
    NIC conf_trigger_20 0.4218656062629734
    NIC conf_trigger_20 0.4211194640870209
    NIC conf_trigger_20 0.39411121387317816
    NIC conf_trigger_35 1.038633894658174
    NIC conf_trigger_35 0.7499409948456374
    NIC conf_trigger_35 0.6807514175023777
    NIC conf_trigger_35 0.5968186930654795
    NIC conf_trigger_35 0.46703210731454
    NIC conf_trigger_50 1.8659555273463864
    NIC conf_trigger_50 1.283569100242551
    NIC conf_trigger_50 0.9191113164455682
    NIC conf_trigger_50 0.7659118787373786
    NIC conf_trigger_50 0.7334553782161988
    NIC conf_trigger_50 0.7198214911896397
    NIC conf_trigger_50 0.7128411971067943
    NIC conf_trigger_50 0.6697306114838751
    NIC conf_trigger_50 0.6146946669234619
    NIC conf_trigger_75 0.9427730356825347
    NIC conf_trigger_75 0.7675031925370025
    NIC conf_trigger_75 0.7593809335045997
    NIC conf_trigger_75 0.7391678271006554
    NIC conf_trigger_75 0.7237365317027299
    NIC conf_trigger_75 0.696363380262258
    NIC conf_trigger_75 0.6400018581790685
    NIC conf_trigger_100 1.3766520797751796
    NIC conf_trigger_100 1.3392491195326635
    NIC conf_trigger_100 1.064428002620557
    NIC conf_trigger_100 1.0510500361121764
    NIC conf_trigger_100 0.8758202788774567
    NIC conf_trigger_100 0.8215329238732753
    NIC conf_trigger_100 0.7999048130288015
    NIC conf_trigger_100 0.7354400205892269
    NIC conf_trigger_100 0.7288672313923449
    IH conf_trigger_3 5.166117728476068
    IH conf_trigger_3 4.030910057574254
    IH conf_trigger_3 3.7723415337569044
    IH conf_trigger_3 2.904993317975993
    IH conf_trigger_3 1.482624708381191
    IH conf_trigger_3 0.9039519541295715
    IH conf_trigger_3 0.6766482726989878
    IH conf_trigger_3 0.6487603727793467
    IH conf_trigger_3 0.24018311316675678
    IH conf_trigger_3 0.24001185124725663
    IH conf_trigger_3 0.17322152241863
    IH conf_trigger_5 2.4498552131315914
    IH conf_trigger_5 1.681628569776701
    IH conf_trigger_5 1.225150508567616
    IH conf_trigger_5 0.9121969340615905
    IH conf_trigger_5 0.6283516123652303
    IH conf_trigger_5 0.6250356044882677
    IH conf_trigger_5 0.5530457747690721
    IH conf_trigger_5 0.4537443189401348
    IH conf_trigger_5 0.44710872204757124
    IH conf_trigger_10 14.221850641135497
    IH conf_trigger_10 1.5549907313046152
    IH conf_trigger_10 1.087114579400216
    IH conf_trigger_10 0.8416869523839673
    IH conf_trigger_10 0.6730140934056706
    IH conf_trigger_15 20.373212719518563
    IH conf_trigger_15 6.110661591548021
    IH conf_trigger_15 3.7745230668698184
    IH conf_trigger_15 2.199210183998938
    IH conf_trigger_15 1.506516351612356
    IH conf_trigger_15 1.3300079691359017
    IH conf_trigger_15 1.0319799874971105
    IH conf_trigger_15 0.8852679230065643
    IH conf_trigger_20 13.632743095964065
    IH conf_trigger_20 2.637930081912961
    IH conf_trigger_20 2.059468035274301
    IH conf_trigger_20 1.689869197468779
    IH conf_trigger_20 1.566859172288654
    IH conf_trigger_20 1.50201521906043
    IH conf_trigger_35 24.45221472926628
    IH conf_trigger_35 2.34295770250929
    IH conf_trigger_35 2.124692082850755
    IH conf_trigger_35 1.9645773883783937
    IH conf_trigger_35 1.6614511923830593
    IH conf_trigger_35 1.531671336163107
    IH conf_trigger_50 18.822366849437543
    IH conf_trigger_50 8.04673488781494
    IH conf_trigger_50 7.080141904883717
    IH conf_trigger_50 3.8667551599800425
    IH conf_trigger_50 2.9238567443570664
    IH conf_trigger_50 2.4972757444077556
    IH conf_trigger_50 2.1939191544886523
    IH conf_trigger_75 23.843253152330448
    IH conf_trigger_75 7.234250581334502
    IH conf_trigger_75 5.561984683991645
    IH conf_trigger_75 4.953042621002254
    IH conf_trigger_75 3.896061050114423
    IH conf_trigger_75 3.671226859000467
    IH conf_trigger_75 2.6270671879219285
    IH conf_trigger_100 29.306598792453872
    IH conf_trigger_100 10.231323601471754
    IH conf_trigger_100 5.43120214083224
    IH conf_trigger_100 4.8272437102112695
    IH conf_trigger_100 4.010881234693455
    IH conf_trigger_100 3.7109794339111497
    IH conf_trigger_100 2.542985732195494
    NIH conf_trigger_3 0.06799083724769588
    NIH conf_trigger_3 0.05079621287880171
    NIH conf_trigger_3 0.046904559697350696
    NIH conf_trigger_3 0.04497350550189136
    NIH conf_trigger_3 0.040884850092427316
    NIH conf_trigger_3 0.04064349847883104
    NIH conf_trigger_3 0.037284933606006716
    NIH conf_trigger_3 0.03563351528117605
    NIH conf_trigger_3 0.025967585004519976
    NIH conf_trigger_5 0.2121968269216516
    NIH conf_trigger_5 0.061090727284985595
    NIH conf_trigger_5 0.05536241602943087
    NIH conf_trigger_5 0.052510414447912344
    NIH conf_trigger_5 0.04808354819215367
    NIH conf_trigger_5 0.04770153990377207
    NIH conf_trigger_10 0.2169320295243056
    NIH conf_trigger_10 0.1797478707887121
    NIH conf_trigger_10 0.15084500930613517
    NIH conf_trigger_10 0.13033860028530825
    NIH conf_trigger_10 0.12603199980318378
    NIH conf_trigger_10 0.12442057204264269
    NIH conf_trigger_10 0.12296693637522574
    NIH conf_trigger_10 0.10604322344195918
    NIH conf_trigger_10 0.10410340671478567
    NIH conf_trigger_10 0.09696641897066566
    NIH conf_trigger_10 0.09107636552534709
    NIH conf_trigger_10 0.09077940415855473
    NIH conf_trigger_15 0.2847763424782712
    NIH conf_trigger_15 0.16132743559905904
    NIH conf_trigger_15 0.1528410567569219
    NIH conf_trigger_15 0.14377834737629436
    NIH conf_trigger_15 0.13884386607083044
    NIH conf_trigger_15 0.1256840118277353
    NIH conf_trigger_15 0.11920717312313145
    NIH conf_trigger_20 0.2722677777368213
    NIH conf_trigger_20 0.16175439394102054
    NIH conf_trigger_20 0.1508908293674304
    NIH conf_trigger_20 0.14004105919352264
    NIH conf_trigger_35 0.35688772677398617
    NIH conf_trigger_35 0.2624005282374836
    NIH conf_trigger_35 0.24805797893256207
    NIH conf_trigger_35 0.18860367810297002
    NIH conf_trigger_50 0.6502322579664314
    NIH conf_trigger_50 0.5494435351158964
    NIH conf_trigger_50 0.3957840641635039
    NIH conf_trigger_50 0.3128782219596193
    NIH conf_trigger_50 0.30616538679724464
    NIH conf_trigger_50 0.29421197286283524
    NIH conf_trigger_50 0.2941277826653961
    NIH conf_trigger_50 0.291401789690904
    NIH conf_trigger_75 1.025238950311537
    NIH conf_trigger_75 0.8099359206340694
    NIH conf_trigger_75 0.48220716709117034
    NIH conf_trigger_75 0.4561007056829099
    NIH conf_trigger_75 0.4224147662330127
    NIH conf_trigger_75 0.4219219097849616
    NIH conf_trigger_75 0.4009252796511748
    NIH conf_trigger_75 0.3115564619121812
    NIH conf_trigger_75 0.3110848331936444
    NIH conf_trigger_75 0.3034141679046757
    NIH conf_trigger_100 0.4691085554929311
    NIH conf_trigger_100 0.3994052454141801
    NIH conf_trigger_100 0.386765318735879
    NIH conf_trigger_100 0.36482091240739767
    NIH conf_trigger_100 0.3514647245594212
    NIH conf_trigger_100 0.30696379566723425
    NIH conf_trigger_100 0.2798808028464319
    E_C conf_trigger_3 232.36475268778076
    E_C conf_trigger_3 98.86084006240398
    E_C conf_trigger_3 78.96638525215423
    E_C conf_trigger_3 34.34100139636885
    E_C conf_trigger_5 489.976077276459
    E_C conf_trigger_5 248.51251218673062
    E_C conf_trigger_5 168.98123659944065
    E_C conf_trigger_5 142.39479405521277
    E_C conf_trigger_5 91.54378408204308
    E_C conf_trigger_5 90.28231314117
    E_C conf_trigger_5 79.89768657890338
    E_C conf_trigger_5 67.10132217479459
    E_C conf_trigger_10 1683.128976413635
    E_C conf_trigger_10 1443.8536888301724
    E_C conf_trigger_10 467.0243620161858
    E_C conf_trigger_10 412.2554281021259
    E_C conf_trigger_10 313.11635455632523
    E_C conf_trigger_10 273.6735540321186
    E_C conf_trigger_10 241.8454206795
    E_C conf_trigger_10 224.6377073675196
    E_C conf_trigger_10 150.26776135917183
    E_C conf_trigger_10 125.19312043500388
    E_C conf_trigger_10 104.42042430426379
    E_C conf_trigger_15 3281.18223944991
    E_C conf_trigger_15 1473.5440735802847
    E_C conf_trigger_15 380.13052026606687
    E_C conf_trigger_15 300.13531679929184
    E_C conf_trigger_15 242.39429389391674
    E_C conf_trigger_15 238.13433647966562
    E_C conf_trigger_15 228.67090787940643
    E_C conf_trigger_15 183.03101029446864
    E_C conf_trigger_15 144.95178987920832
    E_C conf_trigger_20 481.2227537387012
    E_C conf_trigger_20 462.9164667469259
    E_C conf_trigger_20 457.7788465157728
    E_C conf_trigger_20 366.3776282784896
    E_C conf_trigger_20 244.78105741263528
    E_C conf_trigger_20 183.54480380545917
    E_C conf_trigger_35 1657.7219620256221
    E_C conf_trigger_35 1329.4795090651155
    E_C conf_trigger_35 586.7469748475153
    E_C conf_trigger_35 516.5362582529931
    E_C conf_trigger_35 469.12433231272894
    E_C conf_trigger_35 462.32799559506
    E_C conf_trigger_35 452.2649344824047
    E_C conf_trigger_35 434.6376740813171
    E_C conf_trigger_35 382.882105019296
    E_C conf_trigger_35 356.0713422049067
    E_C conf_trigger_50 1819.8619763331258
    E_C conf_trigger_50 1295.2438570003635
    E_C conf_trigger_50 1266.1497425730026
    E_C conf_trigger_50 932.8057107551134
    E_C conf_trigger_50 734.0547578480542
    E_C conf_trigger_50 558.7089479596726
    E_C conf_trigger_50 472.1591548093253
    E_C conf_trigger_50 291.57269236644504
    E_C conf_trigger_75 780.5480526755825
    E_C conf_trigger_75 752.9262948653125
    E_C conf_trigger_75 751.1016644547195
    E_C conf_trigger_75 722.8783628467366
    E_C conf_trigger_75 697.8002707479006
    E_C conf_trigger_75 607.5412016858179
    E_C conf_trigger_75 486.5757978383707
    E_C conf_trigger_100 712.5435311354108
    E_C conf_trigger_100 615.1453747509911
    E_C conf_trigger_100 570.1158112177549
    I_C conf_trigger_3 223.35169155776794
    I_C conf_trigger_3 123.47841516589497
    I_C conf_trigger_3 72.38301630405061
    I_C conf_trigger_3 64.19457096212923
    I_C conf_trigger_3 57.18306543320497
    I_C conf_trigger_3 45.813313558584106
    I_C conf_trigger_3 39.30428381051965
    I_C conf_trigger_3 38.053276227230135
    I_C conf_trigger_5 527.8712143576246
    I_C conf_trigger_5 242.22962731093085
    I_C conf_trigger_5 183.7314699316068
    I_C conf_trigger_5 144.06818780416646
    I_C conf_trigger_5 75.98192684941603
    I_C conf_trigger_5 62.19911192991033
    I_C conf_trigger_10 1733.8952418967558
    I_C conf_trigger_10 1386.952702276823
    I_C conf_trigger_10 467.4798970516505
    I_C conf_trigger_10 327.67033836331825
    I_C conf_trigger_10 325.11241305333357
    I_C conf_trigger_10 271.98863838747224
    I_C conf_trigger_10 202.9257238561036
    I_C conf_trigger_10 152.81279391088262
    I_C conf_trigger_10 147.43686061204588
    I_C conf_trigger_15 3176.945182943654
    I_C conf_trigger_15 1403.956180152772
    I_C conf_trigger_15 422.1081266914988
    I_C conf_trigger_15 411.3230161162304
    I_C conf_trigger_15 302.6129629840801
    I_C conf_trigger_15 209.04671527802705
    I_C conf_trigger_15 172.65168638474162
    I_C conf_trigger_15 145.97974793438945
    I_C conf_trigger_15 127.9699732175595
    I_C conf_trigger_20 655.8600310247509
    I_C conf_trigger_20 605.9895904136738
    I_C conf_trigger_20 412.8747614792121
    I_C conf_trigger_20 271.40678828358205
    I_C conf_trigger_20 267.7284809932167
    I_C conf_trigger_20 224.86270865391714
    I_C conf_trigger_20 209.73218527595063
    I_C conf_trigger_35 1577.9972727266006
    I_C conf_trigger_35 1365.282173074028
    I_C conf_trigger_35 895.061051398978
    I_C conf_trigger_35 793.9102952789298
    I_C conf_trigger_35 505.88908655292516
    I_C conf_trigger_35 490.04977913078983
    I_C conf_trigger_35 373.3562251145012
    I_C conf_trigger_35 290.5307966930606
    I_C conf_trigger_50 1980.6369233162334
    I_C conf_trigger_50 1284.3192370256247
    I_C conf_trigger_50 1209.0417816201673
    I_C conf_trigger_50 1063.6330703390363
    I_C conf_trigger_50 853.7746250933448
    I_C conf_trigger_50 532.4443701944797
    I_C conf_trigger_50 502.12884677623515
    I_C conf_trigger_50 461.8106146927966
    I_C conf_trigger_50 441.6712023368875
    I_C conf_trigger_50 323.9484783622893
    I_C conf_trigger_75 727.5449463225168
    I_C conf_trigger_75 599.8054816186466
    I_C conf_trigger_75 579.027048211312
    I_C conf_trigger_75 539.0274994479101
    I_C conf_trigger_75 506.0783088288739
    I_C conf_trigger_75 502.48370840927095
    I_C conf_trigger_75 492.8075378446448
    I_C conf_trigger_75 478.65147841813365
    I_C conf_trigger_75 475.7334501611737
    I_C conf_trigger_100 645.466684575598
    I_C conf_trigger_100 583.1693058025188
    I_C conf_trigger_100 558.2411999153784
    I_C conf_trigger_100 475.15685866923593
    I_C conf_trigger_100 446.4725895717308
    beh_mod conf_trigger_3 0.05773941027153272
    beh_mod conf_trigger_3 0.05182778480700201
    beh_mod conf_trigger_3 0.04471628977659158
    beh_mod conf_trigger_3 0.04061335090991956
    beh_mod conf_trigger_3 0.03925756033612774
    beh_mod conf_trigger_5 0.07263656874036702
    beh_mod conf_trigger_5 0.05904920501101266
    beh_mod conf_trigger_5 0.049976786216949606
    beh_mod conf_trigger_5 0.04939747100800334
    beh_mod conf_trigger_5 0.045841230634515506
    beh_mod conf_trigger_5 0.04460230894392589
    beh_mod conf_trigger_5 0.043170323054409966
    beh_mod conf_trigger_10 0.25557859346637885
    beh_mod conf_trigger_10 0.06733763245925833
    beh_mod conf_trigger_10 0.05662188244694641
    beh_mod conf_trigger_10 0.04709381439672518
    beh_mod conf_trigger_10 0.04114939163484954
    beh_mod conf_trigger_15 0.10553137985393125
    beh_mod conf_trigger_15 0.06305038219502535
    beh_mod conf_trigger_15 0.0538699776293496
    beh_mod conf_trigger_15 0.05327803867560668
    beh_mod conf_trigger_15 0.051307974445352886
    beh_mod conf_trigger_15 0.045827541404339395
    beh_mod conf_trigger_15 0.04316449657724685
    beh_mod conf_trigger_15 0.041012259953255636
    beh_mod conf_trigger_20 0.05712301187179283
    beh_mod conf_trigger_20 0.05273936192540398
    beh_mod conf_trigger_20 0.04139639573721469
    beh_mod conf_trigger_35 0.06104392367712428
    beh_mod conf_trigger_35 0.057591533550995354
    beh_mod conf_trigger_35 0.05151781481858237
    beh_mod conf_trigger_35 0.04841756331921234
    beh_mod conf_trigger_35 0.043631591011191496
    beh_mod conf_trigger_50 0.09894431368245167
    beh_mod conf_trigger_50 0.07888999209026569
    beh_mod conf_trigger_50 0.07339436103819144
    beh_mod conf_trigger_50 0.0643043103081474
    beh_mod conf_trigger_50 0.05938767496771324
    beh_mod conf_trigger_50 0.054940114898976614
    beh_mod conf_trigger_50 0.053892605576895326
    beh_mod conf_trigger_50 0.05096213683228302
    beh_mod conf_trigger_50 0.05053643970976661
    beh_mod conf_trigger_50 0.04905843162026863
    beh_mod conf_trigger_75 0.09006102101386823
    beh_mod conf_trigger_75 0.0578906386764474
    beh_mod conf_trigger_75 0.05354567222882884
    beh_mod conf_trigger_100 0.09075122226042945
    beh_mod conf_trigger_100 0.08741977916961317
    beh_mod conf_trigger_100 0.0860866669448944
    beh_mod conf_trigger_100 0.08478786420015448
    beh_mod conf_trigger_100 0.08127724663768243
    beh_mod conf_trigger_100 0.0757288821015335
    beh_mod conf_trigger_100 0.07169799289786345
    


```python
filename = 'stats_dict'
outfile = open(filename, 'wb')
pickle.dump(stats_dict, outfile)
outfile.close()
```
