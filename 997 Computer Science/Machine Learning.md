---
tags:
  - compsci
date: 2024-09-18
source: "[[COMPSCI 182]]"
---

## [[Optimization Problems|Optimizational]] Paradigm for Supervised Machine Learning

Let there be Training Data (covariates, labels) $(x_{i}, y_{i})$ for $i \in \{1,2,... n\}$,
Then let $f_{\theta}(\cdot)$ be our model, where $\vec \theta$ is the parameter vector.
And, $l(\vec{y}, \hat{y})$ is the loss function.
Then we minimize empirical risk:$$\hat\theta = \underset{\theta}{\operatorname{arg max}}\frac{1}{n} \sum\limits_{i=1}^{n} l(\vec y - f_{\theta}(x_{i}))$$
$$\hat y= f_{\hat \theta}(x)$$
Goal:
- Good performance in the real world on new $x$ i.e $x$ we didn't see.
- Low generalization error. We assume the $x$'s we didn't seem are drawn from some [[Types of Distributions|distribution]].$$E_{X,Y}[l(y,f_{\hat \theta}(x))]$$
- We __believe__ the distribution of X and Y exists.


### Complications
##### 1. Don't have access to $P(X,Y)$

Solution: We collect a test set: $(x_{\text{text i}}, y_{\text{text i}})$ , which we never touch after collection.
Except to calculate $$\frac{1}{n_{\text{test}}} \sum\limits_{i=1}^{n_{\text{test}}} l(\vec y - f_{\theta}(x_{_{\text{test i}}}))$$
##### 2. The loss we care about is not compatible with your optimizer

Eg: The optimizer wants derivates, but loss is not differentiable, has zero derivatives.
Solution: We use a surrogate loss, that works.
Eg: Logistic loss or Hinge Loss for binary classification or Cross Entropy Loss for multi-class classification.

<br>

>[!NOTE]  Changing Loss Functions
>We only change the training loss function, not the test loss.

##### 3. Get huge values in $\hat \theta$, OVERFITTING

Solution A: Add a Regularizer during training. $$\hat\theta = \underset{\theta}{\operatorname{arg max}}\frac{1}{n} \sum\limits_{i=1}^{n} l(\vec y - f_{\theta}(x_{i})) + R(\theta)$$
	Eg: [[Ridge Regularization]].
		Moving from MLE to MAP.
		Introduces hyperparameter.

Solution B: hyperparameter search -> Hold out additional data (Validation set) to evaluate how your doing on changing the hyperparamter.


##### 4. Optimizer might have it's own hyperparameters

Eg: Gradient Descent Learning Rate.

$$θ_t+1 = θ_t − η∇_θL_{train, \theta}$$
