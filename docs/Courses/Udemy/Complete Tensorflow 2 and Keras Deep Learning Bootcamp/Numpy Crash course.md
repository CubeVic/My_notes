This notes  are notes for the Numpy crash course.

Numpy is a linear library for Python, it is an essential building block for other PyData ecosystem ( Pandas, scipy, scikit-lean, etc)

## Using NumPy

Normally numpy is import as `np`

```python
import numpy as np
```

## NumPy Arrays

NumPy came in vector and matrices, Vectors are 1 dimension, matrix are 2D dimensions.

### Create NumPy Arrays

we can create an array from a python list

```python
my_list = [1,2,3]
np.array(my_list)
# array([1, 2, 3])
```

and can be a list of list as well

```python
my_matrix = [[1,2,3],[4,5,6],[7,8,9]]
np.array(my_matrix)
#array([[1, 2, 3],
#       [4, 5, 6],
#       [7, 8, 9]])
```

## Build-in Methods 

### `arange`

Return evenly spaced value within a given interval

```python
np.arange(0,10)
# array([0,1,2,3,4,5,6,7,8,9])
np.arange(0,11,2)
# array([0, 2, 4, 6, 8, 10])
```

### `zeros` and `ones`

Generate vectors or matrix of zeros or ones

```python
np.zero(3)
# array([0. , 0. , 0.])

np.zero((5,5))
# array([[0., 0., 0., 0., 0.],
#        [0., 0., 0., 0., 0.],
#        [0., 0., 0., 0., 0.],
#        [0., 0., 0., 0., 0.],
#        [0., 0., 0., 0., 0.]])

np.ones(3)
# array([1., 1., 1.])

np.ones((3,3))
# array([[1., 1., 1.],
#       [1., 1., 1.],
#       [1., 1., 1.]])

```
### `linspace`

Return evenly spaced numbers over a specific interval

```python
np.linspace(0,10,3)
# array([0., 5., 10.])

np.linspace(0,5,20)
# array([0.        , 0.26315789, 0.52631579, 0.78947368, 1.05263158,
#       1.31578947, 1.57894737, 1.84210526, 2.10526316, 2.36842105,
#       2.63157895, 2.89473684, 3.15789474, 3.42105263, 3.68421053,
#       3.94736842, 4.21052632, 4.47368421, 4.73684211, 5.        ])

#Note that .linspace() includes the stop value. To obtain an array of common fractions, increase the number of items:

np.linspace(0,5,21)
# array([0.  , 0.25, 0.5 , 0.75, 1.  , 1.25, 1.5 , 1.75, 2.  , 2.25, 2.5 ,
#       2.75, 3.  , 3.25, 3.5 , 3.75, 4.  , 4.25, 4.5 , 4.75, 5.  ])

```

### `eye` identity matrix

Create a identity matrix

```python
np.eye(4)
# array([[1., 0., 0., 0.],
#       [0., 1., 0., 0.],
#       [0., 0., 1., 0.],
#       [0., 0., 0., 1.]])
```

## Random

Here some of the ways we can create random numbers 

### `rand`

Creates an array of the given shape with random uniform distribution over `[0,1)`

```python
np.random.rand(2)
# array([0.37065108, 0.89813878])
np.random.rand(5,5)
# array([[0.03932992, 0.80719137, 0.50145497, 0.68816102, 0.1216304 ],
#       [0.44966851, 0.92572848, 0.70802042, 0.10461719, 0.53768331],
#       [0.12201904, 0.5940684 , 0.89979774, 0.3424078 , 0.77421593],
#       [0.53191409, 0.0112285 , 0.3989947 , 0.8946967 , 0.2497392 ],
#       [0.5814085 , 0.37563686, 0.15266028, 0.42948309, 0.26434141]])

```

### `randint`

This generate a integer from low (inclusive) to high (exclusive)

```python 
np.random.randint(1,100)
#61
np.random.randint(1,100,10)
# array([39, 50, 72, 18,27, 59, 15, 97, 11, 14])
```  

### `seed`

It is use to create a random state that can be reproducible, i means, the result will be the same everything we use the same seed 

```python 
np.random.seed(42)
np.random.rand(4)
# array([0.37454012, 0.95071431, 0.73199394, 0.59865848])

np.random.seed(42)
np.random.rand(4)
# array([0.37454012, 0.95071431, 0.73199394, 0.59865848])
``` 

## Array Attributes and Methods

To explain the attributes and methods we need to create a vector and matrix

```python 
arr = np.arange(25)
# array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
#       17, 18, 19, 20, 21, 22, 23, 24])
ranarr = np.random.randint(0,50,10)
# array([38, 18, 22, 10, 10, 23, 35, 39, 23,  2])
``` 

### Reshape - `reshape`

Return the same data of the vector or matrix but in a different shape

```python 
arr.reshape(5,5)
# array([[ 0,  1,  2,  3,  4],
#       [ 5,  6,  7,  8,  9],
#       [10, 11, 12, 13, 14],
#       [15, 16, 17, 18, 19],
#       [20, 21, 22, 23, 24]])
``` 
### max, min, argmax, argmin - `max`,`min`,`argmax`,`argmin`

Let start with `ranarr`
```python 
ranarr = np.random.randint(0,50,10)
# array([38, 18, 22, 10, 10, 23, 35, 39, 23,  2])
``` 

the maximum number in the array
```python 
ranarr.max()
# 39
``` 
the index of this maximum number
```python 
ranarr.argmax()
# 7
```
now for the minimum 
```python 
ranarr.min()
# 2
ranarr.argmin()
# 9
``` 
  
### Shape - `shape`

shape is an attribute and not a method

```python 
# Vector
arr.shape
#(25,)

# Notice the two sets of brackets
arr.reshape(1,25)
# array([[ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15,
#        16, 17, 18, 19, 20, 21, 22, 23, 24]])

arr.reshape(1,25).shape
# (1, 25)

arr.reshape(25,1)
#array([[ 0],
#       [ 1],
#       [ 2],
#       [ 3],
#       [ 4],
#       [ 5],
#       [ 6],
#       [ 7],
#       [ 8],
#       [ 9],
#       [10],
#       [11],
#       [12],
#       [13],
#       [14],
#       [15],
#       [16],
#       [17],
#       [18],
#       [19],
#       [20],
#       [21],
#       [22],
#       [23],
#       [24]])

arr.reshape(25,1).shape
# (25, 1)
``` 

## 	`dtype`

In order to know the data type of the object 

```python 
arr.dtype
# dtype('int32')

arr2 = np.array([1.2, 3.4, 5.6])
arr2.dtype

#dtype('float64')
``` 
