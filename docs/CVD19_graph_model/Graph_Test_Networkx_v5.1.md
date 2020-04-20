---
layout: default
title: Graph-Based Network SEIR Simulation
parent: CVD19 Graph Network Model
nav_order: 2
---

# Modeling an Epidemic with Graph Theory and Network Simulations
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

## Taking advantage of graph theory and node properties by establishing _personalities_
Unlike in our statistically calculated SEIR ensemble models - in which the behavior of the population was averaged - graphs allow us to provide each person (represented as a node in our graph/network) with a "personality" - or more specifically a behavioral predisposition towards risk.
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
    


![png](/modeling-uncertainty/assets/images/graph_1a.png)


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


![png](/modeling-uncertainty/assets/images/graph_1b.png)


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


![png](/modeling-uncertainty/assets/images/graph_1c.png)


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


![png](/modeling-uncertainty/assets/images/graph_1d.png)


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
