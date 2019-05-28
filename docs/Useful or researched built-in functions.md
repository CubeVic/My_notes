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

