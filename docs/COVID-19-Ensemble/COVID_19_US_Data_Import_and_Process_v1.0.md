---
layout: default
title: US COVID-19 Data Import and Processing Application
parent: COVID-19 SEIR Ensemble with Behavioral Forcing
nav_order: 5
---

# US COVID-19 Data Import and Processing Application


```python
import numpy as np
import pandas as pd
from datetime import datetime, timedelta
from sklearn.metrics import mean_squared_error
import pickle
```


```python
def load_data(filename):
    infile = open(filename, 'rb')
    return pickle.load(infile)

def save_data(filename, data):
    outfile = open(filename, 'wb')
    pickle.dump(data, outfile)
    outfile.close()
```


```python
stats_dict = load_data('stats_dict')
properties_dict = load_data('properties_dict')
```


```python
rw_data_df = pd.read_csv('https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv', parse_dates=['date'])
pop_data_df = pd.read_csv('http://www2.census.gov/programs-surveys/popest/datasets/2010-2019/national/totals/nst-est2019-alldata.csv?#', usecols=['NAME', 'POPESTIMATE2019'])
rw_data_df = pd.merge(rw_data_df, pop_data_df, how='left', left_on='state', right_on='NAME')
```


```python
rw_data_df['norm_IC'] = rw_data_df['cases'] / rw_data_df['POPESTIMATE2019'] * 10_000
rw_data_df['norm_D'] = rw_data_df['deaths'] / rw_data_df['POPESTIMATE2019'] * 10_000
```


```python
df_date = rw_data_df[rw_data_df['date'] == datetime.strftime(datetime.now() - timedelta(2), '%Y-%m-%d')]
```


```python
state_list = list(df_date.sort_values(by='norm_IC', ascending=False)['state'])[:52]
```


```python
save_data('state_list', state_list)
```


```python
filt_data_df = rw_data_df[rw_data_df['state'].isin(state_list)]
filt_data_df = filt_data_df[filt_data_df['date'] >= '2020-02-01']
filt_data_df = filt_data_df.pivot(index='date', columns='state', values='norm_IC')
filt_data_df = filt_data_df.reset_index()
filt_data_df = filt_data_df.reset_index(drop=True)
filt_data_df = filt_data_df.drop(columns='date')
filt_data_df = filt_data_df.fillna(value=0)
us_IC_df = filt_data_df
```


```python
filt_data_df = rw_data_df[rw_data_df['state'].isin(state_list)]
filt_data_df = filt_data_df[filt_data_df['date'] >= '2020-02-01']
filt_data_df = filt_data_df.pivot(index='date', columns='state', values='norm_D')
filt_data_df = filt_data_df.reset_index()
filt_data_df = filt_data_df.reset_index(drop=True)
filt_data_df = filt_data_df.drop(columns='date')
filt_data_df = filt_data_df.fillna(value=0)
us_D_df = filt_data_df
```


```python
def sync_data(state_list, result_type, stats_dict, stats_df):

    state_err = {}

    for state in state_list:
        #test = list(us_IC_df[us_IC_df[state] > 0][state])
        test = list(stats_df[state])
        test_len = len(test)
        lowest_err = {}
        ref_err = {}

        for conf_trig in stats_dict[result_type]:
            check_rms = None
            test_model_col = test
            test_mean_refa = list(stats_dict[result_type][conf_trig]['mean'])
            test_mean_ref = list(np.zeros(60))
            for i in range(len(test_mean_refa)):
                test_mean_ref.append(test_mean_refa[i])
            for x in range(len(test_mean_ref)-test_len):
                xx = x + test_len
                test_mean_col = test_mean_ref[x:xx]
                test_rms = np.sqrt(mean_squared_error(test_model_col, test_mean_col))
                if check_rms == None or test_rms < check_rms:
                    check_rms = test_rms
                    check_col = test_mean_col
                    check_start = x
            lowest_err[conf_trig] = {'mean': check_col, 'real': test_model_col, 'mean long': test_mean_ref[check_start:]}
        state_err[state] = lowest_err
    
    return state_err
```


```python
state_err_IC = sync_data(state_list, 'IC', stats_dict, us_IC_df)
```


```python
save_data('state_err_IC', state_err_IC)
```


```python
state_err_D = sync_data(state_list, 'D', stats_dict, us_D_df)
```


```python
save_data('state_err_D', state_err_D)
```
