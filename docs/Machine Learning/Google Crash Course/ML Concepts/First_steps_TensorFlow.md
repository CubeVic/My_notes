TensorFlow provide different type of toolkits to construct models in a variety of levels of abstraction. It can be a lower_level  with mathematical operations or a higher level with predefine architectures.

![009_TFHierarchy](../images/009_TFHierarchy.svg)


| Tollkit                           | Description                            |
|:----------------------------------|:---------------------------------------|
| Estimator (tf.estimator)	        | High-level, OOP API.                   |
| tf.layers/tf.losses/tf.metrics	| Libraries for common model components. |
| TensorFlow	                    | Lower-level APIs                       |


Similar to how Python has and interpreter that can run in multiple hardware to run python code, TensorFlow can run the graph on multiple hardware platforms, including CPU, GPU, and TPU.


Here will be an example of pseudo code of a linear classification program using tf.estimator

```
import tensorflow as tf

# Set up a linear classifier.
classifier = tf.estimator.LinearClassifier(feature_columns)

# Train the model on some example data.
classifier.train(input_fn=train_input_fn, steps=2000)

# Use it to predict.
predictions = classifier.predict(input_fn=predict_input_fn)
```

>
**Tensor:**
The primary data structure in TensorFlow programs. Tensors are N-dimensional (where N could be very large) data structures, most commonly scalars, vectors, or matrices. The elements of a Tensor can hold integer, floating-point, or string values.

## Common hyperparameter in Machine Learning

Many of the coding exercises contain the following hyperparameters:

* **steps**, which is the total number of training iterations. One step calculates the loss from one batch and uses that value to modify the model's weights once.
* **batch size**, which is the number of examples (chosen at random) for a single step. For example, the batch size for SGD is 1.

The following formula applies:

$$
total\ number\ of\ trained\ examples = batch\ size * steps
$$
