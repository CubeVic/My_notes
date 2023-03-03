
After change the board or flash a new firmware it is necessary center and set the offset for the Z

## Z-Offset Instructions:

1. Home 3D printer
2. ```M851 Z0``` - Reset Z0Offset
3. ```M500``` - Store setting to eeprom
4. ```M501``` - Set active parameters
5. ```M503``` - Display Active Parameters
6. ```G28 Z``` - Home Z Axis
7. ```G1 F60 Z0``` - Move nozzle to true 0 offset
8. ```M211 S0``` - Switch off soft endstops
9. take note of the current Z value and Move nozzle towards bed slowly until the paper can barely move
10. Take note of the new Z value on the printer display (*take that number and add the measurement of the calibration sheet or device used*)
11. ```M851 Z X.XX``` (X.XX being your z offset achieved)
12. ```M211 S1``` - Enable Soft Endstops
13. ```M500``` - Save settings to EEprom
14. ```M501``` - Set Active Parameters
15. ```M503``` - display current settings

base in  this [video](https://www.youtube.com/watch?v=y_1Kg45APko&feature=youtu.be)
and this [article](https://3dprinting.stackexchange.com/questions/6375/how-to-center-my-prints-on-the-build-platform-re-calibrate-homing-offset/6376#6376)


## G-code used

### ```M851``` - XYZ Probe Offset

Not totally clear for me how to make the procedure explained, specially when they mentioned that you can use ```define Z_PROBE_OFFSET_FROM_EXTRUDER``` to define the offset at firmware level, although ti is useful in the calibration procedure.

#### Usage ```M851```
```C
M851 [X<linear>] [Y<linear>] [Z<linear>]
```
>Example:
M851 Z0 - Reset Z0Offset

source: [M851](http://marlinfw.org/docs/gcode/M851.html)

### ```M500``` - Save settings

Save all configuration on the EEPROM

> SKR Mini E3 doesnt have a EEPROM there is several ways to overcome this, that is what Reddit says, one will be with a Virtual EEPROM other using the SD card as EEPROM.

It requires ``` EEPROM_SETTINGS```

#### Usage ```M500```
```
M500
```
source: [M500](http://marlinfw.org/docs/gcode/M500.html)


### ```M501``` -  Restore Settings

Load all saved settings from EEPROM

It requires ``` EEPROM_SETTINGS```
#### Usage ```M501```
```
M501
```
source: [M501](http://marlinfw.org/docs/gcode/M501.html)

### ```M503``` - Report Settings
Print a concise report of all current settings.

Does not require ``` EEPROM_SETTINGS```


#### Usage ```M503```
```
M503
```
source: [M503](http://marlinfw.org/docs/gcode/M503.html)

### ```G28``` - Auto Home
Auto-home one or more axis moving to the end-stop until triggered.

```G28``` disable bed leveling. follow with ```M420 s``` to turn leveling on, or use ```RESTORE_LEVELING_AFTER_G28```

#### Usage ```G28```
```
G28 [O] [R] [X] [Y] [Z]
```
* ```[X]```	Flag to go back to the X axis origin

* ```[Y]```	Flag to go back to the Y axis origin

* ```[Z]```	Flag to go back to the Z axis origin

> Example:
```G28 Z``` home the Z axis

source: [G28](http://marlinfw.org/docs/gcode/G028.html)

### ```G1``` - Linear move

```G0``` and ```G1``` suppose to be similar command, they generate a linear movement, but this command is queue and it is execute when there is a space in the queue, ``` G0 ``` it is use for movements that doesn't include the extrudor and ```G1``` for those that does

All the coordinates are given in millimeters by default (see [G20](http://marlinfw.org/docs/gcode/G020.html) if you want to change to inch)

#### Usage ```G1```
```
G0 [E<pos>] [F<rate>] [X<pos>] [Y<pos>] [Z<pos>]
G1 [E<pos>] [F<rate>] [X<pos>] [Y<pos>] [Z<pos>]
```
* ```[E<pos>]``` The length of filament to feed into the extruder between the start and end point

* ```[F<rate>]``` The maximum movement rate of the move between the start and end point. The feedrate set here applies to subsequent moves that omit this parameter.

* ```[X<pos>]	``` A coordinate on the X axis

* ```[Y<pos>]	``` A coordinate on the Y axis

* ```[Z<pos>]	``` A coordinate on the Z axis


source: [G1](http://marlinfw.org/docs/gcode/G000-G001.html)

### ```M211``` - software Endstops
Optionally enable and disabel software stop, this software stop prevent to go below 0


#### Usage ```M211```
```
M211 [S<flag>]
```

* ```S<flag>``` *flag* 0 for disable and 1 for enable

> Example:
```
M211 S0
```
source: [M211](http://marlinfw.org/docs/gcode/M211.html)
