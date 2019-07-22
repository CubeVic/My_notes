There are 7 steps in this installation, and a small project that include the raspberry camera, we will expand the file system and free some space removing some programs that we are not going to use.

## Step 1: Expanding filesystem on the Raspberry Pi

 The first thing will be expand the filesystem on the raspberry to make use of all the available space in the micro-sd card:

```
$ sudo rasp-config
```

we are going to access to the configuration, after the command a menu will be display and we can select the option "Advance Options"


![001_Advance_Options](../images/001_Advance_Options.jpg)

next, we select the option "Expand filesystem"

![002_Expand_filesystem](../images/002_Expand_filesystem.lpg)

once we select we option we can go t **<Finish>** and reboot the unit

```
$ sudo reboot
```
after the reboot the available space will expand, this can be verify using the command `df -h` 

![003_df_command](../images/003_df_command.png)

This might not be enough, therefore we will proceed to remove libreOffice and Wolfram engine to make more room.

```
$ sudo apt-get purge wolfram-engine
$ sudo apt-get purge libreoffice
$ sudo apt-get clean
$ sudo apt-get autoremove
```

## Step 2: Installing OpenCV 4 dependencies on Raspberry pi

We start by updating and upgrading the system

```
$ sudo apt-get update && sudo apt-get upgrade
```
this process might take some time 

after this, we proceed to include the developer tools on [CMake](https://cmake.org/)

```
$ sudo apt-get install build-essential cmake unzip pkg-config
```

[Resource](https://www.pyimagesearch.com/2018/09/26/install-opencv-4-on-your-raspberry-pi/)