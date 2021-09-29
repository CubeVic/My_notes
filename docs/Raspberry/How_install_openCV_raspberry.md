

# How to install OpenCV on Raspberry pi

I will divide the process into seven steps.

## Step 1: Expanding filesystem on the Raspberry Pi

The raspberry won't be using all the space available. It will have a directory structure by default. The first step will be to expand that directory to get more space  in the micro-sd card: 

### Access the raspberry configuration menu
To access the configuration, I need to type on the terminal the following command.
```
$ sudo raspi-config
```

After entering the command, a configuration menu appears on the screen. 
This menu allows us to change some configurations. 
Using the arrow keys,  I navigate to `Advance Options`.

![001_Advance_Options](images/001_Advance_Options.jpg)

Next, I select the option "Expand filesystem".

![002_Expand_filesystem](images/002_Expand_filesystem.jpg)

Finally, **<Finish>** and reboot the unit.

```
$ sudo reboot
```
After the reboot, the available space will expand. To verify it, I use the command `df -h`.

![003_df_command](images/003_df_command.png)

### Deleting software unuse to release more space. 
Depending on the OS installed, might not be enough space. I can get some extra space if I remove some of the software installed. To remove the software, I can use the terminal. I will remove libreOffice and Wolfram engine.

```
$ sudo apt-get purge wolfram-engine
$ sudo apt-get purge libreoffice*
$ sudo apt-get clean
$ sudo apt-get autoremove
```
> dpkg-query -l  will provide a list all the programs installed, I can remove the following:   
* wolfram-engine.  
* bluej.  
* greenfoot.  
* nodered.  
* nuscratch.  
* scratch.  
* sonic-pi.  
* libreoffice.  
* claws-mail.  
* claws-mail-i18n.  
* minecraft-pi.  
* python-pygame.  

## Step 2: Installing OpenCV 4 dependencies on Raspberry pi

I start by updating and upgrading the system.

```
$ sudo apt-get update && sudo apt-get upgrade
```
>This process might take some time 

### Install developer tools (CMake)
After updating, I have to include the developer tools on [CMake](https://cmake.org/)

```
$ sudo apt-get install build-essential cmake unzip pkg-config
```

### Install libraries to handle video and image.

I'm going to install libraries to work with videos and images.

```
$ sudo apt-get install libjpeg-dev libpng-dev libtiff-dev
$ sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
$ sudo apt-get install libxvidcore-dev libx264-dev
```
### Install GTK
>[GTK](https://www.gtk.org/) is a UI tool kit used to render the different components for a UI.

The next step will be to Install GTK and GUI backend.  I will install an additional package that reduces the GTK warnings.

```
$ sudo apt-get install libgtk-3-dev
$ sudo apt-get install libcanberra-gtk*
```

Now two more packages, one for numerical optimization other for python development headers.

```
$ sudo apt-get install libatlas-base-dev gfortran
$ sudo apt-get install python3-dev
```

## Step 3: Download OpenCV 4 for Raspberry pi

There are two things to download, the `opencv` and the `opencv_contrib`. 
Bellow the code to download the libraries and unzip them. It is a good practice to rename the directories.

```
$ cd ~
```
I will download the zip from github directly
[opencv](https://github.com/opencv/opencv)
[opencv_contrib](https://github.com/opencv/opencv_contrib)
To unzip

```
$ unzip opnecv.zip
$ unzip opencv_contrib.zip
```
To rename

```
$ mv opencv-4.0.0 opencv
$ mv opencv_contrib-4.0.0 opencv_contrib
```
> `opencv_contrib`  is a repository with additional or extra modules to increase the functionality.
 
## Step 4: Python 3 virtual environment for OpenCV 4

### Get PIP
I will use PIP to make the installation of python packages easier.

```
$ sudo apt-get install python3-pip
```

### Install the virtual environment
I will divide the installation into two parts. In the first part, I get the libraries with `pip`. In the second part, I will add the package to the system path.

```
$ sudo pip3 install virtualenv virtualenvwrapper
```

### Create the virtual environment 

I will  create the virtual environment with the commands as follow:

```
$ virtualenv -p python3 cv
```
The virtual environment is called `cv`

Install Numpy 
```
$ pip3 install numpy
```

### Step 5: Cmake and compile OpenCV 4

#### Increase the SWAP on the raspberry 
This increase will help with the compilation and avoid issues with memory.

open `/etc/dphys-swapfile` :
```
$ sudo nano /etc/dphys-swapfile
```

and add:

```
# set the size to absolute value, leaving empty (default) then uses computed value
#   you most likely don't want this, unless you have a special disk situation
# CONF_SWAPSIZE=100
CONF_SWAPSIZE=2048
```

restart the swap service:
```
$ sudo /etc/init.d/dphys-swapfile stop
$ sudo /etc/init.d/dphys-swapfile start
```
> Be aware the increase in the size of SWAP might affect the MicroSD card. It is worthy to remember SD cards have a limited number of write and read. It is a good idea to make a copy of the image including OpenCV and python in case the SD card fails.

#### Run CMake for OpenCV
I will use the Cmake command `make` to compile OpenCV.
> This is a time-consuming task
```
$ cd ~/opencv
$ mkdir build
$ cd build
```
The following code will configure the OpenCV 4 build.

```
$ cmake -D CMAKE_BUILD_TYPE=RELEASE \
    -D CMAKE_INSTALL_PREFIX=/usr/local \
    -D OPENCV_EXTRA_MODULES_PATH=~/opencv_contrib/modules \
    -D ENABLE_NEON=ON \
    -D ENABLE_VFPV3=ON \
    -D BUILD_TESTS=OFF \
    -D OPENCV_ENABLE_NONFREE=ON \
    -D INSTALL_PYTHON_EXAMPLES=OFF \
    -D BUILD_EXAMPLES=OFF
```

Once it is finished, it is a good idea to check the result or the output:

-------image output ------

#### Compile OpenCV4

Compile the OpenCV
```
$ make -j4
```

The `-j4`  argument specifies that I have 4 cores for compilation. if there are problems with the compilation try `make` without `-j4`.

#### Install OpenCV 4

```
$ sudo make install
$ sudo ldconfig
```

#### DON'T FORGET  to reset the SWAP size 
 open the file with `/etc/dphys-swapfile` and reset `CONF_SWAPSIZE` to 100MB, reset the swap service 

```
$ sudo /etc/init.d/dphys-swapfile stop
$ sudo /etc/init.d/dphys-swapfile start
```

### Step 6: Link OpenCV to python virtual environment 

This step is important.

```
$ cd ~/.virtualenvs/cv/lib/python3.5/site-packages/
$ ln -s /usr/local/python/cv2/python-3.5/cv2.cpython-35m-arm-linux-gnueabihf.so cv2.so
$ cd ~
```

### Step 7: Test OpenCV

Using the terminal

```
$ workon cv
$ python
>>> import cv2
>>> cv2.__version__

```



[Resource](https://www.pyimagesearch.com/2018/09/26/install-opencv-4-on-your-raspberry-pi/)

