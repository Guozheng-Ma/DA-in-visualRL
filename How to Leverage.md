# How to Leverage the Augmented Data in Visual RL?

![How to Leverage the Augmented Data in Visual RL?](https://github.com/Guozheng-Ma/DA-in-visualRL/blob/278bec04acfb6a7bc1b98e07cb34baae7c9de950/Image/Form%20and%20Structure.png)

## 1 Implicit Policy Regularization

The initial and naive practice of data augmentations is to expand the training set with augmented (synthesized) samples.
This practice introduces prior-based human knowledge into the data, instead of designing explicit penalty terms or modifying the optimization procedure.
Hence, it is often classified as a type of implicit regularization, formulated as the empirical risk minimization on augmented data (DA-ERM) in supervised learning tasks:

$$
\widehat{h}^{d a-e r m} \triangleq \underset{h \in \mathcal{H}}{\operatorname{argmin}} \sum_{i=1}^{N} l\left(h\left(\mathbf{x}_{i}\right), y_{i}\right)+\sum_{i=1}^{N} \sum_{j=1}^{\alpha} l\left(h\left(\mathbf{x}_{i, j}\right), y_{i}\right)
$$

where $\left(\mathbf{x}_{i}, y_i\right)$ is the original training data ($\mathbf{x}_{i} \in \mathcal{X}$ is the input feature, and $y_{i} \in \mathcal{Y}$ is its label); $\mathbf{x}_{i,j}$ is the augmented data preserving the corresponding label $y_{i}$;
$l: \mathcal{Y} \times \mathcal{Y} \rightarrow \mathbb{R}$ is the loss function and $h(\cdot)$ is the model to be optimized.

In the visual RL community, RAD and DrQ first leverage classical image transformations such as Crop to augment the input observations as implicit regularization.
In the original paper, DrQ suggests two distinct ways to regularize the Q-function.
First, it uses $K$ augmented observations from the original $s_i^{\prime}$ to obtain the target values for each transition tuple $(s_i,a_i,r_i,s_i^{\prime})$:

$$
y_{i}=r_{i}+\gamma \frac{1}{K} \sum_{k=1}^{K} Q_{\theta}(f(s_{i}^{\prime}, \nu_{i, k}^{\prime}), a_{i, k}^{\prime}), a_{i, k}^{\prime} \sim \pi(\cdot \mid f(s_{i}^{\prime}, \nu_{i, k}^{\prime}))
\label{drq1}
$$

where $f: \mathcal{S} \times \mathcal{T} \rightarrow \mathcal{S}$ is the augmentation function and $\nu$ is the parameters of $f(\cdot)$, randomly sampled from the set of all possible parameters $\mathcal{T}$.
Alternatively, DrQ generates $M$ different augmentations of $s_i$ to estimate the Q function:

$$
J_{Q}^{\mathrm{DrQ}}(\theta) = \frac{1}{N M} \sum_{i=1, m=1}^{N, M} ||Q_{\theta}(f(s_{i}, \nu_{i, m}), a_{i})-y_{i}||^{2}_2
\label{drq2}
$$

## 2 Explicit Policy Regularization with Auxiliary Tasks


## 3 Task-Specific Representation Decoupled from Policy Optimization





## 4 Task-Agnostic Representation using Unsupervised Learning
