# ***Machine Learning ***

Linear Regression, Training and loss
====================================

**Linear regression** is a method for finding the straight line or hyperplane that best fits a set of points.

As an example, we can use the relationship between the temperature and the cripts-per-minutes of crickets

![Chirps per Minute vs. Temperature in Celsius.](/images/CricketPoints.png)

As expected, the plot shows the temperature rising with the number of chirps. the relationship between chirps and temperature is linear, you could draw a single straight line like the following to approximate this relationship:

![A linear relationship](/images/CricketLine.png)

the line doesn't pass through every dot, but the line does clearly show the relationship between chirps and temperature. Using the equation for a line:

$$
 y = mx + b
$$

where:

* $y$ is the temperature Celsius - the vale the model need to predict
* $m$ is the slope of the line
* $x$ is the number of chirp per minute
* $b$ is the y-intercept 

in the field of machine learning the **lineal regression** formula change to:

$$
 y' = b_1 + w_1x_1
$$

where:

* $y'$ is the predicted label (the desired output)
* $b$ is the bias, the y-intercept ( sometimes refer as $w_0$)
* $w_1$ is the weight of feature 1.
* $x_1$ is a feature (a known input)

To **infer** (predict) the temperature $y'$ for a new chirps-per-minute $x_1$ value, just substitute the $x_1$ value into this model.

Although this model uses only one feature, a more advance model might rely on multiple features, each having a separate weight ($w_2$,$w_3$, etc.). so a model that relies on three features might look as follows:

$$
 y' = b_1 + w_1x_1 + w_2x_2 + w_3x_3
$$

