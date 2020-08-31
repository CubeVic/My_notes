Similar to many other languages on Arduino we have control structures, some of this structure are: 

* [Do...while](https://www.arduino.cc/reference/en/language/structure/control-structure/dowhile/)
* [while](https://www.arduino.cc/reference/en/language/structure/control-structure/while/)
* [if](https://www.arduino.cc/reference/en/language/structure/control-structure/if/) [(if-else)](https://www.arduino.cc/reference/en/language/structure/control-structure/else/)
* [for](https://www.arduino.cc/reference/en/language/structure/control-structure/for/)
* [switch...case](https://www.arduino.cc/reference/en/language/structure/control-structure/switchcase/)
* [goto](https://www.arduino.cc/reference/en/language/structure/control-structure/goto/)

From this the new one (in comparison with python and swift ) will be the `goto`.

As other language we have ways to jump to return a value, go to the next item, or break the loop all together, for those task we have: 

* [return](https://www.arduino.cc/reference/en/language/structure/control-structure/return/)
* [break](https://www.arduino.cc/reference/en/language/structure/control-structure/break/)
* [continue](https://www.arduino.cc/reference/en/language/structure/control-structure/continue/)

I won't add much about `break`, `continue`, and `return` since they work like in another languages, same as some of the control structures. Although, I will add the syntax of some of those items, to quick reference.

## do...while

Work similar to `while` loop, with the exception the condition is evaluated at the end of the loop, so the loop aways run at least one time.

**Syntax**
```c++
do {
  // statement block
} while (condition);
```

**Example**
```c++
int x = 0;
do {
  delay(50);          // wait for sensors to stabilize
  x = readSensors();  // check the sensors
} while (x < 100);
```

## while

Like any other while loop, i will loop until the condition become `False`

**Syntax**
```c++
while (condition) {
  // statement(s)
}
```
**Example**
```c++
var = 0;
while (var < 200) {
  // do something repetitive 200 times
  var++;
}
```

## switch...case

"switch case controls the flow of programs by allowing programmers to specify different code that should be executed in various conditions"

* `var`: a variable whose value to compare with various cases. Allowed data types: `int`, `char`.
* `label1`, `label2`: constants. Allowed data types: `int`, `char`.

**Syntax**
```c++
switch (var) {
  case label1:
    // statements
    break;
  case label2:
    // statements
    break;
  default:
    // statements
    break;
}
```
**Example**
```c++
switch (var) {
  case 1:
    //do something when var equals 1
    break;
  case 2:
    //do something when var equals 2
    break;
  default:
    // if nothing else matches, do the default
    // default is optional
    break;
}
```

## goto

**Syntax**

**Example**