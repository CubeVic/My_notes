
## Reset lost admin password for Raspberry Pi

I run into several problems when i was trying to connect with the raspberry using VNC viewer, this time was because i forgot the password that I set up so i found a way to reset the password.

### With access to the desktop raspberry

If we have access to the desktop or to the terminal of the raspberry we will need just to use the command
```bash
passwd pi
```

It will ask for the new password and later the confirmation.

### Without access to the desktop

We we don't have access at all we will need to modify some files in the SD card

1. Power down the unit, remove the SD card, and put it in a computer.
2. Open the file **cmdline.txt** and add`init=/bin/sh/`.
3. Put the SD card in the unit again and boot it up.
4. when the unit boot up type `su` that will log you as root but you wont need the password.
5. type ```passwd pi```
6. Power down the unit, remove the SD card, use the computer again and remove the line `init=/bin/sh/`. in the **cmdline.txt**.

If the process is not working it might be because the boot process is in read-only, in that case is is necessary to write in the terminal
```bash
mount -o remount,rw/
```
You will need access to the terminal in order to type that command.
