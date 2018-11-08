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

### Neutrino Wrong Sign Contamination

The neutrino beams are not pure. In the forward horn current (FHC) mode, the beam is mostly composed of muon neutrinos, $\nu_\mu$. However, there is a small amount of muon antineutrino contamination in the beam, and this is called wrong sign contamination. Likewise, in the reversed horn current (RHC) mode, there is $\nu_\mu$ contamination in the antineutrino beam. In RHC, however, the wrong sign proportion is much higher than that in FHC, predominantly due to the higher interaction cross section of $\nu_\mu$ than $\bar{\nu}_\mu$.

The wrong sign component is easily measured if a magnetic field is applied to the detectors. However, since our detectors are not magnetized, it becomes very tricky to estimate the wrong sign background.

### Wrong Sign Classification

My colleagues have been looking into this problem and made impressive achievements. For example, one of the methods is to train a classifier with engineered features that best separates wrong sign from right sign. The algorithm used here is a very popular one in high energy physics for particle identification, the Boosted Decision Tree (BDT). Here is the result[^2] obtained with ROOT's TMVA multivariate analysis package.

![BDT results]({{ site.baseurl }}/assets/wrong_sign_bdt_all_quantiles.png){: .center-image }

The selected features that led to the BDT classifier each has the one dimensional distribution like this:

![selected features]({{ site.baseurl }}/assets/sig_bkg_dists_censored.png){: .center-image }

We can see that for each variable the two components almost overlap completely, and no cut can be made with any one of the variables to effectively separate the two components.

BDT is one of the multivariate classifiers with good performance in general. However, in this case, the BDT scores for both components still have a significant overlap between the two score distributions. Besides, the classifier is trained on features obtained from Monte Carlo simulation, which goes trough both the neutrino generator and the detector simulation. It is well known that neutrino-nucleus interactions are not well understood and could lead to substantial data-Monte Carlo discrepancies. Therefore, a less model dependent method is always welcome if available.

### Linear Discriminant Analysis

A less model dependence way to estimate the wrong sign component is to fit a mixture model to data. Of course one can construct a parametric mixture model in the ten dimensional space. However, this could be very formidable mathematically and computationally. Fortunately, statisticians have considered such kind of problems for a long time, and a method called Linear Discriminant Analysis (LDA) was developed and has been used as a means of dimensionality reduction in many areas.

### References

[^1]: Peter Hall and Xiao-Hua Zhou, Ann. Statist. Volume 31, Number 1 (2003), 201-224.
[^2]: Abhilash Y D, et al., NOVA Document 32976.