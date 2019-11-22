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