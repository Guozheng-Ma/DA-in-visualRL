# How to Augment the Data in Visual RL?


## 1 Observation Augmentation, Transition Augmentation and Trajectory Augmentation

### 1.1 Observation Augmentation

A typical approach to observation augmentation is applying the classical image manipulations to the observed images; and most such manipulations are originally proposed for computer vision applications.

> :bookmark: **[RAD]** Reinforcement Learning with Augmented Data **(NeurIPS 2020)** [*(paper)*](https://proceedings.neurips.cc/paper/2020/hash/e615c82aba461681ade82da2da38004a-Abstract.html) [*(code)*](https://github.com/MishaLaskin/rad)
> 
> **RAD** performs the first extensive study of general data augmentations for RL.

![AugTypes](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/3f6fb63bc8b565e231fbf77ac7f978cf298b82c0/Image/AugTypes_long.png)

### 1.2 Transition Augmentation

Observation augmentation can be viewed as a kind of **local perturbation**, which is inherently limited in increasing data diversity.
An intuitive solution is to apply interpolation among different data points instead of performing the local perturbation on each individual data point.

> :bookmark: **[MixReg]** Improving Generalization in Reinforcement Learning with Mixture Regularization **(NeurIPS 2020)** [*(paper)*](https://proceedings.neurips.cc/paper/2020/hash/5a751d6a0b6ef05cfe51b86e5d1458e6-Abstract.html) [*(code)*](https://github.com/kaixin96/mixreg) 
>
> MixReg convexly combines two observations and their supervised signals to generate augmented data.
For example, let ${y_i}$ and ${y_j}$ denote the associated signals for states ${s_i}$ and ${s_j}$, which can be the reward or state values. 
After interpolating the observations by ${\tilde{s}=\lambda s_{i}+(1-\lambda) s_{j}}$, MixReg introduces the mixture regularization in a similar manner by ${\tilde{y}=\lambda y_{i}+(1-\lambda) y_{j}}$, which helps learn more effective representations and smoother policies.

![MixReg](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/1e7e46d23633f9379da91527f7509cd195008901/Image/Mixreg.png)

### 1.3 Trajectory Augmentation

> **Transition and Trajectory Augmentation specifically consider the properties of RL to expand the scope of augmentation.**

> :bookmark: **[PlayVirtual]** Augmenting Cycle-Consistent Virtual Trajectories for Reinforcement Learning **(NeurIPS 2021)** [*(paper)*](https://proceedings.neurips.cc/paper/2021/hash/2a38a4a9316c49e5a833517c45d31070-Abstract.html) [*(code)*](https://github.com/microsoft/Playvirtual) 
> 
> Since augmenting observations or transitions cannot directly enrich the trajectories experienced in training, to further improve the sample efficiency, PlayVirtual augments the actions to generate synthesized trajectories under the self-supervised cycle consistency constraint.

![PlayVirtual](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/4984287c86b50e0fe37479a0dffec1e0a6996786/Image/Playvirtual.png)


## 2 Context-aware/Semantic-level Data Augmentation

### 2.1 Introducing human guidance.

> :bookmark: **[EXPAND]** Widening the Pipeline in Human-Guided Reinforcement Learning with Explanation and Context-Aware Data Augmentation **(NeurIPS 2021)** [*(paper)*](https://proceedings.neurips.cc/paper/2021/hash/b6f8dc086b2d60c5856e4ff517060392-Abstract.html)
> 
> Human-in-the-loop reinforcement learning (HIRL) is a general paradigm to leverage human guidance to assist the RL process. EXPAND introduces human saliency map to mark the importance of different regions, and only perturbs the irrelevant regions. Saliency maps contain human domain knowledge, allowing context information to be embedded into the augmentation.

![EXPAND](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/059e52c7fd434a4043499a3925c22744c9de7753/Image/EXPAND.png)


### 2.2 Excavating the task-relevance.


> :bookmark: **[TLDA]** Don’t Touch What Matters: Task-Aware Lipschitz Data Augmentation for Visual Reinforcement Learning **(IJCAI 2022)** [*(paper)*](https://arxiv.org/abs/2202.09982)
> 
> TLDA explicitly defines the task-relevance by computing the Lipschitz constants when perturbing the corresponding pixels. Regions with large Lipschitz constants indicate that they are crucial for the current task decision, which will subsequently be protected from augmentation.

![TLDA](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/27ee08c72d57c7b028b48fd7a977ff947cbd5622/Image/TLDA.png)

