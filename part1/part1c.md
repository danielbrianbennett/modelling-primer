# Model comparison

The focus so far has been on parameter estimation for a *Q*-learning model. This is useful, but does not address the question of *model comparison*: does this model explain the data better than other models? That will be the focus of this part of the tutorial.

## A competitor: asymmetric *Q*-learning

To do model comparison, we first need to specify a second model to compare to the *Q*-learning model that we have been working with so far. The one we will use is an asymmetric *Q*-learning model, which is identical to the standard *Q*-learning model, except that it uses a different learning rate depending on whether the reward prediction error is positive:

<img src="https://latex.codecogs.com/gif.latex?Q_{t+1}(a)=\left\{\begin{matrix}Q_t(a)+\eta^+\cdot\delta&\text{if}\quad\delta\geq0\\Q_t(a)+\eta^-\cdot\delta&\text{if}\quad\delta<0\end{matrix}\right."/>

Compared to standard *Q*-learning, which has only one learning rate parameter, this asymmetic *Q*-learning model uses two separate learning rates: <img src="https://latex.codecogs.com/gif.latex?\eta^+"/> when there is a positive reward prediction error, and <img src="https://latex.codecogs.com/gif.latex?\eta^-"/> when the reward prediction error is negative.

As a first step, you should write a likelihood function for this asymmetric model and verify that you can fit its parameters to the data using MLE (not MAP).

## Comparing models

How should we compare the fits of two models to decide which one better explains the data?

The first thing to say is that there is no one right answer to this question. It's a very active topic of discussion in the statistical literature, and different people have different preferred approaches. That means that the guidance in this document represents one reasonable approach, but it's by no means the only way to approach things.

With that disclaimer in mind, we can go over one common metric used to compare models fit with MLE: the Bayesian Information Criterion (BIC). The BIC is a metric that attempts to quantify model fit by trading off two quantities: first, the *goodness-of-fit* of the model and, second, the *complexity* of the model. The idea behind this is that when comparing models, we should choose the simplest model that explains the data well. This is summarised in the following equation:

<img src="https://latex.codecogs.com/gif.latex?\text{BIC}=k\cdot\log(n) - 2\cdot\text{LL}"/>

Where:
- *k* is the number of parameters in the model (i.e., 2 per participant in the symmetric model, 3 per participant in the asymmetric model)
- *n* is the number of data points to which the model is fit (i.e., the number of trials per participant)
- *LL* is the log likelihood of the model at the MLE parameter estimates

Lower BIC values (i.e., closer to 0) indicate better model fit.

The BIC can be calculated separately for each participant and then summed across participants to get an overall score for each model.

## Things to think about

- Why would we not want to use MAP estimation for model comparison?
- How many participants are best fit by each model? Are all participants best explained by the best fitting model? If not, what does this mean?
- An alternative to the BIC is the AIC (Akaike Information Criterion). If you compare models on the basis of the AIC rather than the BIC, how different do things look?
