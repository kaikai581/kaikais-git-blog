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


$f(\boldsymbol{x};\boldsymbol{\theta})$ is referred to as a mixture density, $g$ is the number of component distributions, and $\boldsymbol{\theta}=(\boldsymbol{\pi},\boldsymbol{\theta_1},...,\boldsymbol{\theta_g})$ is the parameter vector we want to estimate.

Note that here the formulation is written down explicitly as parametric modeling. Nonparametric mixture models are much more difficult problems pioneered by Hall and Zhou[^1], and will not be adopted here.

The idea now is to fit the data with some of the most flexible parametric models on the market, such as the noncentral $t$ distribution depicted below.

![](https://upload.wikimedia.org/wikipedia/commons/8/88/Nc_student_t_pdf.svg){: .center-image }

### Neutrino Wrong Sign Contamination

The neutrino beams are not pure. In the forward horn current (FHC) mode, the beam is mostly composed of muon neutrinos, $\nu_\mu$. However, there is a small amount of muon antineutrino contamination in the beam, and this is called wrong sign contamination. Likewise, in the reversed horn current (RHC) mode, there is $\nu_\mu$ contamination in the antineutrino beam. In RHC, however, the wrong sign proportion is much higher than that in FHC, predominantly due to the higher interaction cross section of $\nu_\mu$ than $\bar{\nu}_\mu$.

The wrong sign component is easily measured if a magnetic field is applied to the detectors. However, since NOvA detectors are not magnetized, it becomes very difficult to estimate the wrong sign background.

### References

[^1]: Peter Hall and Xiao-Hua Zhou, Ann. Statist. Volume 31, Number 1 (2003), 201-224.