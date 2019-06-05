## What are convolutions and pooling

One thing, we can see from the previous exercise is that there is a lot of wasted space in each image. while there are only 784 pixels, it will be interesting if there is a way to condense this image to those important features that make a bag, a shoe or a bag, that's is where convolutions come in.

###What is convolution?

To use an analogy, in image processing normally involve having a filter and passing that filter over the image in order to change the underlying image.
The convolution will work in a similar way.
 ![Convolution](../images/convolution.png)

**The process** will be a little bit like this:

* For every pixel, take its value, and take a look at the value of its neighbors. let say 192 in the image above.

```
|   0    |    64    |   128  |
|--------|----------|--------|
|   48   |    192   |   144  |
|--------|----------|--------|
|  142   |    226   |   168  |
```


* If the filter is $3x3$, then we can take a look at the immediate neighbor, so we will have a corresponding $3x3$ grid.

```
|   -1   |    0     |   -2   |
|--------|----------|--------|
|  0.5   |    4.5   |  -1.5  |
|--------|----------|--------|
|  1.5   |    2     |   -3   |
```

* Now we can get the new value for the pixel, we simply multiply each neighbor by the corresponding value in the filter.

$$ Current pixel = 192$$

$$ New pixel = (-1 * 0)+(0 * 64)+(-2 * 128)+(0.5 * 48)+(4.5 * 192)+(-1.5 * 144)+(1.5 * 142)+(2 * 226)+(-3 * 168) $$

* we have the new pixel with the sum of each of the neighbor values multiplied by the corresponding filter value, and that's a convolution. 


The idea here is that some convolutions will change the image in such a way that certain features in the image get emphasized. So, for example, if you look at this filter. 

![vertical line](../images/vertical_line.png)


Then the vertical lines in the image really pop out.

![horizontal line](../images/horizontal_line.png)

Now with this filter, the horizontal lines pop out. 

When convolution is combine with something call *pooling* they will become really powerful, a quick and easy way to do this, is to go over the image of four pixels at a time, of these four, pick the biggest value and keep just that. So, for example: 

![pooling](../images/pooling.png)

So 16 pixels on the left are turned into the four pixels on the right, by looking at them in two-by-two grids and picking the biggest value. This will preserve the features that were highlighted by the convolution, while simultaneously quartering the size of the image. We have the horizontal and vertical axes.

