### <b>Time Series Chart</b>
The goal was to come up with a time series chart , cleaning the data and explore using different visualizations.

- Started by importing libraries 
~~~
import numpy as np # linear algebra

import pandas as pd

import warnings

import matplotlib.pyplot as plt

%matplotlib inline 

warnings.filterwarnings('ignore', category=FutureWarning)

import seaborn as sns

from statsmodels.graphics.tsaplots import plot_acf,plot_pacf

from statsmodels.tsa.arima_model import ARIMA
~~~

- Loading the dataset
~~~
dataset=pd.read_csv('/kaggle/input/craigslist-vehicles/craigslist_vehicles.csv')
~~~

- Converting the 'posting_date' column to datetime 
~~~
# Convert 'posting_date' column to datetime
dataset['posting_date'] = pd.to_datetime(dataset['posting_date'])
~~~

- Dropped the columns that were not useful.

- Cleaned the data by removing the null/Nan values.

-