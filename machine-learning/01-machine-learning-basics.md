# Machine Learning Fundamentals

## Traditional programming

To get an expected outcome, programmers send data to a program which contains set of rules that are process the data and derive the outcome.
- So set of rules and data are sent for programming and an outcome arrives
- The number of rules are derived by the complexity of the process.

## Machine Learning

- In machine learning set of input data is sent paired with the outcome for it to a ML black box
- The ML black box will try to derive a relation to result from the input data.
- This derived relation will be a mathematical function which is now used to test on new set of data to get expected results.

Example: bunch of photos will be marked as cars or not cars and sent to an ML processor which will try to derive a mathematical function. This process is called training.

Once training is done ML processor or black box will, will output a trained model which is a mathematical function. This trained model is used on new images to find out if it a car or not.

## What is artificial intelligence?
Artificial intelligence is a term used for a program which can perform multiple coordinated tasks, with multiple sources of inputs with maximum accuracy.

### Strong AI | Generalized AI
- At present we do not have which can perform human like coordinated tasks.
- If at all, once such program can be derived it is called as **strong AI or generalized AI**
- Strong AI can take multiple inputs with vast number of features from each input and derive an output.
- Like a human processing smell, taste and touch at same time.

### Weak AI | Applied AI

- A program which will perform a simple task (also know as narrow task)
- Which takes one input related features and derive a mathematical function to get the desired output.
- Identifying color of a flower, identifying human or not human in an image ..,

## Few AI took kits providers

- AWS sagemaker
- python
- scikits learn
- caffe
- pytorch
- keras
- tensorflow

## Black box metaphor

Generally the program that is used for determining the mathematical function to identify a relationship between input and output based on features of the input is called as an ML blackbox.

General question on ML black box:
- How is it created?
- What kind of knowledge does it have?
- What is the expected accuracy from it?

## General terms in Machine learning

### Features:
Input data related attributes are called features, in the above cars examples image is input data, we can derive as many features from the input data as possible. The color, shape, number of pixels, width and height. if we consider `x` as a feature we will have `n` number of features like `x1, x2, x3 ... xn`

### Label
Marking a data with its outcome, example image is marked as a car or not car. Attaching an answer to the input data is called labelling, there can be `labelled` data or `unlabelled` data.

## Training a Model
Process of finding a mathematical function to derive a relation between input data and its labels is called training a ML model. This is the toughest task in Machine learning.

> Trained model is used on new input which is not labelled to find it if the model is working or not

So `x1, x2, ..xn` is passed to get an outcome y which can be represented by `y=f(x)`

Labelled data is passed for training a model (x1,y1), (x2,y2) where x is a feature set and y is out come ML model will try to get an accurate f(x) which is used to get an expected out come from a new data set.

## Generalization

Making a good prediction on new data is called generalization. We might not get a good generalized model at initial stages of training a model. Algorithms are optimized to find a better mathematical function to achieve a well generalized models

### Problems while generalizing
#### Under Fitting
- Trained model is not working properly on training data as well as new data.
- This happens when
	- When trained with simple model
	- Trained with not good enough data
#### Over fitting
- Trained model is performing well on trained data but not on new data.
- This happens when:
	- Trained data is only a sample data with small number
	- Too complex model is used
	- Model should fit the data as simple as possible

## Inference
Using a a trained model on new data to identify expected result is called inference.

## Classification of ML systems

- Supervised learning
- Un supervised learning
- Reinforcement learning

## Python modules that can be used for data science projects

- Numpy
- Pandas
- matplotlib
- scikit-learn
- TensorFlow
- Pytorch
- Keras