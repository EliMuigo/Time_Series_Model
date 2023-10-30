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

- ### Creating a time series chart
Create a function that is that takes posting_date as the argument.

The if condition checks if posting_date is timezone-aware and if it is not it converts it to a timezone datatime object by setting the timezone to UTC using 'pytz.utc'.

The size() is used to count the number of entries in each group, effectively counting in the number of records with the same combination of 'region','type' and 'posting_date'.

~~~

def convert_tz_aware(posting_date):
    if not posting_date.tzinfo:
        return posting_date.replace(tzinfo=pytz.utc)
    else:
        return posting_date

dataset['posting_date'] = dataset['posting_date'].apply(convert_tz_aware)

dataset_new = dataset.groupby([ 'type','region', 'posting_date']).size().reset_index(name='count')

dataset_new = dataset_new.sort_values(by='posting_date')
~~~

### Plotting the time series 
Use the plotly library
~~~
import plotly.express as px
~~~
Define the x-axis as posting_date, the y-axis as the count and color as region.
~~~

# Create a time-series chart
fig = px.line(dataset_new, x='posting_date', y='count', color='region', line_group='type',
              title='Number of Vehicles Over Time by Type and Region',
              labels={'count': 'Number of Vehicles'},
               color_discrete_sequence=px.colors.qualitative.Set1)  # Change the color scale)

# Customize the layout
fig.update_layout(
    xaxis_title='Posting Date',
    yaxis_title='Number of Vehicles',
    showlegend=True,
)

fig.show()
~~~
### Time Series Chart

[Time Series Chart]![Time Series Chart](<Screenshot 2023-10-30 212502-1.png>))














### <b>NOTE BETTER</b>
The changing of the datetime is a bit of a challenge since creating a time series chart you need a Dataseries instead of a DataFrame. When creating the time series chart you have to run the date to datetime code constantly.