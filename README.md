
# Monte Carlo Simulation





## Table of Content


**1. NSE - Monte-Carlo-Simulation**
 - NSE - Monte Carlo - Forecasting Stock Price - INFY.ipynb
 - NSE - Monte Carlo - Black-Scholes - Merton - INFY.ipynb
 - NSE - Monte Carlo - Euler Discretization - INFY.ipynb

**2. USA Stocks - Monte-Carlo-Simulation**
 - Monte Carlo - Forecasting Stock Price - MSFT.ipynb
 - Monte Carlo - Black-Scholes - Merton - MSFT.ipynb
 - Monte Carlo - Euler Discretization - MSFT.ipynb

## Project Description

**Monte-Carlo-Simulation:**
 

**1. Forecasting Stock Price formula:**
```bash

 daily_returns = np.exp(drift.values + stdev.values * norm.ppf(np.random.rand(t_intervals,iterations)))

```
![image](https://user-images.githubusercontent.com/128286364/231461101-f8e6db14-a85f-4666-97d9-ccb6e903852d.png)

```bash
for t in range(1,t_intervals):
    price_list[t] = price_list[t - 1] * daily_returns[t]

```

![image](https://user-images.githubusercontent.com/128286364/231461216-7ea3df3b-598b-4b2b-8067-93c33e258cc5.png)

**2. Monte Carlo - Black-Scholes - Merton formula:**

```bash
def d1(S, K, r, stdev,T):
    return (np.log(S/K) +  (r + stdev**2/2) * T)/(stdev * np.sqrt(T))

def d2(S, K, r, stdev,T):
    return (np.log(S/K) +  (r - stdev**2/2) * T)/(stdev * np.sqrt(T))
```
![image](https://user-images.githubusercontent.com/128286364/231461628-c0567df2-aa80-4989-9355-07b2839e7d06.png)

```bash
def BSM(S, K, r, stdev,T):
    return (S * norm.cdf(d1(S, K, r, stdev, T))) - (K * np.exp(-r * T) * norm.cdf(d2(S, K, r, stdev, T)))
```
![image](https://user-images.githubusercontent.com/128286364/231461738-a974db62-5ad7-495c-9446-1e9c99e00901.png)


**3. Monte Carlo - Euler Discretization formula:**

```bash
Z = np.random.standard_normal((t_intervals + 1, iterations))
S = np.zeros_like(Z)
S0 = sec_data.iloc[-1]
S[0] = S0
```
![image](https://user-images.githubusercontent.com/128286364/231462303-2680b77e-6b08-4951-bc89-49a97f6c6bde.png)


```bash
for t in range(1, t_intervals + 1):
    S[t] = S[t-1] * np.exp((r-0.5*stdev**2)*delta_t+stdev*delta_t**0.5*Z[t])
```
![image](https://user-images.githubusercontent.com/128286364/231462070-1fdd7573-54fc-44a8-baee-bccdabe9b425.png)


## Installation

To install iexfinance:

url: <https://pypi.org/project/iexfinance/>

url: <https://iexcloud.io/>
```bash
pip install iexfinance
```
To install NSEpy:

url: <https://nsepy.xyz/>
```bash
pip install nsepy
```
## Deployment

To deploy this project run

```bash
  import numpy as np
  import pandas as pd
  import matplotlib.pyplot as plt
  from datetime import datetime
  from pandas_datareader import data as wb
```

```bash
  from iexfinance.stocks import Stock, get_historical_data

  start = datetime(2018, 1, 1)
  end = datetime(2023, 3, 23)

  api_key = 'API_KEY'
```

Creating a portfolio:
```bash
tickers = ['Stocks']
mydata = pd.DataFrame()
for t in tickers:
    mydata[t] = get_historical_data(t, start, end, output_format = 'pandas', token=api_key)['close']
```
