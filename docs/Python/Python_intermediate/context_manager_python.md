In other programming languages we use the `try/expect/finally` block to handle resource or to manage those resources, in python we can use the `with` statement and context managers to simplify that operation 

Here and example in of how `try` statement is use to handle open and close a file 

```python 
try:
	f = open('text.txt','r')
	print(f.read())
finally:
	f.close()
```

Now the same operation but using the `with` statement 

```python 
with open('text.txt','r') as f:
	print(f.read())
``` 

the context manager will take care of opening the file and later close it when we are done.

## Usages of `with` statement 

#### Database 
```python 
def database_example():
	with sqlite3.connect('db/test.db') as connection:
		cursor = connection.cursor()
		cursor.execute("SELECT * FROM test ORDER BY id desc")
		test_data = cursor.fetchall()
		return test_data
``` 

#### Locks
```python 
lock = threading.Lock()
with lock:
	#do something
``` 

#### TensorFlow
```python 
#using the context manager
with tf.Session() as sess:
	sess.run(...)
``` 

## Context Manager

Although the definition of context manager was a bit confusing for me the first time i read it, it make sense with the time. A *context Manager* is an object that defines the runtime context to be establish when executing a `with` statement.

The context manager will handle the enter *into*, and exit *from* a desired runtime.

#### The Syntax
```python 
with EXPR as VAR:
	Block
``` 

* `with` and `as` are keywords 
* `VAR` is just a variable it can be use to call the result of the expression
* `Block` just the block of code.

## Implementing a Context manager

Like in everything we can create our own implementation of a context manager. There are two ways to do it:

* User-defined classes. 
* Generators. 

### User-defined Classes 
to implement a context manager we will need to create a class that contain two methods `__enter__()` and `__exit__()`.

```python 
class OpenFile(object):
  
  def __init__(self, file_name, mode):
    print('calling __init__ Method')
    self.file_name = file_name
    self.mode = mode
    self.file = None
    return
    
  def __enter__(self):
    print('calling __enter__ Method')
    self.file_handler = open(self.file_name, self.mode)
    return self.file_handler
  
  def __exit__(self, exc_type, exc_val, traceback):
    print('calling __exit__:', exc_type, exc_val, traceback)
    if self.file_handler:
      self.file_handler.close()
    return True

# Using OpenFile 
with OpenFile('test.txt', 'r') as f:
  print('Read a file:')
  print(f.read())
  
  
# test.txt
# Hello World, Implementing the Context Manager as a Class.
  
# Expected Output:
# calling __init__ Method
# calling __enter__ Method
# Read a file:
# Hello World, Implementing the Context Manager as a Class.
# calling __exit__: None None None
``` 

Few things to remark in the example:

1. We have two variables `file_name` and `mode`. `mode` is how we wnat to open the file, write mode or read mode.
2. In the method `__enter__()` we open the file.
3. In the method `__exit__()` whe make sure to close the file.

In some cases we can use this implementation to handle exceptions.

### Implementing the context manager with generator

To implemented in this way we will need the library `contextlib.contextmanager` this library will provide a decorator `@contextmanager`  If a generator function is decorated with the `contextlib.contextmanager` decorator, it will return a context manager implementing the necessary` __enter__()` and `__exit__()` methods.

```python 
from contextlib import contextmanager

@contextmanager
def open_file(filename, mode):
    try:
        # __enter__ method
        f = open(filename, mode)
        # yield method 
        yield f
    finally:
        # __exit__ method
        f.close()

with open_file('test.txt', 'r') as f:
    print(f.read())
    
# Expect output:
# Hello World, Implementing the Context Manager as a Class.
``` 
The Python interpreter recognizes the yield statement in the middle of the function definition. The code before the yield statement is equivalent to`__enter__()` method. and the code after the yield statement is equivalent to`__exit__()` method.




