---
layout: default
title: Graph-Based Network SEIR Simulation
parent: CVD19 Graph Network Model
nav_order: 2
---

# Modeling an Epidemic with Graphs
## Using Graphs and Networks to Simulate a SEIR Model
To create and utilize graphs we first expand our imports and include the python library __networkx__, as well as number of other libraries that will assist in graph plotting and visualizations.


```python
import itertools
import networkx as nx
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import numpy as np
import random
import pickle
import holoviews as hv
from holoviews import opts
import panel

sns.set()
plt.rcParams["figure.figsize"] = (10, 5)

%matplotlib inline
hv.extension('bokeh')

# defaults = dict(width=400, height=400)
# hv.opts.defaults(
#     opts.EdgePaths(**defaults), opts.Graph(**defaults), opts.Nodes(**defaults))
```







<div class="logo-block">
<img src='data:image/png;base64,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
roTBs2RqAAAAAElFTkSuQmCC'
     style='height:25px; border-radius:12px; display: inline-block; float: left; vertical-align: middle'></img>


  <img src='data:image/png;base64,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'
       style='height:15px; border-radius:12px; display: inline-block; float: left'></img>





</div>



## Setting a few global variables
We will define a few of the variables we will be working with going forward:
- __N__: The population of each model run. 
    - Currently working with a max of around 1,000. 
    - Above 1,000 the model slows exponentially. 
    - We will need to consider ways to increase efficiency if we want to run simulations of >1,000 population size regularly or as part of an ensemble. 
    - Worth considering and testing how the magnitudes of difference in the dynamics and outcomes with different population variations.
- We set the infectious case types up in a cascading probability equation (summing to 1) for use in a future algorithm check. Infectious case types:
    - __i_asym__ = asymptomatic rate
    - __i_mild__ = mild infection rate
    - __i_mod__ = moderate infection rate
    - __i_severe__ = severe infection rate
    - __i_critical__ = critical rate


```python
N = 1_000 # default 1,000

i_asym = .044 # (def 0.044) asymptomatic rate
i_mild = i_asym + .51 # (def 0.51) mild infection rate
i_mod = i_mild + .388 # (def 0.388) mod inf rate
i_severe = i_mod + .052 # (def 0.052) severe inf rate
i_critical = i_severe + .006 # (def 0.006) critical rate

beh_max_mean, beh_max_low, beh_max_high = 10, 5, 15
```

## Recycle the _df_dist_ class from the Ensemble Model
This will allow us to import and reuse the distribution files created by the ensemble modeling application (see below).


```python
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
        
        fig, cp1 = plt.subplots(figsize=(10,4))
        cp1.hist(self.pert, 20)
        cp1.set_title(f'{self.name} Distribution Histogram')
        plt.tight_layout()
        
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

## Import Probability Distributions from the Ensemble Model Application
We take advantage of the distribution files created in our previous project and import the same distributions directly to avoid having to recalculate, reprocess, and reorganize similar data.


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

## Take advantage of graph properties with _personalities_
Unlike in our statistically calculated SEIR ensemble models, in which the behavior of the population was averaged, graphs allow us to provide each person (represented as a node in our graph/network) a "personality" - or more specifically a behavioral predisposition towards risk.
- The distribution created below represents a signal at which a person would be most cautious - least risky - in their daily contact behaviors.
- In the same manner as the SEIR ensemble models, as the number of confirmed cases nears the sampled behavioral max number, the "danger signal" becomes stronger and the person is less likely to have a person-to-person contact.


```python
beh_max_dist = df_dist(beh_max_mean, beh_max_low, beh_max_high)
```

Below, we once again take advantage of the built-in __checkParams()__ function of the __df_dist__ class to ensure both gain insight into our distribution and to verify it matches our desired outcome.


```python
beh_max_dist.checkParams()
```

    Pert vars: mu: 9.871794871794872, low: 0.7692307692307692, high: 20.769230769230766
    Original inputs: Mean=10, Low=5, High=15
    New outputs: Mean=10.163034972936682, Low=5.174634107080426, High=15.307316713150028
    


![png](output_11_1.png)


## Estimating the fatality rate of the critical cases
As we are breaking out the critical cases of COVID-19, we can do a check against the expected number of fatilities as the critical cases are identified. 
- This will then ensure that the fatalities are generated from the likely cases (the most ill) and are of the expected proportion to the population size.
- To estimate the appropriate number of fatalities per critical case, we use the confirmed and cfr rates against critical and critical fatality rates as seen in the following calculation:
$$Confirmed Cases * Case Fatality Rate = Critical Cases * Critical Fatalitiy Rate$$
- As we have values for the mean of the expected confirmed cases (per infected population), cfr, and critical cases, we can refine the equation as thus:
$$Critical Fatalitiy Rate = \frac{Confirmed Cases * Case Fatality Rate}{Critical Cases}$$
- The critical case rate is then updated to reflect the range set aside for the case fatality rate.
- Finally, we check the critical case rate


```python
crit_case_rate = .006
crit_fat_rate = (c2i.mu * cfr.mu) / crit_case_rate
i_critical = i_severe + .006 - (.006 * crit_fat_rate) # (def 0.006) critical rate
crit_case_range = i_critical - i_severe
crit_fat_range = 1 - i_critical
print(f'For all infected the crit case percentage is {crit_case_range*100} and crit fat percentage is {crit_fat_range*100}')
```

    For all infected the crit case percentage is 0.5810126582278419 and crit fat percentage is 0.01898734177214756
    

## Creating the graph
We are ready to generate the graph (__G__), which we do using a method from the networkx library: __nx.Graph()__
- When invoked without arguments, __G__ is created as an empty graph, which must then be populated.
- We then add a node representing each person in our simulated population (of size __N__).
    - Each person begins with in the state of _susceptible_ (__'S'__)
    - A behavior predisposition is also assigned to each person which will govern how they likely they are to have contact with their frequent and  infrequent contacts given the current _danger signal_ -> the total number of confirmed cases.


```python
G = nx.Graph()

for i in range(N):
    G.add_node(i, entity=f'Person {i}')
    nx.set_node_attributes(G, {i: {'state':'S'}})
    nx.set_node_attributes(G, {i: {'beh_max': beh_max_dist.getSample()}})
```

Below, we display and verify the first 10 nodes of our graph.


```python
list(G.nodes.data())[:10]
```




    [(0, {'entity': 'Person 0', 'state': 'S', 'beh_max': 13.276124248262928}),
     (1, {'entity': 'Person 1', 'state': 'S', 'beh_max': 9.897497608529193}),
     (2, {'entity': 'Person 2', 'state': 'S', 'beh_max': 2.6783071885987195}),
     (3, {'entity': 'Person 3', 'state': 'S', 'beh_max': 14.471545084817024}),
     (4, {'entity': 'Person 4', 'state': 'S', 'beh_max': 8.371324269159299}),
     (5, {'entity': 'Person 5', 'state': 'S', 'beh_max': 9.850166143463145}),
     (6, {'entity': 'Person 6', 'state': 'S', 'beh_max': 7.507666049474548}),
     (7, {'entity': 'Person 7', 'state': 'S', 'beh_max': 12.041658644634538}),
     (8, {'entity': 'Person 8', 'state': 'S', 'beh_max': 10.97357699185915}),
     (9, {'entity': 'Person 9', 'state': 'S', 'beh_max': 2.9664317115518095})]



## Introduce the virus
Here we randomly select a person to be the introduction vector of the disease into the population.
- We then set their current _state_ to _exposed_ (__'E'__)
- We also set the period  of the individuals infection by sampling the incubation period distribution.
- Finally we create and add the person to the list of exposed persons and print the node information for display and verification.


```python
rand_start = np.random.randint(len(G))

nx.set_node_attributes(G, {rand_start: {'state':'E', 'E_date': 1, 'I_date': 1 + int(e2i.getSample())}})
E = [rand_start]
print(rand_start, G.nodes[rand_start])
```

    676 {'entity': 'Person 676', 'state': 'E', 'beh_max': 14.426779617910498, 'E_date': 1, 'I_date': 9}
    

## Creating the network
Next we create the actual network of daily contacts the population normally engages in. 
- Each person has two types of person-to-person contact groups: frequent and infrequent.
    - These are similar to the  SEIR ensemble model variables and are intended to represent close, daily person-to-person contacts. Generally familial or close friends that are interacted with on a regular bases.
    - Because these types of groups are usually shared, we create these networks in overlapping clusters. 
    - Infrequent contacts, however, are generally smaller in number (per the distributions), and are additionally randomly assigned from the total population, representing contact outside the normal, close group.
    - Weights are assigned to each _edge_ between contacts.
        - Frequent contacts have generally smaller weights, indicating a closer relationship.
        - Infrequent contacts, converselly, generally have larger weights.
    - As behavior is modified to be more risk-adverse, higher weighted contacts will be less likely to be interacted with.
- Again, similar the SEIR ensemble models, we are aiming for an average total of ~7 daily contacts per person in normal circumstances.
    - As such, we have balanced the numbers below for an avg connectivity - or degree - of ~7 per node. 
    - We check this by printing the density and graph info.


```python
for n in G:
    freq_deg = (freq_cont.getSample() - 1)

    while G.degree(n) < freq_deg:
        a = (n + 1) / 3
        b = (len(G) - (n + 1)) / 3
        if b <= 0:
            b = 1
        ran_node = int(np.random.beta(a, b) * (len(G)))
        if ran_node < 1:
            ran_node = 1
        ran_weight = np.random.beta(2,5)
        if n != ran_node and G.degree(ran_node) < 16:
            G.add_edge(n, ran_node, weight=ran_weight)
            
    infreq_deg = (infreq_cont.getSample() - 1)

    while G.degree(n) < (freq_deg + infreq_deg):
        ran_node_2 = np.random.randint(len(G))
        ran_weight_2 = np.random.beta(4,2)
        if n != ran_node_2 and G.degree(ran_node) < 16:
            G.add_edge(n, ran_node_2, weight=ran_weight_2)
            

print(nx.density(G))

print(nx.info(G))
```

    0.006962962962962963
    Name: 
    Type: Graph
    Number of nodes: 1000
    Number of edges: 3478
    Average degree:   6.9560
    

We can then display and verify the first 10 edges (relationships).


```python
list(G.edges.data())[:10]
```




    [(0, 1, {'weight': 0.164194416949933}),
     (0, 9, {'weight': 0.46379306228017686}),
     (0, 2, {'weight': 0.2738317443159551}),
     (0, 3, {'weight': 0.16943974202637746}),
     (0, 5, {'weight': 0.20927612787563984}),
     (0, 4, {'weight': 0.39195943983679665}),
     (0, 6, {'weight': 0.45052075481997045}),
     (0, 7, {'weight': 0.43008603040857246}),
     (0, 984, {'weight': 0.6618673947130549}),
     (0, 83, {'weight': 0.21825381375073094})]



We can also plot a histogram of each node's degree, as well as see the bimodal shape of the weights, indicating the frequent vs infrequent contact regimes.


```python
wgt = [lis[2] for lis in list(G.edges.data('weight'))]

fig, (bx1, bx2) = plt.subplots(2, figsize=(10,8))
bx1.plot(nx.degree_histogram(G))
bx1.set_title('Node Degree Histogram')
bx2.hist(wgt, 20)
bx2.set_title('Relationship Edge Weights Histogram')
plt.tight_layout()
```


![png](output_25_0.png)


## The Simulation
After setting a few initial conditions, counters, and tally lists, we are ready to run the simulation!
- The simulation runs as long as there is at least one exposed or infectious person.
- Each simulated day, each person's state is checked and their current risk assessment is computed and a behavioral modifier updated given the current numbers of confirmed cases.
- If infectious, their type of illness is checked and their behavioral modifier updated.
    - This is done with the intuition that the sicker the person, the less likely they are to behave normally.
    - More severe and critical cases drastically limit contact, while moderate illness cuts contact behavior in half.
- Once behavior is set, each contact is checked for susceptibility, and if susceptible, we test if contact occurs.
    - If contact occurs, change state to exposed, and sample an incubation period.
- If the infectious person has reached their recovery day, they are checked to determine if they will recover or die from the illness, and the appropriate state is then updated.
- If the person is in the incubation period - a state of __'E'__ - the person is checked for the end of the incubation period.
    - If incubation is at an end, the person's state is changed to infectious.
    - Once determined to be infectious, the severity of the illness is calculated.
    - A recovery period is determined based on the type of illness.  
    
  
Finally, we tally and append the final statistics and update counters and markers and print out a suitable log to follow the simulation as it runs.


```python
test_c2i = c2i.getSample()
I_C = 0
IC_C = 0
tally_I = [0]
tally_IC = [0]
inf_hist = []
sim_day  = 2

while len(E) > 0 or len(I) > 0:
    S = []
    E = []
    I = []
    R = []
    D = []
    
    for n in G:
          
        test_state = nx.get_node_attributes(G,'state')[n]
        test_beh_max = nx.get_node_attributes(G,'beh_max')[n]
        beh_mod = behaviorModifier(IC_C, test_beh_max)

        if test_state == 'S':
            S.append(n)
        if test_state == 'R':
            R.append(n)
        if test_state == 'D':
            D.append(n)
         
        if test_state == 'I':
            I.append(n)
            test_I = G.nodes[n]['I_type']
            
            if test_I == 'I_crit' or test_I == 'I_crit_fat' or test_I == 'I_sev':
                beh_num = beh_mod * 0.25
            elif test_I == 'I_Mod':
                beh_num = beh_mod * 0.75
            else:
                beh_num = beh_mod

            for nn in G[n]:
                check_st = G.nodes[nn]['state']
                check_wgt = G[n][nn]['weight']
                # print(f'contact {nn} has state {check_st} and weight {check_wgt} and checking beh mod {beh_num}')
                if G.nodes[nn]['state'] == 'S' and G[n][nn]['weight'] < beh_num:
                    E_date = sim_day

                    inc_per = int(e2i.getSample())
                    if inc_per < 1:
                        inc_per = 1
                    I_date = sim_day + inc_per
                    
                    nx.set_edge_attributes(G, {(n, nn): {'Infection Path': str(n) + ' to ' + str(nn)}})
                    nx.set_node_attributes(G, {nn: {'state':'E', 
                                                    'E_date': E_date,
                                                   'I_date': I_date}})
            if G.nodes[n]['R_date'] == sim_day:
                if test_I == 'I_crit_fat':
                    nx.set_node_attributes(G, {n: {'state':'D'}})
                else:
                    nx.set_node_attributes(G, {n: {'state':'R'}})
            
        if test_state == 'E':
            
            E.append(n)
            
            if G.nodes[n]['I_date'] == sim_day:
                I_C += 1
                inf_per = int(i2r.getSample())
                if inf_per < 1:
                    inf_per = 1
                R_date = sim_day + inf_per

                i_test = np.random.random_sample()
                if i_test < i_asym:
                    I_type = 'I_asym'                   
                elif i_test < i_mild:
                    I_type = 'I_mild'
                elif i_test < i_mod:
                    I_type = 'I_mod'
                elif i_test < i_severe:
                    I_type = 'I_sev'
                    R_date = R_date + np.random.randint(1,8)
                elif i_test < i_critical:
                    I_type = 'I_crit'
                    R_date = R_date + np.random.randint(1,15)
                else:
                    I_type = 'I_crit_fat'
                    R_date = R_date + np.random.randint(1,15)
                
                nx.set_node_attributes(G, {n: {'state':'I',
                                                'R_date': R_date,
                                               'I_type': I_type}})
                
   
    print(f'Day: {sim_day}')                                   
    print('S', len(S))
    print('E', len(E))
    print('I', len(I))
    print('R', len(R))
    print('D', len(D))

    G.nodes.data('state')
    inf_hist.append([sim_day, len(I)])
    sim_day += 1
    IC_C = (I_C * test_c2i)
    tally_I.append(I_C)
    tally_IC.append(IC_C)
    
    print(f'Number of confirmed cases is {IC_C}')
    print('')
```

    Day: 2
    S 999
    E 1
    I 0
    R 0
    D 0
    Number of confirmed cases is 0.0
    
    Day: 3
    S 999
    E 1
    I 0
    R 0
    D 0
    Number of confirmed cases is 0.0
    
    ...
    
    Day: 65
    S 185
    E 0
    I 1
    R 814
    D 0
    Number of confirmed cases is 13.459486465805735
    
    Day: 66
    S 185
    E 0
    I 1
    R 814
    D 0
    Number of confirmed cases is 13.459486465805735
    
    Day: 67
    S 185
    E 0
    I 1
    R 814
    D 0
    Number of confirmed cases is 13.459486465805735
    
    Day: 68
    S 185
    E 0
    I 0
    R 815
    D 0
    Number of confirmed cases is 13.459486465805735
    
    

## Details in the Graph
Each node - _i.e. person_ - in the graph now possesses details from the simulation. These include:
- Final state
- Behavior Signal Max (Risk Level - lower is more risk adverse)
- Dates of exposure, infectiousness/illness, and recover or death
- The serverity of illness  
  
This can be seen by invoking the command below.


```python
list(G.nodes.data())[:3]
```




    [(0,
      {'entity': 'Person 0',
       'state': 'R',
       'beh_max': 13.276124248262928,
       'E_date': 23,
       'I_date': 29,
       'R_date': 34,
       'I_type': 'I_asym'}),
     (1,
      {'entity': 'Person 1',
       'state': 'R',
       'beh_max': 9.897497608529193,
       'E_date': 19,
       'I_date': 22,
       'R_date': 26,
       'I_type': 'I_mod'}),
     (2,
      {'entity': 'Person 2',
       'state': 'R',
       'beh_max': 2.6783071885987195,
       'E_date': 20,
       'I_date': 24,
       'R_date': 28,
       'I_type': 'I_mild'})]



## Edge Data including Disease Transmission
Similarly, the edge data now contains additional data:
- A record of infectious transmission now exists.  
  
This can be observed by printing the edge data, as seen below.


```python
list(G.edges.data())[:10]
```




    [(0, 1, {'weight': 0.164194416949933, 'Infection Path': '1 to 0'}),
     (0, 9, {'weight': 0.46379306228017686}),
     (0, 2, {'weight': 0.2738317443159551}),
     (0, 3, {'weight': 0.16943974202637746}),
     (0, 5, {'weight': 0.20927612787563984}),
     (0, 4, {'weight': 0.39195943983679665, 'Infection Path': '0 to 4'}),
     (0, 6, {'weight': 0.45052075481997045}),
     (0, 7, {'weight': 0.43008603040857246, 'Infection Path': '0 to 7'}),
     (0, 984, {'weight': 0.6618673947130549}),
     (0, 83, {'weight': 0.21825381375073094, 'Infection Path': '0 to 83'})]



## Other Important Statistics
We can also access and even print a number of important statitistics to the simulation.  

Below is a quick plot of the cumulative confirmed cases over the simulation period.


```python
plt.plot(tally_IC)
plt.show()
```


![png](output_33_0.png)


We have multiple ways to create lists or series of daily concurrent infectious from our log data. Below are two different methods and printed verifications of similar results.
- Note: the first creats a list, the second creates a tuple.


```python
inf_day = [lis[1] for lis in inf_hist]
inf_day_2 =  list(zip(*inf_hist))[1]
print(f"type 1 {inf_day}")
print(f"type 2 {inf_day_2}")
```

    type 1 [0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 2, 3, 5, 8, 11, 19, 31, 38, 53, 68, 82, 111, 156, 207, 226, 249, 269, 308, 334, 336, 336, 311, 304, 296, 273, 245, 228, 207, 179, 148, 126, 102, 88, 67, 54, 42, 29, 25, 22, 23, 17, 17, 16, 12, 10, 8, 7, 5, 5, 4, 4, 2, 2, 1, 1, 1, 0]
    type 2 (0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 2, 3, 5, 8, 11, 19, 31, 38, 53, 68, 82, 111, 156, 207, 226, 249, 269, 308, 334, 336, 336, 311, 304, 296, 273, 245, 228, 207, 179, 148, 126, 102, 88, 67, 54, 42, 29, 25, 22, 23, 17, 17, 16, 12, 10, 8, 7, 5, 5, 4, 4, 2, 2, 1, 1, 1, 0)
    

With either the list or tuple, a plot of the daily concurrent infectious can then be plotted alongside the cumulative infectious.


```python
plt.plot(inf_day)
plt.plot(tally_I)
plt.show()
```


![png](output_37_0.png)


## Exporting the Graph
The graph can be exported in a variety of formats. Below we save and export the file in the _graphml_ format.


```python
nx.write_graphml_lxml(G, 'test_graph_v5.0.graphml')
```

## Future Work
In later applications we will take this simulation further and explore:
- Graph plotting and visualizations
- Animating the spread of the disease throughout the population
- Created an ensemble of graph simulations to gain insight into the variability of results


```python

```
