

```python
from scipy.stats import beta
import matplotlib.pyplot as plt
import math
import numpy as np
import random
import seaborn as sns
import pandas as pd

sns.set()

master_dict = {}
master_dict = {'test_period': 'Test Period','test_S': 'Susceptible Population', 'test_E': 'Exposed Population', 'test_NE': 'Newly Exposed', 
'test_I': 'Infectious Population', 'test_NI': 'Newly infectious', 'test_NI_C': 'Total infectious', 'test_IC': 'Daily confirmed infections',
'test_IC_H': 'Daily hospitalized', 'test_IC_No_H': 'Daily Confirmed, Not Hospitalized', 'test_IU': 'Daily Uncomfirmed Infected', 
'test_IC_C': 'Cumulative confirmed infections', 'test_R': 'Recovered Population', 'test_NR': 'Newly Recovered', 'test_D': 'Dead Population',
'test_ND': 'Newly Dead', 'test_D_C': 'Cumulative Dead'}


#conf_perc = 444 / 10_000_000
#print(conf_perc)
print(master_dict.get('test_I'))

N = 10_000 # population size
S = 0 # susceptible
E = 0 # exposed
I = 0 # infectious
H = C_H = 0 # hospitalizations, confirmed and hospitalized
C = 250 # confirmed case
C_NH = 0 # confirmed not in hospital
U = 0 # unconfirmed case
R = 0 # recovering
D = 0 # dead
S_R = 0 # recovered but susceptible again

C = H + C_NH
I = C + U

h2i = .0045 # H1N1 ratio for hospitalized to infected
h2i_max = .012
h2i_min = .0016

c2i = 1 / 79 # H1N1 ratio for confirmed cases to estimated total infected
c2i_min = 1 / 148
c2i_max = 1 / 47

# person-to-person spread: primary means of propagation https://www.cdc.gov/coronavirus/2019-ncov/prepare/transmission.html?CDC_AA_refVal=https%3A%2F%2Fwww.cdc.gov%2Fcoronavirus%2F2019-ncov%2Fabout%2Ftransmission.html
rep_contact = 4
rep_contact_std = 2
new_contact = 2
new_contact_std = 1

E_dt_mean = 5.1 # length of incubation period
E_dt_max = 11.5 # max CI value of 15.6
E_dt_min = 2.5 # min CI value of 1.9

i_mild = .51 # mild infection rate
i_mod = .388 # mod inf rate
i_severe = .052 # severe inf rate
i_critical = .006 # critical rate
i_asym = .044 # asymptomatic rate

# spread mostly likely during infectious period, unlikely once recovery begins: https://www.statnews.com/2020/03/09/people-shed-high-levels-of-coronavirus-study-finds-but-most-are-likely-not-infectious-after-recovery-begins/
i_rec_mean = 7 # infectious period, time to begining recovery after exposure to infectious transition
i_rec_max = 12
i_rec_min = 4

f_rate_mean = .015 # (.009 default) case fatality rate, https://wwwnc.cdc.gov/eid/article/26/6/20-0320_article
f_rate_min = .0025 # max CFR (.0025)
f_rate_max = .03 # max CFR (.03 default)

C = 395
quar_num = 500 # number of confirmed cases to trigger quarantine

def dangerPerception(dp_c, dp_q):
    #print(dp_c/dp_q)
    if (dp_c/dp_q) <= 0.05:
        return .05
    elif (dp_c/dp_q) <= 0.95:
        return dp_c / dp_q
    else:
        return 0.95

#dang_perc = dangerPerception(C, quar_num)
#print(dang_perc)


def behaviorModifier(bm_dp):
    beta_a = 10 - (10 * bm_dp)
    beta_b = 10 - beta_a
    #print(beta_a, beta_b)
    return np.random.beta(beta_a, beta_b)

#beh_mod = behaviorModifier(dang_perc)
#print(beh_mod)


def calc_stdv(cs_mean, cs_min, cs_max):
    cs_avg = ((cs_mean - cs_min) + (cs_max - cs_mean)) / 2
    return cs_avg / 1.65

i_rec_stdv = calc_stdv(i_rec_mean, i_rec_min, i_rec_max)
#print(i_rec_stdv)

e_dt_stdv = calc_stdv(E_dt_mean, E_dt_min, E_dt_max)
#print(e_dt_stdv)


def offset_normal(m, a, b, r):
    a_sd = (m - a) / 1.69
    b_sd = (b - m) / 1.69
    o_n = []
    for x in range(r):
        i = np.random.uniform(a, b)
        if i < m:
            av = np.random.normal(m, a_sd)
            if av > m:
                av = m - (av - m)
            if av < 0:
                av = 0
            o_n.append(av)
        if i >= m:
            bv = np.random.normal(m, b_sd)
            if bv < m:
                bv = m + (m - bv)
            o_n.append(bv)
    return o_n

def norm_norm(m, s, r):
    n_n = []
    for x in range(r):
        i = np.random.normal(m, s)
        if i < 0:
            i = 0
        n_n.append(i)
    return n_n

infectious_period_offset = offset_normal(i_rec_mean, i_rec_min, i_rec_max, N)
# plt.hist(infectious_period_offset, 50)
# plt.show()

incubation_period_offset = offset_normal(E_dt_mean, E_dt_min, E_dt_max, N)
# plt.hist(incubation_period_offset, 50)
# plt.show()

h2i_offset = offset_normal(h2i, h2i_min, h2i_max, N)
# plt.hist(h2i_offset, 50)
# plt.show()

r_contact_norm = norm_norm(rep_contact, rep_contact_std, N)
# plt.hist(r_contact_norm, 50)
# plt.show()

n_contact_norm = norm_norm(new_contact, new_contact_std, N)
# plt.hist(n_contact_norm, 50)
# plt.show()

c2i_offset = offset_normal(c2i, c2i_min, c2i_max, N)
# plt.hist(c2i_offset, 50)
# plt.show()

f_rate_offset = offset_normal(f_rate_mean, f_rate_min, f_rate_max, N)


# Running the main ensemble test here:

quar_num_test = 10
big_S = []

for num in range(1_000):

    test_period = 180 # days in test period
    test_S = [N] # total susceptible
    test_E = [1] # total exposed
    test_NE = [0] # new exposed
    test_I = [0] # total infectious
    test_NI = [0] # new infectious
    test_NI_C = [0] # total infectious
    test_IC = [0] # confirmed infections
    test_IC_H, test_IC_No_H, test_IU = [0], [0], [0]
    test_IC_C = [0] # cumulative confirmed infections
    test_R = [0] # total recovered
    test_NR = [0] # new recovered
    test_D = [0] # total dead
    test_ND = [0] # new dead
    test_D_C = [0] # cumulative dead

    inf_per = random.sample(infectious_period_offset, 1)[0]
    if inf_per < 1:
        inf_per = 1
    inc_per = random.sample(incubation_period_offset, 1)[0]
    if inc_per < 1:
        inc_per = 1
    h2i_test = random.sample(h2i_offset, 1)[0]
    c2i_test = random.sample(c2i_offset, 1)[0]
    r_cont_test = random.sample(r_contact_norm, 1)[0]
    n_cont_test = random.sample(n_contact_norm, 1)[0]
    f_rate_test = random.sample(f_rate_offset, 1)[0]

    rec_rate = 1 / inf_per # recovery rate, conversion rate from infectious to recovering
    lat_rate = 1 / inc_per # latent rate, conversion rate from exposed to infectious
    f_rate_rate = f_rate_test / inf_per # case fatality rate *per day* of infectiousness

    for day in range(test_period):
        
        today = day + 1
        yesterday = day

        cur_sus = test_S[yesterday] # today's number of currently susceptible - the population that has not been exposed yet
        confirmed_cases = test_IC_C[yesterday] # confirmed cases based on the the H1N1 study proportions of infectious to confirmed

        dang_per_test = dangerPerception(confirmed_cases, quar_num_test) # testing for danger perception given the number of confirmed cases and max risk or quarantine number
        beh_mod_test = behaviorModifier(dang_per_test) # behavioral modification multiplier given the danger/risk perception

        new_NE = (beh_mod_test * r_cont_test * test_NI[yesterday]) + (beh_mod_test * n_cont_test * test_NI[yesterday]) # personal/close contacts and exposures for the newly infectious
        
        not_new_I = test_I[yesterday] - test_NI[yesterday] - test_IC_H[yesterday]
        if not_new_I < 0:
            not_new_I = 0
        not_new_NE = beh_mod_test * n_cont_test * not_new_I # continued personal/close contacts with non-repeat persons for the infectious at date of infectious > 1
        
        next_NE = new_NE + not_new_NE # new exposed population today
        if next_NE >= cur_sus:
            next_NE = test_S[yesterday]

        next_NI = test_E[yesterday] * lat_rate # new infectious population today
        next_NI_C = test_NI_C[yesterday] + next_NI # cumulative infectous population

        next_E = test_E[yesterday] + next_NE - next_NI # total exposed -> adds new exposures, loses new infectious
        if next_E < 0:
            next_E = 0
        
        next_IC = c2i_test * test_I[yesterday] # current confirmed infectious based on H1N1 ratios and estimated total infectious
        new_IC = next_IC - test_IC[yesterday]
        if new_IC < 0:
            new_IC = 0

        next_IC_C = test_IC_C[yesterday] + new_IC # cumulative confirmed infectious
        
        next_IC_H = h2i_test * test_I[yesterday] # current hospitalized infectious based on H1N1 ratios and estimated total infectious

        next_NR = test_I[yesterday] * rec_rate # new recoveries today
        next_R = test_R[yesterday] + next_NR # cumulative recovery rate

        next_D = test_IC[yesterday] * f_rate_rate
        next_ND = next_D - test_D[yesterday]
        if next_ND < 0:
            next_ND = 0

        next_D_C = test_D_C[yesterday] + next_D

        next_I = test_I[yesterday] + next_NI - next_NR - next_ND
        if next_I < 0:
            next_I = 0
        
        next_S = N - next_E - next_I - next_R - next_D
        if next_S < 0:
            next_S = 0

        test_S.append(next_S)
        test_E.append(next_E)
        test_NI.append(next_NI)
        test_NI_C.append(next_NI_C)
        test_I.append(next_I)
        test_NR.append(next_NR)
        test_R.append(next_R)
        test_ND.append(next_ND)
        test_D.append(next_D)
        test_D_C.append(next_D_C)
        test_IC.append(next_IC)
        test_IC_H.append(next_IC_H)
        test_IC_C.append(next_IC_C)

    # if len(big_S) > 0:
    #     big_S = np.vstack((big_S, test_IC))
    # else:
    #     big_S = test_IC

    test_num = num
    test_name = "Test #" + str(num)
    test_1 = test_I
    test_2 = test_D
    try: df
    except NameError: df = None
    if df is None:
        df = pd.DataFrame({test_name: test_1})
    else:
        df_new = pd.DataFrame({test_name: test_1})
        df = pd.concat([df, df_new], axis=1)

    try: df2
    except NameError: df2 = None
    if df2 is None:
        df2 = pd.DataFrame({test_name: test_2})
    else:
        df_new2 = pd.DataFrame({test_name: test_2})
        df2 = pd.concat([df2, df_new2], axis=1)

# big_array = np.stack([test_S, test_E, test_I, test_IC, test_IC_H, test_R, test_D]).T
# plt.plot(big_array)
# plt.legend(['Sus', 'Exp', 'Inf', 'Conf', 'Hosp', 'Rec', 'Dead'])
# plt.xlabel('Days')
# plt.show()

lombard_conf_new = [0, 0, 15, 40, 57, 61,67,65,98,128,84,369,270,266,300,431,361,808,769,1280,322,1489,1445,1095,1865,1587,1377,1571,1493,2171, 2380, 3251, 1691, 1555, 1942, 1643, 2543, 2409]
hubei_conf = [0, 0, 0, 0, 0, 444,444,549,761,1058,1423,3554,3554,4903,5806,7153,11177,13522,16678,19665,22112,24953,27100,29631,31728,33366,33366,48206,54406,56249,58182,59989,61682,62031,62442,62662,64084,64084,64287,64786,65187,65596,65914,66337,66907,67103,67217,67332,67466,67592,67666,67707,67743,67760,67773,67781,67786,67790,67794,67798,67799,67800,67800]
ny_conf = [1, 1,2,2,4,5,12,14,20,37,52,96,155,269,330,464,645,1339,2468,4408,6211,9045,12305,14905,20011,23112,25399]


hubei_fat = [0, 0, 0, 0, 0, 0, 0, 0, 0, 17,17,24,40,52,76,125,125,162,204,249,350,414,479,549,618,699,780,871,974,1068,1068,1310,1457,1596,1696,1789,1921,2029,2144,2144,2346,2346,2495,2563,2615,2641,2682,2727,2761,2803,2835,2871,2902,2931,2959,2986,3008,3024,3046,3056,3062,3075,3085,3099,3111,3122,3130]
lombard_fat = [0, 0, 0, 1, 1, 4, 2, 1, 5, 3, 6, 1, 14, 17, 18, 25, 37, 19, 113, 66, 135, 149, 127, 146, 76, 252, 202, 220, 319, 209, 381, 546, 361, 320, 402, 296, 387, 541]
ny_deaths = [0, 0, 0,0,0,0,0,0,0,0,0,0,0,0,1,5,7,10,20,22,43,60,99,131,192,280,365,450]

lombard_conf = np.cumsum(lombard_conf_new) # Lombardi region only (pop 10m) - population density probably doesn't work for calc entire countries
lombard_cum = np.cumsum(lombard_fat)
italy_norm = [i/1000 for i in lombard_conf] # Lombardi region only
hubei_norm = [i/1100 for i in hubei_conf]
ny_norm = [i/1880 for i in ny_conf]

hubei_fat_norm = [i/1100 for i in hubei_fat]
lombard_fat_norm = [i/1000 for i in lombard_cum]
ny_deaths_norm = [i/1880 for i in ny_deaths]


print(hubei_fat_norm)


df.plot(alpha=0.3, legend=False).set(title = f'COVID-19 per 10k Population - 1k Model Runs', xlabel='Day', ylabel='Per 10k Population')
plt.show()

df_mean = df.mean(axis = 1)
df_10 = df.quantile(.1, axis=1)
df_90 = df.quantile(.9, axis=1)

df2_mean = df2.mean(axis = 1)

df_mean.plot()
df_10.plot()
df_90.plot()
plt.show()


sns.lineplot(data=df_mean, label='Model 1').set(title = 'COVID-19 Models per 10,000 Simulated', xlabel = 'Day', ylabel = 'Per 10,000')
df_90.plot(label='90 percentile')
df_10.plot(label='10 percentile')
# plt.plot(hubei_norm, label='Hubei')
# plt.plot(lombard_fat_norm, label='Lombardy (ITA)')
plt.plot(ny_deaths_norm, label='NYC Confirmed Cases')
#sns.lineplot(data=df2_mean, label='Model 2')
# plt.plot(ny_norm, label='New York')
# plt.plot(italy_norm, label='Lombardi (ITA)')
# legend = plt.legend()
# legend.get_texts()[0].set_text('Hubei')
plt.legend()
plt.show()

# plt.plot(big_S_stack.T)
# plt.show()

df_mean.to_csv('test_df_1.csv')
```
