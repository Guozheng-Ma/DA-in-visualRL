# How to Augment the Data in Visual RL?


## 1 Observation Augmentation, Transition Augmentation and Trajectory Augmentation

### 1.1 Observation Augmentation

A typical approach to observation augmentation is applying the classical image manipulations to the observed images; and most such manipulations are originally proposed for computer vision applications.

> :bookmark: **[RAD]** Reinforcement Learning with Augmented Data **(NeurIPS 2020)** [*(paper)*](https://proceedings.neurips.cc/paper/2020/hash/e615c82aba461681ade82da2da38004a-Abstract.html) [*(code)*](https://github.com/MishaLaskin/rad)
> 
> **RAD** performs the first extensive study of general data augmentations for RL.

![AugTypes](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/3f6fb63bc8b565e231fbf77ac7f978cf298b82c0/Image/AugTypes_long.png)

### 1.2 Transition Augmentation

Augmenting $s_t$ with fixed supervised signals (e.g., reward $r_t$ and action $a_t$) can be viewed as a kind of local perturbation of $s_t$.
To ensure the the validity of the augmented transition $<s_t^{aug}, a_t, r_t, s_{t+1}^{aug}>$, the augmented observation $s_t^{aug}$ is only allowed to be in the vicinity of $s_t$.
Hence, local perturbation is inherently limited in increasing data diversity, which is a common issue of all observation augmentations.
