##define

###Description
`#define` is a useful C++ component that allows the programmer to give a name to a constant value before the program is compiled. Defined constants in arduino don’t take up any program memory space on the chip. The compiler will replace references to these constants with the defined value at compile time.

**Unwanted side effects:** 
A constant name that had been `#defined` is included in some other constant or variable name. In that case the text would be replaced by the `#defined` number (or text).

The `const` keyword is preferred for defining constants and should be used instead of `#define`.

**Syntax**

```C++
#define constantName value
```

**Parameters:**

* *constantName:* the name of the macro to define.
* *value:* the value to assign to the macro.

####Example Code
```C++
#define ledPin 3
```