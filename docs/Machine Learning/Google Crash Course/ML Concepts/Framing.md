**Supervised machine learning:** ML systems learn how to combine input to produce useful predictions on never-before-seen data.

the fundamental machine learning terminology

## Key ML Terminology

### Label

It is the thing we're predicting, the $y$ variable in a lineal regression. It can be the future price of the wheat, kind of animal shown in a picture, just about anything.

### Features

A **Feature** is a input variable, the $x$ in a simple linear regression. A ML project might have several $x$ depending of the complexity of the project.

$$
x_1, x_2,...,x_n
$$

Lets take a spam detector as an example, the features include the following:

* words in the email text
* sender's address
* time of day the email was sent
* email contains the phrase "one weird trick"

### Examples

An _Example_  is a particular instance of Data, this data can be represented as **x**, ( were **x** can be a vector), we have to categories:

* Labeled examples
* Unlabeled examples

#### Labeled Examples

`labeled examples: {features, labels}: (x,y)`

use label example to train the model, for the example of the spam detector , the label example will be those mails mark as "spam" or "not spam".

#### Unlabeled Examples

`unlabeled examples: {features, ?}: (x,?)`

once the model is trained using the label examples, we can use the model to predict the labels of the unlabeled examples.

### Models

It defines the relationship between features and labels. The main phases of the model's life are:

* **Training:** means creating or _learning_ the model, in this phase the label example are use to feed the model, so it  will learn the relationship between features and labels.

* **Inference:** means apply the trained model to the unlabeled example,  in other words, it is use the trained model to make a prediction, if the example are $x$ the prediction will be $y$.

###Regressions vs Classifications

**Regression models** are used to predict continues values, for example, given a temperature in Celsius what is the equivalent in Fahrenheit, or:

* What is the value of a house in California?
* What is the probability that a  user click on this ad?

**Classification models** are used to predict discrete values, for example:

* Is a given email message Spam or not Spam?
* Is this an image of a dog, a cat or a hamster?
