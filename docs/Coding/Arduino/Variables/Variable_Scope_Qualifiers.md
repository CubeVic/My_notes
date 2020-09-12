## Scope

Arduino use C++ for programing, have a property called **Scope**, a global variable is one that can be access by evey function on the program, local variable are just visible by the function in whihc they are declared. In the arduiono enviroment, any varivable declared outside ouside of the function( example: `setup()` and `loop()`, etc), is a **global** variable.

**Example**
```C++
int gPWMval; //any function will see this variable

void setup() {
	//...
}

void loop() {
	//...
}
```

## const

The keyword `const` is a constant. it is a variable *qualifier* that modify the behavior of the variable making a variable *"read-only"*.

The `const` keyword is a superior method for defining constants and is preferred over using `#define`.

**Example**
```C++
const float pi = 3.14;
float x;
// ..
x = pi * 2; // it's fine to use consts in math
pi = 7;     // illegal - you can't write to (modify) a constant
```

## static

The `static` keyword is used to create variables that are visible to only one function. but the difference with a normal variable that are create and destroy every time a function is called, static variables persist beyond the function call, preserving their data between function calls.

> Variables declared as static will only be created and initialized the first time a function is called.

```C++
static int count = 0;
```

