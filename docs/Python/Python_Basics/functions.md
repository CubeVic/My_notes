## Default arguments
We can add default arguments in a function to have default values for parameters that are unspecified in a function call:

```python
def cylinder_volume(height, radius=5):
    pi = 3.14159
    return height * pi * radius ** 2
```

## Variable

check the code

```python
egg_bag = 0

def buy_eggs()
    egg_bag += 12

buy_eggs()
```

This causes an UnboundLocalError, since Python doesn't allow functions to modify variables that are outside the function's scope. A better way would be to pass the variable as an argument and reassign it outside the function.

a better solution will be:

```python
egg_count = 0

def buy_eggs(count):
    return count + 12  # purchase a dozen eggs

egg_count = buy_eggs(egg_count)
```

## Lambda Expressions

You can use lambda expressions to create anonymous functions. These are functions that don’t have a name. They are helpful for creating quick functions that aren’t needed later in your code. This can be especially useful for higher order functions, or functions that take in other functions as arguments.


With a lambda expression, this function:

```python
def multiply(x, y):
    return x * y
```

can be reduced to:

```python
multiply = lambda x, y: x * y
```

**Components of a Lambda Function**

1. The `lambda` keyword is used to indicate that this is a lambda expression.
2. Following `lambda` are one or more arguments for the anonymous function separated by commas, followed by a colon `:`. Similar to functions, the way the arguments are named in a lambda expression is arbitrary.
3. Last is an expression that is evaluated and returned in this function. This is a lot like an expression you might see as a return statement in a function.

`map()` is a higher-order built-in function that takes a function and iterable as inputs, and returns an iterator that applies the function to each element of the iterable.

```python
numbers = [
              [34, 63, 88, 71, 29],
              [90, 78, 51, 27, 45],
              [63, 37, 85, 46, 22],
              [51, 22, 34, 11, 18]
           ]

averages = list(map(lambda num_list: sum(num_list) / len(num_list), numbers))
print(averages)
```

in this case `maps()` is getting the value of numbers (an iterable variable) and use it in the `lambda` expression, it will get the values in `numbers`  and will get the average.

`filter()` is a higher-order built-in function that takes a function and iterable as inputs and returns an iterator with the elements from the iterable for which the function returns True, here and example:

```python
cities = ["New York City", "Los Angeles", "Chicago", "Mountain View", "Denver", "Boston"]

short_cities = list(filter(lambda name: len(name) < 10, cities))
print(short_cities)
```
