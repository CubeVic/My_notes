
## Key concepts about dataset

**Feature:** The input(s) to our model.
**Examples:** An input/output pair used for training (Output, are the labels we mentioned in other notes).
**Labels:** the output of the model.
**Layer:** A collection of nodes connected together within a neural network.

## Key concept about the model

**Model:** The representation of your neural network.
**Dense and Fully Connected (FC):** Each node in one layer is connected to each node in the previous layer.
**Weights and Biases:** the internal variable of model.
**Loss:** The discrepancy between the desired output and the actual output.
**MSE:** Mean squared error, a type of loss function that counts a small number of large discrepancies as worse than a large number of small ones.
**Gradient Descent:** An algorithm that changes the internal variables a bit at a time to gradually reduce the loss function.
**Optimizer:** A specific implementation of the gradient descent algorithm.( There are many algorithms for this. in this course we will only use the "Adam" Optimizer, which stands for _ADAptive with Momentum_ it is considered the best-practice optimizer.
**Learning rate:** The 'step size" for loss improvement during gradient descent.
**Batch:** The set of examples used during training of the neural network.
**Epoch:** A full pass over the entire training dataset.
**Forward pass:** The computation of output values from input.
**Backward pass (back-propagation):** The calculation of internal variable adjustments according to the optimizer algorithm, starting from the output layer and working back through each layer to the input. (it is the tunning process)

## Different type of models

**Regression:** A model that outputs a single value. For example, an estimate of a house's value.
**Classification:** A model that outputs a probability distribution across several categories. For example, in Fashion MNIST, the output was 10 probabilities, one for each of the different types of clothing. Remember, we use _Softmax_ as the activation function in our last Dense layer to create this probability Distribution.

 +                             | Classification                                             | Regression            |
:-----------------------------:| :---------------------------------------------------------:|:---------------------:|
Output                         | List of numbers that represent probabilities for each class| Single Number         |
Example                        | Fashion MNIST                                              | Celsius to Fahrenheit |
Loss                           | Spare categorical cross-entropy                            | Mean squared error    |
Last Layer Activation Function | Softmax                                                    | None                  |

## Key concepts in the model and the Dense function

**Flattening:** The process of converting a 2d image into 1d vector.
**ReLU:** An activation function that allows a model to solve nonlinear problems.
**Softmax:** A function that provides probabilities for each possible output class.
**Classification:** A machine learning model used for distinguishing among two or more output categories.

A convolution is the process of applying a filter ("kernel") to an image. Max pooling is the process of reducing the size of the image through downsampling.

## Key concept about convolutional networks

**CNNs:** Convolutional neural network, that is, a network which has at least one convolutional layer. A typical CNN also includes other types of Layers, such as pooling layers and dense layers.
**Convolution:** The process of applying a kernel (filter) to an image.
**Kernel / Filter:** A matrix which is smaller than the input, used to transform the input into chunks.
**Padding:** adding pixels of some value usually 0, around the input image.
**Pooling:** The process of reducing the size of an image through downsampling. There are several types of pooling layers. For example, average pooling converts many values into a single value by talking the average. However, maxpooling is the most common.
**Maxpooling:** A pooling process in which many values are converted into a single value by talking the maximum value from among them.
**Stride:**the number of pixels to slide the kernel (filter) across the image.
**Downsampling:** The act of reducing the size of an image.

## Example of  a script with convolutional and fashion MNIST data set

```python
#Imports
import tensorflow as tf
from tensorflow import keras
import numpy as np
import matplotlib.pyplot as plt

#import dataset

fashion_mnist = keras.datasets.fashion_mnist
(train_image, train_label), (test_image, test_labels) = fashion_mnist.load_data()

#classes name ( name of the classes of clothes)
class_name = ['t-shirt/top','trouser','pullover','dress','coat','sandal','shirt','sneakers','bag','Ankle boot']

#Explore data/ process data
train_image = train_image / 255
test_image = test_image / 255

#build a model
#setup layer

model = keras.Sequencial([keras.layers.Flatten(input_shape(28,28)),
	keras.layers.Dense(128, activation=tf.np.relu),
	keras.layers.Dense(10,activation=tf.np.softmax)
	])

#compile the model
model.compile(optimizer='adam', loss='sparse_categorical_crossentropy',metrics=['accuracy'])

#train the model
model.fit(train_image,train_label, epochs = 5)

#Evaluate accuracy
test_loss, test_acc = model.evaluate(test_image,test_labels)
print('Test accuracy: ', test_acc)

#make predictions
predictions = model.predict(test_image)
predictions[0]
np.argmax(predictions[0])
test_labels[0]

```
