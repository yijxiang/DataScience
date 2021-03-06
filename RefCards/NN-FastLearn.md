# Fast Learning Algorithms

## Overview

<div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
  <a href="http://page.mi.fu-berlin.de/rojas/neural/chapter/K8.pdf" ismap target="_blank">
    <img src="../ML/MLNN-Hinton/img/a12-24.png" style="margin: 0.1em;" alt="Taxonomy of learning algorithms" title="Taxonomy of learning algorithms" width=450>
  </a>
</div>

+ The fast variations of backpropagation divided into two main methods
  + gradient descent
    + using information about the error function's partial derivatives
  + relaxation
    + trying to adjust the weights to fit the problem in stochastic way or solving a linear subproblem

+ Class of derivatives
  + first order
    + standard backpropagation
    + on-line propagation not exactly following the gradient's direction, but also partially qualify as a relaxation method
  + adaptive first order
    + a combination of gradient descent and relaxation
    + two groups
      + single global learning rate
      + a learning rate for each weight
  + second order
    + the conjugate gradient methods of numerical analysis rely also on a first-order approximation of second-order features of the error function

+ [Oscillations along vertical direction](../ML/MLNN-Hinton/a03-Optimization.md#adaptive-learning-rates)

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/neural-network-optimization-7ca72d4db3e0" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/1*0v0zucWChoudFcJRPpB74Q.png" style="margin: 0.1em;" alt="Gradient descent oscillates along vertical direction" title="Gradient descent oscillates along vertical direction" width=300>
    </a>
  </div>


## Momentum

### Classical Momentum

+ [Momentum](../ML/MLNN-Hinton/a03-Optimization.md#momentum)
  + an inertia motion of object to move in the direction of motion
  + the general direction that the optimization algorithm is moving
  + optimization algorithm moving in a general direction, the momentum causes it to 'resist' changes in the direction
  + dampening of oscillations for high curvature surfaces
  + an added term in the objective function
  + a value in $[0, 1]$ increasing the size of the steps taken towards the minimum by trying to jump from a local minimum
  + large momentum & small learning rate: fast convergence
  + large momentum & large learning rate: skip the minimum with a huge step
  + small momentum: not reliably avoid local minima and slow down  the training of the system
  + help in smoothing out the variations, if the gradient keeps changing direction
  + right value of momentum: either learned by hit and trial or through cross-validation

+ Overview
  + applied to both full batch or mini-batch learning
  + probably the commonest recipe for big neural nets: combining stochastic gradient descent with mini matches and momentum

+ [Momentum Method](https://trongr.github.io/neural-network-course/neuralnetworks.html)
  
  __Intuition: rolling ball.__ Modify the Delta Rule

    \[\Delta w(t) = -\varepsilon \frac{\partial E}{\partial w}(t)\]

  to include a "momentum" term

    \[\Delta w(t) = \alpha \Delta w(t-1) - \varepsilon \frac{\partial E}{\partial w} (t)\]

  + $\alpha$: a factor slightly less than 1
  + $\Delta w(t)$ remembers a little bit of its previous direction via $\alpha \Delta w(t-1)$
  + [Implementation of Stochastic Gradient Descent w/ Momentum](../ML/MLNN-Hinton/src/sgd_momentum.py)

+ [The intuition behind the momentum method](../ML/MLNN-Hinton/06-MiniBatch.md#the-momentum-method)
  + Analogy
    + a ball on the error surface
    + weight vector: the location of the ball in the horizontal plane
    + the ball starting stationary
    + initialized by following the direction of steepest descent, the gradient
    + once gaining velocity, the ball no longer in the same direction as the gradient
    + its momentum making it keep going in the previous direction
  + damping oscillations in directions of high curvature by combining gradients w/ opposite signs
    + eventually getting to a low point on the surface
    + viscosity: making the velocity die off gently on each or update
  + built up speed in directions w/ a gradient but consistent gradient

+ [Mathematical representation](../ML/MLNN-Hinton/06-MiniBatch.md#the-momentum-method)
  
  \[\begin{align*}
    \mathbf{v}(t) &= \alpha \, \mathbf{v}(t-1) - \varepsilon \frac{\partial E}{\partial \mathbf{w}}(t) \tag*{(1)} \\\\
    \Delta \mathbf{w}(t) &= \mathbf{v} (t) \tag*{(2)} \\
     &= \alpha \, \mathbf{v}(t-1) - \varepsilon \frac{\partial E}{\partial \mathbf{w}}(t) \\
     &= \alpha \, \Delta \mathbf{w} (t-1) - \varepsilon \frac{\partial E}{\partial \mathbf{w}}(t) \tag*{(3)}
  \end{align*}\]

  + Eq. (1):
    + the velocity at time $t$: the mini-batch w/ $t-1$ attenuated by a number, like $0.9$, and adding the effect of the current gradient
    + $t$: the updates of weights
    + (alpha) momentum = the viscosity (0.9)
    + effect of gradient: downhill by a given learning rate times the gradient at time $t$
    + The effect of the gradient is to increment the previous velocity.
    + The velocity also decays by $\alpha$ which is slightly less than 1.
  + Eq. (2): The weight change is equal to the current velocity.
  + Eq. (3): The weight change can be expressed in terms of the previous weight change and the current gradient.

+ [The behavior of the momentum method](../ML/MLNN-Hinton/06-MiniBatch.md#the-momentum-method)
  + error surface as a tilted plane
    + the gain of velocity from the gradient balanced by the multiplicative attenuation of the velocity due to the momentum term
    + the ball reaches a terminal velocity
    + if momentum $\rightarrow 1$, going down much faster than simple gradient descent
    + terminal velocity: as $t \rightarrow \infty$

    \[\mathbf{v}(\infty) = \frac{1}{1 - \alpha} \left( -\varepsilon \frac{\partial E}{\partial \mathbf{w}} \right)\]

    + Derivation

      \[\begin{align*}
        & v(\infty) = \alpha \, v(\infty) - \varepsilon \, \frac{\partial E}{\partial w} (t) \\
        & (1 - \alpha) \, v(\infty) = - \varepsilon \frac{\partial E}{\partial w} (t) \\
        & v(\infty) = \frac{1}{(1 - \alpha)} \, \left(-\varepsilon \frac{\partial E}{\partial w}(t)\right)
      \end{align*}\]

    + $\alpha = 0.99$: 100 times as fast as the learning rate alone
  + preventing big momentum to change quickly $\rightarrow$ difficult to find the right relative values of different weights
    + playing w/ a small momentum (e.g. 0.5) to average out sloshes in obvious ravines
    + once the large gradients disappeared and the weights stuck in a ravine the momentum
  + using a small learning rate with a big momentum to get rid of an overall learning rate
  + learning at a rate alone that would cause divergent oscillations without the momentum

+ [Formula for Momentum](../ML/MLNN-Hinton/a03-Optimization.md#classical-momentum)
  + using past gradients for updating values
  + $v$: velocity
  + more weight applied to more recent gradients, creating an exponentially decaying average of gradients

  \[\begin{array}{rcl} g &=& \frac{1}{m} \displaystyle \sum_i \Delta_\theta L(f(x^{(i)}; \theta), y^{(i)}) \\ v &=& \alpha v + (-\varepsilon g) \end{array}\]

  + $\alpha \in [0, 1)$ controls how quickly effect of past gradients decay
  + $\varepsilon$: current gradient update

+ [Compute gradient estimate](../ML/MLNN-Hinton/a03-Optimization.md#classical-momentum)

    \[g = \frac{1}{m} \sum_i \Delta_\theta L(f(x^{(i)}; \theta), y^{(i)})\]
  + Update velocity: $v = \alpha v - \varepsilon g$
  + Update parameters: $\theta = \theta + v$
  + Impacts
    + SGD w/ momentum updates no real advantage at the first few updates over vanilla SGD
    + As the number of updates increases the momentum kickstarts and allows faster convergence.


### Backpropagation for Classical Momentum

+ [Momentum method](../ML/MLNN-Hinton/a12-Learning.md#811-backpropagation-with-momentum)
  + minimizing the error function: wide oscillation of the search process w/ the gradient descent
  + traditional gradient descent: computed for each new combination of weights
  + momentum approach: compute the negative gradient direction a weighted average of the current gradient and the previous correction direction for each step
  + accelerating convergence: increasing the learning rate up to an optimal value
  + purpose: allowing the attenuation of oscillations in the iteration process

+ [Mathematical representation for momentum](../ML/MLNN-Hinton/a12-Learning.md#811-backpropagation-with-momentum)
  + A network with $n$ different weights $w_1, w_2, \dots, w_n$
  + Assumption and Notations
    + $E$: the error function
    + $\gamma$: the learning rate
    + $\alpha$: the momentum rate
  + The $i$-th correction for weight $w_k$

    \[\Delta w_k(i) = -\gamma \, \frac{\partial E}{\partial w_k} + \alpha \, \Delta w_k (i-1)\]

+ [Optimization](../ML/MLNN-Hinton/a12-Learning.md#811-backpropagation-with-momentum)
  + optimal parameters highly depends on the learning task
  + no general strategy to deal with the problem
  + tradeoffs: choosing the a specific learning and momentum rates
  + observing the oscillating behavior on backpropagation feedback rule and large momentum rates

+ [Linear associator](../ML/MLNN-Hinton/a12-Learning.md#the-linear-associator)
  + a single computing element with associated weights $w_1, w_2, \dots, w_n$
  + input: $x_1, x_2, \dots, x_n$
  + output: $w_1x_1 + w_2x_2 + \cdots + w_n x_n$

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="http://page.mi.fu-berlin.de/rojas/neural/chapter/K8.pdf" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/a12-02.png" style="margin: 0.1em;" alt="Linear associator" title="Linear associator" width=200>
    </a>
  </div>

+ [Mathematical Representation for Linear Associator](../ML/MLNN-Hinton/a12-Learning.md#the-linear-associator)
  + Assumptions & Notations
    + $(\mathbf{x_1}, y_1), (\mathbf{x_2}, y_2), \dots, (\mathbf{x_p}, y_p)$: the input-output $p$ ordered pairs
    + $\mathbf{x}$: vector of input patterns w/ $n$-dimensional rows
    + $\mathbf{w}$: vector of the weights of the linear associator w/ $n$-dimensional columns
    + $\mathbf{X}$: a $p \times m$ matrix w/ $\mathbf{x_1}, \mathbf{x_2}, \dots \mathbf{x_p}$ as rows
    + $\mathbf{y}$: a column vector of the scalars $y_1, y_2, \dots, y_p$
  + the learning task objective: minimize the quadratic error

    \[\begin{align*}
    E &= \sum_{i=1}^{n} \| \mathbf{x_i} \cdot \mathbf{w} - y_i \|^2 \\
      &= \| \mathbf{X}\mathbf{w} - \mathbf{y} \|^2 = (\mathbf{X}\mathbf{w} - \mathbf{y})^T(\mathbf{X}\mathbf{w} - \mathbf{y}) \\
      &= \mathbf{w}(\mathbf{X}^T \mathbf{X})\mathbf{w} -2 \: \mathbf{y}^T\mathbf{X}\mathbf{w} + \mathbf{y}^T\mathbf{y}
    \end{align*}\]

  + the lengths of the principal axes: determined by the magnitude of the eigenvalues of the correlation of matrix $\mathbf{X}^T\mathbf{X}$
  + gradient descent: most effective w/ the same length when the principal axes of the quadratic form

+ [Eigenvlaues in the correlation matrix $\mathbf{X}^T\mathbf{X}$](../ML/MLNN-Hinton/a12-Learning.md#the-linear-associator)
  + the eigenvalues $\to$ the lengths of the principal axes of the error function
  + the range of possible values of $\gamma$ reduces as one of these eigenvalues much larger than the others

+ [Convergence and Divergence zones](../ML/MLNN-Hinton/a12-Learning.md#the-linear-associator)
  + parameters combinations in the boundary btw regions: stable oscillations
  + $\gamma > 4 \cdot 2/k$: not balanced with any value of $\alpha$
  + $\gamma > 1$: a geometric explosion of the iteration process
  + $1/k < \gamma < 2/k$: stable oscillation; the boundaries between regions
  + $\gamma < 1/2k$: optimal convergence speed w/ a unique $\alpha$
  + jagged line: the optimal combinations of $\gamma$ and $\alpha$

+ [Critical parameter combinations](../ML/MLNN-Hinton/a12-Learning.md#critical-parameter-combinations)
  + Backpropagation: choosing a learn rate $\gamma$ w/o any previous knowledge of the correlation matrix of the input
  + Conservative approach: choosing a very small learning rate
  + In case of a correlation matrix $\mathbf{X}^T\mathbf{X}$ with some very large eigenvalues, a given choice of $\gamma$ could led to divergence in the associated direction in weight space.

+ [Error function in weight space](../ML/MLNN-Hinton/a12-Learning.md#critical-parameter-combinations)
  + Paths for backpropagation learning w/ linear associator
  + Bounded nonlinear error function and the result of several iterations

+ [learning rate considerations](../ML/MLNN-Hinton/a12-Learning.md#critical-parameter-combinations)
  + too small: possible to get stuck in local minima
  + too big: possible oscillatory traps

+ [Remedy](../ML/MLNN-Hinton/a12-Learning.md#critical-parameter-combinations)
  + adaptive learning rates
  + statistical preprocessing of the learning set w/ decorrelation; ie. no excessively large eigenvalues of the correlation matrix


### Nesterov Momentum

+ [A better type of momentum](../ML/MLNN-Hinton/06-MiniBatch.md#the-momentum-method) (Nesterov 1983)
  + standard momentum method
    1. compute the gradient at the current location
    2. take a big jump in the direction of the updated accumulated gradient
  + Ilya Sutskever (2012)
    + a new form of momentum working better
    + inspired by the Nesterov method for optimizing convex functions
  + Nesterov approach
    1. make a big jump in the direction of the previous accumulated gradient
    2. measure the gradient where ending up and making a correction: better to correct a mistake after you have made it
  + standard vs Nesterov
    + standard: adding the current gradient and then gambling on the big jump
    + Nesterov: using the previous accumulated gradient to make the big  and then correct itself at the place

+ [Nesterov Method](https://trongr.github.io/neural-network-course/neuralnetworks.html)
  + old momentum method: calculate gradient, i.e., correct your previous mistake, at current point, then jump

    \[\Delta w(t) = \alpha \Delta w(t-1) - \varepsilon \frac{\partial E}{\partial w} (t-1)\]

  + new and improved momentum method: jump first, then correct your mistake at the description

    \[\Delta w(t) = \alpha \Delta w(t-1) - \varepsilon \frac{\partial E}{\partial w} (t)\]

+ [Nesterov momentum](../ML/MLNN-Hinton/a03-Optimization.md#nesterov-momentum)
  + Sutskever, Martens et al. "[On the importance of initialization and momentum in deep learning](http://proceedings.mlr.press/v28/sutskever13.pdf)" 2013
  + Classical vs Nesterov Momentum
    + Classical
      + first correct velocity
      + make a big step according to that velocity (and then repeat)
  + Nesterov
    + first make a step into velocity direction
    + make a correction to a velocity vector based on a new location (then repeat)

  + Hugh difference in practice
    + Apply an interim update: $\tilde{\theta} = \theta + v$
    + Perform a correction based on gradient at the interim point

      \[\begin{array}{rcl} g &=& \frac{1}{m} \sum_i \Delta_\theta L(f(x^{(i)}; \tilde{\theta}), y^{(i)}) \\ v &=& \alpha v - \varepsilon g \\ \theta & = & \theta + v \end{array}\]

    + momentum based on look-ahead slope
    + visual representation of the difference between the traditional momentum update and Nesterov momentum

    <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
      <a href="https://towardsdatascience.com/neural-network-optimization-7ca72d4db3e0" ismap target="_blank">
        <img src="https://miro.medium.com/max/875/1*hJSLxZMjYVzgF5A_MoqeVQ.jpeg" style="margin: 0.1em;" alt="Nesterov momentum. Instead of evaluating gradient at the current position (red circle), we know that our momentum is about to carry us to the tip of the green arrow. With Nesterov momentum we therefore instead evaluate the gradient at this 'looked-ahead' position." title="Nesterov momentum. Instead of evaluating gradient at the current position (red circle), we know that our momentum is about to carry us to the tip of the green arrow. With Nesterov momentum we therefore instead evaluate the gradient at this 'looked-ahead' position." width=450>
      </a>
    </div>  


### Cyclical Momentum

+ [Momentum and learning rate](../ML/MLNN-Hinton/a13-HyperParam.md#43-cyclical-momentum)
  + closely related
  + optimal learning rate dependent on the momentum; momentum dependent on th elearning rate
  + learning rate: the most important hyper-parameter to tune
  + Yoshua Bengio. [Practical recommendations for gradient-based training of deep architectures](https://www.arxiv-vanity.com/papers/1206.5533/). In Neural networks: Tricks of the trade, pp. 437–478. Springer, 2012.
  + momentum also important
  + setting momentum as large as possible w/o causing instabilities during training

+ [Mathematical Representation of Momentum](../ML/MLNN-Hinton/a13-HyperParam.md#43-cyclical-momentum)
  + momentum: designed to accelerate network training but its effect on updating the weights is of the sam magnitude as the learning rate
  + Assumptions & Notations
    + $\theta$: all the network parameter
    + $\epsilon$: the learning rate
    + $\delta F(x, \theta)$: the gradient
    + $\v$: velocity
    + $\alpha$: the momentum coefficient
  + Stochastic gradient descent (SGD): updating the weight using the negative gradient

    \[\theta_{iter + 1} = \theta_{iter} - \epsilon \delta L(F(x, \theta), \theta) \tag{1}\]

  + update weight with momenum

    \[v_{iter + 1} = \alpha \, v_{iter} - \epsilon \delta F(x, \theta), \theta) \tag{2}\]

    \[\theta_{iter + 1} = \theta_{iter} + v \tag{3}\]

  + momentum: similar impact on the weight updates as the learning rate
  + velocity: a moving average of the gradient

+ [Cyclic Momentum](../ML/MLNN-Hinton/a13-HyperParam.md#43-cyclical-momentum)
  + cyclic learning rate, in particular, the learning rate range test: usful methods to find an optimal learning rate
  + experiment: moment range test NOT useful for finding an optimal momentum (Fig. 7(b))
  + using a decreasing cyclical momentum when the learning rate increases provides an equivalent result to the best constant momentum value but stablizes the training to allow larger learning rates
  + useful for starting with a large momentum and decreasing momentum while the learning rate is increasing
  + the learning rate improves the test accuracy and makes the training more robust to large learning rates
  + implementation is straightforward
  + example code in Appendix

+ [Momentum effect](../ML/MLNN-Hinton/a13-HyperParam.md#43-cyclical-momentum)
  + a larger value of momentum
    + speeding up the training
    + threaten the stability
    + causing divergence
  + a large momentum helping escape saddle points but can hurt the final convergence
  + cyclical momentum not better than a constant value
  + better proceure: test momentum in the range $[0.9, 0.99]$ and choose a value that performs best



## Parameter Initialization

### Initialization Strategies

+ [Convergence w/ initialization](../ML/MLNN-Hinton/a14-Advanced.md#6-initialization-strategies)
  + convex problem w/ a small learning rate: convergence guaranteed, no matter what the initialization
  + non-convex
    + not well understood to have principled, mathematically nice initialization strategies
    + heuristics used to select a reasonable set of starting weights from which the network is trained

+ [Initialization strategies](../ML/MLNN-Hinton/a14-Advanced.md#6-initialization-strategies)
  + architecture: a fully connected layer with $m$ inputs and $n$ outputs
  + uniform distributed to obtain the initial weights

    \[ W_{ij} \sim U \left( 1\frac{1}{\sqrt{m}}, \frac{1}{sqrt{m}} \right) \]

  + popular Xavier initialization for its uniform distribution

    \[ w_{ij} \sim U \left( -\frac{6}{\sqrt{m+n}}, \frac{6}{\sqrt{m+n}} \right) \]

    + derived considering that the network consists of matrix multiplication with no nonlinearites
    + seems to perform well in practice

+ List of weight initialization: [initializers section of the Kreas documentation](https://keras.io/initializers/)


### Xavier Initialization

+ [Xavier initialization](../ML/MLNN-Hinton/a03-Optimization.md#xavier-initialization) is a simple heuristic for assigning network weights.

+ Objective: the variance to remain the same with each passing layer

+ Keep the signal from exploding to high values or vanishing to zero

+ To initialize the weights in such a way that the variance remains the same for both the input and the output

+ The weights drawn from a distribution with zero mean and a specific variance.

+ For a fully-connected layer with $m$ inputs:

  \[W_{ij} \sim N \left(0, \frac{1}{m} \right)\]

  + $m$: fan-in; the number of incoming neurons (input units in the weight tensor)
  + heuristic value: merely empirically observed to perform well


### HE Normal Initialization

+ [HE normal initialization](../ML/MLNN-Hinton/a03-Optimization.md#he-normal-initialization)
  + the same as Xavier Initialization, except that the variance multiplied by a factor of two
  + initialized the size of the previous layer which helps in attaining a global minimum of the cost function faster and more efficiently
  + random but differ in range depending on the size of the previous layer of neurons
  + controlled initialization hence the faster and more efficient gradient descent

+ For ReLU units

  \[W_{ij} \sim N \left(0, \frac{2}{m} \right)\]


### Bias Initialization

+ [Bias initialization](../ML/MLNN-Hinton/a03-Optimization.md#bias-initialization): how the biases of the neurons should be initialized

+ The simplest and a common way of initializing biases is to set them to zero.

+ Asymmetry breaking: provided by the small random numbers in th weights

+ ReLU non-linearity
  + using small constant values such as 0.01 for all biases
  + ensure that all ReLU units fire in the beginning and obtain and propagate some gradient

+ Main concern: avoid saturation at initialization within hidden units, ReLU by initializing biases to 0.1 instead of zero


### Pre-initialization

+ [Pre-initialization](../ML/MLNN-Hinton/a03-Optimization.md#pre-initialization):
  + common for convolutional networks used for examining images
  + involve importing the weights of an already trained network
  + used as the initial weights of the network to be trained
  + a tenable method to utilize for analyzing images with few data samples
  + underlying concept behind transfer learning


## Normalization

### Internal Covariate Shift

+ [Internal Covariate Shift](../ML/MLNN-Hinton/a03-Optimization.md#internal-covariate-shift):
  + the change in the distribution of network activation due to the change in network parameters during training
  + the parameters of a layer changed, the distribution of inputs to subsequent layers also changes
  + Issue: the shifts in input distributions tend to slow down learning, especially deep neural networks

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/neural-network-optimization-7ca72d4db3e0" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/1*Dnxnj2STbo-42DfalLMi-g.png" style="margin: 0.1em;" alt="Deep neural network: multiple hidden layers" title="Deep neural network: multiple hidden layers" width=250>
    </a>
  </div>

+ Whitened inputs
  + converge faster and uncorrelated
  + internal covariate shift leads to just the opposite

+ Ref: [Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift](https://arxiv.org/abs/1502.03167)
  + gradient descent converges much faster with feature scaling than without it


### Batch Normalization

+ [Batch normalization](../ML/MLNN-Hinton/a03-Optimization.md#batch-normalization)
  + a method intended to mitigate internal covariate shift for neral networks
  + an extension to the idea of feature standardization to other layers of the neural network

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/neural-network-optimization-7ca72d4db3e0" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/1*x3FtLuoYjWeNctiNPlTBjw.png" style="margin: 0.1em;" alt="Matrix representation of weights for hidden layers" title="Matrix representation of weights for hidden layers" width=250>
    </a>
  </div>

  + reducing overfit due to a slight regularization effect
  + similar to dropout, add some noise to each hidden layer's activations

+ [Batch normalization transformation](../ML/MLNN-Hinton/a03-Optimization.md#batch-normalization)
  + normalizes the output of a previous activation layer by subtracting the batch mean and dividing by the batch standard deviation.

    \[\begin{array}{lcl} H^\prime &=& \frac{H - \mu}{\sigma} \\ \mu &=& \frac{1}{m} \sum_i H_{i,:} \\ \sigma &=& \sqrt{\frac{1}{m} \sum_i (H - \mu)^2 + \delta}\end{array}\]

    + $\mu$: vector of mean activations across mini-batch
    + $\sigma$: vector of SD of each unit across mini-batch
  + allowing each layer of a network to learn by itself more independently of other layers
  + after shift/scale of activation outputs by some randomly initialized parameters, the weights in the next layer are no longer optimal.
  + Adding two trainable (learnable) parameters to each layer
    + normalized output multiplied by a "standard deviation" parameter ($\gamma$) and add a "mean" parameter ($\beta$)
    + let SGD do the denormalization by changing only these two wrights for each activation
    + not losing the stability of the network by changing all the weights

    \[\gamma H^\prime + \beta\]

  + For each of the N mini-batches, calculate the mean and standard deviation of the output

    <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
      <a href="https://towardsdatascience.com/neural-network-optimization-7ca72d4db3e0" ismap target="_blank">
        <img src="https://miro.medium.com/max/875/1*a-B6jX8B-8lfz5ZrIFQyFw.png" style="margin: 0.1em;" alt="Add normalization operations for layer 1" title="Add normalization operations for layer 1" height=200>
        <img src="https://miro.medium.com/max/875/1*LdQ7HKaqDYtszL8R0bdb4Q.png" style="margin: 0.1em;" alt="Add normalization operations for layer 2" title="Add normalization operations for layer 2" height=200>
      </a>
    </div>

  + subsequently repeated for all subsequent hidden layers
  + differentiate the joint loss for the N mini-batches and then backpropagate through the normalization operations

+ Testing time
  + the mean and standard deviations replaced with running average collected during training time
  + same as using the population statistics instead of mini-batch statistics
  + the output deterministically depends on the input

+ Advantages
  1. reduces internal covariate shift
  2. reduces the dependence of gradients on the scale of the parameters or their initial values
  3. regularizes the model ad reduces the need for dropout, photometric distortions, local response normalization and other regularization techniques
  4. allows use of saturating nonlinearities and higher learning rates



## Second-order algorithms

### General Representation

+ [Idea](../ML/MLNN-Hinton/a12-Learning.md#84-second-order-algorithms)
  + considering more information about the shape of the error function than the mere value of the gradient
  + considering the curvature of the error function at each step for better performance

+ [Quadratic approximation of the error function](../ML/MLNN-Hinton/a12-Learning.md#84-second-order-algorithms)
  + Assumptions & Notations
    + Quadratic error function
    + $\mathbf{w}$: the vector denoting all weights of a network
    + $E(\mathbf{w})$: the error function
    + $\Delta^2 E(\mathbf{w})$: the $n \times n$ Hessian matrix of second order partial derivatives
    + $\mathbf{w}^{(k)}$: the wright vector at the $k$-th iteration
  + Truncated Taylor series to approximate the error function $E$

    \[E(\mathbf{w} + \mathbf{h}) \approx E(\mathbf{w)} + \Delta E(\mathbf{w})^T \mathbf{h} + \frac{1}{2} \mathbf{h}^T \Delta^2 E(\mathbf{w}) \mathbf{h} \tag{6}\]
  
  + the $n \times n$ Hessian matrix of second order partial derivatives, $\Delta^2 E(\mathbf{w})$

    \[\Delta^2 E(\mathbf{w}) = \begin{bmatrix}
      \frac{\partial^2 E(\mathbf{w})}{\partial w_1^2} & \frac{\partial^2 E(\mathbf{w})}{\partial w_1 w_2} & \cdots & \frac{\partial^2 E(\mathbf{w})}{\partial w_1 w_n} \\
      \frac{\partial^2 E(\mathbf{w})}{\partial w_2 w_1} & \frac{\partial^2 E(\mathbf{w})}{\partial w_2^2} & \cdots & \frac{\partial^2 E(\mathbf{w})}{\partial w_2 w_n} \\
      \vdots & \vdots & \ddots & \vdots \\
      \frac{\partial^2 E(\mathbf{w})}{\partial w_n w_1} & \frac{\partial^2 E(\mathbf{w})}{\partial w_n w_2} & \cdots & \frac{\partial^2 E(\mathbf{w})}{\partial w_n^2}
    \end{bmatrix}\]

  + [The gradient of the error function](../ML/MLNN-Hinton/a12-Learning.md#84-second-order-algorithms)

    \[\Delta E(\mathbf{w} + \mathbf{h})^T \approx \Delta E(\mathbf{w}^T + \mathbf{h}^2 \Delta^2 E(\mathbf{w})\]

  + Solving Eq.(6) = 0

    \[\mathbf{h} = -(\Delta^2 E(\mathbf{w}))^{-1} \Delta E(\mathbf{w}) \tag{7}\]
  
  + The solution can be done in a single step if the Hessian matrix and the gradient have computed
  + Applying Newton's method to get the $(k+1)$-th iteration

    \[\mathbf{w}^{(k+1)} = \mathbf{w}^{(k)} - (\Delta^2 E(\mathbf{w}))^{-1} \Delta E(\mathbf{w}) \tag{8}\]

  + Eq. (8) as a position where the gradient w/ reduced magnitude
  + Retain the minimum of the error function with several iterations

+ [Computing Hessian matrix, $\Delta^2 E(\mathbf{w})$](../ML/MLNN-Hinton/a12-Learning.md#84-second-order-algorithms)
  + Becker, S., and Y. le Cun (1989), “Improving the Convergence of BackPropagation Learning with Second Order Methods”, in: [Touretzky et al. 1989], pp. 29–37.
  + a difficult task
  + requiring the inverse of the Hessian matrix
  + many proposals to approximate the second-order information using certain heuristic
  + Pseudo-Newton's methods
    + variants of Newton's method working w/ a simplified form of the Hessian matrix
    + non-diagonal elements set all zeros and only diagonal elements computed
    + therefor, only computing $\partial^2 E(\mathbf{w})/\partial w_i^2$
    + Simplifying Eq. (8) to 

      \[w_i^{(k+1)} = w_i^{(k)} - \frac{\Delta_i E(\mathbf{w})}{\partial^2 E(\mathbf{w})/\partial w_i^2} \tag{9}\]

    + No inverse of the Hessian matrix required
    + limited effort in finding the second order partial derivatives
    + working well w/ nice quadratic error function
    + extremely large corrections required if a small second-order partial derivatives


### QuickProp

+ See info at [Fast Learning Algorithms](./NN-AdaptiveLearn.md#quickprop)


### QRProp

+ See info at [Fast Learning Algorithms](./NN-AdaptiveLearn.md#qrprop)


## Relaxation methods

### Overview

+ [Class of relaxation methods](../ML/MLNN-Hinton/a12-Learning.md#85-relaxation-methods)
  + perturbed network weights
  + comparing to the new network error with the directly previous one


### Weight and node perturbation

+ [Weight perturbation](../ML/MLNN-Hinton/a12-Learning.md#851-weight-and-node-perturbation)
  + a learning strategy proposed to avoid calculating the gradient of the error function at each step
  + discrete approximation to the gradient at each iteration
    + taking the initial weight $\mathbf{w}$ in weight space
    + the value $E(w)$ of the error function for this computation of parameters
  + Assumptions & Notations
    + $\beta$: a small perturbation added to the weight $w_i$
    + $E(\mathbf{w}^{\prime})$: the error at the new point $\mathbf{w}^{\prime}$ in weight space
  + updating the weight $w_i$

    \[\Delta w_i = - \gamma \frac{E(w^{\prime}) - E(w)}{\beta}\]

    + repeating iteratively, randomly selecting the weight to be updated
  + the discrete approximation to be gradient: important for chip where the learning algorithm implemented w/ minimal hardware additional to that needed for the feed-forward phase

+ [Node perturbation](../ML/MLNN-Hinton/a12-Learning.md#851-weight-and-node-perturbation)
  + perturbing the output $o_i$ of the $i$-th node by $\Delta o_i$
  + Assumptions & Notations
    + $E - E^{\prime}$: the difference in the error function
    + $E^{\prime}$: the new error achieved with the output $o_i + \Delta o_i$
    + activation function: sigmoid
  + the desired weighted input to node $i$ w/ sigmoid

    \[\sum_{k=1}^m w_k^{\prime}x_k = s^{-1}(o_i + \Delta o_i)\]

  + the new weight w/ the previous weighted input $\sum_{k=1}^m w_k x_k$

    \[w_k^{\prime} = w_k \frac{s^{-1} (o_i + \Delta o_i)}{\sum_{k=1}^m w_k x_k} \qquad \text{for } k=1, \dots, m\]

  + weights updated in proportion to their relative size
  + a stochastic introduced or a node perturbation step alternated w/ a weight perturbation step


### Symmetric and asymmetric relaxation

+ [Assumptions & Notations](../ML/MLNN-Hinton/a12-Learning.md#852-symmetric-and-asymmetric-relaxation)
  + Three layered neural network

    <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
      <a href="url" ismap target="_blank">
        <img src="img/a12-25.png" style="margin: 0.1em;" alt="Notation for the three-layered network" title="Notation for the three-layered network" width=350>
      </a>
    </div>

  + $o_j^{(1)}$: the output w/ sigmoid activation function

    \[o_j^{(1)} = s \left(\sum_{i=1}^{n+1} w_{ij}^{(1)} \hat{o}_i\right)\]

  + $\mathbf{o}^{(1)}$: the outputs of the hidden units

    \[\mathbf{o}^{(1)} = s(\mathbf{\hat{o}} \mathbf{\overline{W}_1})\]

  + $\mathbf{o}^{(2)}$: the outputs of the network, 

    \[\mathbf{o}^{(1)} = s(\mathbf{\hat{o}}^{(1)} \mathbf{\overline{W}_2})\]

  + $\mathbf{e}$: the column vector whose components are the derivatives of the corresponding components of the quadratic error

    \[\mathbf{e} = \begin{bmatrix}
      (o_1^{(2)} - t_1) \\ (o_2^{(2)} - t_2) \\ \vdots \\ (o_3^{(2)} - t_3)
    \end{bmatrix}\]

  + $\mathbf{D_1}$: a diagonal matrix

    \[\mathbf{D_1} = \begin{bmatrix}
      o_1^{(1)}(1 - o_1^{(1)}) & 0 & \cdots & 0 \\
      0 & o_2^{(1)}(1 - o_2^{(1)}) & \cdots & 0 \\
      \vdots & \vdots & \ddots & \vdots \\
      0 & 0 & \cdots & o_k^{(1)}(1 - o_k^{(1)}) \\
    \end{bmatrix}\]

  + $\mathbf{D_2}$: a diagonal matrix

    \[\mathbf{D_2} = \begin{bmatrix}
      o_1^{(2)}(1 - o_1^{(2)}) & 0 & \cdots & 0 \\
      0 & o_2^{(2)}(1 - o_2^{(2)}) & \cdots & 0 \\
      \vdots & \vdots & \ddots & \vdots \\
      0 & 0 & \cdots & o_m^{(2)}(1 - o_m^{(2)}) \\
    \end{bmatrix}\]

  + $\mathbf{W_2}$: a connection/weight matrix between hidden and output layers
  + $\mathbf{O_1}$: the output $p \times k$ matrix of the hidden layer w/ the arranged all rows, $o^{(1)}$
  + $\mathbf{T}$: target matrix w/ all targets as the rows of a $p \times m$ matrix
  + $\mathbf{O}_1^+$: pseudoinverse of $\mathbf{O}_1$

+ [Objective: the target vector $\mathbf{t}$](../ML/MLNN-Hinton/a12-Learning.md#852-symmetric-and-asymmetric-relaxation)
  + the backpropagated error of the output layer

    \[\delta^{(2)} = \mathbf{D_2 e}\]

  + reducing the magnitude of the error $\mathbf{e}$ to zero by adjusting the matrix $\mathbf{W_2}$ in a single step
  + $s^{-1}(t)$: the necessary weighted input at the output nodes
  + the following equation holds for all the $p$ possible input patterns

    \[\mathbf{o}^{(1)} \mathbf{W_2} = s^{-1}(\mathbf{t})\]

    therefore,the matrix $\mathbf{W_2}$ for which

    \[\mathbf{O_1 W_2} = s^{-1}(\mathbf{T}) \tag{12}\]

  + the matrix equation may have no solution for $\mathbf{W_2}$, but compute the matrix minimizing the quadratic error for this equality
  + Computing the connection matrix $\mathbf{W}_2$

    \[\mathbf{W}_2 = \mathbf{O}_1^+ s^{-1}(\mathbf{T})\]

  + obtaining the matrix $\mathbf{O}_1$ by minimizing the quadratic deviation from Eq.(12)
  + computing intermediate targets for the hidden units, which are given by the rows of the matrix

    \[\mathbf{O}_1^{\prime} = s^{(-1)}(\mathbf{T})\mathbf{W}_2^+\]

  + the new intermediate targets used to obtain an update for the matrix $\mathbf{W}_1$ of weights between input and hidden units

+ [Computing complexity](../ML/MLNN-Hinton/a12-Learning.md#852-symmetric-and-asymmetric-relaxation)
  + computationally intensively for every "pseudoinverse" step
  + weight corrections of the method
    + more accurate than other algorithms
    + these high-powered iterations demand many computations for each of the two matrices
  + highly redundant data: pseudoinverse step very inefficient
  + symmetric relaxation
    + the targets $\mathbf{T}$
    + the outputs of the hidden units are determined in the back and forth kind of approach





