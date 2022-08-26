# How to Leverage the Augmented Data in Visual RL?

![How to Leverage the Augmented Data in Visual RL?](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/278bec04acfb6a7bc1b98e07cb34baae7c9de950/Image/Form%20and%20Structure.png)

## 1 Implicit Policy Regularization

In the visual RL community, :bookmark:**RAD** and :bookmark:**DrQ** first leverage classical image transformations such as Crop to augment the input observations as implicit regularization.

> :bookmark: **[DrQ]** Image Augmentation is All You Need: Regularizing Deep Reinforcement Learning from Pixels **(ICLR 2021)** [*(paper)*](https://openreview.net/forum?id=GY6-6sTvGaf) [*(code)*](https://github.com/denisyarats/drq)

DrQ suggests two distinct ways to regularize the Q-function.
the optimization objective of DrQ can be rewritten as:

$$
J_{Q}^{\mathrm{DrQ}}(\theta) = \frac{1}{N M K} \sum_{i=1}^{N}\sum_{m=1}^{M}\sum_{k=1}^{K} l(f(s_{i}, \nu_{i, m}) ,a_i,r_i, f(s_{i}^{\prime}, \nu_{i, k}^{\prime}))
$$

> :bookmark: **[RAD]** Reinforcement Learning with Augmented Data **(NeurIPS 2020)** [*(paper)*](https://proceedings.neurips.cc/paper/2020/hash/e615c82aba461681ade82da2da38004a-Abstract.html) [*(code)*](https://github.com/MishaLaskin/rad) 

RAD can be regarded as a specific form of DrQ with 𝐾 = 1 and 𝑀 = 1, which is a plug-and-play module that can be plugged into any reinforcement learning method without making any changes to the underlying algorithm.

## 2 Explicit Policy Regularization with Auxiliary Tasks


## 3 Task-Specific Representation Decoupled from Policy Optimization





## 4 Task-Agnostic Representation using Unsupervised Learning
