# 6 Powerful Feature Engineering Techniques For Time Series Data (using Python)

Author: Aishwarya Singh

Date: Dec. 9, 2019

[Origin](https://www.analyticsvidhya.com/blog/2019/12/6-powerful-feature-engineering-techniques-time-series/)

## Overview

+ Feature engineering: a skill every data scientist should know how to perform, especially in the case of time series
+ 6 powerful feature engineering techniques for time series in this article
+ feature engineering technique w/ Python


## Introduction

+ a lot of nuance to time series data to consider when working with datasets that are time-sensitive

+ feature engineering for time series: the potential to transform time series model from just a good one to a powerful forecasting model


## Quick Introduction to Time Series

+ In a time series, the data is captured at equal intervals and each successive data point in the series depends on its past values.

+ Examples:
  + predicting stock price at a certain company
  + predicting the traffic on a website

+ time series data may also have certain trends or seasonality


## Setting up the Problem Statement for Time Series Data

+ Problem
  + historical data for ‘JetRail’, a form of public rail transport, that uses advanced technology to run rails at a high speed
  + to forecast the traffic on JetRail for the next 7 months based on past data
  + detailed problem statement and the dataset: [download](https://datahack.analyticsvidhya.com/contest/practice-problem-time-series-2/?utm_source=blog&utm_medium=6-powerful-feature-engineering-techniques-time-series)

+ Loading data

  ```python
  import pandas as pd
  data = pd.read_csv('Train_SU63ISt.csv')
  data.dtypes
  ```

+ Convert categorical variable into a DateTime variable

  ```python
  import pandas as pd
  data = pd.read_csv('Train_SU63ISt.csv')
  data['Datetime'] = pd.to_datetime(data['Datetime'],format='%d-%m-%Y %H:%M')
  data.dtypes
  ```


## Date-Related Features

+ the sales pattern for weekdays and weekends based on historical data

+ forecast the count of people who will take the JetRail on an hourly basis for the next 7 months

+ important factor: the day of the week (weekday or weekend) or month

  ```python
  import pandas as pd
  data = pd.read_csv('Train_SU63ISt.csv')
  data['Datetime'] = pd.to_datetime(data['Datetime'],format='%d-%m-%Y %H:%M')

  data['year']=data['Datetime'].dt.year 
  data['month']=data['Datetime'].dt.month 
  data['day']=data['Datetime'].dt.day

  data['dayofweek_num']=data['Datetime'].dt.dayofweek  
  data['dayofweek_name']=data['Datetime'].dt.weekday_name

  data.head()
  ```

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://www.analyticsvidhya.com/blog/2019/12/6-powerful-feature-engineering-techniques-time-series/" ismap target="_blank">
      <img src="https://s3-ap-south-1.amazonaws.com/av-blog-media/wp-content/uploads/2019/11/fets1.png" style="margin: 0.1em;" alt="Extracting these features" title="Extracting these features" width=450>
    </a>
  </div>


## Time-Related Features

+ extract more granular features if we have the time stamp

+ more insightful conclusions about the data
  + extract the ‘hour’ feature from the time stamp
  + determine the average hourly traffic throughout the week

+ converting the column to DateTime format and use the .dt accessor

  ```python
  import pandas as pd
  data = pd.read_csv('Train_SU63ISt.csv')
  data['Datetime'] = pd.to_datetime(data['Datetime'],format='%d-%m-%Y %H:%M')

  data['Hour'] = data['Datetime'].dt.hour
  data['minute'] = data['Datetime'].dt.minute

  data.head()
  ```

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://www.analyticsvidhya.com/blog/2019/12/6-powerful-feature-engineering-techniques-time-series/" ismap target="_blank">
      <img src="https://s3-ap-south-1.amazonaws.com/av-blog-media/wp-content/uploads/2019/11/fets2.png" style="margin: 0.1em;" alt="Extracting Time-Related Features" title="Extracting Time-Related Features" width=250>
    </a>
  </div>

+ Complete list of features able to generate

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://www.analyticsvidhya.com/blog/2019/12/6-powerful-feature-engineering-techniques-time-series/" ismap target="_blank">
      <img src="https://s3-ap-south-1.amazonaws.com/av-blog-media/wp-content/uploads/2019/11/time-features.png" style="margin: 0.1em;" alt="List of time-related features" title="List of time-related features" width=650>
    </a>
  </div>

  + example code for these features

    ```python
    # Time Based Features

    # importing required libraries
    import pandas as pd
    data = pd.read_csv('Train_SU63ISt.csv')
    data['Datetime'] = pd.to_datetime(data['Datetime'],format='%d-%m-%Y %H:%M')

    # day
    data['day']=data['Datetime'].dt.day
    # hour
    data['Hour'] = data['Datetime'].dt.hour

    print(data.head())
    ```


## Lag Features

+ the value at time $t$ is greatly affected by the value at time $t-1$

  ```python
  import pandas as pd
  data = pd.read_csv('Train_SU63ISt.csv')
  data['Datetime'] = pd.to_datetime(data['Datetime'],format='%d-%m-%Y %H:%M')

  data['lag_1'] = data['Count'].shift(1)
  data = data[['Datetime', 'lag_1', 'Count']]
  data.head()
  ```

+ The lag value we choose will depend on the correlation of individual values with its past values.

+ assign appropriate weights (or coefficients) to the lag features:

  ```python
  import pandas as pd
  data = pd.read_csv('Train_SU63ISt.csv')
  data['Datetime'] = pd.to_datetime(data['Datetime'],format='%d-%m-%Y %H:%M')

  data['lag_1'] = data['Count'].shift(1)
  data['lag_2'] = data['Count'].shift(2)
  data['lag_3'] = data['Count'].shift(3)
  data['lag_4'] = data['Count'].shift(4)
  data['lag_5'] = data['Count'].shift(5)
  data['lag_6'] = data['Count'].shift(6)
  data['lag_7'] = data['Count'].shift(7)

  data = data[['Datetime', 'lag_1', 'lag_2', 'lag_3', 'lag_4', 'lag_5', 'lag_6', 'lag_7', 'Count']]
  data.head(10)
  ```

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://www.analyticsvidhya.com/blog/2019/12/6-powerful-feature-engineering-techniques-time-series/" ismap target="_blank">
      <img src="https://s3-ap-south-1.amazonaws.com/av-blog-media/wp-content/uploads/2019/11/fests4-300x186.png" style="margin: 0.1em;" alt="List of time-related features" title="List of time-related features" width=300>
    </a>
  </div>

+ Correlation about the lag
  + using the ACF (Autocorrelation Function) and PACF (Partial Autocorrelation Function) plots
    + __ACF__: The ACF plot is a measure of the correlation between the time series and the lagged version of itself
    + __PACF__: The PACF plot is a measure of the correlation between the time series with a lagged version of itself but after eliminating the variations already explained by the intervening comparisons
  + example for the ACF and PACF plots

    ```python
    from statsmodels.graphics.tsaplots import plot_acf
    plot_acf(data['Count'], lags=10)
    plot_pacf(data['Count'], lags=10)
    ```

+ The partial autocorrelation function shows a high correlation with the first lag and lesser correlation with the second and third lag. The autocorrelation function shows a slow decay, which means that the future values have a very high correlation with its past values.

+ The number of times you shift, the same number of values will be reduced from the data. You would see some rows with NaNs at the start. That’s because the first observation has no lag. You’ll need to discard these rows from the training data.


## Rolling Window

+ How about calculating some statistical values based on past values? This method is called the rolling window method because the window would be different for every data point.

+ Pictorial example of rolling windows

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://www.analyticsvidhya.com/blog/2019/12/6-powerful-feature-engineering-techniques-time-series/" ismap target="_blank">
      <img src="https://s3-ap-south-1.amazonaws.com/av-blog-media/wp-content/uploads/2019/11/3hotmk.gif" style="margin: 0.1em;" alt="Example of rolling window" title="Example of rolling window" width=150>
    </a>
  </div>

+ Example

  ```python
  import pandas as pd
  data = pd.read_csv('Train_SU63ISt.csv')
  data['Datetime'] = pd.to_datetime(data['Datetime'],format='%d-%m-%Y %H:%M')

  data['rolling_mean'] = data['Count'].rolling(window=7).mean()
  data = data[['Datetime', 'rolling_mean', 'Count']]
  data.head(10)
  ```

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://www.analyticsvidhya.com/blog/2019/12/6-powerful-feature-engineering-techniques-time-series/" ismap target="_blank">
      <img src="https://s3-ap-south-1.amazonaws.com/av-blog-media/wp-content/uploads/2019/12/Screenshot-from-2019-12-07-13-33-19-300x168.png" style="margin: 0.1em;" alt="Result of rolling window features" title="Result of rolling window features" width=250>
    </a>
  </div>

+ Recency in an important factor in a time series. Values closer to the current date would hold more information.

+ weighted average
  + weighted average at time t for the past 7 values
  + math representation

    \[ w_{agv} = w_1 * (t-1) + w_2 * (t-2) + \cdots + w_7 * (t-7) \]

    where $w_1 > w_2 > \cdots > w_7$


## Expanding Window

+ rolling window, the size of the window is constant while the window slides as moveing forward in time

+ expanding windows
  + The idea behind the expanding window feature is that it takes all the past values into account.
  + pictorial example

    <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
      <a href="https://www.analyticsvidhya.com/blog/2019/12/6-powerful-feature-engineering-techniques-time-series/" ismap target="_blank">
        <img src="https://s3-ap-south-1.amazonaws.com/av-blog-media/wp-content/uploads/2019/12/output_B4KHcT-225x300.gif" style="margin: 0.1em;" alt="Example of expanding window features" title="Example of expanding window features" width=150>
      </a>
    </div>

  + the size of the window increases by one as it takes into account every new value in the series

+ Implementation of expanding window
  + using the `expanding()` function
  + code

    ```python
    import pandas as pd
    data = pd.read_csv('Train_SU63ISt.csv')
    data['Datetime'] = pd.to_datetime(data['Datetime'],format='%d-%m-%Y %H:%M')

    data['expanding_mean'] = data['Count'].expanding(2).mean()
    data = data[['Datetime','Count', 'expanding_mean']]
    data.head(10)

    #              Datetime  Count  expanding_mean
    # 0 2012-08-25 00:00:00      8             NaN
    # 1 2012-08-25 01:00:00      2        5.000000
    # 2 2012-08-25 02:00:00      6        5.333333
    # 3 2012-08-25 03:00:00      2        4.500000
    # 4 2012-08-25 04:00:00      2        4.000000
    # 5 2012-08-25 05:00:00      2        3.666667
    # 6 2012-08-25 06:00:00      2        3.428571
    # 7 2012-08-25 07:00:00      2        3.250000
    # 8 2012-08-25 08:00:00      6        3.555556
    # 9 2012-08-25 09:00:00      2        3.400000
    ```


## Domain-Specific

+ Having a good understanding of the problem statement, clarity of the end objective and knowledge of the available data is essential to engineer domain-specific features for the model.

+ creating lag features considering the store-product combination
  + knowledge about the products and the trends in the market, we would be able to generate more accurate (and fewer) feature
  + good understanding about the domain and data $to$ selecting the lag value and the window size
  + domain knowledge: able to pull external data that adds more value to the model


## Validation Technique for Time Series

+ convert a time series problem into a supervised machine learning problem

+ there is one important step that you should know before you jump to the model building process – creating a validation set for time series.

+ Validation data set
  + traditional machine learning problems: randomly select subsets of data for the validation and test sets
  + time series: each data point is dependent on its past values
  + It is important that we carefully build a validation set when working on a time series problem, without destroying the sequential order within the data.
  + example code

    ```python
    import pandas as pd
    data = pd.read_csv('Train_SU63ISt.csv')
    data['Datetime'] = pd.to_datetime(data['Datetime'],format='%d-%m-%Y %H:%M')
    data['Datetime'].min(), data['Datetime'].max(), (data['Datetime'].max() -data['Datetime'].min())
    # (Timestamp('2012-08-25 00:00:00'),
    #  Timestamp('2014-09-25 23:00:00'),
    #  Timedelta('761 days 23:00:00'))

    data.index = data.Datetime
    Train=data.loc['2012-08-25':'2014-06-24'] 
    valid=data.loc['2014-06-25':'2014-09-25']

    Train.shape, valid.shape
    # ((16056, 3), (2232, 3))
    ```
  

