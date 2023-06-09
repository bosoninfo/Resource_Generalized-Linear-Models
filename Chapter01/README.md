# 1 Introduction to Generalized Linear Models

|Table of Sections|
|--|
|[:herb: 1.1 Linear Models Vs. Generalized Linear Models](https://github.com/bosoninfo/Resource_Generalized-Linear-Models/blob/main/Chapter01/README.md#herb-11-linear-models-vs-generalized-linear-models)<br>+-- [:apple: 1.1.1 Linear Models](https://github.com/bosoninfo/Resource_Generalized-Linear-Models/blob/main/Chapter01/README.md#apple-111-linear-models)<br>+-- [:apple: 1.1.2 Generalized Linear Models](https://github.com/bosoninfo/Resource_Generalized-Linear-Models/blob/main/Chapter01/README.md#apple-112-generalized-linear-models)<br>[:herb: 1.2 Least Squares Vs. Maximum Likelihood](https://github.com/bosoninfo/Resource_Generalized-Linear-Models/blob/main/Chapter01/README.md#herb-12-least-squares-vs-maximum-likelihood)<br>+-- [:apple: 1.2.1 Least Squares](https://github.com/bosoninfo/Resource_Generalized-Linear-Models/blob/main/Chapter01/README.md#apple-121-least-squares)<br>+-- [:apple: 1.2.2 Maximum Likelihood](https://github.com/bosoninfo/Resource_Generalized-Linear-Models/blob/main/Chapter01/README.md#apple-122-maximum-likelihood)<br>[:herb: 1.3 Saturated Vs. Constrained Models](https://github.com/bosoninfo/Resource_Generalized-Linear-Models/blob/main/Chapter01/README.md#herb-13-saturated-vs-constrained-models)<br>[:herb: 1.4 Link Functions](https://github.com/bosoninfo/Resource_Generalized-Linear-Models/blob/main/Chapter01/README.md#herb-14-link-functions)<br>+-- [:apple: 1.4.1 Why Use Link Functions?](https://github.com/bosoninfo/Resource_Generalized-Linear-Models/blob/main/Chapter01/README.md#apple-141-why-use-link-functions)<br>+-- [:apple: 1.4.2 Invertibility](https://github.com/bosoninfo/Resource_Generalized-Linear-Models/blob/main/Chapter01/README.md#apple-142-invertibility)<br>+-- [:apple: 1.4.3 Canonical Link Function](https://github.com/bosoninfo/Resource_Generalized-Linear-Models/blob/main/Chapter01/README.md#apple-143-canonical-link-function)<br>+-- [:apple: 1.4.4 What Isn'T A Link Function?](https://github.com/bosoninfo/Resource_Generalized-Linear-Models/blob/main/Chapter01/README.md#apple-144-what-isnt-a-link-function)|

<p align="center"><img src="https://user-images.githubusercontent.com/19381768/230614263-feff794c-64ca-404b-9e44-849eaebc22fd.png" width=50%/></p>

## :herb: 1.1 Linear Models vs. Generalized Linear Models
### :apple: 1.1.1 Linear Models
3 assumptions:
  1. $y$'s are independent
  2. Each observation comes from a normal distribution: $y_i \sim (\mu, \sigma^2)$
  3. Means $\mu_i$ are related to predictor variables $x_i$ by a linear model: $\mu_i = x_i^T \beta = \beta_0+\beta_1x_1 + \beta_2x_2 \cdots$

- Coefficients are linear
- Predictor variables can be transformed, but coefficients must be linear

### :apple: 1.1.2 Generalized Linear Models
Takes linear models and generalizes it by:
  1. Allowing $y$'s to come from any exponential family distribution
  2. Allowing means $\mu$ to be related to predictor variables $x_i$ by some function of $\mu$: $g(\mu_i) = x_i^T \beta$

In regular linear model, method for finding coefficients is ordinary least squears (OLS) and maximum likelihood estimation (MLE), they both gives the same results.

In generalized linear model, you can only use maximum likelihood. Ordinary least squares and maximum likelihood can be seen as a special case of the more general generalized linear model or GLM.

|Linear Model|Generalized Linear Model|
|--|--|
|1. iid|1. iid|
|2. $y\sim N(\mu, \sigma^2)$|2. $y\sim Expo. Family$|
|3. $\mu = x^T \beta$|3. $g(\mu) = x^T \beta$|
|4. OLS or MLE|4. MLE|

<p align="center"><img src="https://user-images.githubusercontent.com/19381768/230614263-feff794c-64ca-404b-9e44-849eaebc22fd.png" width=50%/></p>

## :herb: 1.2 Least Squares vs. Maximum Likelihood

### :apple: 1.2.1 Least Squares
Least squares is typically portrayed as an optimization problem where a line is fit to lots of points in two or more dimensions. The best line is one where the squared distance between the points and the line is minimized. The problem can be generalized to multiple predictor variables where the goal is to find some linear combination that is as close as possible to the Y values. This problem is solved by differentiating and equating to zero.

- In Least-Squares one tries to minimize the square distance between the observed points and the points predicted by the model (e.g. $\hat{y} = \beta_0+\beta_1x$)
- The minimization is done with regards to (w.r.t. = with reference to) the parameters of the model, i.e. to the $\beta$'s: $\beta_0,\beta_1$ (in 2d example) - which can also be written in vector form simply as $\beta$.
  - The move to vector notation allows us to move to higher dimension. Instead of a line we will fit a plane or a hyperplane.

$$
\min \sum^n_{i=1} (y_i-\hat{y_i})^2 = \min_{\beta_0, \beta_1} \sum^n_{i=1} (y_i-[\beta_0+\beta_1x_i])^2 = \min_{\beta} \sum^n_{i=1} (y_i-\beta^Tx_i])^2
$$

- By differentiating and equating to zero, we can find the best parameters.
  - In the linear case (linear in the parameters, that is linear in $\beta$'s: $\beta^Tx$), we can find a closed form solution.

### :apple: 1.2.2 Maximum Likelihood
Maximum likelihood assumes a distribution on the Y values. In the case of a normal distribution, the mean is assumed to be at the center of the distribution with some standard deviation. The goal is to choose beta coefficients that maximize the likelihood function, which is the product of the probability density function of the normal distribution for each observation. This function is maximized by differentiating the log of the likelihood function and equating to zero.

In the case of a normal distribution, the results of the maximum likelihood method and least squares method are the same. However, if the Y values come from a non-normal distribution such as a Bernoulli distribution or a Poisson distribution, the maximum likelihood method is used to compute the values of the coefficients that will maximize the distribution. In generalized linear models, the Y values are not necessarily from a normal distribution and can come from skewed distributions like a gamma distribution or a chi-squared distribution. 

|![image](https://user-images.githubusercontent.com/19381768/230558868-e7ed823a-caf1-42d7-bb7f-57f8a43d4840.png)|
|:--:|
|Maximum Likelihood Estimation|

In maximum likelihood we assume that the $y$'s distribute, with a mean that depends on $x$;  that means, e.g. for the $y\sim N(\beta^Tx, \sigma^2) case, that for each $x$, we have a normal Gaussian centered around some point. 
- If we connect the centers we would get a straight line
- The means (centers) are different depending on the value of $x$. In the graph, for the lower $x$, the means are lower than for the higher $x$.

How do you compute the maximum likelihood?
- For each $y_i$ I have some probability of obtaining it
  - E.g. in the normal case: $\frac{1}{\sqrt{2\pi}\sigma} e^{-\frac{1}{2\sigma^2}(y_i - \beta^T x_i)^2}$
- Let's take the product across all observations; Continuing with the normal case:

$$
\mathcal{L} = \prod_{i=1}^n \frac{1}{\sqrt{2\pi}\sigma} e^{-\frac{1}{2\sigma^2}(y_i - \beta^T x_i)^2}
$$

- The $\arg\max$ is the same for the likelihood or the log-likelihood, so easier to take the log and turn the product into a sum; Continuing:

$$
\begin{aligned}
\ell := log\mathcal{L} &= log \prod_{i=1}^n \frac{1}{\sqrt{2\pi}\sigma} e^{-\frac{1}{2\sigma^2}(y_i - \beta^T x_i)^2}\\
&= \sum_{i=1}^n log (\frac{1}{\sqrt{2\pi}\sigma} e^{-\frac{1}{2\sigma^2}(y_i - \beta^T x_i)^2})\\
&= \sum_{i=1}^n [log (\frac{1}{\sqrt{2\pi}\sigma}) - \frac{1}{2\sigma^2}(y_i - \beta^T x_i)^2]
\end{aligned}
$$
  
  - The first term $log (\frac{1}{\sqrt{2\pi}\sigma})$ doesn't depend on the parameters we optimize, so we can discard it

$$
\begin{aligned}
\arg\max_{\beta} \ell &= \arg\max_{\beta} - \sum_{i=1}^n [\frac{1}{2\sigma^2}(y_i - \beta^T x_i)^2] \\
&= \arg\min_{\beta} \sum_{i=1}^n [\frac{1}{2\sigma^2}(y_i - \beta^T x_i)^2]
\end{aligned}
$$

  - Maximizing a negative quantity is the same as minimizing the positive quantity

$$
\arg\min_{\beta} \sum_{i=1}^n [\frac{1}{2\sigma^2}(y_i - \beta^T x_i)^2] = \arg\min_{\beta} \sum_{i=1}^n (y_i - \beta^Tx_i)^2
$$

  - Again, we see a multiplying constant $\frac{1}{2\sigma^2}$ that doesn't affect the $\arg\min$.

We see that for the normal distribution, the least squares and the maximum likelihood methods are actually equivalent - we are doing exactly the same.

BUT - if we assume a different distribution for the $y$ - e.g., Bernoulli, Poisson, etc., the methods won't be equivalent - and we will only use Maximum Likelihood. 

<p align="center"><img src="https://user-images.githubusercontent.com/19381768/230614263-feff794c-64ca-404b-9e44-849eaebc22fd.png" width=50%/></p>

## :herb: 1.3 Saturated vs. Constrained Models

In this section, we gain some more intuition about maximum likelihood by contrasting two possible models: the Saturated (or unconstrained) model and the Constraint (or regular) model. Both models assume the same assumptions as mentioned in a previous video, which are that the observations, after some random response variable, are independent, that they come from some exponential family distribution, and that there is a relation between the means of the distribution and some predictor variable X.

|Generalized Linear Model|
|--|
|1. $y$'s are iid|
|2. $y \sim Expo.Family$|
|3. $g(\mu) = x^T\beta$|

The regular model tries to fit some linear line or other model to the points, and it does it by the method of maximum likelihood. Under the assumption that the mean is the maximum likelihood of the normal distribution, we get our betas that maximize the overall likelihood of all those means.

The saturated model, on the other hand, focuses all the means exactly on the points, so this is the maximum likelihood that is ever possible. You can think of it as if we are fitting some high order polynomial axes to the data. 

In the context of GLM, the method of maximum likelihood finds the maximum likelihood that is possible under some constrained model. We try to find a linear line that maximizes these values that are as close as possible to the center to the maximum likelihood of each observation. The difference between the log likelihood of the saturated model and the regular model is a quantity called a `unit deviance`, which we will talk about in a future section.

One possible question is if there is a distribution that is not normal or asymmetric, where should we put the mean of this distribution? Should we put the mode of the distribution on this point instead of the mean? The way GLM works is that you always put the mean, and we will also see in the upcoming video is that the math works out for the mean.

Of note is that predicting the mode would cause greater error on average than predicting the mean, so it makes sense for a given model to predict the mean and not the mode. Still, for the saturated modelwe could get higher likelihood if we positioned the points on the mode and not on the mean. But, if we restrict ourselves to placing them on the means, the saturated model is still the highest likelihood we can hope for comparing to any type of (additional) structural constraints.

<p align="center"><img src="https://user-images.githubusercontent.com/19381768/230614263-feff794c-64ca-404b-9e44-849eaebc22fd.png" width=50%/></p>

## :herb: 1.4 Link Functions
One of the generalizations that GLM actually generalizes, is the relation between the mean and the linear predictor.
- Mean = $\mu_i$
- Linear predictor = $LP_i$ = $\beta^Tx_i$ (or in 2d, $\beta_0+\beta_1x_i$)

In the Linear model, we assume an identity relation: $\mu_i=\beta^Tx_i$

In GLM's, we assume some function relation: $g(\mu_i)=\beta^Tx_i$

### :apple: 1.4.1 Why use link functions?
There are a few reasons:
- To preserve the linearity structure
  - If our data seems like a straight line, maybe we don't need any transformation
  - But if our data doesn't look like a line, maybe we need some transformation
- Another reason is interpretability
  - Linear relations are unconstrained: $\beta^Tx_i$ can take any values from $-\infty$ to $\infty$
    - Evan if we take a very small slope
  - But if $y\sim Ber(p)$, the mean, $p$ ($\mu=\mathbb{E}[y]=p$) can only take values between 0 and 1.

So one of the main reason to use link function is to make sure that the values you get for $\mu$ makes sense.

For Bernoulli distribution (logistic regression) the most common link function is the `logit`:
- Dividing $p$ by $(1-p)$ will give us values from 0 to $\infty$
- Taking the log of this will give us values from $-\infty$ to $\infty$
- $g(\mu_i)=logit(\mu_i)=log(\frac{\mu_i}{1-mu_i})=log(\frac{p_i}{1-p_i})=LP_i=\beta^Tx_i$

Same goes for Poisson and Gamma distribution 
- For these distributions the mean can only be positive, so we have to use some transformations that give possible values for the means.
- In these case a log transformation might be plausible

### :apple: 1.4.2 Invertibility
Link functions must be monotonic and invertible. For th logit, the inverse function is the sigmoid:

$$
\begin{aligned}
log(\frac{\mu_i}{1-\mu_i}) &= LP_i\\
\frac{\mu_i}{1-\mu_i} &= e^{LP_i} \\
\mu_i &= \frac{e^{LP_i}}{1+e^{LP_i}} = \sigma(LP_i)\\
\mu_i &= \frac{e^{\beta^Tx_i}}{1+e^{\beta^Tx_i}} = \sigma(\beta^Tx_i)\\
\end{aligned}
$$

Link functions must also be differentiable (we use differentiation in Maximum Likelihood).

### :apple: 1.4.3 Canonical Link Function

The "natural parameter" of the Exponential Family is equal to the linear predictor
- We will see what is the natural parameter in the next part; Each exponential family has a natural parameter
- The natural parameter is some function of the mean
- Let's for now denote it by: $\theta(\mu_i) = \theta_i$
- The canonical link function states: $\theta_i=LP_i=\beta^Tx_i$

Using the canonical link simplifies some of the math when doing maximum likelihood. But it doesn't always make sense, and abides the reasons stated above (e.g., in Gamma regression, the canonical link function is not interpretable in some cases)

### :apple: 1.4.4 What isn't a link function?
- A link function isn't transforming the predictors / covariates, i.e. if we take the function to be log, it's not saying $y=\beta_0+\beta_1 \log(x)$
- And it's also not transforming the response and leaving the distribution to be normal. I.e., it's not saying: $\log (y_i)=\beta_0+\beta_1x_i+\epsilon_i, \epsilon_i \sim N(0, \sigma^2)$
- The response and predictors remain the same. Only the mean changes.

In summary,
- The function $g(\mu)$ is needed to transform the structure to a linear structure in cases where the linear structure is inadequate. 
- The link function is also used for interpretability, ensuring that the values of mu make sense. 
- The link function must be monotonic, invertible, and differentiable. 
- The canonical link function relates the natural parameter to the linear predictor.
- The link function is not transforming the predictor or the response but only the $\mu$. 
