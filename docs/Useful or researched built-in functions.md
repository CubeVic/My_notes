#Useful or researched built-in functions

## `reduce()` from functools  

 The `reduce(fun,seq)` function is used to *apply a particular function passed in its argument to all of the list elements* mentioned in the sequence passed along. This function is defined in “functools” module.

**Working :** 

* At first step, first two elements of sequence are picked and the result is obtained.  
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

int he previous code the idea to solve the problem [Between Two Sets](https://www.hackerrank.com/challenges/between-two-sets/problem)

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

print(x)
```
 the output will be:

```
White
```