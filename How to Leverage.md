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
![SVEA](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/8e5f915c20c1a7f20bb2b1b9fe4c77094b303601/Image/SVEA.png)
- First, SVEA uses only unaugmented data copies to estimate 𝑄 -targets to avoid erroneous bootstrapping caused by data augmentation.
- Second, SVEA formulates a modified 𝑄 -objective to estimate the 𝑄 -value over both augmented and unaugmented copies of the observations, which can be expressed in a modified ERM form as:

$$
\begin{aligned}
J_{Q}^{\mathrm{SVEA}}(\theta) &= \alpha \sum_{i=1}^{N} ||Q_{\theta}(s_{i}, a_{i})-y_{i}||^{2} + \beta\sum_{i=1}^{N}\sum_{m=1}^{M}  ||Q_{\theta}(f(s_{i}, \nu_{i, m}), a_{i})-y_{i}||^{2} \\
&= \alpha\sum_{i=1}^{N} l(s_{i},a_i,r_i, s_{i}^{\prime}) + \beta \sum_{i=1}^{N} \sum_{m=1}^{M} l(f(s_{i}, \nu_{i, m}) ,a_i,r_i, s_{i}^{\prime})
\end{aligned}
$$

> The detailed discussion of :bookmark:**DrQ** and :bookmark:**SVEA** can be viewed in [our survey paper]().

## 2 Explicit Policy Regularization with Auxiliary Tasks



### 2.1 Contrastive-based Auxiliary Tasks

> :bookmark: **[CURL]** Contrastive Unsupervised Representations for Reinforcement Learning **(ICML 2020)** [*(paper)*](http://proceedings.mlr.press/v119/laskin20a.html) [*(code)*](https://github.com/MishaLaskin/curl) [:bookmark:](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/main/How%20to%20Leverage.md)

CURL is the first general framework for combining multi-view contrastive learning and data augmentation in visual RL.
It builds an auxiliary contrastive task to learn useful state representations by maximizing the mutual information between the different augmented views of the same observations to improve transformation invariance of the learned embedding. 

Note that the contrastive representation is trained **jointly** with the RL algorithm, and the latent encode receives gradients from both the contrastive learning objective and the RL objective.

![CURL](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/main/Image/CURL.png)

> :bookmark: **[DRIBO]** DRIBO: Robust Deep Reinforcement Learning via Multi-View Information Bottleneck **(ICML 2022)** [*(paper)*](https://proceedings.mlr.press/v162/fan22b.html) [*(code)*](https://github.com/BU-DEPEND-Lab/DRIBO)

Although maximizing the similarity between augmented versions of the same observation is valuable to state representation, maximizing the lower-bound of mutual information may inevitably retain some task-irrelevant information, limiting the generalization ability of agents. 

To tackle this issue, DRIBO uses contrastive learning combined with a multi-view information bottleneck (MIB) auxiliary objective to learn representations that only contain taskrelevant information predictive of the future while eliminating task-irrelevant information.

### 2.2 Predictive-based Auxiliary Tasks






## 3 Task-Specific Representation Decoupled from Policy Optimization





## 4 Task-Agnostic Representation using Unsupervised Learning
