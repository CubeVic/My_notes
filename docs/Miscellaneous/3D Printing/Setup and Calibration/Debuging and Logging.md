## Debug

### `M111` - Debug Level

There are several debug bits, to enable it is necessary add up the bits need it

|Mask	   | Name 		|  	Description 	|
|:---------|:-----------|:------------------|
|1		   | ECHO       | Echo all commands sent to the parser.	|
|2		   | INFO		| Print extra informational messages.|
|4		   | ERRORS		| Print extra error messages.|
|8		   | DRYRUN 	| Don’t extrude, don’t save leveling data, etc.|
|16		   | COMMUNICATION| Not currently used.|
|32		   | LEVELING	|Detailed messages for homing, probing, and leveling. (Requires ```DEBUG_LEVELING_FEATURE```.)  |
|64        | Reserved	|  Reserved for future usage|
|128       | Reserved	|  Reserved for future usage|

#### Usage ```M111```
```
M111 [S<flags>]
```

* ```[S<flags>]``` debug flag  bits

>Example:

Enable extra messages

```M111 S38 ; LEVELING, ERRORS, INFO```

Enable everything except dry-run mode

```M111 S247 ; 255 - 8 ```

Disable previously set extra debugging output.

```M111 S0 ```


source: [M111](http://marlinfw.org/docs/gcode/M111.html)

### `M280` - Servo Position

Set or get the position of a servo.

#### Using ```M280```
```
M280 P<index> S<pos>
```

* ```P<index>``` Servo index to set or get

* ```S<pos>```	Servo position to set. Omit to read the current position.

source: [M280](http://marlinfw.org/docs/gcode/M111.html)


## Logging

This are G-code to get the logs of the printer or the board.

### ```M928``` - Start SD Logging


Use this command to start logging all console and host input into the SD card

> use ```M29``` to stop logging

#### Usage ```M928```
```
M928 filename
```

* *filename*  File name of log file

> Example:
```M928 log.txt```

source: [M928](http://marlinfw.org/docs/gcode/M928.html)

### ```M28``` - Start SD Write

This Commands start a file write, the firmware will log all commands, this command wont be execute until ```M29``` closes the file.

> Required ```SDSUPPORT```
To write file while printing use ```M928```

#### Usage ```M28```
```
M28 filename
```
* *filename*  File name of log file

> Example:
```M28 file.txt```

source: [M28](http://marlinfw.org/docs/gcode/M028.htmll)

### ```M29``` - Stop SD Write

Stop Writing to file begun with ```M28``` or ```M928```

> Require ```SDSUPPORT```

#### Usage ```M28```
```
M29
```

source: [M29](http://marlinfw.org/docs/gcode/M029.html)
