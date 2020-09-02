## Iterators And Generators

Iterables are objects that can return one of their elements at a time, such as a list. Many of the built-in functions we’ve used so far, like 'enumerate,' return an iterator.

An iterator is an object that represents a stream of data. This is different from a list, which is also an iterable, but is not an iterator because it is not a stream of data.

Generators are a simple way to create iterators using functions. You can also define iterators using classes, here [documentation](https://docs.python.org/3/tutorial/classes.html#iterators) about it 

Here is an example of a generator function called my_range, which produces an iterator that is a stream of numbers from 0 to (x - 1).

```python
def my_range(x):
    i = 0
    while i < x:
        yield i
        i += 1
```

Notice that instead of using the return keyword, it uses yield. This allows the function to return values one at a time, and start where it left off each time it’s called. This yield keyword is what differentiates a generator from a typical function.

we can use  the for loop to iterate over the iterator.

```python
for x in my_range(5):
    print(x)
```

outputs:

```
0
1
2
3
4
```

Another example will be the implementation of the built-in function `enumerate`

having this:

```python
lessons = ["Why Python Programming", "Data Types and Operators", "Control Flow", "Functions", "Scripting"]

for i, lesson in my_enumerate(lessons, 1):
    print("Lesson {}: {}".format(i, lesson))
```
 
We need to output:

```
Lesson 1: Why Python Programming
Lesson 2: Data Types and Operators
Lesson 3: Control Flow
Lesson 4: Functions
Lesson 5: Scripting
```

so the code will be:

```python
lessons = ["Why Python Programming", "Data Types and Operators", "Control Flow", "Functions", "Scripting"]

def my_enumerate(iterable, start=0):
    # Implement your generator function here
   count = start
   for item in iterable:
    	yield count, item
    	count += 1
   
for i, lesson in my_enumerate(lessons, 1):
    print("Lesson {}: {}".format(i, lesson))
```

## Chunker 
If you have an iterable that is too large to fit in memory in full (e.g., when dealing with large files), being able to take and use chunks of it at a time can be very valuable.

Implement a generator function, `chunker`, that takes in an iterable and yields a chunk of a specified size at a time.

```python
def chunker(iterable, size):
    """Yield successive chunks from iterable of length size."""
    for i in range(0, len(iterable), size):
        yield iterable[i:i + size]

for chunk in chunker(range(25), 4):
    print(list(chunk))
```

Output:

```
[0, 1, 2, 3]
[4, 5, 6, 7]
[8, 9, 10, 11]
[12, 13, 14, 15]
[16, 17, 18, 19]
[20, 21, 22, 23]
[24]
```
## Why Generators?

Generators are a lazy way to build iterables. They are useful when the fully realized list would not fit in memory, or when the cost to calculate each list element is high and you want to do it as late as possible. But they can only be iterated over once.

## Generator Expressions

Here's a cool concept that combines generators and list comprehensions! You can actually create a generator in the same way you'd normally write a list comprehension, except with parentheses instead of square brackets. For example:

```python
sq_list = [x**2 for x in range(10)]  # this produces a list of squares

sq_iterator = (x**2 for x in range(10))  # this produces an iterator of squares

```
