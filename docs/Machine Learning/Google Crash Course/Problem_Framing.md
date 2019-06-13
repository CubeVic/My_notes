![001_Introduction](../images/001_Introduction.png)

## Common ML Problem 

In basic terms, ML is the process of training a piece of software, called a model, to make useful predictions using a data set.

There are two common paradigms mentioned in ML, Supervised and Unsupervised training.

### What is Supervised Learning?
Supervised learning is a type of ML where the model is provided with labeled training data, this means that we feed the model with **features** ( $x$ If you want) and the answer or so call **label** ($y$) and it will learn the relationship between these two.


### What is Unsupervised Learning?

In unsupervised learning, the goal is to identify meaningful patterns in the data. To accomplish this, the machine must learn from an unlabeled data set. In other words, the model has no hints how to categorize each piece of data and must infer its own rules for doing so.


## Types of ML Problems

There are several subclass of ML, depending of the prediction task

|type of ML Problem | Description | Example|
|:-----------------:|:-----------:|:-------|
|Classification|Pick one of N labels|Cat, dog, horse, or bear|
|Regression|Predict numerical values|Click-through rate|
|Clustering|Group similar examples|Most relevant documents (unsupervised)|
|Association rule learning|Infer likely association patterns in data|If you buy hamburger buns, you're likely to buy hamburgers (unsupervised)|
|Structured output|Create complex output|   Natural language parse trees, image recognition bounding boxes|
|Ranking|Identify position on a scale or status|Search result ranking|

## The ML Mindset

In traditional software, you can trick, tune and reason to find the design that fit the requirements, but in machine learning, more often than not, it will be necessary to experiment to find the correct or rather the workable model.

ML produce models that interpret signals in a different way ( compare with humans), for example a Neural network might interpret the words "tree" liek something like this `[0.37,0.24,0.2]` and "car" as `[0.1,0.78, 0.9]` the Neural network might use this interpretation to do an accurate translation or a sentiment analysis, but humans looking to this embeddings would find them very hard to understand, this can make machine learning difficult but not impossible for humans to evaluate and understand.

## Experimental Design Prime

### Get Comfortable with Some Uncertainty

One of the difference between ML and the traditional programming, is that in traditional programming you will end with a set of parameters that you understand and you know how they should behave, but with ML, the non-coding work can be very complicated, but the code usually far less code. you might get the code correctly and expect a result, but the result you will find suitable might be obtain after several changes and tunning that you might not fully understand.

### Scientific Method

It is useful to think ML process as an experiment where we run test after test to converge on a workable model.

| Step | Example |
|:----------------------------|:----------------------------|
|1. Set the research goal.    | I want to predict how heavy traffic will be on a given day|
|2. Make a hypothesis.        | I think the weather forecast is an informative signal.     |
|3. Collect the data.         | Collect historical traffic data and weather on each day. |
|4. Test your hypothesis.     | Train a model using this data.|
|5. Analyze your results.     | Is this model better than existing systems?|
|6. Reach a conclusion. | I should (not) use this model to make predictions, because of X, Y, and Z. |
|7. Refine hypothesis and repeat.| Time of year could be a helpful signal.|

## Identifying Good Problems for ML

### Clear Use Case

>Start with the problem, not the solution. Make sure you aren't treating ML as a hammer for your problems.

Ask yourself the following question in order:

1. What problem is my product facing?
2. Would it be a good problem for ML?


### Know the Problem Before Focusing on the Data

>Be prepared to have your assumptions challenged.

If you understand the problem clearly, you should be able to list some potential solutions to test in order to generate the best model. Understand that you will likely have to try out a few solutions before you land on a good working model.

### Predictive Power

You should not try to make ML do the hard work of discovering which features are relevant for you. If you simply throw everything at the model and see what looks useful, your model will likely wind up overly complicated, expensive, and filled with unimportant features.


### Predictions vs. Decisions

Make sure your predictions allow you to take a useful action. For example, a model that predicts the likelihood of clicking certain videos could allow a system to prefetch the videos most likely to be clicked.

Conversely, a model that predicts the probability that someone will click "thumbs down" for a specific YouTube video might be interesting, but we can't do anything useful with that knowledge.

|   Prediction         |            Decision                |
|:---------------------|:-----------------------------------|
| What video the learner wants to watch next. | Show those videos in the recommendation bar.|
| Probability someone will click on a search result.| If P(click) > 0.12, prefetch the web page.|
| What fraction of a video ad the user will watch. | If a small fraction, don't show the user the ad.|