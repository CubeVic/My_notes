## What are G-code Commands?

G-code stands for **"Geometric code"**, it is a rudimentary programing language, a numerical control programing language, that lacks of data structure such as variable, control blocks as conditionals and loops, its main function is to provide instruction to the machine  of how to move in the 3 geometrical dimension, how ever it can send non-geometric instruction, like  heat the bed, extrude specific amount of material at a specific extrusion rate, etc.

## How to read G-code Commands?

A typical G-code line will look like:

```
G1 X-10 Y4.5 Z0.5 F30000.0 E 0.0377
```

This line tell the machine to move in a straight line toward the coordinates `X-10`, `Y4.5`, `Z0.5` at a feed rate of `3000.0` and extrude `0.0377mm` of material while moving.

But how to read it, well each line start with a specific code, in this case the code is `G1`, which it means "move in a straight line in a controlled fashion".

```
G1 X-10 Y4.5 Z0.5 F30000.0 E 0.0377
```

The values after the code are the arguments, it start with a English letter and then the value:

* `XYZ` Are values for the Cartesian coordinates 
* `F` is the Feed rate
* `E`  is the Extrusion

So the code:
```
G1 X2 Y4 Z0 F30000.0 E 0.02
```

Reads "*Move towards X=2,Y=4, Z=0 in a straight line in a control fashion at a feed rate 3000.00 while extruding 0.02mm of material*".

SOmething that help use to understand the code faster, is the fact that all g-code that start with **G** is code related with geometric commands. But a machine do more that geometric movements, there fore we have another type of commands, Non-geometroc and those command start with M.

Each English letter in a G-code has an specific meaning here a reference table from [reprap](https://reprap.org/wiki/G-code#Fields), for example G for Geometric commands, M for Non-geometric, X means $x$ coordinate, Y $y$ coordinate, Z  $z$ coordinate, F means feed rate, E Extruder, etc

> `G1` command means “move the nozzle in a controlled fashion in a straight line”