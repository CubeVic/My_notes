>This session will cover numpy, this is specially useful since the images are going to be represented as numpy arrays most of the time, here the [numpy documentation](https://docs.scipy.org/doc/numpy/user/quickstart.html)

## The Basics

NumPy’s main object is the homogeneous multidimensional array. It is a table of elements (usually numbers), all of the same type, indexed by a tuple of positive integers. In NumPy dimensions are called axes.

For example, the coordinates of a point in 3D space `[1, 2, 1] `has one axis. That axis has 3 elements in it, so we say it has a length of 3. In the example pictured below, the array has 2 axes.

```python
[[1.,0.,0.],
[0.,1.,2.]]
```

The NumPy's class is call `ndarray` also know by its alias `array`, but make sure not confuse it with the Standard Python library class `array.array`, in this case the NumPy is `numpy.array`, the Standard python `array` only handles one-dimensional arrays and offers less functionality.

### the Important objects
The most importation objects for the `ndarray`:

* `ndarray.ndim`: the number of axis (dimensions) of the array
* `ndarray.shape`: this is a tuple that indicate the size of the array in each direction, for example, shape of (m,n) will be a matrix with _n_ rows and _m_ columns, the length of the tuple is the numbers of axis, `ndim`.
* `ndarray.size`: total number of elements in the array, this is equal to the product of the elements in the shape.
* `ndarray.dtype`: an object describing the type of the elements in the array.
* `ndarray.itemsize`: the size in bytes of each element on the array.
* `ndarray.data`:the buffer that contain the actual elements of the array, normally is not use since we access the elements using the indexing facilities  
### The code Example

```python
import numpy as np
a = np.arange(15).reshape(3,5)
# a
# array([ [0,  1,  2,  3,  4,],
#         [5,  6,  7,  8,  9],
#         [10, 11, 12, 13, 14]])

a.shape
# (3,5)
a,ndim
# 2
a.dtype.name
#'int64'
a.itemsize
#8
a.size
#15
type(a)
# <type 'numpy.ndarray'>
```
##Numpy arrays

### Creation
you can create a NumPy array with a simple python list

```python
import numpy as np

a = np.array([1,2,3])
# array([1, 2, 3])
a.dtype
#dtype('int64')
```
>A frequent error consists in calling array with multiple numeric arguments, rather than providing a single list of numbers as an argument.

```python
a = np.array(1,2,3,4)    # WRONG
a = np.array([1,2,3,4])  # RIGHT
```
now, if you use `np.array` in a sequence of sequence, example `[(1,2,3), (4,5,6)]` you will get a two-dimension array

```python
b = np.array([(1,2,3),(4,5,6)])
# array([[1, 2, 3],
#       [4, 5, 6]])
```

### Creation Functions (`zeros`,`ones`,`empty`,)

Often, the elements of an array are originally unknown, but its size is known. Hence, NumPy offers several functions to create arrays with initial placeholder content. These minimize the necessity of growing arrays, an expensive operation

#### `zeros`

The function `zeros` will create an array and will be use as placeholder `0.` this means a float 0, at least you specify the `dtype`

**Syntax**

```python
np.zeros(shape=(n,m), dtype= np type)
```
> shape is optional, instead we can use just the tuple (n,m), and the dtype if it is not specify it will use the float.

```python
c = np.zeros(shape=(3,5))
#array([[0., 0., 0., 0., 0.],
#       [0., 0., 0., 0., 0.],
#       [0., 0., 0., 0., 0.]])

d = np.zeros((3,5))
#array([[0., 0., 0., 0., 0.],
#       [0., 0., 0., 0., 0.],
#       [0., 0., 0., 0., 0.]])
type(d)
# numpy.ndarray

e = np.zeros((3,5), dtype=np.int16)
#array([[0, 0, 0, 0, 0],
#       [0, 0, 0, 0, 0],
#       [0, 0, 0, 0, 0]], dtype=int16)
```

### `ones`

The function `ones` in the same way that `zeros` will create and array but instead of use `0` it will use the placeholder `1`.

**Syntax**

```python
np.ones(shape=(n,m), dtype= np type)
```
> shape is optional, instead we can use just the tuple (n,m), and the dtype if it is not specify it will use the float.

```python
c = np.ones(shape=(3,5))
#array([[1., 1., 1., 1., 1.],
#       [1., 1., 1., 1., 1.],
#       [1., 1., 1., 1., 1.]])

e = np.ones((3,5), dtype=np.int16)
#array([[1, 1, 1, 1, 1],
#       [1, 1, 1, 1, 1],
#       [1, 1, 1, 1, 1]], dtype=int16)
```

### `empty`

This will create an array with random numbers, the numbers will depend of the state of the memory in that moment 

```python
np.empty( (2,3) )
#array([[  3.73603959e-262,   6.02658058e-154,   6.55490914e-260],
#       [  5.30498948e-313,   3.14673309e-307,   1.00000000e+000]])
```

### Create sequence of numbers (`arange`,`linspace`)

