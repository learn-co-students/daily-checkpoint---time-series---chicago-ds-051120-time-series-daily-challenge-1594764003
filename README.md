## Time Series

<!---Create stock_df and save as .pkl
stocks_df = pd.read_csv("raw_data/all_stocks_5yr.csv")
stocks_df["clean_date"] = pd.to_datetime(stocks_df["date"], format="%Y-%m-%d")
stocks_df.drop(["date", "clean_date", "volume", "Name"], axis=1, inplace=True)
stocks_df.rename(columns={"string_date": "date"}, inplace=True)
pickle.dump(stocks_df, open("write_data/all_stocks_5yr.pkl", "wb"))
--->


```python
import pickle
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np

from pandas.plotting import register_matplotlib_converters
register_matplotlib_converters()
```


```python
stocks_df = pickle.load(open("write_data/all_stocks_5yr.pkl", "rb"))
stocks_df.head()
```

### 1. Transform the `date` feature so that it becomes a `datetime` object that contains the following format: YYYY-MM-DD and set `date` to be the index of `stocks_df`.


```python
# Your code here
```

### 2. Perform monthly downsampling on `stocks_df` that takes the mean of the `open`, `high`, `low`, and `close` features on a monthly basis. Store the results in `stocks_monthly_df`.

> Hint: `stocks_monthly_df` should have 61 rows and 4 columns after you perform downsampling.


```python
# Your code here
```


```python
stocks_monthly_df.shape
```

### 3. Create a line graph that visualizes the monthly open stock prices from `stocks_monthly_df` for the purposes of identifying if average monthly open stock price is stationary or not using the rolling mean and rolling standard deviation.

> Hint: 
> * store your sliced version of `stocks_monthly_df` in a new variable called `open_monthly_series`;
> * use a window size of 3 to represent one quarter of time in a year


```python
# Your code here

open_monthly_series = None

rolmean = None
rolstd = None

# note: do not rename the variables otherwise the plot code will not work
```


```python
fig, ax = plt.subplots(figsize=(13, 10))
ax.plot(open_monthly_series, color="blue",label="Average monthly opening stock price")
ax.plot(rolmean, color="red", label="Rolling quarterly mean")
ax.plot(rolstd, color="black", label="Rolling quarterly std. deviation")
ax.set_ylim(0, 120)
ax.legend()
fig.suptitle("Average monthly open stock prices, Feb. 2013 to Feb. 2018")
fig.tight_layout()
```

Based on your visual inspection of the graph, is the monthly open stock price stationary?


```python
# Your written answer here
```

### 4. Use the Dickey-Fuller Test to identify if `open_monthly_series` is stationary


```python
# Your code here
```

Does this confirm your answer from Question 3? Explain why the time series is stationary or not based on the output from the Dickey-Fuller Test.


```python
# Your answer here
```

### 5. Looking at the decomposition of the time series in `open_monthly_series`, it looks like the peaks are the same value. To confirm or deny this, create a function that returns a dictionary where each key is a year and each value is the maximum value from the `seasonal` object for a given year.


```python
from statsmodels.tsa.seasonal import seasonal_decompose
decomposition = seasonal_decompose(np.log(open_monthly_series))

# Gather the trend, seasonality and noise of decomposed object
seasonal = decomposition.seasonal

# Plot gathered statistics
plt.figure(figsize=(13, 10))
plt.plot(seasonal,label='Seasonality', color="blue")
plt.title("Seasonality of average monthly open stock prices, Feb. 2013 to Feb. 2018")
plt.ylabel("Average monthly open stock prices")
plt.tight_layout()
plt.show()
```


```python
def calc_yearly_max(seasonal_series):
    """Returns the max seasonal value for each year"""
    # Your code here
```


```python
calc_yearly_max(seasonal)
```


