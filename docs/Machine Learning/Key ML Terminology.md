
# Key ML ( Machine Learning ) Terminology



__Supervised machine learning:__ ML systems learn how to combine input to produce useful predictions on never-before-seen data.

the fundamental machine learning terminology

## Label

it is the thing we're predicting, the `y` variable in a lineal regression.
It can be the future price of the wheat, kind of animal shown in a picture, just about anything.

## Features

A **feature** is an input variable, the `x` variable in a simple linear regression, a Machine learning project might have one or several `x` depending of the complexity of the project.


$$
x_1, x_2, ... , x_N
$$


For an example such as an Spam detector, the feature could include:

* words in the email text
* sender's address
* time of day the email was sent
* email contains the phrase "one weird trick"

## Examples

An **example** is a particular instance of data (**x** can be a vector).
We have two category of examples:

* Labeled examples
* Unlabeled examples

**Label examples** include both features and labels

`labeled examples: {features, label}: (x,y)`

Use label examples to **train** the model, for the example of sSpam detector, the label  example will be those mails mark as "Spam" or "not Spam"

**Unlabeled examples** contains features but not the label:

`unlabeled examples: {features, ?}: (x, ?)`

Once the model is trained using the label examples, we can use the model to predict the labels of the unlabeled examples

## Models

It defines the relationship between features and label, the two main phases of the model's life are:

* **Training** means creating or **learning** the model, in this phase the label example are use to feed the model, so it will learn the relationship between features and label.
* **Inference** means apply the trained model to the unlabeled example, that is, you use the trained model to make predictions, if the examples are `x` the prediction will be `y` 

## Regression vs Classification

**Regression models** are used to predict continues values, for example, given a temperature in Celsius what is the equivalent in Fahrenheit, another examples:

* What is the value of a house in California?
* What is the probability that a user click on this ad?

**Classification models** are used to predict discrete values, for example:

* Is a given email message Spam or not Spam?
* IS this an image of a dog, a cat or a hamster?