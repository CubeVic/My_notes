#Useful functions or Statements

## `reduce()` from functools  

 The `reduce(fun,seq)` function is used to *apply a particular function passed in its argument to all of the list elements* mentioned in the sequence passed along. This function is defined in “functools” module.

**Working :** 

* First two elements of sequence are picked and the result is obtained.  
* Next step is to apply the same function to the previously attained result and the number just succeeding the second element and the result is again stored.  
* This process continues till no more elements are left in the container.  
* The final returned result is returned and printed on console.  

```python
import sys
from math import gcd
from functools import reduce

n,m = input().strip().split(' ')
n,m = [int(n),int(m)]
A = map(int,input().strip().split(' '))
B = map(int,input().strip().split(' '))

def LCM(a, b):
    return (a*b)//gcd(a,b)

lcm = reduce(LCM, A, 1)
gcd = reduce(gcd, B)

lcm_copy = lcm

count = 0
while lcm <= gcd:
    if(gcd % lcm) == 0:
        count += 1
    lcm = lcm + lcm_copy

print(count)
```

in the previous code the idea to solve the problem [Between Two Sets](https://www.hackerrank.com/challenges/between-two-sets/problem)

here more information about [GCD](https://en.wikipedia.org/wiki/Greatest_common_divisor) and [LCM](https://en.wikipedia.org/wiki/Least_common_multiple) 

## `GCD()` from math
The Highest Common Factor (HCF) , also called *gcd*, can be computed in python using a single function offered by math module and hence can make tasks easier in many situations.

```python
# Python code to demonstrate gcd() 
# method to compute gcd 

import math 

# prints 12 
print ("The gcd of 60 and 48 is : ",end="") 
print (math.gcd(60,48)) 
```

##`Counter()` from collection  
A `Counter` is a `dict` subclass for counting hashable objects. It is a collection where elements are stored as dictionary keys and their counts are stored as dictionary values. Counts are allowed to be any integer value including zero or negative counts. 

for example: assume an array `arr=[1,1,2,2,3]` and you are asked to find the number of occurrence of each integer, in this case you can use `Counter` whihc will return a dictionary using the value as key and the count as value, like this:

```python

from collection import Counter

arr=[1,1,2,2,3]

dict_arr=Counter(arr)
print(dict_arr)
```

the result will be:

```
{1:2, 2:2, 3:1}
```

##`iter()` from the build-in functions

Before start to talk about `iter()` better start by remembering what is a [Iterator](https://www.w3schools.com/python/python_iterators.asp) and what is the difference with iterable

### Python Iterators
An iterator is an object that contains a countable number of values, and it can be iterated upon, meaning that you can traverse through all the values.

Technically, in Python, an iterator is an object which implements the iterator protocol, which consist of the methods __iter__() and __next__().

### Iterator vs Iterable

Lists, tuples, dictionaries, and sets are all iterable objects. They are iterable containers which you can get an iterator from.

All these objects have a `iter()` method which is used to get an iterator:

```python
mytuple = ("apple", "banana", "cherry")
myit = iter(mytuple)

print(next(myit))
print(next(myit))
print(next(myit))
```
it will output:

```
apple
banana
cherry
```


## `setdefault()` method from Dictionaries

The setdefault() method returns the value of the item with the specified key.

If the key does not exist, insert the key, with the specified value, see example below

**Syntax**
```
dictionary.setdefault(keyname,value)
```

**Example**
```python
car = {
  "brand": "Ford",
  "model": "Mustang",
  "year": 1964
}

x = car.setdefault("color", "white")

print(x.color)
```
 the output will be:

```
White
```

## `map()` Built-in function

**Basic Syntax**
```python
map(functions_object, iterable1, iterable2,...)
```
`map` functions expects a function object and any number of iterables like list, dictionary, etc. It executes the function_object for each element in the sequence and returns a list of the elements modified by the function object.

**Example:**
```python
def multiply2(x):
  return x * 2
    
map(multiply2, [1, 2, 3, 4])  # Output [2, 4, 6, 8]
```
In the above example, map executes multiply2 function for each element in the list i.e. 1, 2, 3, 4 and returns [2, 4, 6, 8]

Let’s see how we can write the above code using map and lambda.

```python
map(lambda x : x*2, [1, 2, 3, 4]) #Output [2, 4, 6, 8]
```

We can pass multiple sequences to the map functions as shown below:
```python

list_a = [1, 2, 3]
list_b = [10, 20, 30]
  
map(lambda x, y: x + y, list_a, list_b) # Output: [11, 22, 33]
```
Neither we can access the elements of the map object with index nor we can use len() to find the length of the map object

We can force convert the map output i.e. the map object to list as shown below:

```python
map_output = map(lambda x: x*2, [1, 2, 3, 4])
print(map_output) # Output: map object: <map object at 0x04D6BAB0>

list_map_output = list(map_output)

print(list_map_output) # Output: [2, 4, 6, 8]
```

## `filter()` Built-in function

**Basic Syntax**
```python
filter(function_object, iterable)
```

filter function expects two arguments, function_object and an iterable. function_object returns a boolean value. function_object is called for each element of the iterable and filter returns only those element for which the function_object returns true.

Like map function, filter function also returns a list of element. Unlike map function filter function can only have one iterable as input.

**Example:**

Even number using filter function
```python

a = [1, 2, 3, 4, 5, 6]
filter(lambda x : x % 2 == 0, a) # Output: [2, 4, 6]
```

Similar to map, filter function in Python3 returns a filter object or the iterator which gets lazily evaluated. Neither we can access the elements of the filter object with index nor we can use len() to find the length of the filter object.

```python
list_a = [1, 2, 3, 4, 5]

filter_obj = filter(lambda x: x % 2 == 0, list_a) # filter object <filter at 0x4e45890>

even_num = list(filter_obj) # Converts the filer obj to a list

print(even_num) # Output: [2, 4]
```

## `pass` Statement 

The pass statement does nothing. It can be used when a statement is required syntactically but the program requires no action. For example:

```python
while True:
     pass  # Busy-wait for keyboard interrupt (Ctrl+C)
```
This is commonly used for creating minimal classes:

```python
class MyEmptyClass:
     pass
```

Another place pass can be used is as a place-holder for a function or conditional body when you are working on new code, allowing you to keep thinking at a more abstract level. The pass is silently ignored:

```python
def initlog(*args):
     pass   # Remember to implement this!
```