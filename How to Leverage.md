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

> :bookmark: **[SVEA]** Stabilizing Deep Q-Learning with ConvNets and Vision Transformers under Data Augmentation **(NeurIPS 2021)** [*(paper)*](https://proceedings.neurips.cc/paper/2021/hash/1e0f65eb20acbfb27ee05ddc000b50ec-Abstract.html) [*(code)*](https://github.com/nicklashansen/dmcontrol-generalization-benchmark)

SVEA aims to enhance the stability of optimizing the RL objective with DA. It consists of two main components:
- First, SVEA uses only unaugmented data copies to estimate 𝑄 -targets to avoid erroneous bootstrapping caused by data augmentation.
- Second, SVEA formulates a modified 𝑄 -objective to estimate the 𝑄 -value over both augmented and unaugmented copies of the observations, which can be expressed in a modified ERM form as:

$$
\begin{aligned}
J_{Q}^{\mathrm{SVEA}}(\theta) &= \alpha \sum_{i=1}^{N} ||Q_{\theta}(s_{i}, a_{i})-y_{i}||^{2} + \beta\sum_{i=1}^{N}\sum_{m=1}^{M}  ||Q_{\theta}(f(s_{i}, \nu_{i, m}), a_{i})-y_{i}||^{2} \\
&= \alpha\sum_{i=1}^{N} l(s_{i},a_i,r_i, s_{i}^{\prime}) + \beta \sum_{i=1}^{N} \sum_{m=1}^{M} l(f(s_{i}, \nu_{i, m}) ,a_i,r_i, s_{i}^{\prime})
\end{aligned}
$$

## 2 Explicit Policy Regularization with Auxiliary Tasks


## 3 Task-Specific Representation Decoupled from Policy Optimization





## 4 Task-Agnostic Representation using Unsupervised Learning
