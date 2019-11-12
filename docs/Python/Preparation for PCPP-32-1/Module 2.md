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

