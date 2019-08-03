In this case we are going to create and script that will allow me to use the mouse to draw different shapes.

## Connecting a Function for Drawing

We will need to create the 'canvas', later connect the functions to support hte mouse and a way to close the window.
We will build the script step by step.

### Basic structure 

1. We are going to import the libraries 
2. Create the 'canvas' to draw
3. A loop to keep the window open and a way to close it
4. Destroy all the windows 

```python
import cv2
import numpy as np


#Create the 'Canvas'
black_img = np.zeros((512,512,3), np.uint8)


#Create a loop to keep the windows open and a way to close it
while True:

	if cv2.waitKey(20) & 0xFF == 27:
		break

#Destroy all windows
cv2.destroyAllWindows()
```

### Giving a name to the window

1. giving a name to the window
2. show the window 

```python
import cv2
import numpy as np



black_img = np.zeros((512,512,3), np.uint8)

#giving a name to the window
cv2.namedWindow(winname='my_drawing')

while True:

	#Showing the window
	cv2.imshow('my_drawing',black_img)

	if cv2.waitKey(20) & 0xFF == 27:
		break

#Destroy all windows
cv2.destroyAllWindows()
```

### link the Window to the event and set the mouse callback

1. Set the mouse callback
2. Create the function called for that callback
3. Define the event, or what is the result of the event

```python
import cv2
import numpy as np

# 2. Create the function

def draw_circle(event,x,y,flags,param):
	# 3. Define de event
	if event == cv2.EVENT_LBUTTONDOWN:
		cv2.circle(black_img,(x,y),100,color=(0,255,0),-1)


black_img = np.zeros((512,512,3), np.uint8)
cv2.namedWindow(winname='my_drawing')

# 1. set the mouse callback
cv2.setMouseCallback('my_drawing',draw_circle)

while True:
	
	cv2.imshow('my_drawing',black_img)

	if cv2.waitKey(20) & 0xFF == 27:
		break


cv2.destroyAllWindows()
```

the result 

![023_drawing_circles](../images/023_drawing_circles.png)

## Adding functionality with Event Choices

Now, we are going to use other event to provide additional functionality, in this case we are going to use the right button to make a circle with other color.

1. Add a `elif`
2. Use other event to draw a circle with other color

```python
import cv2
import numpy as np



def draw_circle(event,x,y,flags,param):
	if event == cv2.EVENT_LBUTTONDOWN:
		cv2.circle(black_img,(x,y),100,(0,255,0),-1)
	# Define new event 
	elif event == cv2.EVENT_RBUTTONDOWN:
		cv2.circle(black_img,(x,y),50,(0,0,255), -1)


black_img = np.zeros((512,512,3), np.uint8)
cv2.namedWindow(winname='my_drawing')


cv2.setMouseCallback('my_drawing',draw_circle)

while True:
	
	cv2.imshow('my_drawing',black_img)

	if cv2.waitKey(20) & 0xFF == 27:
		break


cv2.destroyAllWindows()
```

![024_drawing_circles](../images/024_drawing_circles.png)


## Dragging with Mouse

In this case we are going to use the rectangle, we will need to create some variable to keep track of the status of the 'drawing', in other words, when the user stop drawing, also some variable for the initial $x$ and $y$ points.

```python 
import cv2
import numpy as np

#create a function base in the CV2 events 

drawing = False # true if the mouse is press
ix,iy = -1,-1  # this variable will keep track of the initial point 

def draw_rectangle(event,x,y,flags,param):
	global ix,iy,drawing,mode

	if event == cv2.EVENT_LBUTTONDOWN:
		drawing = True
		ix,iy = x,y

	# with this event we will see the the rect getting bigger or smaller when we drag it
	elif event == cv2.EVENT_MOUSEMOVE:
		if drawing ==  True:
			cv2.rectangle(black_img,(ix,iy),(x,y),(0,255,0),-1)
	# here we finished drawing 
	elif event == cv2.EVENT_LBUTTONUP:
		drawing = False
		cv2.rectangle(black_img,(ix,iy),(x,y),(0,255,0),-1)


# Create the 'canvas'

black_img = np.zeros((512,512,3), np.uint8)
cv2.namedWindow(winname='my_drawing')
cv2.setMouseCallback('my_drawing', draw_rectangle)

while True:

	cv2.imshow('my_drawing', black_img)

	if cv2.waitKey(1) & 0xFF == 27:
		break

cv2.destroyAllWindows()
``` 

The result is:


![025_drawing_rectangles](../images/025_drawing_rectangles.png)
