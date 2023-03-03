> This notes are base in the Medium post called ["five Python tricks you need to learn today"](https://towardsdatascience.com/five-python-tricks-you-need-to-learn-today-9dbe03c790ab) and different articles or answers i found on Internet.


## TIp 1: Clean - Powerful One-liners

### Conditional statements

A normal If conditional will look like this:

```python
if alpha > 7 :
	beta = 999
elif alpha == 7:
	beta = 99
else:
	beta = 0
```

but this can be one line, it can be simplified in this way:

```python
beta == 999 if alpha > 7 else 99 if alpha == 7 else 0
```

### `for` loops

for example, doubling a list of integers in four lines:

```python
lst = [1,3,5]
doubled = []
for num in lst:
	doubled.append(num*2)
```

and it can be simplify to just one line:

```python
double = [num * 2 for num in lst]
```

## Tip 2: String Manipulation

### Reverse a string

we can use `::-1` to reverse a string, like this:

```python
a = "ilovemyjob"
print a[::-1]
#bojymevoli
```

### `join` strings

we can print the result of join different strings, or item of a list together:

let say we have this:
```python
str1 = "Totally"
str2 = "Awesome"
lst3 = ["Omg", "You", "Are"]
```

so we can use `join()` method to create the outcome:

```python
print ' '.join(lst3)
#Omg You Are
print ' '.join(lst3)+' '+str1+' '+str2
#Omg You Are Totally Awesome
```

## Tip 3: Replace loops for Map, Filter, and Reduce

In some cases what we want to achieve with the loops can be done by `map()`, `filter()`, and `reduce()`, we need to keep in mine the following:

* **Map:** Apply the same set of steps to each item, storing the result.
* **Filter:** Apply validation criteria, storing items that evaluate True.
* **Reduce:** Return a value that is passed from element to element.

here a simple example, first how it will be done by loops

```python
numbers = [1,2,3,4,5,6]
odd_numbers = []
squared_odd_numbers = []
total = 0
# filter for odd numbers
for number in numbers:
   if number % 2 == 1:
      odd_numbers.append(number)
# square all odd numbers
for number in odd_numbers:
   squared_odd_numbers.append(number * number)
# calculate total
for number in squared_odd_numbers:
   total += number
# calculate average
```

now let's do it with the functions

```py hl_lines="2 3"
from functools import reduce
numbers = [1,2,3,4,5,6]
odd_numbers = filter(lambda n: n % 2 == 1, numbers)
squared_odd_numbers = map(lambda n: n * n, odd_numbers)
total = reduce(lambda acc, n: acc + n, squared_odd_numbers)
```
Few things to keep in mine:

* `map()` and `filter()` are native available, but `reduce()` is part of the library `functools`.
* The lambda expression is the first argument, and the second is an iterable.
* The lambda expression for `reduce()` requires two arguments: the accumulator (the value that is passed to each element) and the individual element itself.
