---
mathjax: true
---

## Mixture Models and Kernel Discriminant Analysis

### Mixture Models

Suppose you have a dataset drawn from an unknown distribution, which you already know is a combination of two component distributions. Can we estimate the component distributions as well as the frequencies the two distributions are chosen to draw samples with the observed data?

The answer is yes. Statisticians have developed models that are built for such kind of problems, which are known as finite mixture models (FMMs). The mathematical formulation of the density function goes like this:


$$
f(\boldsymbol{x};\boldsymbol{\theta})=\sum_{i=1}^g\pi_if_i(\boldsymbol{x};\boldsymbol{\theta_i}).
$$


$f(\boldsymbol{x};\boldsymbol{\theta})$ is referred to as a mixture density, $g$ is the number of component distributions, and $\boldsymbol{\theta}=(\boldsymbol{\pi},\boldsymbol{\theta_1},...,\boldsymbol{\theta_g})$ is the parameter vector we want to estimate subject to the constraint $\sum_{i=1}^g\pi_i=1$.

Note that here the formulation is written down explicitly as parametric modeling. Nonparametric mixture models are much more difficult problems pioneered by Hall and Zhou[^1], and will not be adopted here.

The idea now is to fit the data with some of the most flexible parametric models on the market, such as the noncentral $t$ distribution depicted below.

![](https://upload.wikimedia.org/wikipedia/commons/8/88/Nc_student_t_pdf.svg){: .center-image }

### Hardly Separable Distributions

Suppose I have engineered ten variables from my data that lead to a Boosted Decision Tree (BDT) classifier with some discrimination power. For example, the two component distributions' BDT scores look like the following:

![BDT results]({{ site.baseurl }}/assets/mixture-model-kda/bdt_scores_hand.png){: .center-image }

The selected features that lead to the BDT classifier each has the one dimensional distribution like this:

![selected features]({{ site.baseurl }}/assets/mixture-model-kda/sig_bkg_dists_censored.png){: .center-image }

Obviously, for each one dimensional feature, no simple selection can be applied to separate component 1 from component 2 effectively. If we want to estimate the proportion of each component, a classifier or transformation is required to separate the two groups, otherwise we will never get a good mixture model fit to data.

By looking at the shapes of the component distributions of the BDT scores, it is not clear whether there exist parametric models that fit the data well. Therefore, I would like to try some transformation to see if that gives me more familiar distribution shapes.

### Linear Discriminant Analysis

A less model-dependent way to estimate the wrong sign component is to fit a mixture model to data. Of course one can construct a parametric mixture model in the ten dimensional space. However, this could be very formidable mathematically and computationally. Fortunately, statisticians have considered such kind of problems for a long time, and a method called Linear Discriminant Analysis (LDA) was developed and has been used as a means of dimensionality reduction in many areas.

### References

[^1]: Peter Hall and Xiao-Hua Zhou, Ann. Statist. Volume 31, Number 1 (2003), 201-224.