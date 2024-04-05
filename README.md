# Uber-trip-data-analysis
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt
import numpy as np
import os
uber_15=pd.read_csv(r'./uber-raw-data-janjune-15.csv')
uber_15.tail()
uber_15.shape()
uber_15.duplicated()
uber_15.drop_duplicates(inplace=True)
uber_15.shape
uber_15.dtypes
uber_15['Pickup_date']=pd.to_datetime(uber_15['Pickup_date'],format='%Y-%m-%d %H:%M:%S')
uber_15['Pickup_date'].dtype
uber_15['month']=uber_15['Pickup_date'].dt.month
uber_15['month'].value_counts().plot(kind='bar')
uber_15['weekday']=uber_15['Pickup_date'].dt.day_name()
uber_15['day']=uber_15['Pickup_date'].dt.day
uber_15['hour']=uber_15['Pickup_date'].dt.hour
uber_15['month']=uber_15['Pickup_date'].dt.month
uber_15['minute']=uber_15['Pickup_date'].dt.minute
uber_15.tail()
temp=uber_15.groupby(['month','weekday'],as_index=False).size()
temp.head()
temp['month'].unique()
dict_month={1:'Jan',2:'Feb',3:'March',4:'april',5:'May',6:'June'}
temp['month']=temp['month'].map(dict_month)
temp['month']
type(uber_15.groupby(['month','weekday']).size())
temp
plt.figure(figsize=(12,8))
sns.barplot(x='month',y='size',hue='weekday',data=temp)
summary=uber_15.groupby(['weekday','hour'],as_index=False).size()
 summary
 plt.figure(figsize=(12,8))
sns.pointplot(x='hour',y='size',hue='weekday',data=summary)
