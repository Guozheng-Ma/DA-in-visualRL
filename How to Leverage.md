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
With the information bottleneck principle, DRIBO constructs a relaxed Lagrangian loss to obtain a sufficient representation with minimal task-irrelevant information.

![DRIBO](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/main/Image/DRIBO.png)


### 2.2 Predictive-based Auxiliary Tasks

The motivation of future prediction tasks is to encourage state representations to be predictive of future states given the current state and future action sequence.

> :bookmark: **[SPR]** Data-Efficient Reinforcement Learning with Self-Predictive Representations **(ICLR 2021)** [*(paper)*](https://openreview.net/forum?id=uCQfPZwRaUu&fbclid=IwAR3FMvlynXXYEMJaJzPki1x1wC9jjA3aBDC_moWxrI91hLaDvtk7nnnIXT8) [*(code)*](https://github.com/mila-iqia/spr)

SPR produces state representations by minimizing the prediction error between the true future states and predicted future states using the explicit multi-step dynamics model.
It also incorporates data augmentation into the future prediction task, which enforces the consistency across different views of each observation.

Dynamics model (DM) h(·, ·) operates entirely in the latent space to predict the transition dynamics, and the prediction loss is computed by summing up the difference (error) between the predicted representations and observed representations.

![SPR](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/main/Image/SPR.png)

## 3 Task-Specific Representation Decoupled from Policy Optimization

Since the training of RL is fragile to excessive data variations, a naive application of data augmentation may severely damage the training stability.
This poses a dilemma: aggressive augmentations are necessary for achieving good generalization in the visual domain, while injecting heavy data augmentations into the optimization of RL objective may cause a deterioration in both the sample efficiency and the training stability.

Recent works argue that this is mainly due to **the conflation of two objectives: policy optimization and robust representation learning**.
Hence, an intuitive idea is to **decouple the training data flow: using non-augmented or weak-augmented data for RL optimization while using strongaugmented data for representation learning**.

![classfication](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/main/Image/classfication.png)

As shown in Figure above, there are two strategies to achieve the decoupling:
1. Dividing the training data into two streams to **separately** optimize RL objective and repersentation learning objective; and the model’s parameters are iteratively updated by the two objectives.
2. Optimizing the RL objective first and then leveraging DA for knowledge distillation **sequentially**.

> :bookmark: **[SODA]** Generalization in Reinforcement Learning by Soft Data Augmentation **(ICRA 2021)** [*(paper)*](https://ieeexplore.ieee.org/abstract/document/9561103) [*(code)*](https://github.com/nicklashansen/dmcontrol-generalization-benchmark)

SODA maximizes the mutual information between the latent representations of augmented and non-augmented data as the auxiliary objective, and continuously alternates between optimizing RL objective with non-augmented data and representation pbjective with augmented data.
While the policy is learned only from non-augmented data, SODA still benefits substantially from data augmentation through representation learning.

![SODA](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/main/Image/SODA.png)

> :bookmark: **[SECANT]** Self-Expert Cloning for Zero-Shot Generalization of Visual Policies **(ICML 2021)** [*(paper)*](https://proceedings.mlr.press/v139/fan21c.html) [*(code)*](https://github.com/LinxiFan/SECANT)

SECANT first trains a sample-efficient expert with Random Crop (weak augmentation).
In the second stage, a student network learns a generalizable policy by mimicking the behavior of the expert at every time step, but with a crucial difference: the expert computes the ground-truth actions from unmodified observations, while the student learns to predict the same actions from heavily corrupted observations.

The student optimizes the imitation objective by gradient descent on a supervised regression loss, which has better training stability than the RL loss. Meanwhile, the policy distillation through strong augmentations can greatly remedy overfitting to acquire robust representation without sacrificing policy performance.

![SECANT](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/main/Image/SECANT.png)

## 4 Task-Agnostic Representation using Unsupervised Learning

> **It can also be considered as a type of unsupervised pre-training.**

The visual representations of standard end-to-end RL methods heavily rely on the task-specific reward, making them ineffective for other tasks.
To overcome this limitation, the environment can be first explored in a **task-agnostic fashion** to learn its visual representations **without any task-specific rewards**, and specific downstream tasks can be subsequently solved efficiently.

> :bookmark: **[ATC]** Decoupling Representation Learning from Reinforcement Learning **(ICML 2021)** [*(paper)*](http://proceedings.mlr.press/v139/stooke21a.html) [*(code)*](https://github.com/astooke/rlpyt/tree/master/rlpyt/ul)

**Augmented Temporal Contrast (ATC)** trains the CNN encoder with an unsupervised objective and then learns RL policies on top of the extracted features.
The unsupervised objective is temporal contrast of an observation with one from a specified, near-future time step.

**NOTE:** In contrast to CURL, which maximizes information between views of the same observation, ATC maximizes information between observations separated by a short time interval.

![ATC](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/main/Image/ATC.png)


> :bookmark: **[Proto-RL]** Reinforcement Learning with Prototypical Representations **(ICML 2021)** [*(paper)*](http://proceedings.mlr.press/v139/yarats21a.html) [*(code)*](https://github.com/denisyarats/proto) 

Proto-RL designs a self-supervised scheme that fits an encoder that embeds high-dimensional observations to lowdimensional latent states and defines an exploration strategy that allows for the discovery of diverse transitions.
-  Learning is done by optimizing the (self-supervised) clustering assignment loss.
-  To encourage exploration, prototypes are simultaneously used to compute an entropy-based intrinsic reward rˆt
that is maximized by the exploration agent.

![Proto RL](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/main/Image/Proto%20RL.png)



