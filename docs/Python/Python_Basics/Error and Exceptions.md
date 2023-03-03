## Error and Exceptions

* **Syntax errors** occur when Python can’t interpret our code, since we didn’t follow the correct syntax for Python. These are errors you’re likely to get when you make a typo, or you’re first starting to learn Python.

* **Exceptions** occur when unexpected things happen during execution of a program, even if the code is syntactically correct. There are different types of built-in exceptions in Python, and you can see which exception is thrown in the error message.

## `try` statement
We can use `try` statement to catch exceptions and define how to handle it, the `try`  statement has for parts:

* `try`: this is the only mandatory clause in a `try` statement. this is the first block python will run (and is where we suspect can be and error).
* `except`: if Python runs into an exception while running the `try` block, it will jump to the `except` block that handle the exception ( they are different type of exception that i will mention down).
* `else`: if Python runs into no exception while running the `try` block, it will run the code in this block after running the `try`.
* `finally`: before Python leave the `try` block, it will run the code in the `finally` block.

an example of the simple `try` will be:

```python
while True:
	try:
		x = int(input("Enter a number: "))
		break
	except:
		print("Please enter a number")
	finally:
		print("Attempt input")
```

so, in the previous code if the user enter other value that a valid `int` the `except` block will be run and after that the code in `finally`

now, if the user try to stop the execution using the `ctrl + c` in the terminal the `except`  block will be run, to avoid this we can select specific exceptions to be capture.

## Specifying Exceptions

the exception to handle can be specify in the code, for example:

```python
try:
	# some code
except valueError:
	#some code
```

Now, in this case the `except` block will catch the exception `ValueErrror` but not other exception. We can catch the exception `KeyboardInterrupt` at the same time ( this apply to other exception not this two)

```python
try:
	# some code
except (ValueError, KeyboardInterrupt):
	# some code
```

in the previous case the exception are going to be handle in the same way, but if we required different response to a different exception, it can be done in the following way:

```python
try:
	#some code
except ValueError:
	#some code
except KeyboardInterrupt:
	# some code
```
## Accessing Error Messages

Previously we saw how to handle the error, basically how to avoid the program crash when a error appears, but we don't get information about the error, but, there is a way to display this errors, and it is as follow:

```python
try:
	# some code
except ZeroDivisionError as e:
	#some code
	print("ZeroDivisionErro occurred: {}".format(e))
```

this would print something like this:

```
ZeroDivisionError occurred: integer division or modulo by zero
```

so in that way you can handle errors, preventing the program for crashing and at the same time get information about the error.

In those case where there are not specific errors to handle, you can use a general form to access to those messages:

```python
try:
	#some code
except Exception as e:
	#some code
	print("Exception occurred: {} ".format(e))
```

for more information about exception check this [link](https://docs.python.org/3/library/exceptions.html#bltin-exceptions)
