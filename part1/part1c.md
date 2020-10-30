# Model comparison

The focus so far has been on parameter estimation for a *Q*-learning model. This is useful, but does not address the question of *model comparison*: does this model explain the data better than other models? That will be the focus of this part of the tutorial.

## A competitor: asymmetric *Q*-learning

To do model comparison, we first need to specify a second model to compare to the *Q*-learning model that we have been working with so far. The one we will use is an asymmetric *Q*-learning model, which is identical to the standard *Q*-learning model, except that it uses a different learning rate depending on whether the reward prediction error is positive:

<img src="https://latex.codecogs.com/gif.latex?Q_{t+1}(a)=\left\{\begin{matrix}Q_t(a)+\eta^+\cdot\delta&\text{if}\quad\delta\geq0\\Q_t(a)+\eta^-\cdot\delta&\text{if}\quad\delta<0\end{matrix}\right."/>

Compared to standard *Q*-learning, which has only one learning rate parameter, this asymmetic *Q*-learning model has two separate learning rates: <img src="https://latex.codecogs.com/gif.latex?\eta^+"/> when there is a positive reward prediction error, and <img src="https://latex.codecogs.com/gif.latex?\eta^-"/> when the reward prediction error is negative.

As a first step, you should write a likelihood function for this asymmetric model and verify that you can fit its parameters to the data.
