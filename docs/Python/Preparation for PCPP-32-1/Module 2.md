## Function

A function in the context of Python is separate part of code that is able to do:

* **Cause some effect** as an example the function `print()` allow use to display something in the console
* **Evaluate a value or some values** this is closer to the definition of function in mathematics

A function in python can do one of the previous mentioned things or it can do both at the same time.


A function might be include it in python, the so call **Build-in** functions, can be an add-on, and might required installation, or can be done by ourselves.

For the name of the function, if those are created by use, we need to pay attention to the name, the name must be **self-Evident** or significant.

### Anatomy of a function 

The function will have 3 components:

* An Effect.
* A Result.
* An Argument or Arguments. 

Python functions can take none, one or more arguments. A standard convention that we need to follow are the pair of parenthesis ad the end of the function's name.

```
print("Hello, World!")
```

in this example the parameter is a *string* this is one of the data types present in python, as it is shown in the example the *string* is delimited by quotes.

The **Invocation** of a python function will be

```
function_name(argument)
```
the work flow will be as follow:

1. Python check if the name of the function is legal or if it exist within its domain.  
2. Python check if the function's requirements for the number and type of argument is correct
3. Python leave the current part of the code momentarily and jump to the function.  
4. Python execute the code, causes the desired effect (if any), evaluates the results (if any) and finished the task
5. Python return to the main code and resume the execution.

### Keyword arguments

This are special arguments that can be pass to the function, these arguments can modify the behavior of the function, as and example:

```python
print("My name is", "Python.", end=" ")
print("Monty Python.")
```
the result is 

```
My name is Python. Monty Python.
```
Which is different for the normal behavior

in order to use this arguments we need some rules:

* the keyword arguments consist of three elements the keyword, in this case `end` the equal `=` and the value, in this case `" "`
* the keyword argument must be add at the end of the last positional argument.

In this case the keyword argument modify the behavior of the `print()` function, by default at the end of this function it is a change of line, but in this case we change it to a space.

For the `print()` function we have other keyword argument, in this case is `sep` this argument will modify the way python separate each argument pass to the function, example:

```python 
print("My", "name", "is", "Monty", "Python.", sep="-")
```

will give as a result:
```
My-name-is-Monty-Python.
```

## Literals 

The closest definition for literals is the word itself, it is a literal value, for example, lets check this two values:

```
123
```
and 
```
c
```

the first one it is $123$ the second will be more difficult, it can be the speed of light or the hypotenuse in a Pythagorean theorem.

In this case what is the literal? $123$ is the literal and `c` it is not.

### Mode about literals

Lets see the following example
```python
print("2")
print(2)
```
if we execute the code we will see the same number, but these two are not the same, the first one is a "String" a series of characters the second is a numerical value, python will take this numerical value and will converted to machine representation ( bits ).

### Notes about integer notation

In case we need to make a integer in a base different from the decimal, let say octal or hexadecimal we can use the notation that python provide.

#### Octal 
For octal we ca us de prefix `0o`, for example `0o123` ( that is 83) we can print it like this:

```python
print(0o123)
```

#### Hexadecimal

For the hexadecimal we will use `0x` example, `ox123` ( that is 291), we can print it like this:

```python
print(0x123)
```