## Getting started

The goal for the first step is to write a *Q*-learning likelihood function that specifies the likelihood of a particular subject's choices under a basic *Q*-learning algorithm.

Concretely, what this will involve is
- writing some code that updates learned values according to the equations below, and
- calculating the probability of a particular sequence of choices (say, those of the first participant) for any given values of the parameters <img src="https://latex.codecogs.com/gif.latex?\eta"/> and <img src="https://latex.codecogs.com/gif.latex?\beta"/>.

### Learning rule

In this algorithm, we assume that the subject learns different values (denoted $Q$) for different actions (denoted *a*) via trial and error. At each trial (denoted *t*), after choosing action *a* and observing the corresponding reward outcome <img src="https://latex.codecogs.com/gif.latex?r_t"/>, the agent updates the *Q*-value of the chosen action as follows:

<img src="https://latex.codecogs.com/gif.latex?Q_{t+1}(a)=Q_{t}(a)+\eta\cdot\delta"/>

In this equation,

- <img src="https://latex.codecogs.com/gif.latex?\eta"/>  is a learning rate parameter between 0 and 1
- <img src="https://latex.codecogs.com/gif.latex?\delta"/>  is a Rescorla-Wagner prediction error defined as <img src="https://latex.codecogs.com/gif.latex?\delta=r_t-Q_t(a)"/> (i.e., the difference between the experienced reward for the action and the learned *Q*-value)

This way, if more reward is received than the agent expects (i.e., <img src="https://latex.codecogs.com/gif.latex?\delta>0"/>), the *Q*-value of the chosen action is increased. If less reward is received than the agent expects (i.e., <img src="https://latex.codecogs.com/gif.latex?\delta<0"/>), the *Q*-value of the chosen action is decreased.

### Choice rule

The equations above specify how the agent updates the learned values of different actions after choosing one action and observing its outcome. However, they do not specify how the agent chooses between different acitons. For this, we need to specify a *policy function*, which maps the learned *Q*-values into different choice probabilities.

There are different options that we can use here, but a standard one is the *softmax* function:

<img src="https://latex.codecogs.com/gif.latex?\Pr(a=i)=\frac{e^{\beta\cdot\,Q(i)}}{\sum_{a}e^{\beta\cdot\,Q(a)}}"/>


In words, this equation states that the probability that an agent will choose action *i* on a given trial depends on both the *Q*-value of this action (numerator of fraction) and the *Q*-values of all other actions (denominator of fraction).

Here, the parameter <img src="https://latex.codecogs.com/gif.latex?\beta"/>(called the *inverse temperature*) controls the randomness of choices. If <img src="https://latex.codecogs.com/gif.latex?\beta = 0"/>, the agent will choose randomly among the different actions. As <img src="https://latex.codecogs.com/gif.latex?\beta \to \text{Infinity}"/>, the probability that the agent will choose the action with the highest *Q*-value approaches 1. In practice, intermediate values of <img src="https://latex.codecogs.com/gif.latex?\beta"/> tend to perform best, since they balance the demands of exploitation (i.e., choosing the best option) with the demands of exploration (i.e., the agent should sometimes choose actions with lower *Q*-values so that it can keep learning about them).
