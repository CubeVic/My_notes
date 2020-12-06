## Shape and Reshape

Something really useful is be able to change or create an array in a specific shape, we will start with the same array that before:

```python
np.random.seed(101)
arr =  np.random.randint(0, 100,10)
#array([95, 11, 81, 70, 63, 87, 75,  9, 77, 40])
```

### Find the shape

now we can use `shape` to find what shape our array has in this moment

```python
arr.shape
# (10,)
```
this mean that is an array, or, better a vector with 10 items.

### How to `reshape`

we can use the function `reshape` to change the previous vector

**Syntax**

```python
arr.reshape((2,5))
# array([[95, 11, 81, 70, 63],
#       [87, 75,  9, 77, 40]])
```
> we need to reshape to values that make sense, in this case 2 rows and 5 columns does, because $2*5 = 10$

if i try to create a shape that is not correct i will get a `valueError` exception, like here

```python
 arr.reshape((2,10))
 ---------------------------------------------------------------------------
ValueError                                Traceback (most recent call last)
<ipython-input-35-ef8eb80c29ad> in <module>()
----> 1 arr.reshape((2,10))

ValueError: cannot reshape array of size 10 into shape (2,10)
```

## Indexing 

it is important to be able to get back rows, columns or slice of the matrix we create, in this case we enter to scope of indexing.

```python
mat = np.arange(0,100).reshape(10,10)
# array([[ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9],
#       [10, 11, 12, 13, 14, 15, 16, 17, 18, 19],
#       [20, 21, 22, 23, 24, 25, 26, 27, 28, 29],
#       [30, 31, 32, 33, 34, 35, 36, 37, 38, 39],
#       [40, 41, 42, 43, 44, 45, 46, 47, 48, 49],
#       [50, 51, 52, 53, 54, 55, 56, 57, 58, 59],
#       [60, 61, 62, 63, 64, 65, 66, 67, 68, 69],
#       [70, 71, 72, 73, 74, 75, 76, 77, 78, 79],
#       [80, 81, 82, 83, 84, 85, 86, 87, 88, 89],
#       [90, 91, 92, 93, 94, 95, 96, 97, 98, 99]])
```

### Find a single digit in the matrix

let say that i want to get the element in `row = 0` and `col = 1`

**Syntax**

```python
mat[row,col]
# 1
```

we don't need to define the variables 'row' and 'col' we can simply 

```python
mat[5,5]
# 55
```

### How to slice a matrix

let say that we want 

**1. Get all the values in a row or column**
we want to get all the values in the row 1

**Syntax**

```python
mat[:,1]
# array([ 1, 11, 21, 31, 41, 51, 61, 71, 81, 91])
```

now for the column

```python
mat[1,:]
# array([10, 11, 12, 13, 14, 15, 16, 17, 18, 19])
```

we can change the shape of the new array

```python
mat[1,:].reshape(10,1)
# array([[10],
#       [11],
#       [12],
#       [13],
#       [14],
#       [15],
#       [16],
#       [17],
#       [18],
#       [19]])
```


**2. Get all the values from n rows and m columns**
We want to get back part of the original matrix 

```python
mat[:3,:3]
# array([[ 0,  1,  2],
#       [10, 11, 12],
#       [20, 21, 22]])
```

we can replace part of the matrix as well

```python
mat[0:4,0:4] = 0
#array([[ 0,  0,  0,  0,  4,  5,  6,  7,  8,  9],
#       [ 0,  0,  0,  0, 14, 15, 16, 17, 18, 19],
#       [ 0,  0,  0,  0, 24, 25, 26, 27, 28, 29],
#       [ 0,  0,  0,  0, 34, 35, 36, 37, 38, 39],
#       [40, 41, 42, 43, 44, 45, 46, 47, 48, 49],
#       [50, 51, 52, 53, 54, 55, 56, 57, 58, 59],
#       [60, 61, 62, 63, 64, 65, 66, 67, 68, 69],
#       [70, 71, 72, 73, 74, 75, 76, 77, 78, 79],
#       [80, 81, 82, 83, 84, 85, 86, 87, 88, 89],
#       [90, 91, 92, 93, 94, 95, 96, 97, 98, 99]])
```

