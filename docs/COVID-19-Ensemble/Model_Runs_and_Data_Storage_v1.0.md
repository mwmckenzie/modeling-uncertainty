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
## Create a properties dictionary for future reference and labeling tasks
This is created primarily for outward facing visualization and display applications, though it can be useful for reference with the various results calculations, as well.
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
## Export the properties dictionary
```python
filename = 'properties_dict'
outfile = open(filename, 'wb')
pickle.dump(properties_dict, outfile)
outfile.close()
```
## Create a function that will return a key if a value is known
Be careful of using this with non-unique values, as this funciton returns the first match encountered. Advise _only_ using with unique value dictionaries.
```python
def getKeyWithID(in_dict, in_id, in_value):
    for key in in_dict:
        if properties_dict['results'][key] == {in_id: in_value}:
            return key
            
getKeyWithID(properties_dict['results'], 'id', 'I_C')
```




    'Infectious (Cumulative)'

## Create a results dictionary repository that bundles results by type
This allows for quick and easy statistics calculations by type (mean, percentiles, std, etc), as well as plotting visualizations.
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
## Export and save the results dictionary
Note that due to the number of ensembles, models, and result types this file is going to be quite large with the default number of models (~1.5gb).
```python
filename = 'results_dict'
outfile = open(filename, 'wb')
pickle.dump(results_dict, outfile)
outfile.close()
```
## Create a seperate statistics dictionary
The dictionary is created to store summarized statistical calculations of all ensemble model results.
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
## Finding a _best fit_ model run compared against the calculated mean from the 1000 models
This is done for two reasons:
- Curiosity. It seems very interesting to compare the mean against the models and see how they differ.
- To attempt to capture inconsistencies. If the mean is not well represented or reflected by a single model run (out of 1000 total model runs) there should be consideration in how the mean is used. The mean can still provide insights into trends and potential outcomes, but the less similar the mean is with actual model runs, the more the individual model runs should be examined to better understand the expected nature of real world results.
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
## Exporting the much smaller statistics dictionary for later use in visualizations or other applications
Compared against the results dictionary/file, the statistics dictionary is a tiny fraction of the size, and much easier to export, import, store, and share.
```python
filename = 'stats_dict'
outfile = open(filename, 'wb')
pickle.dump(stats_dict, outfile)
outfile.close()
```
