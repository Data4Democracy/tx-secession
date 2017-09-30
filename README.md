# TX Secession
Exploration of Texas secession conversation on Twitter

### Getting started
Here's a quick demo of loading the tweets into a pandas dataframe for exploratory analysis. Pro tip: try this out in our example [jupyter notebook]()

### To actually run this code...
First setup your environment. 

```
pip install -r requirements.txt
```

You'd probably do that in an Anaconda or virtual environment, but you don't have to. Now you should be able to poke around the dataset using pandas.

```python
%matplotlib inline
import matplotlib.pyplot as plt
import pandas as pd

# Get the tweets
df = pd.read_csv('data/tweets.csv')

# Check out the column headers
print(df.columns)

# Count tweets by date. 

# First convert datetime strings to datetime objects
df['created_at_tweet_dt'] = pd.to_datetime(df['created_at_tweet'],errors='coerce')

# Set that Series of datetime objects as your index
df_idx = df.set_index(pd.DatetimeIndex(df['created_at_tweet_dt']))

# Group by day
grouper = pd.TimeGrouper(freq='D')
grouped = df_idx.groupby(grouper)
df_grouped_by_date = grouped.size().reset_index()

# Name the columns something easier to read
df_grouped_by_date.columns = ['date','count']

# See what it looks like
df_grouped_by_date.plot()