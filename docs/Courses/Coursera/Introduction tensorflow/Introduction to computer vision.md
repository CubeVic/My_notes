#Introduction to computer vision

so in the previous notes we use the numpy array as a way to provide the examples and the arrays for training the model, but in a real scenario hard coding the data wont be possible, in the following example we are going to use a data set call [fashion-mnist](https://github.com/zalandoresearch/fashion-mnist) and since this is a data set with 60.000 example for training and 10.000 examples for testing we will need to load the data in a different way.

Fortunately, it's still quite simple because Fashion-MNIST is available as a data set with an API call in TensorFlow. We simply declare an object of type MNIST loading it from the Keras database.

```python
fashion_mnist = keras.dataset.fashion_mnist
(train_images, train_label), (test_images, test_labels) = fashion_mnist.load_data()
```

We simply declare an object of type MNIST loading it from the Keras database. On this object, if we call the load data method, it will return four lists to us. That's the training data, the training labels, the testing data, and the testing labels.

Here you saw how the data can be loaded into Python data structures that make it easy to train a neural network. You saw how the image is represented as a 28x28 array of greyscales, and how its label is a number. Using a number is a first step in avoiding bias -- instead of labelling it with words in a specific language and excluding people who don’t speak that language!

we will look at the code for the neural network definition. before we have just one layer, now we have three layers, the important think to look at are the first and the last layers.

```python
model = keras.Sequential([
	keras.layers.Flatten(input_shape=(28,28)),
	keras.layers.Dense(128, activation=tf.nn.relu),
	keras.layers.Dense(10, activation=tf.nn.softmax)])
```

The last layer has 10 neurons in it because we have ten classes of clothing in the dataset. They should always match. The first layer is a flatten layer with the input shaping 28 by 28, this is because the images are 28X28, so we're specifying that this is the shape that we should expect the data to be in. Flatten takes this 28 by 28 square and turns it into a simple linear array. 

The interesting stuff happens in the middle layer, sometimes also called a hidden layer. This is a 128 neurons in it, we can think these neurons as variables in a function. Maybe call them x1, x2 x3, etc.

![Hidden layer](images/computer_vision-hidden_layer.png)

if you then say the function was `y` equals `w1` times `x1`, plus `w2` times `x2`, plus `w3` times `x3`, all the way up to a `w128` times x128. By figuring out the values of `w`, then `y` will be `9`, which is the category of the shoe.

