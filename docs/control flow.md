## Iterating through Dictionaries with `For` loops

The iteration through Dictionaries in pyhton is a different than Swift, in this case to iterate and get back both *key* and *value* you need to use a built-in method `item`.

For example: 

```python

cast = {
           "Jerry Seinfeld": "Jerry Seinfeld",
           "Julia Louis-Dreyfus": "Elaine Benes",
           "Jason Alexander": "George Costanza",
           "Michael Richards": "Cosmo Kramer"
       }

for key,value in cast.items():
	print("Actor: {}   Role: {}".format(key,value))

```

which will result in something like: 

```
Actor: Jerry Seinfeld    Role: Jerry Seinfeld
Actor: Julia Louis-Dreyfus    Role: Elaine Benes
Actor: Jason Alexander    Role: George Costanza
Actor: Michael Richards    Role: Cosmo Kramer
```

## `for` Loops vs. `While` Loops

`for` loops are idea when the *number of iteration* are _known_ or _finite_.  

Examples:  

* When you have an iterable collection (list, string, set, tuple, dictionary):  
```python
for name in names:
```

* When you want to iterate through a loop for a definite number of times, using `range()`
```python
for i in range(5):
```

`while` loop are ideal when the *iterations* are to _continue until a condition is met_  

Examples:

* When you want to use comparison operations:
``` python
while count <= 100:
```

* When you want to loop base on receiving specific user input
```python
while user_input == 'y'
```

the following are required to build a correct `while` loop: 

* The condition for existing the while loop should be included.  
* Check if the iteration conditions is met.  
* Body of the loop should change the value of condition variables.  
##Break and continue.  

* `break` terminates a loop.  
* `continue` skips one iteration of a loop.  

## Zip and Enumerate
`zip` and `enumerate` are build-in functions that can come handy when dealing with loops.

**Zip**

`zip` will return  an iterator that combine multiples iterables into one sequence of tuples, this will be more clear with an example:

```python
list(zip(['a','b','c'], [1,2,3]))
```

which out put will be:

```python
[('a',1),('b',2),('c',3)]
```

so in this case we can see that `zip` create a iterator that combine the two provided and each iterator is a tuple with items in the in that position.

the reverse or Unzip process can be done using the *

```python
letters = ['a','b','c']
nums = [1,2,3]

for letter, num in zip(letters,nums):
	print("{}:{}".format(letter,num))

some_list = [('a',1),('b',2),('c',3)]
letters, nums = zip(*some_list)
```

**Enumerate**  
`enumerate` is a built in function that return an iterator of tuples containing indexes and values of a list, example:

```python
letters = ['a','b','c','d','e']

for i, letter in enumerate(letters):
	print(i, letter)
```

this will be the output:

```
0 a
1 b
2 c
3 d
4 e
```

an example of `enumerate`, here:

```python
cast = ["Barney Stinson", "Robin Scherbatsky", "Ted Mosby", "Lily Aldrin", "Marshall Eriksen"]
heights = [72, 68, 72, 66, 76]

for i, character in enumerate(cast):
    cast[i] = character + " " + str(heights[i])

print(cast)
```

It will take 2 list and it will out put a single list of items that include a both original list as a single string

```
['Barney Stinson 72', 'Robin Scherbatsky 68', 'Ted Mosby 72', 'Lily Aldrin 66', 'Marshall Eriksen 76']
```