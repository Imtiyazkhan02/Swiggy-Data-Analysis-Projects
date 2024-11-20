# Swiggy-Data-Analysis-Projects
#Importing Libraries

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
#Reading CSV
df = pd.read_csv('r downloads\Swiggy Data.csv')
df.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 201 entries, 0 to 200
Data columns (total 9 columns):
 #   Column                       Non-Null Count  Dtype 
---  ------                       --------------  ----- 
 0   name                         201 non-null    object
 1   online_order                 201 non-null    object
 2   book_table                   201 non-null    object
 3   rate                         197 non-null    object
 4   votes                        201 non-null    int64 
 5   approx_cost(for two people)  201 non-null    object
 6   listed_in(type)              201 non-null    object
 7   listed_in(city)              193 non-null    object
 8   cuisines                     201 non-null    object
dtypes: int64(1), object(8)
memory usage: 14.3+ KB
#Dropping Duplicates
df.drop_duplicates(inplace = True)
df.shape
(201, 9)
#Cleaning Rate Column
df['rate'].unique()
array(['4.1/5', '3.8/5', '3.7/5', '3.6/5', '4.6/5', '4.0/5', '4.2/5',
       '3.9/5', '3.1/5', '3.0/5', '3.2/5', '3.3/5', '2.8/5', '4.4/5',
       '4.3/5', '2.9/5', '3.5/5', '2.6/5', '3.8 /5', '3.4/5', nan, 'NEW',
       '4.5/5'], dtype=object)
#Removing "NEW" , "-" and "/5" from Rate Column
def handlerate(value):
    if(value=='NEW' or value=='-'):
        return np.nan
    else:
        value = str(value).split('/')
        value = value[0]
        return float(value)
df['rate'] = df['rate'].apply(handlerate)
df['rate'].head()
0    4.1
1    4.1
2    3.8
3    3.7
4    3.8
Name: rate, dtype: float64
#Filling Null Values in Rate Column with Mean
df['rate'].fillna(df['rate'].mean(), inplace = True)
df['rate'].isnull().sum()
0
df.info()
<class 'pandas.core.frame.DataFrame'>
Int64Index: 201 entries, 0 to 200
Data columns (total 9 columns):
 #   Column                       Non-Null Count  Dtype  
---  ------                       --------------  -----  
 0   name                         201 non-null    object 
 1   online_order                 201 non-null    object 
 2   book_table                   201 non-null    object 
 3   rate                         201 non-null    float64
 4   votes                        201 non-null    int64  
 5   approx_cost(for two people)  201 non-null    object 
 6   listed_in(type)              201 non-null    object 
 7   listed_in(city)              193 non-null    object 
 8   cuisines                     201 non-null    object 
dtypes: float64(1), int64(1), object(7)
memory usage: 15.7+ KB
