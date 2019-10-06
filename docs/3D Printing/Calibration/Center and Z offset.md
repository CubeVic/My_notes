base in  https://www.youtube.com/watch?v=y_1Kg45APko&feature=youtu.be
and https://3dprinting.stackexchange.com/questions/6375/how-to-center-my-prints-on-the-build-platform-re-calibrate-homing-offset/6376#6376

http://marlinfw.org/docs/gcode/M851.html

http://marlinfw.org/docs/gcode/M501.html

http://marlinfw.org/docs/gcode/M503.html

http://marlinfw.org/docs/gcode/G000-G001.html


http://marlinfw.org/docs/gcode/M206.html

Z-Offset Instructions:

Home 3D printer
M851 Z0 - Reset Z0Offset
M500 - Store setting to eeprom
M501 - Set active parameters
M503 - Display Active Parameters
G28 Z - Home Z Axis
G1 F60 Z0 - Move nozzle to true 0 offset
M211 S0 - Switch off soft endstops
Move nozzle towards bed slowly until the paper can barely move
Take note of the Z on the printer display (take that number and add the measurment of the calibration sheet or device used)
M851 Z X.XX (X.XX being your z offset achieved)
M211 S1 - Enable Soft Endstops
M500 - Save settings to Eeprom
M501 - Set Active Parameters
M503 - display current settings