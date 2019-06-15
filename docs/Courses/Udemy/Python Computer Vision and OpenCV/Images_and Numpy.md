> in this case i will use Jupyter lab for the code, so the code in this document will have some parts specific for Jupyter lab, additionally the course gave me some images that i will use, so i will refer to those images too.

First we need to remember that python alone is not able to handle the images, it needs a library to do so, in this case we are going to use [`PLI` or `pillow`](https://pillow.readthedocs.io/en/stable/installation.html)

## Get the image with Python

so in this case we are going to use the function `open()` to get the image, in the next step we will transfor the image in a Numpy array

```python
import numpy as np
import mathplotlib.pyplot as plt
%matplotlib inline #--> this line is just for Jupyter Lab, in order to disply images
```
We imported the mathplotlib in order to display the image in the Jypyter lab, now we are going to import `Image` from `PIL`

```python
from PIL import Image
```
 next, we need to load the image

```python
import numpy as np
import mathplotlib.pyplot as plt
%matplotlib inline #--> this line is just for Jupyter Lab, in order to disply images
from PIL import Image

pic = Image.open('path-to/the-image.jpg')

```
## Transform the image to a Numpy array

At this point the image is load but it

```python
pic = Image.open('Computer-Vision-with-Python/DATA/00-puppy.jpg')
type(pic)
# PIL.JpegImagePlugin.JpegImageFile
```

in this case we have a Jpeg Image file, now we need to transform it to Numpy array

```python
pic_arr = np.asarray(pic)
type(pic_arr)
# numpy.ndarray
```

with the function called `asarray` we transform this image field to a Numpy array.

##  Display the image with `imshow`

```python
pic_arr.shape
(1300, 1950, 3)
```
 in this case we have an array with 1300x1950 with 3 channels, this means, that the image is a color image, so, now lest display this array as an image

```python
 plt.imshow(pic_arr)
```
 you will get 

 ![001.image_from_npArray_using_matplotlib](../images/001.image_from_npArray_using_matplotlib.png)

 `plt.imshow(image_numpy_array)` the *plt.imshow* is a special function from  *matplotlib* use to display images that are in a Numpy array format.

 ### Inspect one of the color channels

 