#The ‘Hello World’ of neural networks

A neural network is basically a set of functions which can learn patterns.

##The layers and the neurons
The simplest possible neural network is one that has only one neuron in it, and that's what this line of code does. In keras, you use the word dense to define a layer of connected neurons. There's only one dense here

```python
model = keras.Sequential([keras.layers.Dense(unit = 1, input_shape[1])])
```

There's only one dense here. So there's only one layer and there's only one unit in it, so it's a single neuron. Successive layers are defined in sequence, hence the word sequential.

You define the shape of what's input to the neural network in the first and in this case the only layer, and you can see that our input shape is super simple. It's just one value

## The `optimizer` and the `loss`
Here are two function roles that you should be aware of though and these are loss functions and optimizers. This code defines them.

```python
model.compile(optimizer='sgd', loss='mean_squared_error')
```
The loss function measures this and then gives the data to the optimizer which figures out the next guess. So the optimizer thinks about how good or how badly the guess was done using the data from the loss function.

As the guesses get better and better, an accuracy approaches 100 percent, the term **convergence** is used.

##The data
the next step is the data, in this case we use the library `numpy`

```python
xs = np.array([-1.0, 0.0, 1.0, 2.0, 3.0, 4.0], dtype=float)
xy = np.array([-3.0, -1.0, 1.0, 3.0, 5.0, 9.0], dtype=float)
```

## The training
The training takes place in the fit command.

```python
model.fit(xs,ys, epochs=500)
```

The epochs equals 500 value means that it will go through the training loop 500 times.Then the model has finished training, it will then give you back values using the predict method.

## The prediction
```python
print(model.predict([10.0]))
```

you'll see that it will return a value very close to 19 but not exactly 19.
there are two main reasons. The first is that you trained it using very little data. There's only six points.

The second main reason, when we use neural networks, as they try to figure out the answers for everything, they deal in probability. You'll see that a lot and you'll have to adjust how you handle answers to fit.

##Example:

Imagine if house pricing was as easy as a house costs 50k + 50k per bedroom, so that a 1 bedroom house costs 100k, a 2 bedroom house costs 150k etc.

How would you create a neural network that learns this relationship so that it would predict a 7 bedroom house as costing close to 400k etc.

**Hint:** Your network might work better if you scale the house price down. You don't have to give the answer 400...it might be better to create something that predicts the number 4, and then your answer is in the 'hundreds of thousands' etc.

```python
import tensorflow as tf
import numpy as np
from tensorflow import keras
model = tf.keras.Sequential([keras.layers.Dense(units=1, input_shape=[1])])
model.compile(optimizer='sgd', loss='mean_squared_error')
xs = np.array([1.0, 2.0, 3.0, 4.0, 5.0, 6.0], dtype=float)
ys = np.array([1.0, 1.5, 2.0, 2.5, 3.0, 3.5], dtype=float)
model.fit(xs, ys, epochs=1000)
print(model.predict([7.0]))
```

[Interesting info](https://research.google.com/seedbank/)
