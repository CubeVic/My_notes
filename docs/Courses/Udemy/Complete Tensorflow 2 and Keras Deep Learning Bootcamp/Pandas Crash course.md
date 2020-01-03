For the review or refresh of pandas we will follow the structure bellow:

* Series.  
* DataFrames.  
* Missing Data.  
* GroupBy.  
* Operations.  
* Data Input and Output.  

##Series

Series are similar to Numpy arrays ( they are build on top of Numpy arrays)  and the difference is that SEris can have axis labels, that means that can be located not just by numbers but by labels, and they can hold much more than just numbers, they can hold any type of python object.

We are going to create Series in different ways: 

###Creating a series.

First we will need to import numpy and pandas

```python 
import numpy as np
import pandas as pd
``` 

now we are going to create a list, a numpy array and a dictionary that later will be use to create the series

```python 
lables = ['a','b','c']
my_list = [10,20,30]
arr = np.array([10,20,30])
d = {'a':10,'b':20,'c':30}
``` 

####1. Using List

```python 
pd.Series(data=mylist)
#0    10
#1    20
#2    30
#dtype: int64
``` 
The about is a Series that use just number as labels, now let use the labels defined before with the list `lables`

```python 
pd.Series(data=my_list,index=labels)
#a    10
#b    20
#c    30
#dtype: int64
``` 
now a shorter way

```python 
pd.Series(my_list,labels)
#a    10
#b    20
#c    30
#dtype: int64
``` 

####2. Using NumPy arrays

```python 
pd.Series(arr)
#0    10
#1    20
#2    30
#dtype: int64
``` 
now with the labels

```python 
pd.Series(arr,labels)
#a    10
#b    20
#c    30
#dtype: int64
``` 





























































