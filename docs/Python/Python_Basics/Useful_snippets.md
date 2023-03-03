## 1. All Unique

This method check if there is any duplicate element
```python
def all_unique(lst):
		return len(str) == len(set(lst))

x = [1,1,2,2,3,2,3,4,5,6]
y = [1,2,3,4,5]
all_unique(x) # False
all_unique(y) # True
```

##2. Anagrams

Check if a string is an anagram

```python
from collections import Counter

def anagram(first, second):
	return Counter(first) == Counter(second)

anagram("abcd3","3acdb") #True
```

##3. Memory
This is use to check the memory usage of an object

```python
import sys

variable = 30
print(sys.getsizeof(variable))# 24
```

##4. Byte size
This Method return the length of a string in bytes

```python
def byte_size(string):
	return(len(String.encode('utf-8')))

byte_size('😀') # 4
byte_size('Hello World') # 11
```

##5. Print a String N times
This will print a string N times

```python
n = 2;
s = 'programing'

print(s*n) # ProgrammingProgramming
```

##6. Capitalize first letters
```python
s = "programming is awesome"

print(s.title()) # Programming Is Awesome
```

##7. Chunk
This method chunk a list in a smaller list of specific size

```python
from math import ceil

def chunk(lst, size):
    return list(map(lambda x: lst[x * size:x * size + size],list(range(0, ceil(len(lst) / size)))))

chunk([1,2,3,4,5],2) # [[1,2],[3,4],5]
```

##8. Compact

This method remove the "Falsy" values, in other words, False, 0, None,"".

```python
def compact(lst):
	return list(filter(bool,lst))

compact([0, 1, False, 2, '', 3, 'a', 's', 34]) # [ 1, 2, 3, 'a', 's', 34 ]
```
##9. Count by
This use ZIP() method to transpose a 2D array

```python
array = [['a'.'b'],['c','d'],['e'.'f']]
transposed = zip(*array)
print(transposed) # [('a', 'c', 'e'), ('b', 'd', 'f')]
```

##10. chained comparison
multiple comparison in a single line

```python
a = 3
print( 2 < a < 8) # True
print(1 == a < 2) # False
```

##11. Comma-separated
This snippet use the method `.join()` turn a list of strings into a single string with each element from the list separated by commas.

```python
hobbies = ["basketball", "football", "swimming"]

print("My hobbies are: " + ", ".join(hobbies)) # My hobbies are: basketball, football, swimming
```


##12. Count vowels
This method counts the number of vowels (‘a’, ‘e’, ‘i’, ‘o’, ‘u’) found in a string, using regular expressions.

```python
import re

def count_vowels(str):
    return len(len(re.findall(r'[aeiou]', str, re.IGNORECASE)))


count_vowels('foobar') # 3
count_vowels('gym') # 0
```

##13. Decapitalize
This method can be used to turn the first letter of the given string into lowercase.

```python

def decapitalize(string):
    return str[:1].lower() + str[1:]


decapitalize('FooBar') # 'fooBar'
decapitalize('FooBar') # 'fooBar'
```

##14. Flatten
The following methods flatten a potentially deep list using recursion.

```python
def spread(arg):
    ret = []
    for i in arg:
        if isinstance(i, list):
            ret.extend(i)
        else:
            ret.append(i)
    return ret

def deep_flatten(lst):
    result = []
    result.extend(
        spread(list(map(lambda x: deep_flatten(x) if type(x) == list else x, lst))))
    return result


deep_flatten([1, [2], [[3], 4], 5]) # [1,2,3,4,5]
```

##15. Difference
This method finds the difference between two iterables and display just the different number in the first iterable

```python
def difference(a, b):
    set_a = set(a)
    set_b = set(b)
    comparison = set_a.difference(set_b)
    return list(comparison)


difference([1,2,3], [1,2,4]) # [3]
```

##16. Difference by
The following method returns the difference between two lists after applying a given function to each element of both lists.

```python
def difference_by(a, b, fn):
    b = set(map(fn, b))
    return [item for item in a if fn(item) not in b]


from math import floor
difference_by([2.1, 1.2], [2.3, 3.4],floor) # [1.2]
difference_by([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], lambda v : v['x']) # [ { x: 2 } ]
```

##17. Chained function call
You can call multiple functions inside a single line.

```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

a, b = 4, 5
print((subtract if a > b else add)(a, b)) # 9
```

##18. Has duplicates
The following method checks whether a list has duplicate values by using the fact that `set()` contains only unique elements.

```python
def has_duplicates(lst):
    return len(lst) != len(set(lst))


x = [1,2,3,4,5,5]
y = [1,2,3,4,5]
has_duplicates(x) # True
has_duplicates(y) # False
```
##19. Merge two dictionaries
The following method can be used to merge two dictionaries.

```python
def merge_dictionaries(a, b)
   return {**a, **b}


a = { 'x': 1, 'y': 2}
b = { 'y': 3, 'z': 4}
print(merge_dictionaries(a, b)) # {'y': 3, 'x': 1, 'z': 4}
```

##20. Convert two lists into a dictionary
The following method can be used to convert two lists into a dictionary.

```python
def to_dictionary(keys, values):
    return dict(zip(keys, values))


keys = ["a", "b", "c"]
values = [2, 3, 4]
print(to_dictionary(keys, values)) # {'a': 2, 'c': 4, 'b': 3}
```

##21. Use enumerate
This method gets a dictionary as an input and then returns only the keys that are in this dictionary.

```python
list = ["a", "b", "c", "d"]
for index, element in enumerate(list):
    print("Value", element, "Index ", index, )
# ('Value', 'a', 'Index ', 0)
# ('Value', 'b', 'Index ', 1)
#('Value', 'c', 'Index ', 2)
# ('Value', 'd', 'Index ', 3)
```

##22. Time spent
This snippet can be used to calculate the time it takes to execute a particular code.

```python
import time

start_time = time.time()

a = 1
b = 2
c = a + b
print(c) #3

end_time = time.time()
total_time = end_time - start_time
print("Time: ", total_time)

# ('Time: ', 1.1205673217773438e-05)
```

##23. Try else
You can have an else clause as part of a try/except block, which is executed if no exception is thrown.

```python
try:
    2*3
except TypeError:
    print("An exception was raised")
else:
    print("Thank God, no exceptions were raised.")

#Thank God, no exceptions were raised.
```

##24. Most frequent
This method returns the most frequent element that appears in a list.

```python
def most_frequent(list):
    return max(set(list), key = list.count)


list = [1,2,1,2,3,2,1,4,2]
most_frequent(list)
```

##25. Palindrome
This method checks whether a given string is a palindrome. It initially converts the string into lower case, then removes non-alphanumeric characters from it. In the end, it compares the new string with the reversed version.

```python
def palindrome(string):
    from re import sub
    s = sub('[\W_]', '', string.lower())
    return s == s[::-1]


palindrome('taco cat') # True
```

##26. Calculator without if-else
The following snippet shows how you can write a simple calculator without the need to use if-else conditions.

```python
import operator
action = {
    "+": operator.add,
    "-": operator.sub,
    "/": operator.truediv,
    "*": operator.mul,
    "**": pow
}
print(action['-'](50, 25)) # 25
```

##27. Shuffle
This algorithm randomizes the order of the elements in a list by implementing the Fisher-Yates algorithm to do the ordering in the new list.

```python
from copy import deepcopy
from random import randint

def shuffle(lst):
    temp_lst = deepcopy(lst)
    m = len(temp_lst)
    while (m):
        m -= 1
        i = randint(0, m)
        temp_lst[m], temp_lst[i] = temp_lst[i], temp_lst[m]
    return temp_lst


foo = [1,2,3]
shuffle(foo) # [2,3,1] , foo = [1,2,3]
```

##28. Spread
This method flattens a list similarly like `[].concat(…arr)` in JavaScript.

```python

def spread(arg):
    ret = []
    for i in arg:
        if isinstance(i, list):
            ret.extend(i)
        else:
            ret.append(i)
    return ret


spread([1,2,3,[4,5,6],[7],8,9]) # [1,2,3,4,5,6,7,8,9]
```

##29. Swap values
A really quick way for swapping two variables without having to use an additional one.

```python
def swap(a, b):
  return b, a

a, b = -1, 14
swap(a, b) # (14, -1)
```

##30. Get default value for missing keys
This snippet shows how you can get a default value in case a key you are looking for is not included in the dictionary.

```python
d = {'a': 1, 'b': 2}

print(d.get('c', 3)) # 3
```
