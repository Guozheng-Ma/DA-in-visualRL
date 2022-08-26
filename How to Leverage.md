# How to Leverage the Augmented Data in Visual RL?

![How to Leverage the Augmented Data in Visual RL?](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/278bec04acfb6a7bc1b98e07cb34baae7c9de950/Image/Form%20and%20Structure.png)

## 1 Implicit Policy Regularization

The initial and naive practice of data augmentations is to expand the training set with augmented (synthesized) samples.
This practice introduces prior-based human knowledge into the data, instead of designing explicit penalty terms or modifying the optimization procedure.
Hence, it is often classified as a type of implicit regularization, formulated as the empirical risk minimization on augmented data (DA-ERM) in supervised learning tasks:

$$
\widehat{h}^{d a-e r m} \triangleq \underset{h \in \mathcal{H}}{\operatorname{argmin}} \sum_{i=1}^{N} l\left(h\left(\mathbf{x}_{i}\right), y_{i}\right)+\sum_{i=1}^{N} \sum_{j=1}^{\alpha} l\left(h\left(\mathbf{x}_{i, j}\right), y_{i}\right)
$$

In the visual RL community, RAD and DrQ first leverage classical image transformations such as Crop to augment the input observations as implicit regularization.

> 

## 2 Explicit Policy Regularization with Auxiliary Tasks


## 3 Task-Specific Representation Decoupled from Policy Optimization





## 4 Task-Agnostic Representation using Unsupervised Learning
