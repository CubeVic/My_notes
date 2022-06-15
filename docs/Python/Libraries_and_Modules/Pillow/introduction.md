#Pillow - Python Imaging Library (Fork)

![Pillow_logo](images/pillow_logo.png){:.center}

>Pillow is the friendly PIL fork by Alex Clark and Contributors. PIL is the Python Imaging Library by Fredrik Lundh and Contributors. As of 2019, Pillow development is supported by Tidelift.

1. [Pypi page](https://pypi.org/project/Pillow/)
2. [Documentation](https://pillow.readthedocs.io/en/stable/)

Form the librtary description we know that this is a library that give image processing capabilities to python 

## How I use it/ How I find it

I was working in my personal project `Project_Horus` and i was getting the thumbnail and snaposhot of a CCTV camera using other libraries, but this snapshot and the thumbnail where given in bytes, so i need it something to render and display the image so: 

1. I imported the library
```python
from PIL import Image
import io
```
2. open and read the bytes, `snapshot` is a variable holding the bytes
```python 
	#read the bytes
	im = Image.open(io.BytesIO(snapshot))
	#display the image
	# im.show() 
	#display the thumbnail
	thumbnail_size = 128,128
	im.thumbnail(thumbnail_size)
	im.show()
```
