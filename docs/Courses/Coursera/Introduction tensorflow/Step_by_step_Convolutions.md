Let's look at the code again, and see, step by step how the Convolutions were built:

## Step 1: Gather the Data

The training data needs to be reshaped, this is because the convolution layer is expecting a single **Tensor** but instead we have a 60,000 28x28x1 in a list, so what we need is to create a single 4D, the tensor mentioned before, a list that will look like 60000x28x28x1, and the same for the rest of the images. If you don't do this, you'll get an error when training as the Convolutions do not recognize the shape.

```python
import tensorflow as tf
mnist = tf.keras.datasets.fashion_mnist
(training_images, training_labels), (test_images, test_labels) = mnist.load_data()
#Here is where we reshape
training_images=training_images.reshape(60000, 28, 28, 1)
#Here we normalize 
training_images=training_images / 255.0
test_images = test_images.reshape(10000, 28, 28, 1)
test_images=test_images/255.0
```
### Reshaping the list

```python
training_images = training_images.reshape(6000,28,28,1)
```
where `60000` is the amount of pictures, `28,28` is the size of the pictures 28x28, and, finally `1` is the number of channels in this case is a gray scale pictures thus 1 channel.

### Normalize 

this is something we already mentioned before, this models work better with smaller number, there fore normalization of information is quite common, and recommended practice.

```python
training_images = training_images / 255.0
```

## Step 2: Define the model (Convolutional and Maxpooling Layers)

Next is to define the models, the first type of model we saw, we started with the `Flatten` layer, but in this case we are going to start with the convolutional layer.

### Convolutional Layer
So the Layer will have a series of parameters:

1. The number of convolution, or filters (check [here](http://127.0.0.1:8000/Courses/Coursera/Introduction%20tensorflow/Convolutional_Neural_network_Overview/#convolution_layer) for more info), at this point, it is purely arbitrary, but the suggesting start is with something in the order of 32.
2. The size  of the Convolution, in this case a 3x3 grid.
3. The activation to use in this case will the the **Rectified Linear Unit** or **ReLU** ( which it will return X when x>0, else return 0)
4. In the first layer of the convolution, we need to add the input data.

```python
tf.keras.layers.Conv2D(32, (3,3), activation='relu', input_shape=(28, 28, 1))
```
### MaxPooling Layer

The next layer will be a MaxPooling layer which will compress the image, it will maintain the content of the features that were previously highlighted by the convolution, by specifying (2,2) for the Maxpooling (check [here](http://127.0.0.1:8000/Courses/Coursera/Introduction%20tensorflow/Convolutional_Neural_network_Overview/#pooling_layer) for more information about maxpooling), the effect is to quarter the size of the image. this layer create a 2x2 array of pixels, and picks the biggest one thus turning 4 pixels into 1, effectively reducing the image by 25%.

```python
tf.keras.layers.MaxPooling2D(2, 2)
```

>You can call `model.summary()` to see the size and shape of the network, and you'll notice that after every MaxPooling layer, the image size is reduced in this way.

Add another convolution and Maxpooling

```python
tf.keras.layers.Conv2D(64, (3,3), activation='relu'),
tf.keras.layers.MaxPooling2D(2,2)
```
At this point we have part of the model, the first part that deal with the data preparation.

```python
model = tf.keras.models.Sequential([
    tf.keras.layers.Conv2D(32, (3,3), activation='relu', input_shape=(28, 28, 1)),
    tf.keras.layers.MaxPooling2D(2, 2),
    tf.keras.layers.Conv2D(64, (3,3), activation='relu'),
    tf.keras.layers.MaxPooling2D(2,2)
    ...
```
## Step 3: Define the model (Deep neural network)

Now flatten the output. After this you'll just have the same DNN structure as the non convolutional version

```python
tf.keras.layers.Flatten(),
```
The same 128 dense layers, and 10 output layers as in the pre-convolution example:

```python
    ...
  tf.keras.layers.Dense(128, activation='relu'),
  tf.keras.layers.Dense(10, activation='softmax')
])
```
so the full model will look like 

```python
model = tf.keras.models.Sequential([
    tf.keras.layers.Conv2D(32, (3,3), activation='relu', input_shape=(28, 28, 1)),
    tf.keras.layers.MaxPooling2D(2, 2),
    tf.keras.layers.Conv2D(64, (3,3), activation='relu'),
    tf.keras.layers.MaxPooling2D(2,2),
    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(128, activation='relu'),
    tf.keras.layers.Dense(10, activation='softmax')
])
```

## Step 4: Compile and Train the model

Now compile the model, call the fit method to do the training, and evaluate the loss and accuracy from the test set.

```python
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
model.fit(training_images, training_labels, epochs=5)
test_loss, test_acc = model.evaluate(test_images, test_labels)
print(test_acc)
```

## The whole model

>This model we use just one layer of convolution and Max pooling

```python
import tensorflow as tf
print(tf.__version__)
#getting the Data set
mnist = tf.keras.datasets.mnist
#Load the Data
(training_images, training_labels), (test_images, test_labels) = mnist.load_data()
#Reshape the Training Data
training_images=training_images.reshape(60000, 28, 28, 1)
#Normalizing the Training Data
training_images=training_images / 255.0
#Reshape the Testing Data
test_images = test_images.reshape(10000, 28, 28, 1)
#Normalizing the Test Data
test_images=test_images/255.0
#Build the model
model = tf.keras.models.Sequential([
  tf.keras.layers.Conv2D(32, (3,3), activation='relu', input_shape=(28, 28, 1)),
  tf.keras.layers.MaxPooling2D(2, 2),
  tf.keras.layers.Flatten(),
  tf.keras.layers.Dense(128, activation='relu'),
  tf.keras.layers.Dense(10, activation='softmax')
])
#Compile the model
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy', metrics=['accuracy'])
#Fit or train the model
model.fit(training_images, training_labels, epochs=10)
#Evaluate the model and get the accuracy
test_loss, test_acc = model.evaluate(test_images, test_labels)
print(test_acc)
```