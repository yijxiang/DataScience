# Neural Networks

## Fundamentals

### Motivations

+ [A spectrum of machine learning tasks](../ML/MLNN-Hinton/13-BeliefNets.md#131-the-ups-and-downs-of-backpropagation)
  + Typical Statistics $\longleftrightarrow$ Artificial Intelligence
  + typical statistics
    + low-dimensional data; e.g., less than 100 dimensions
    + lots of noise in the data
    + not much structure in the data; structure able to captured by a fairly simple model
    + main problem: separating true structure from noise, not thinking noise is a structure
    + solution: good for Bayesian nets but not ideal for non-Bayesian neural nets $\implies$ trying SVM or Gaussian Process (GP - regression)
  + artificial intelligence
    + high-dimensional data; e.g., more than 100 dimensions, such images and coefficients representing speech
    + noise: not the main problem
    + huge amount structure in the data, but too complicated to be represented by a simple model
    + main problem: figuring out a way to represent the complicated structure so that it can be learned
      + try to hand design appropriate representations
      + earier to resolve by letting backpropagation figure out what representations to use by given a multiple layers
      + using computation power to decide what the representation should be
    + solution: using backpropagation to figure it out

+ [Machine learning problems](../ML/MLNN-Hinton/a01-IntroNN.md#the-motivation-for-neural-networks)
  + regressions (and Ridge, LASSO, etc.)
  + classification problem
  + binary classification problem


### Anatomy

+ [Neural networks:](../ML/MLNN-Hinton/a02-IntermediateNN.md#anatomy-of-a-neural-network)
  + excellent tools for finding patterns
  + backpropagation
  + make use of affine __transformations__ to concatenate input features
  + concatenated input passed through an activation function
  + Neural network
    + an abstract representation of the data at each stage of the network
    + designed to detect specific features of the network

+ [Activation function](../ML/MLNN-Hinton/a02-IntermediateNN.md#anatomy-of-a-neural-network)
  + evaluate the signal response and determine whether the neuron should be activated given the current inputs
  + extended to multilayer and multi feature networks
    + the number of degrees of freedom (weights and biases) of the network
    + the number of features available which the network can use to make predictions

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/comprehensive-introduction-to-neural-network-architecture-c08c6d8e5d98" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/1*L_lfAEddxxAg2EqJfB5i6Q.png" style="margin: 0.1em;" alt="Activation function with affine transformation" title="Activation function with affine transformation" height=150>
      <img src="https://miro.medium.com/max/1250/1*l57B0pjXoO-1H1xZYV7QBA.png" style="margin: 0.1em;" alt="A neural network with one hidden layer and two features (the simplest possible multi-layer multi-feature network)." title="A neural network with one hidden layer and two features (the simplest possible multi-layer multi-feature network)." height=150>
    </a>
  </div>

+ [Network parameters (weights and biases)](../ML/MLNN-Hinton/a02-IntermediateNN.md#anatomy-of-a-neural-network)
  + updated by assigning the error of the network
  + using backpropagation through the network to obtain the derivatives for each of the parameters w.r.t. the loss function
  + gradient descent used to update these parameters

+ [Training network](../ML/MLNN-Hinton/a02-IntermediateNN.md#anatomy-of-a-neural-network)
  + the process of accessing the error and updating the parameters
  + a training set to generate a functional network
  + performance of the network
  + test set: unseen data accessed by testing

+ [Degrees of freedom](../ML/MLNN-Hinton/a02-IntermediateNN.md#anatomy-of-a-neural-network)
  + neural network having a large number of degrees
  + required a large amount of data for training to be able to make adequate predictions
  + useful for high dimensionality of the data

+ [Generalized multilayer and multi-feature network](../ML/MLNN-Hinton/a02-IntermediateNN.md#anatomy-of-a-neural-)

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/comprehensive-introduction-to-neural-network-architecture-c08c6d8e5d98" ismap target="_blank">
      <img src="https://miro.medium.com/max/1250/1*GApLZ60775yXfUzO65PfEA.png" style="margin: 0.1em;" alt="Generalized multilayer perceptron with n hidden layers, m nodes, and d input features." title="Generalized multilayer perceptron with n hidden layers, m nodes, and d input features." width=350>
    </a>
  </div>

  + $m$ nodes: the width of a layer within the network
  + $n$ hidden layers: the depth of the network
  + $d$ inputs: pre-specified by the available data
    + normal Pandas data frame: equal to the number of feature columns
  + the hidden layers of the network have the same width (number of nodes)
  + the number of nodes may vary across the hidden layers
  + the output layer may also be of an arbitrary dimension depending on the required output

+ [Convolutional neural networks](../ML/MLNN-Hinton/a02-IntermediateNN.md#anatomy-of-a-neural-network)
  + commonly used to study images
  + hidden layers closer to the output of a deep network, the highly interpretable representations, such as faces, clothing, etc.
  + the first layers of the network: detecting very basic features such as corners, curves, and so on
  + abstract representations quickly become too complex to comprehend
  + the workings of neural networks to produce highly complex abstractions seen as somewhat magical

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/comprehensive-introduction-to-neural-network-architecture-c08c6d8e5d98" ismap target="_blank">
      <img src="https://miro.medium.com/max/1250/1*9AC8C_ybj-yeAS8OqpK1Eg.png" style="margin: 0.1em;" alt="An example of a neural network with multiple hidden layers classifying an image of a human face." title="An example of a neural network with multiple hidden layers classifying an image of a human face." width=400>
      <img src="https://miro.medium.com/max/1250/1*qpdTBdx8D-Z2WAMT24onLQ.png" style="margin: 0.1em;" alt="An example of a neural network with multiple hidden layers classifying written digits from the MNIST dataset." title="An example of a neural network with multiple hidden layers classifying written digits from the MNIST dataset." width=400>
    </a>
  </div>


### Concepts and Neural Networks

+ [Concepts in cognition science](../ML/MLNN-Hinton/04-Multiclasses.md#a-brief-diversion-into-cognitive-science)
  + The feature theory: a concept is a set of semantic features
  + The structuralist theory: the meaning of a concept lies in its relationships to other concepts
  + Minsky (1970s): in favor of relational graph representations with structuralist theory
  + Hinton - both applicable
    + able to use vectors of semantic features to implement a relational graph
    + no intervening conscious steps but many computation in interactions of neurons
    + explicit rules for conscious, deliberate, reasoning
    + commonsense, analogical reasoning: seeing the answer w/o conscious intervening steps

+ [Localist and distributed representations of concepts](../ML/MLNN-Hinton/04-Multiclasses.md#a-brief-diversion-into-cognitive-science)
  + Localist representation
    + implementation of relational graph in a neural net
    + neuron = node in the graph
    + connection = a binary relationship
    + "localist" method not working: many different types of relationship and the connections in neural nets w/o discrete labels
  + Distributed representations
    + open issue: how to implement relational knowledge in a neural net
    + many-to-many mapping btw concepts and neurons

+ [Neural Network Algorithm](../ML/MLNN-Hinton/a01-IntroNN.md#the-motivation-for-neural-networks)

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/simple-introduction-to-neural-networks-ac1d7c3d7a2c" ismap target="_blank">
      <img src="https://miro.medium.com/max/1250/1*QIKMKejAH9cjXxe-PIIU7g.png" style="margin: 0.1em;" alt="Formulation of Neural Networks" title="Formulation of Neural Networks" width=400>
    </a>
  </div>

  + weights in neural networks: these regression parameters of our various incoming functions
  + passed to an activation function which decides whether the result is significant enough to 'fire' the node
  + start with some arbitrary formulation of values in order for us to start updating and optimizing the parameters
  + assessing the loss function after each update and performing gradient descent

+ [Ways to minimize the loss function](../ML/MLNN-Hinton/a01-IntroNN.md#the-motivation-for-neural-networks)
  + Descent
    + The value of $w$ to minimize $\mathcal{L}(w)$
    + to find the optimal point of a function$\mathcal{L}(w)$: $\frac{d \mathcal{L}(W)}{dW} = 0$
    + find the $w$ that satisfies the equation
  + more flexible method
    + start from any point and then determine which direction to go to reduce the loss (left or right in this case)
    + calculate the slope of the function at this point
    + then shift to the right if the slope is negative or shift to the left if the slope is positive

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/simple-introduction-to-neural-networks-ac1d7c3d7a2c" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/1*qbvfebFdO7rxU4QVl6tQtw.png" style="margin: 0.1em;" alt="Diagram of the loss function" title="Diagram of the loss function" height=150>
      <img src="https://miro.medium.com/max/875/1*4l_ZpZRZ6mwKAXWo4Q20QA.png" style="margin: 0.1em;" alt="Diagram of the loss function with starting point" title="Diagram of the loss function with starting point" height=150>
    </a>
  </div>


### Types of Learning

+ [Problem Modeling](../ML/MLNN-Hinton/01-IntroML.md#three-types-of-learning)
  + Supervised learning: Regression & Classification
  + Reinforcement learning
  + Unsupervised learning

+ [Typical Supervised learning procedure](../ML/MLNN-Hinton/01-IntroML.md#three-types-of-learning)
  1. Choosing a model class: $y = f(\mathbf{x}; \mathbf{W})$
    + $\mathbf{x}$: input vector
    + $\mathbf{W}$: weight vector
    + $f$: activation function to transform input $\mathbf{x}$ with weight vector $\mathbf{W}$ to the output $y$
  2. Learning by adjust $\mathbf{W}$ with cost function
    + reduce the difference between target value $t$ and actual output $y$
    + Regression measurement: usually $\frac{1}{2} (t - y)^2$
    + Classification measurement: other sensible measures

+ [Reinforcement learning](../ML/MLNN-Hinton/01-IntroML.md#three-types-of-learning)
  + Output: an action or sequence of actions
  + The only supervisory signal: an occasional scalar reward
  + Decision of action(s) selected: maximize the expected sum of the future reward
  + typically delayed reward makes model hard

+ [Unsupervised learning](../ML/MLNN-Hinton/01-IntroML.md#three-types-of-learning)
  + no clear goal
  + typically find sensible clusters


### Learning Methodologies

+ [Learning by perturbing weights](../ML/MLNN-Hinton/03-Backpropagation.md#the-backpropagation-algorithm)
  + randomly perturb one weight and see if it improves performance: very inefficient
  + Alternative: randomly perturb all the weights in parallel and correlate the performance gain with the weight changes
  + Better: randomly perturb the activities of the hidden units

+ [Randomly perturb the activities of the hidden units](../ML/MLNN-Hinton/03-Backpropagation.md#the-backpropagation-algorithm)
  + adding a layer of hand-coded features
    + more powerful but hard to design the features
    + finding good features w/o requiring insights into the task or repeated trial and error
    + guess features and see how well they work
  + automate the loop of designing features for a particular task and seeing ho well they work


### Bias & Variance

+ [Point estimation](../ML/MLNN-Hinton/a14-Advanced.md#41-estimators)
  + providing the single "best" prediction of some quantity of interest

    \[ \hat{\mathbf{\theta}}_m = g(\mathbf{x}^{(1)}, \dots, \mathbf{x}^{(m)}) \]

    + $\mathbf{\theta}$: true value
    + $\hat{\mathbf{\theta}}_m$: estimator for $m$ samples
  + more often, $\mathbf{\theta}$ fixed but unknown and the data is random

+ [Bias & Variance](../ML/MLNN-Hinton/a14-Advanced.md#41-estimators)
  + estimator: a random variable
  + random variable susceptible to bias and variance
    + bias: expected deviation from the true value
    + variance: deviation from the expected estimator

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/advanced-topics-in-neural-networks-f27fbcc638ae" ismap target="_blank">
      <img src="https://miro.medium.com/max/1475/1*hk99PbiLpVCHnMPEkP2YdA.png" style="margin: 0.1em;" alt="Examples of bais and variance" title="Examples of bais and variance" width=300>
    </a>
  </div>

+ [Bias-variance trade-off](../ML/MLNN-Hinton/a14-Advanced.md#42-diagnosing-bias-variance)
  + high dimensions: no decision curves to inspect bias-variance
  + calculating error values to infer the source of errors on the training set, as well as on the validation set

+ [Bayes error rate](../ML/MLNN-Hinton/a14-Advanced.md#42-diagnosing-bias-variance)
  + bias: baseline required, such as human-level performance
  + the lowest possible error rate for any classifier of a random outcome
  + the minimum error able to obtain with a perfect model stripped of all avoidable bias and variance

+ [Analyzing the errors](../ML/MLNN-Hinton/a14-Advanced.md#42-diagnosing-bias-variance)
  + analyzing and comparing the errors on the training and validation sets to deduce the cause of the error (see diagram)
  + techniques to analyze the errors of estimator
    + orthogonalization
    + early stopping
  + ways to reduce the bias
    + train a bigger model (increasing the explainability of the model)
    + train longer (reaching convergence)
    + adapt the neural architecture or perform an extensive hyperparameter search
  + ways to reduce the variance
    + get more data
    + use regularization mechanisms

+ extremely helpful way to troubleshoot the network: analyze network's results and determine whether the issue is caused by biasing or variance


### Considerations of Learning Procedures

+ [Main decisions about how to use error derivatives](../ML/MLNN-Hinton/03-Backpropagation.md#how-to-use-the-derivatives-computed-by-the-backpropagation-algorithm)
  + Optimization issue: how to discover a good set of weights with the error derivatives on individual cases?
  + Generalization issue: how to ensure non-seen cases during training work well with trained weights?

+ [Optimization Concerns](../ML/MLNN-Hinton/03-Backpropagation.md#how-to-use-the-derivatives-computed-by-the-backpropagation-algorithm)
  + How often to update the weights
    + Online
    + Full batch
    + Mini-batch
  + How much to update the weights
    + fixed learning rate
    + adaptive learning rate globally
    + adaptive learning rate on each connection separately

+ [Generalization Concern - Overfitting](../ML/MLNN-Hinton/03-Backpropagation.md#how-to-use-the-derivatives-computed-by-the-backpropagation-algorithm)
  + Unable to identify which regularities causing errors
  + Possible solutions:
    + Weight-decay
    + Weight-sharing
    + Early stopping
    + Model averaging
    + Bayesian fitting on neural nets
    + Dropout
    + Generative pre-training


### Backpropagation

+ [A brief history of backpropagation](../ML/MLNN-Hinton/13-BeliefNets.md#131-the-ups-and-downs-of-backpropagation)
  + backpropagation algorithm: clearly having great promise for learning multiple layers for non-linear feature detector
  + Give up at the late 1990's by most serious researchers
  + still widely used in psychological models and in practical applications such as credit card fraud detection

+ [Why backpropagation failed in the late 1990's](../ML/MLNN-Hinton/13-BeliefNets.md#131-the-ups-and-downs-of-backpropagation)
  + popular reasons for giving up
    + not good use of multiple hidden layers of non-linear features
    + not work well in recurrent networks or deep auto-encoders
    + Support Vector Machine (SVM)
      + working better
      + required less expertise
      + produced repeatable results
      + much better and fancier theory
  + actual reasons
    + computers: thousands of times too slow
    + labeled datasets: hundreds of times too small for the regime in which backpropagation would really shine
    + deep networks:
      + too small and not initialized sensibly
      + gradient die too fast because of small initialized weights
  + these issues preventing from being successful for tasks, including vision and speech, where it would eventually  be a big win


+ [Backpropagation algorithm](../ML/MLNN-Hinton/a12-Learning.md#81-introduction---classical-backpropagation)
  + a rather slow learning algorithm
  + malicious selection of parameters made even slower
  + non-linear optimization: accelerate the training method with practically no effort

+ [Artificial neural networks](../ML/MLNN-Hinton/a12-Learning.md#81-introduction---classical-backpropagation)
  + NP-complete in the worst cases
  + network parameters grow exponentially w/ the number of unknown

+ [Standard online backpropagation](../ML/MLNN-Hinton/a12-Learning.md#81-introduction---classical-backpropagation) performs better than many fast learning algorithms when
  + a realistic level of complexity in the learning task
  + the size of the training set beyond a critical threshold

+ [online backpropagation](../ML/MLNN-Hinton/a12-Learning.md#the-gauss-jacobi-and-gauss-seidel-methods-and-backpropagation)
  + not converge to a single point in weight space
  + oscillation around the minimum of the error function
  + expected value of the derivation based on the learning step size used
  + linear associator = Iterated Function System [Barnsley, M. (1988), Fractals Everywhere, Academic Press, London.]

+ [Visualization online & offline backpropagation approach](../ML/MLNN-Hinton/a12-Learning.md#the-gauss-jacobi-and-gauss-seidel-methods-and-backpropagation)
  + Gauss-Jacobi method
    + starting at some point in search space
    + projecting the point in the directions of the axes on the two lines considered
    + next iteration point: the $x$-coordinate of the horizontal projection & $y$-coordinate of the vertical projection
  + Gauss-Seidel method
    + dealing with each line equation individually
    + 1st projection in the $x$ direction
    + 2nd projection in the $y$ direction
    + usually converge faster than the Gauss-Jacobi method

+ [Limitations of backpropagation](../ML/MLNN-Hinton/13-BeliefNets.md#132-belief-networks)
  + labeled training data: almost all data unlabeled
  + learning time: not scale well
  + poor local optima
    + usually quite good but far from optimal for deep nets (small initialized random weights)
    + should we retreat to models that allow convex optimization?
      + mathematically good
      + in practice, running away from the complexity of real data

+ [Unsupervised learning](../ML/MLNN-Hinton/13-BeliefNets.md#132-belief-networks)
  + overcoming the limtations of backpropagation
  + gradient method and stochastic mini-batch descent
  + learning objective for a generative model as w/ Boltzmann Machines: maximize $p(x)$ (probability of observed data)  not $p(y|x)$ (probability of labels w/ given inputs)
  + what generative model to use?
    + an energy-based model like a Boltzmann machine
    + a causal mode made of idealized neurons
    + a hybrid of the two


## Architectures

### Types of Architectures

+ [A mostly complete chart of Neural Networks](https://towardsdatascience.com/the-mostly-complete-chart-of-neural-networks-explained-3fb6f2367464)

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/the-mostly-complete-chart-of-neural-networks-explained-3fb6f2367464" ismap target="_blank">
      <img src="https://miro.medium.com/max/2500/1*cuTSPlTq0a_327iTPJyD-Q.png" style="margin: 0.1em;" alt="Mostly complete neural network architecture" title="Mostly complete neural network architecture" width=100%>
    </a>
  </div>

  + Perceptron (P)
    + simplest and oldest model
    + takes some inputs, sums them up, applies activation function and pass them to output layer

  + Feed-forward neural networks
    + all nodes fully connected
    + activation flows from input layer to output, w/o back loops
    + one hidden layer between input and output layers
    + training using backpropagation method

  + Radical Basis Neural (RBF) Networks
    + FF (feed-forward) NNs
    + activation function: radial basis function
    + perfect for function approximation, and machine control

  + Deep Feed Forward (DFF) Neural Network
    + FF NN w/ more than one hidden layer
    + stacking errors with more layers resulted in exponential growth of training times
    + approaches developed in 00s allowed to train DFFs effectively

  + Recurrent Neural network (RNN)
    + a.k.a Jordan network
    + each of hidden cell received its own output with fixed delay
    + mainly used when context is important

+ [Feed-forward neural Networks](../ML/MLNN-Hinton/02-Perceprtons.md#an-overview-of-the-main-types-of-network-architecture)
  + Input layer: the first layer
  + Output layer: the last layer
  + Hidden layer(s): layer(s) between the Input & Output layers
  + Deep Neural network: more than one hidden layer

+ [Recurrent neural network](../ML/MLNN-Hinton/02-Perceprtons.md#an-overview-of-the-main-types-of-network-architecture) (RNN)
  + the previous network state influencing the output
  + a function with inputs $x_t$ (input vector) and previous state $h_{t-1}$
  + complicated dynamics and difficult to train
  + a very natural way to model sequential data
  + able to remember information in their hidden state for a long time

<div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
  <a href="https://subscription.packtpub.com/book/big_data_and_business_intelligence/9781788397872/1/ch01lvl1sec21/feed-forward-and-feedback-networks" ismap target="_blank">
    <img src="https://static.packt-cdn.com/products/9781788397872/graphics/1ebc2a0a-2123-4351-b7e1-eb57f098bafa.png" style="margin: 0.1em;" alt="Feed-forward network" title="Feed-forward network" height=130>
  </a>
  <a href="https://leonardoaraujosantos.gitbooks.io/artificial-inteligence/content/recurrent_neural_networks.html" ismap target="_blank">
    <img src="https://leonardoaraujosantos.gitbooks.io/artificial-inteligence/content/image_folder_6/recurrent.jpg" style="margin: 0.1em;" alt="Recurrent Neural Network" title="Recurrent Neural Network" height=130>
  </a>
</div>

+ [Symmetrically connected neural networks](../ML/MLNN-Hinton/02-Perceprtons.md#an-overview-of-the-main-types-of-network-architecture)
  + Hopfield neural networks
    + an example of recurrent network
    + output of neurons connected to input of every neuron by means of appropriate weights
    + much easier to analyze than recurrent networks
    + the same weight in both direction
  + Boltzman machines
    + symmetrically connected networks with hidden units
    + more powerful than Hopfield networks but less powerful than recurrent networks
    + fully connected within and between layers
    + the stochastic, generative counterpart of Hopfield networks
    + Restricted Boltzmann Machine (RBM): the lateral connections in the visible and hidden layers are removed

<div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
  <a href="http://galaxy.agh.edu.pl/~vlsi/AI/hopf/hopfield_eng.html" ismap target="_blank">
    <img src="http://galaxy.agh.edu.pl/~vlsi/AI/hopf/hopfield_eng_pliki/image002.jpg" style="margin: 0.1em;" alt="Hopfield Neural Network" title="Hopfield Neural Network" height=130>
  </a>
  <a href="https://www.researchgate.net/figure/Boltzmann-and-Restricted-Boltzmann-Machines-A-Boltzmann-machine-is-fully-connected_fig8_257649811" ismap target="_blank">
    <img src="https://www.researchgate.net/profile/Dan_Neil/publication/257649811/figure/fig8/AS:272067278929927@1441877302138/Boltzmann-and-Restricted-Boltzmann-Machines-A-Boltzmann-machine-is-fully-connected.png" style="margin: 0.1em;" alt="Boltzmann and Restricted Boltzmann Machines" title="Boltzmann and Restricted Boltzmann Machines" height=130>
  </a>
</div>

+ [Model the function $y = x \cdot sin(x)$ using a neural network (NN)](../ML/MLNN-Hinton/a02-IntermediateNN.md#architecture)
  + Assume NN using ReLU activation function (Fig.1)
  + NN with a two-node single hidden layer as one degree of freedom (Fig.2)
  + NN with a three-node single hidden layer as two degree of freedom (Fig.3)
  + NN with a multi-node hidden layer (Fig.4)
  + NN with 2 one-node hidden layers (Fig.5) approximates the function as a single hidden layer (Fig.1)
  + NN with 3 hidden layers and 3 nodes in each layer (Fig.7) gives a pretty good approximation

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/comprehensive-introduction-to-neural-network-architecture-c08c6d8e5d98" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/1*Ghcl9sY_91pf7EY4H35SvQ.png" style="margin: 0.1em;" alt="neural network using ReLU activation functions" title="Fig.1 neural network using ReLU activation functions" height=200>
      <img src="https://miro.medium.com/max/875/1*xelnKarSd6ueNrROyOuCrA.png" style="margin: 0.1em;" alt="neural network with a single hidden layer" title="Fig.2 neural network with a single hidden layer" height=200>
      <img src="https://miro.medium.com/max/875/1*3JeEUpze45bJFMvKpE8_MQ.png" style="margin: 0.1em;" alt="neural network with a hidden layer adding another hidden node" title="Fig.3 neural network with a hidden layer adding another hidden node" height=200>
      <img src="https://miro.medium.com/max/875/1*qCxqhOgQeE_7fonbIMTIOw.png" style="margin: 0.1em;" alt="neural network with a multi-node hidden layer" title="Fig.4 neural network with a multi-node hidden layer" height=200>
    </a>
  </div>

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="url" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/1*Hg3nySTNWb9N9sMYXRJ32g.png" style="margin: 0.1em;" alt="neural network with 2 one-node hidden layers" title="Fig.5 neural network with 2 one-node hidden layers" height=200>
      <img src="https://miro.medium.com/max/875/1*RkQ1s4RXBaz909vXnPBzJg.png" style="margin: 0.1em;" alt="neural network with 2 2-node hidden layers" title="Fig.6 neural network with 2 2-node hidden layers" height=200>
      <img src="https://miro.medium.com/max/875/1*Jx9Pol3A-ofo8Xl1oalpVw.png" style="margin: 0.1em;" alt="neural network with 3 3-node hidden layers" title="Fig.7 neural network with 3 3-node hidden layers" height=200>
    </a>
  </div>

+ [Architectures for neural networks](../ML/MLNN-Hinton/a02-IntermediateNN.md#architecture)
  + tradeoff by selecting a network architecture 
    + large enough to approximate the function of interest
    + not too large taken an excessive amount of time to train
  + large network requiring large amounts of data to train

+ [Good practice](../ML/MLNN-Hinton/a02-IntermediateNN.md#architecture)
  + using multiple hidden layers as well as multiple nodes within the hidden layers
  + Goodfellow shown that
    + increasing the number of layers of neural networks tends to improve overall test set accuracy
    + large, shallow networks tend to overfit more

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/comprehensive-introduction-to-neural-network-architecture-c08c6d8e5d98" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/1*LtzuTUh0kkCfvlwKxx2zvw.png" style="margin: 0.1em;" alt="increasing the number of layers of neural networks tends to improve overall test set accuracy" title="increasing the number of layers of neural networks tends to improve overall test set accuracy" height=150>
      <img src="https://miro.medium.com/max/875/1*nUHyEEaHEMy3Kl72xTu9Pg.png" style="margin: 0.1em;" alt="large, shallow networks tend to overfit more" title="large, shallow networks tend to overfit more" height=150>
    </a>
  </div>



### Simple Neuron Model

+ A biological neuron with a basic mathematical mode

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://www.embedded-vision.com/platinum-members/cadence/embedded-vision-training/documents/pages/neuralnetworksimagerecognition" ismap target="_blank">
      <img src="https://www.embedded-vision.com/sites/default/files/technical-articles/CadenceCNN/Figure3a.jpg" style="margin: 0.1em;" alt="Illustration of a biological neuron" title="Illustration of a biological neuron" width=350>
      <img src="https://www.embedded-vision.com/sites/default/files/technical-articles/CadenceCNN/Figure3b.jpg" style="margin: 0.1em;" alt="Illustration of a biological neuron's mathematical model" title="Illustration of a biological neuron's mathematical model" width=350>
    </a>
  </div>

+ [Linear neuron](../ML/MLNN-Hinton/01-IntroML.md#some-simple-models-of-neurons)

  \[z = b + \sum_i w_i x_i\]

  + $y$: the output
  + $b$: the bias
  + $w_i$: the weight on the $i$-th input
  + $x_i$: the $i$-th input

+ [Typical Activation functions $f(\cdot)$](../ML/MLNN-Hinton/01-IntroML.md#some-simple-models-of-neurons)
  + Binary threshold

    \[z = b + \sum_i w_i x_i \implies y = \begin{cases} 1 & \text{if } z > 0 \\ 0 & \text{otherwise} \end{cases}\]

  + Rectified Linear Neurons

      \[z = b + \sum_i x_i w_i \implies y = \begin{cases} z & \text{if } z > 0 \\ 0 & \text{otherwise} \end{cases}\]

  + Sigmoid neurons

    \[z = b + \sum_i x_i w_i \implies y = \frac{1}{1 + e^{-z}}\]

  + Stochastic binary neurons

    \[z = b + \displaystyle \sum_i x_i w_i \implies p(s = 1) = \frac{1}{1 + e^{-z}}\]

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://blog.zaletskyy.com/some-simple-models-of-neurons" ismap target="_blank">
      <img src="https://blog.zaletskyy.com/Media/Default/NeuralNetworks/binaryNeuron.png" style="margin: 0.1em;" alt="Binary threshold neuron" title="Binary threshold neuron" height=120>
    </a>
    <a href="https://www.bo-song.com/coursera-neural-networks-for-machine-learning/" ismap target="_blank">
      <img src="https://www.bo-song.com/wp-content/uploads/2015/12/Untitled-2.png" style="margin: 0.1em;" alt="Rectified Linear Neurons" title="Rectified Linear Neurons  (ReLU)" height=120>
      <img src="https://www.bo-song.com/wp-content/uploads/2015/12/Untitled-5.png" style="margin: 0.1em;" alt="Sigmoid neurons" title="Sigmoid neurons" height=120>
      <img src="https://www.bo-song.com/wp-content/uploads/2015/12/Untitled-6.png" style="margin: 0.1em;" alt="Stochastic binary neurons" title="Stochastic binary neurons" height=120>
    </a>
  </div>


### Perceptrons

+ [The standard Perceptron architectures](../ML/MLNN-Hinton/02-Perceprtons.md#perceptrons-the-first-generation-of-neural-networks)

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://sebastianraschka.com/Articles/2015_singlelayer_neurons.html" ismap target="_blank">
      <img src="https://sebastianraschka.com/images/blog/2015/singlelayer_neural_networks_files/perceptron_schematic.png" style="margin: 0.1em;" alt="Rosenblatt's Perceptron architecture" title="Rosenblatt's Perceptron architecture" height=150>
    </a>
    <a href="https://towardsdatascience.com/perceptron-the-artificial-neuron-4d8c70d5cc8d" ismap target="_blank">
      <img src="https://miro.medium.com/max/806/1*-JtN9TWuoZMz7z9QKbT85A.png" style="margin: 0.1em;" alt="Minsky-Papert Perceptron architecture" title="Minsky-Papert  Perceptron architecture" height=150>
    </a>
    <a href="https://www.researchgate.net/figure/The-McCulloch-Pitts-Neuron_fig1_265486784" ismap target="_blank">
      <img src="https://www.researchgate.net/profile/Sean_Doherty2/publication/265486784/figure/fig1/AS:669465553432601@1536624434844/The-McCulloch-Pitts-Neuron.png" style="margin: 0.1em; background-color: white;" alt="McCulloch-Pitts Perceptron architecture" title="McCulloch-Pitts Perceptron architecture" height=150>
    </a>
  </div>

+ Frank Rosenblatt (1960's)
  + a very powerful learning algorithm
  + clams on what they can learn to do

+ Minsky & Papert, "Perceptrons" (1969)
  + analyze what they could do and their limitations
  + people think the limitations applied to all neural network models

+ McCulloch-Pitts (1943): Binary threshold neurons

  \[z = b + \sum_i x_i w_i \implies y = \begin{cases}1 & \text{if } z > 0 \\ 0 & \text{otherwise}\end{cases}\]


+ [Structure of neurons & model](../ML/MLNN-Hinton/a01-IntroNN.md#artificial-neural-network-ann)

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/simple-introduction-to-neural-networks-ac1d7c3d7a2c" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/0*6CQ5E2qYm1kOwEW2.png" style="margin: 0.1em;" alt="The structure of a neuron looks a lot more complicated than a neural network, but the functioning is similar." title="Structure of neuron" height=150>
      <img src="https://miro.medium.com/max/875/1*TiQJRO4b3--hIBmEccukUg.png" style="margin: 0.1em;" alt="a neural diagram that makes the analogy between the neuron structure and the artificial neurons in a neural network." title="artificial neurons in a neural network" height=150>
    </a>
  </div>

+ [Affine transformation](../ML/MLNN-Hinton/a01-IntroNN.md#artificial-neural-network-ann)
  + basically an addition (or subtraction) and/or multiplication
  + resembling a regression equation
  + becomes important with multiple nodes converging at a node in a multilayer perceptron
  + abstract the affine and activation blocks into a single block

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/simple-introduction-to-neural-networks-ac1d7c3d7a2c" ismap target="_blank">
      <img src="https://miro.medium.com/max/1250/1*t5H6ohP8hC2bMr680XX9xw.png" style="margin: 0.1em;" alt="Analogous of single neural network with perceptron" title="Analogous of single neural network with perceptron" width=450>
    </a>
  </div>

  + the amalgamation of the outputs from upstream nodes and the summed output is then passed to an activation function, which assesses the probability to determine whether it’s the quantitative value (the probability) sufficient to make the neuron fire

+ [Perceptron convergence procedure:](../ML/MLNN-Hinton/02-Perceprtons.md#perceptrons-the-first-generation-of-neural-networks)
  + training binary output as classifier
  + bias
    + adding extra component with value 1 to each input vector
    + minus the threshold
  + using policy to ensure the correct cases should be picked
  + find a set of weights to pick all correct ones

+ [Weight space](../ML/MLNN-Hinton/02-Perceprtons.md#a-geometrical-view-of-perceptrons)
  + 1-dim per weight
  + point: a particular setting of all the weights
  + a training case as a hyperplane though the origin
  + cone of feasible solutions
    + find a point on the right side of all planes
    + any weight vectors for all training cases correct

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="http://www.cs.toronto.edu/~hinton/coursera/lecture2/lec2.pptx" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/m02-05.png" style="margin: 0.1em;" alt="Weight space: input vector with correct answer=1" title="Weight space: input vector with correct answer=1" height=200>
      <img src="../ML/MLNN-Hinton/img/m02-06.png" style="margin: 0.1em;" alt="Weight space: input vector with correct answer=0" title="Weight space: input vector with correct answer=0" height=200>
    </a>  $\implies$
    <a href="http://www.cs.toronto.edu/~hinton/coursera/lecture2/lec2.pptx" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/m02-07.png" style="margin: 0.1em;" alt="Feasible solutions" title="Feasible solutions" height=200>
    </a>
  </div>

+ [Learning procedure](../ML/MLNN-Hinton/02-Perceprtons.md#why-the-learning-works)
  + using margin instead of squared distance
  + provide a feasible region by a margin at least as large as the length of the input vector

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="url" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/m02-08.png" style="margin: 0.1em;" alt="Distance btw the current and feasible vectors" title="Distance btw the current & feasible vectors" height=100>
      <img src="../ML/MLNN-Hinton/img/m02-09.png" style="margin: 0.1em;" alt="margin: the squared length btw hyperplan and feasible weight vectors" title="margin: the squared length btw hyperplan and feasible weight vectors" height=100>
    </a>
  </div>

+ [Limitations of Perceptrons](../ML/MLNN-Hinton/02-Perceprtons.md#what-perceptrons-can-not-do)
  + hard-coded features restrict what a perceptron do
    + Solution: adding extra feature(s) to separate
  + Minsky & Papert, "Group Invariance Theorem": unable to discriminating simple patterns under translation w/ wrap-around
    + Solution: adding multiple layers of adaptive, non-linear hidden units

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://www.youtube.com/watch?v=mI6jTc-8sUY&list=PLoRl3Ht4JOcdU872GhiYWf6jwrk_SNhz9&index=11&t=0s" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/m02-10.png" style="margin: 0.1em;" alt="A geometric view of what binary threshold neurons cannot do" title="A geometric view of what binary threshold neurons cannot do" height=150>
      <img src="../ML/MLNN-Hinton/img/m02-11.png" style="margin: 0.1em;" alt="Discriminating simple patterns under translation with wrap-around" title="Discriminating simple patterns under translation with wrap-around" height=150>
    </a>
  </div>



## Activation Functions

### Overview of Activation Functions

+ [Activation functions](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)
  + analogous to the build-up of electrical potential in biological neurons
  + activation potential: mimicked in artificial neural networks using a probability
  + Characteristics:
    + non-linearity: ensures not linearity
    + differentiable: ensure gradients remain large through the hidden unit
  + The general form of an activation function

    \[h = f(W^T X + b)\]

    + $h$: the neural output
    + $f(.)$: the activation function acting on the weights and bases

+ [Non-linearity](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)
  + linear function
    + a polynomial of one degree
    + linear equation easy to solve
    + limited in complexity and less power to learn complex functional mappings from data
  + Neural network w/o activation function
    + a linear regression model
    + limited in the set of functions able to approximate
  + Universal approximation theorem: generalized non-linear function approximations
  + non-linear activation able to generate non-linear mappings from inputs to outputs

+ [nonlinear layer (or activation layer)](../ML/MLNN-Hinton/a10-CNNsGuide.md#relu-rectified-linear-units-layers)
  + introduce nonlinearity to system that basically has been computing linear operations during the convolutional layer
  + linear operation: element wise multiplications and summations
  + nonlinearity: tanh, sigmoid, and ReLU
  + increasing the nonlinearity properties of the model and the overall network without affecting the receptive fields of the convolutional layer

+ [Differentiable](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)
  + required to perform backpropagation in the network
  + required to compute gradients of errors (loss) w.r.t. to the weights updated using gradient descent
  + linear activation function
    + an easily differentiable function
    + optimized using convex optimization
    + limited model capacity

+ [Vanishing gradient problem](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)
  + small gradients and several hidden layers results in multiplied gradient during backpropagation
  + computer limitation on precision when multiply many small numbers
  + the value of the gradient quickly vanished
  + important challenge generated in deep neural networks

+ [Common choices of activation function](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/comprehensive-introduction-to-neural-network-architecture-c08c6d8e5d98" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/1*22g-mJEUfAWBT7lzgiyIiw.png" style="margin: 0.1em;" alt="Summary of activation functions for neural networks." title="Summary of activation functions for neural networks." width=550>
    </a>
  </div>


### Sigmoid and Softmax Functions

+ Logistic regression as a special case of Softmax regression with 2 classes

+ [Softmax classifier](../ML/MLNN-Hinton/a09-SoftmaxClass.md#possible-confusion-naming-conventions)
  + using the cross-entropy loss
  + using softmax function: used to squash the raw class scores into normalized positive values that sum to one

+ [Sigmoid and softmax functions](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)

  \[\phi(z) = \frac{1}{1 + e^{-z}}\]

  + used as output functions for binary classification
  + generally not used within hidden layers
  + softmax function
    + multidimensional version of the sigmoid
    + used for multiclass classification
  + issue: zero centeredness

+ [Architecture for Softmax](../ML/MLNN-Hinton/04-Multiclasses.md#another-diversion-the-softmax-output-function)

    <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
      <a href="http://www.cs.toronto.edu/~hinton/coursera/lecture4/lec4.pptx" ismap target="_blank">
        <img src="../ML/MLNN-Hinton/img/m04-13.png" style="margin: 0.1em;" alt="Representation of Softmax group" title="Representation of Softmax group" width=200>
      </a>
      <a href="https://www.ritchieng.com/machine-learning/deep-learning/neural-nets/" ismap target="_blank">
        <img src="https://raw.githubusercontent.com/ritchieng/machine-learning-nanodegree/master/deep_learning/introduction/lr2.png" style="margin: 0.1em;" alt=" multinomial logistic regression or softmax logistic regression" title=" multinomial logistic regression or softmax logistic regression" width=300>
      </a>
    </div>

+ [Softmax Definition](../ML/MLNN-Hinton/04-Multiclasses.md#another-diversion-the-softmax-output-function)

  A softmax group $G$ is a group of output neurons whose outputs use the softmax activation defined by

  \[y_i = \frac{e^{z_i}}{\displaystyle \sum_{j \in G} e^{z_j}}\]

  so that the outputs sum to 1. The cost function is given by

  \[C = - \sum_j t_j \ln(y_j)\]

+ [Proposition of Softmax](../ML/MLNN-Hinton/04-Multiclasses.md#another-diversion-the-softmax-output-function)

  By the Quotient Rule, the derivatives are

  \[\frac{\partial y_i}{\partial z_i} = \frac{\partial}{\partial z_i} \left(\frac{e^{z_i}}{\sum_{j \in G} e^{z_j}}\right) = y_i(1 - y_i) \qquad\qquad \frac{\partial y_i}{\partial z_j} = \frac{\partial}{\partial z_j} \frac{1}{2} (t_j - y_j)^2 = - y_i y_j\]

  or more fancy-like using the Kronecker Delta:

  \[\frac{\partial y_i}{\partial z_j} = y_i (\delta_{ij} - y_j)\]

+ [Proposition of Softmax](../ML/MLNN-Hinton/04-Multiclasses.md#another-diversion-the-softmax-output-function)

  The derivatives of the cost function are

  \[\frac{\partial C}{\partial z_i} = y_i - t_i.\]

+ [Cross-entropy for Softmax](../ML/MLNN-Hinton/04-Multiclasses.md#another-diversion-the-softmax-output-function)

  the suggested cost function to use with softmax

  \[C = - \sum_j t_j \ln(y_j) = -\ln(y_i)\]

  + $t_j$: target values
  + $t_j = \begin{cases} 1 & j \in I \subset G \\ 0 & j \in G-I \end{cases}$
  + $y_i$: the probability of the input belonging to class $I$
  + simply put 0 on the wrong answers and 1 for the right answer ($t_i$)
  + Cross-entropy cost function

+ [Property of Softmax](../ML/MLNN-Hinton/04-Multiclasses.md#another-diversion-the-softmax-output-function)

  $C$ w/ very big gradient descent if target value = 1 and actual value approx. 0.

+ Softmax better than the gradient descent w/ squared error

+ [Softmax regression](../ML/MLNN-Hinton/a08-SoftmaxReg.md#introduction)
  + a generalized form of logistic regression
  + used in multi-class classification problems where the classes are mutually exclusive
  + Formula

    \[h_\theta(x^{(i)}) = \begin{bmatrix} p(y^{(i)} = 1 | x^{(i)}; \theta) \\ p(y^{(i)} = 2 | x^{(i)}; \theta) \\ \vdots \\ p(y^{(i)} = k | x^{(i)}; \theta) \end{bmatrix} = \frac{1}{\sum_{j=1}^k e^{\theta_j^T} x{(i)}} \begin{bmatrix} e^{\theta_1^T x^{(i)}} \\ e^{\theta_2^T x^{(i)}} \\ \vdots \\ e^{\theta_k^T x^{(i)}}\end{bmatrix}\]

  + $x^{(i)}$: the input vector of the $i$th sampling case
  + $y^{(i)}$: the actual calculated output value of the $i$th sampling case
  + The output is a vector of the probability w/ actual output value of $y^{(k)} = i$ where $i = 1, 2, \dots, k$

+ [Softmax classifier](../ML/MLNN-Hinton/a09-SoftmaxClass.md#introduction)
  + a generalization of Logistic Regression classifier to multiple classes
  + providing a intuitive output (normalized class probabilities)
  + a probabilistic interpretation 
  + function mapping $f(x_i; W) - Wx_i$ stays unchanged
  + interpret these scores as the uncommonalized log probabilities for each class


### Hyperbolic Tangent (tanh) Function

+ [Hyperbolic tangent function (Tanh) function](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)

  \[\phi(z) = \frac{e^z - e^{-z}}{e^z + e^{-z}}\]

  + resolving the zero centeredness issue of the sigmoid function
  + always preferred to the sigmoid function within hidden layers
  + suffer from the other problems plaguing the sigmoid function, including the vanishing gradient problem


### Softplus Functions

+ [Softplus functions](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)

  \[\phi(z) = \ln(1 + e^z)\]

  + a slight variation of ReLU where the transition at zero is somewhat smooth
  + benefit: no discontinuities in the activation function

  + sigmoid for binary classification
  + softmax for multiclass classification
  + linear for a regression problem


### Rectified Linear Unit (ReLU)

+ [Rectified Linear Unit (ReLU)](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)

  \[\phi(z) = max(o, x)\]

  + simplest non-linear activation function
  + avoid and rectify the vanishing gradient problem
  + used by almost all deep learning models
  + only used within hidden layers of a neural network
  + issue: maybe unstable during training and die
  + the most successful and widely-used activation function

+ [Leaky ReLU and Generalized ReLU](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)
  + dead neurons: ReLU unstable causes network never activated on any data point
  + Leaky ReLU

    \[g(x_i, \alpha) = \max{a, x_i} + \alpha \min{0, x_i}\]

    + contain a small slope
    + purpose of slope: keep the updates alive and prevent the production of dead neurons
    + still discontinuity at zero
    + no longer flat below zero
    + merely having a reduced gradient
    + a subset of generalized ReLU

  + Leaky ReLU & Generalized ReLU
    + slight variations on the basic ReLU function
    + difference: merely depend on the chosen value of $\alpha$

+ [Rectified Linear Units](../ML/MLNN-Hinton/a10-CNNsGuide.md#relu-rectified-linear-units-layers)
  + working far better
  + able to train a lot faster (computational efficiency) w/o making a significant difference to the accuracy
  + alleviating the vanishing gradient problem
  + applying yje function $f(x) = \max(0, x)$ to all of the values in the input volume


### Maxout Function

+ [Maxout function](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)

  \[g(x) = \max_{i \in \{ 1, \dots, k\}} \alpha_i x_i + \beta\]

  + simply the maximum of $k$ linear functions
  + a hybrid approach consisting of linear combinations of ReLU and leaky ReLU units


### Self-Gated Activation Function

+ [Swish: A Self-Gated Activation Function](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)

  \[f(x) = x \cdot sigmoid(x)\]

  + tend to work better than ReLU on deeper models across a number of challenging datasets
  + a smooth non-monotonic function that does not suffer from the problem of zero derivatives
  + seen as a somewhat magical improvement to neural networks
  + a clear improvement for deep networks


<div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
  <a href="https://towardsdatascience.com/comprehensive-introduction-to-neural-network-architecture-c08c6d8e5d98" ismap target="_blank">
    <img src="https://miro.medium.com/max/1400/0*WYB0K0zk1MiIB6xp.png" style="margin: 0.1em;" alt="Curve of Sigmoid function" title="Curve of Sigmoid function" height=140>
    <img src="https://miro.medium.com/max/1400/0*VHhGS4NwibecRjIa.png" style="margin: 0.1em;" alt="Curve of hyperbolic tangent function" title="Curve of hyperbolic tangent function" height=140>
    <img src="https://miro.medium.com/max/875/0*TsH2CNeu5Qlt32Oj.png" style="margin: 0.1em;" alt="Curves of the ReLU & Softplus function" title="Curve of the ReLU & Softplus function" height=140>
    <img src="https://miro.medium.com/max/875/1*pTuWvoEIiHQFBvosVjmW5A.png" style="margin: 0.1em;" alt="Curves of Leaky ReLU & Generalized ReLU functions" title="Curves of Leaky ReLU & Generalized ReLU functions" height=140><br/>
    <img src="https://miro.medium.com/max/875/1*XZQ-Op5RiB2gwXQqOlCvkA.png" style="margin: 0.1em;" alt="Curves of Maxout function" title="Curves of Maxout function" height=150>
    <img src="https://miro.medium.com/max/1250/1*2c9kIQBN0gV-fk4cmr2sAQ.png" style="margin: 0.1em;" alt="Curves of swish functions" title="Curves of swish functions" height=150>
  </a>
</div>



## Lost/Cost Function and Gradient Descent

### Overview of Lost Function

+ [Loss function/cost function](../ML/MLNN-Hinton/a02-IntermediateNN.md#loss-functions)
  + NN trained using an optimization process that requires a loss function to calculate the model error
  + many functions used to estimate the error of a set of weights in a neural network
  + prefer a function where the space of candidate solutions maps onto a smooth (but high-dimensional) landscape that the optimization algorithm can reasonably navigate via iterative updates to the model wights
  + maximum likelihood: a framework for choosing a loss function when training neural networks and machine models in general
  + what loss function to use depends on the output data distribution and is closely coupled to the output unit
  + main types of loss functions: cross-entropy and mean squared error
  + cross-entropy loss function > mean squared error: classification that use a sigmoid or softmax activation function in the output layer learn faster and more robustly
  + The use of cross-entropy looses greatly improved the performance of models with sigmoid and softmax outputs, which had previously suffered from saturation and slow learning when using the mean squared error loss. - Deep Learning, 2016

+ [Cross-entropy loss function](../ML/MLNN-Hinton/a09-SoftmaxClass.md#introduction)

  \[L_i = -\log \left( \frac{e^{f_{y_i}}}{\sum_j e^{f_j}} \right) \qquad \text{or equivalently} \qquad L_i = -f_{y_i} + \log \sum_j e^{f_j}\]

  + $f_j$: the $i$-th element of the vector of class score $f$
  + the full loss for the database: the mean of $L-i$ over all training examples together with a regularization term $R(W)$
  + softmax function: $f_j(z) = \frac{e^{z_j}}{\sum_k e^{f_j}}$; taking a vector of arbitrary real-valued scores (in $z$) and squashing it to a vector of values between zero and one that sum to one

+ [Cross-entropy vs. Mean Squared Error](../ML/MLNN-Hinton/a02-IntermediateNN.md#loss-functions)
  + form for training data and model distribution (i.e., negative log-likelihood)

    \[J(W) = - \displaystyle \mathbb{E}_{x, y \sim \hat{p}_{data}} \log(p_{\text{model}}(y|x))\]

  + example of cost functions

    <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
      <a href="https://towardsdatascience.com/comprehensive-introduction-to-neural-network-architecture-c08c6d8e5d98" ismap target="_blank">
        <img src="https://miro.medium.com/max/1250/1*ERuk0wZZw7sejFI9zwd7zQ.png" style="margin: 0.1em;" alt="an example of a sigmoid output coupled with a mean squared error loss" title="an example of a sigmoid output coupled with a mean squared error loss" height=180>
        <img src="https://miro.medium.com/max/1250/1*mJRBxNfU_mjhmi2lvZLxBg.png" style="margin: 0.1em;" alt="example using a sigmoid output and cross-entropy loss" title="example using a sigmoid output and cross-entropy loss" height=180>
      </a>
    </div>


### Lost Function for Softmax Function

+ The [cost function](../ML/MLNN-Hinton/a08-SoftmaxReg.md#cost-function) with weight decay for Softmax Regression

  \[J(\theta) = -\frac{1}{m} \left[ \sum_{i=1}^m \sum_{j=1}^k \mathbf{1}\{y^{(i)}=j\} \log\left( \frac{e^{\theta_j^T x^{(i)}}}{\sum_{l=1}^k} e^{\theta_i^T x{(i)}} \right) \right] + \frac{2}{\lambda} \sum_{i=1}^k \sum_{j=0}^n \theta_{ij}^2 \]

  + $\mathbf{1}\{y^{(i)} = j\}$: an indicator function; only the output of the classifier corresponding to the correct class label
  + $log(x) \in (-\infty, 0] \text{ when } x \in [0, 1]$
  + if the classifier outputs 1 for the training example, then the cos is zero.


### Gradient Descent for Softmax Function

+ [The gradient descent function](../ML/MLNN-Hinton/a08-SoftmaxReg.md#gradients)

  \[\Delta_{\theta_j}J(\theta) = -\frac{1}{m} \sum_{i=1}^m \left[ x^{(i)} \left(\mathbf{1}\{y^{(i)} = j\} - p(y^{(i)} = j | x^{(i)}; \theta)\right) \right] + \lambda \theta_j \]

  + the function computes the gradients for a single class $j$

  + $\left(\mathbf{1}\{y^{(i)} = j\} - p(y^{(i)} = j | x^{(i)}; \theta)\right)$: evaluate a single value btw 0 and 1

  + multiplied by a vector $x^{(i)}$ to get the weight updates for a single training example $i$ and a single class $j$

+ [Vectorization and dimensional analysis](../ML/MLNN-Hinton/a08-SoftmaxReg.md#gradients)
  + $M$: outputs for all classes and all training examples; dimensions: [numClass x numExamples]
  + $grad$: gradient matrix; dimension: [numClass x input Size]
  + $data$: data matrix; dimension: [inputSize x numExamples]

  \[grad = M * data\]


## Output Units

### Overview of Output Units

+ [Summary of data types, distributions, output layers and cost functions](../ML/MLNN-Hinton/a02-IntermediateNN.md#output-units)

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/comprehensive-introduction-to-neural-network-architecture-c08c6d8e5d98" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/1*s83dd-WhOgE6ZckGST-C8Q.png" style="margin: 0.1em;" alt="Summary of data types, distributions, output layers and cost functions" title="Summary of data types, distributions, output layers and cost functions" width=500>
    </a>
  </div>


## Activation Functions

### Overview of Activation Functions

+ [Activation functions](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)
  + analogous to the build-up of electrical potential in biological neurons
  + activation potential: mimicked in artificial neural networks using a probability
  + Characteristics:
    + non-linearity: ensures not linearity
    + differentiable: ensure gradients remain large through the hidden unit
  + The general form of an activation function

    \[h = f(W^T X + b)\]

    + $h$: the neural output
    + $f(.)$: the activation function acting on the weights and bases

+ [Non-linearity](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)
  + linear function
    + a polynomial of one degree
    + linear equation easy to solve
    + limited in complexity and less power to learn complex functional mappings from data
  + Neural network w/o activation function
    + a linear regression model
    + limited in the set of functions able to approximate
  + Universal approximation theorem: generalized non-linear function approximations
  + non-linear activation able to generate non-linear mappings from inputs to outputs

+ [nonlinear layer (or activation layer)](../ML/MLNN-Hinton/a10-CNNsGuide.md#relu-rectified-linear-units-layers)
  + introduce nonlinearity to system that basically has been computing linear operations during the convolutional layer
  + linear operation: element wise multiplications and summations
  + nonlinearity: tanh, sigmoid, and ReLU
  + increasing the nonlinearity properties of the model and the overall network without affecting the receptive fields of the convolutional layer

+ [Differentiable](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)
  + required to perform backpropagation in the network
  + required to compute gradients of errors (loss) w.r.t. to the weights updated using gradient descent
  + linear activation function
    + an easily differentiable function
    + optimized using convex optimization
    + limited model capacity

+ [Vanishing gradient problem](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)
  + small gradients and several hidden layers results in multiplied gradient during backpropagation
  + computer limitation on precision when multiply many small numbers
  + the value of the gradient quickly vanished
  + important challenge generated in deep neural networks

+ [Common choices of activation function](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/comprehensive-introduction-to-neural-network-architecture-c08c6d8e5d98" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/1*22g-mJEUfAWBT7lzgiyIiw.png" style="margin: 0.1em;" alt="Summary of activation functions for neural networks." title="Summary of activation functions for neural networks." width=550>
    </a>
  </div>


### Sigmoid and Softmax Functions

+ Logistic regression as a special case of Softmax regression with 2 classes

+ [Softmax classifier](../ML/MLNN-Hinton/a09-SoftmaxClass.md#possible-confusion-naming-conventions)
  + using the cross-entropy loss
  + using softmax function: used to squash the raw class scores into normalized positive values that sum to one

+ [Sigmoid and softmax functions](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)

  \[\phi(z) = \frac{1}{1 + e^{-z}}\]

  + used as output functions for binary classification
  + generally not used within hidden layers
  + softmax function
    + multidimensional version of the sigmoid
    + used for multiclass classification
  + issue: zero centeredness

+ [Architecture for Softmax](../ML/MLNN-Hinton/04-Multiclasses.md#another-diversion-the-softmax-output-function)

    <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
      <a href="http://www.cs.toronto.edu/~hinton/coursera/lecture4/lec4.pptx" ismap target="_blank">
        <img src="../ML/MLNN-Hinton/img/m04-13.png" style="margin: 0.1em;" alt="Representation of Softmax group" title="Representation of Softmax group" width=200>
      </a>
      <a href="https://www.ritchieng.com/machine-learning/deep-learning/neural-nets/" ismap target="_blank">
        <img src="https://raw.githubusercontent.com/ritchieng/machine-learning-nanodegree/master/deep_learning/introduction/lr2.png" style="margin: 0.1em;" alt=" multinomial logistic regression or softmax logistic regression" title=" multinomial logistic regression or softmax logistic regression" width=300>
      </a>
    </div>

+ [Softmax Definition](../ML/MLNN-Hinton/04-Multiclasses.md#another-diversion-the-softmax-output-function)

  A softmax group $G$ is a group of output neurons whose outputs use the softmax activation defined by

  \[y_i = \frac{e^{z_i}}{\displaystyle \sum_{j \in G} e^{z_j}}\]

  so that the outputs sum to 1. The cost function is given by

  \[C = - \sum_j t_j \ln(y_j)\]

+ [Proposition of Softmax](../ML/MLNN-Hinton/04-Multiclasses.md#another-diversion-the-softmax-output-function)

  By the Quotient Rule, the derivatives are

  \[\frac{\partial y_i}{\partial z_i} = \frac{\partial}{\partial z_i} \left(\frac{e^{z_i}}{\sum_{j \in G} e^{z_j}}\right) = y_i(1 - y_i) \qquad\qquad \frac{\partial y_i}{\partial z_j} = \frac{\partial}{\partial z_j} \frac{1}{2} (t_j - y_j)^2 = - y_i y_j\]

  or more fancy-like using the Kronecker Delta:

  \[\frac{\partial y_i}{\partial z_j} = y_i (\delta_{ij} - y_j)\]

+ [Proposition of Softmax](../ML/MLNN-Hinton/04-Multiclasses.md#another-diversion-the-softmax-output-function)

  The derivatives of the cost function are

  \[\frac{\partial C}{\partial z_i} = y_i - t_i.\]

+ [Cross-entropy for Softmax](../ML/MLNN-Hinton/04-Multiclasses.md#another-diversion-the-softmax-output-function)

  the suggested cost function to use with softmax

  \[C = - \sum_j t_j \ln(y_j) = -\ln(y_i)\]

  + $t_j$: target values
  + $t_j = \begin{cases} 1 & j \in I \subset G \\ 0 & j \in G-I \end{cases}$
  + $y_i$: the probability of the input belonging to class $I$
  + simply put 0 on the wrong answers and 1 for the right answer ($t_i$)
  + Cross-entropy cost function

+ [Property of Softmax](../ML/MLNN-Hinton/04-Multiclasses.md#another-diversion-the-softmax-output-function)

  $C$ w/ very big gradient descent if target value = 1 and actual value approx. 0.

+ Softmax better than the gradient descent w/ squared error

+ [Softmax regression](../ML/MLNN-Hinton/a08-SoftmaxReg.md#introduction)
  + a generalized form of logistic regression
  + used in multi-class classification problems where the classes are mutually exclusive
  + Formula

    \[h_\theta(x^{(i)}) = \begin{bmatrix} p(y^{(i)} = 1 | x^{(i)}; \theta) \\ p(y^{(i)} = 2 | x^{(i)}; \theta) \\ \vdots \\ p(y^{(i)} = k | x^{(i)}; \theta) \end{bmatrix} = \frac{1}{\sum_{j=1}^k e^{\theta_j^T} x{(i)}} \begin{bmatrix} e^{\theta_1^T x^{(i)}} \\ e^{\theta_2^T x^{(i)}} \\ \vdots \\ e^{\theta_k^T x^{(i)}}\end{bmatrix}\]

  + $x^{(i)}$: the input vector of the $i$th sampling case
  + $y^{(i)}$: the actual calculated output value of the $i$th sampling case
  + The output is a vector of the probability w/ actual output value of $y^{(k)} = i$ where $i = 1, 2, \dots, k$

+ [Softmax classifier](../ML/MLNN-Hinton/a09-SoftmaxClass.md#introduction)
  + a generalization of Logistic Regression classifier to multiple classes
  + providing a intuitive output (normalized class probabilities)
  + a probabilistic interpretation 
  + function mapping $f(x_i; W) - Wx_i$ stays unchanged
  + interpret these scores as the uncommonalized log probabilities for each class


### Hyperbolic Tangent (tanh) Function

+ [Hyperbolic tangent function (Tanh) function](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)

  \[\phi(z) = \frac{e^z - e^{-z}}{e^z + e^{-z}}\]

  + resolving the zero centeredness issue of the sigmoid function
  + always preferred to the sigmoid function within hidden layers
  + suffer from the other problems plaguing the sigmoid function, including the vanishing gradient problem


### Softplus Functions

+ [Softplus functions](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)

  \[\phi(z) = \ln(1 + e^z)\]

  + a slight variation of ReLU where the transition at zero is somewhat smooth
  + benefit: no discontinuities in the activation function

  + sigmoid for binary classification
  + softmax for multiclass classification
  + linear for a regression problem


### Rectified Linear Unit (ReLU)

+ [Rectified Linear Unit (ReLU)](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)

  \[\phi(z) = max(o, x)\]

  + simplest non-linear activation function
  + avoid and rectify the vanishing gradient problem
  + used by almost all deep learning models
  + only used within hidden layers of a neural network
  + issue: maybe unstable during training and die
  + the most successful and widely-used activation function

+ [Leaky ReLU and Generalized ReLU](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)
  + dead neurons: ReLU unstable causes network never activated on any data point
  + Leaky ReLU

    \[g(x_i, \alpha) = \max{a, x_i} + \alpha \min{0, x_i}\]

    + contain a small slope
    + purpose of slope: keep the updates alive and prevent the production of dead neurons
    + still discontinuity at zero
    + no longer flat below zero
    + merely having a reduced gradient
    + a subset of generalized ReLU

  + Leaky ReLU & Generalized ReLU
    + slight variations on the basic ReLU function
    + difference: merely depend on the chosen value of $\alpha$

+ [Rectified Linear Units](../ML/MLNN-Hinton/a10-CNNsGuide.md#relu-rectified-linear-units-layers)
  + working far better
  + able to train a lot faster (computational efficiency) w/o making a significant difference to the accuracy
  + alleviating the vanishing gradient problem
  + applying yje function $f(x) = \max(0, x)$ to all of the values in the input volume


### Maxout Function

+ [Maxout function](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)

  \[g(x) = \max_{i \in \{ 1, \dots, k\}} \alpha_i x_i + \beta\]

  + simply the maximum of $k$ linear functions
  + a hybrid approach consisting of linear combinations of ReLU and leaky ReLU units


### Self-Gated Activation Function

+ [Swish: A Self-Gated Activation Function](../ML/MLNN-Hinton/a02-IntermediateNN.md#activation-functions)

  \[f(x) = x \cdot sigmoid(x)\]

  + tend to work better than ReLU on deeper models across a number of challenging datasets
  + a smooth non-monotonic function that does not suffer from the problem of zero derivatives
  + seen as a somewhat magical improvement to neural networks
  + a clear improvement for deep networks


<div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
  <a href="https://towardsdatascience.com/comprehensive-introduction-to-neural-network-architecture-c08c6d8e5d98" ismap target="_blank">
    <img src="https://miro.medium.com/max/1400/0*WYB0K0zk1MiIB6xp.png" style="margin: 0.1em;" alt="Curve of Sigmoid function" title="Curve of Sigmoid function" height=140>
    <img src="https://miro.medium.com/max/1400/0*VHhGS4NwibecRjIa.png" style="margin: 0.1em;" alt="Curve of hyperbolic tangent function" title="Curve of hyperbolic tangent function" height=140>
    <img src="https://miro.medium.com/max/875/0*TsH2CNeu5Qlt32Oj.png" style="margin: 0.1em;" alt="Curves of the ReLU & Softplus function" title="Curve of the ReLU & Softplus function" height=140>
    <img src="https://miro.medium.com/max/875/1*pTuWvoEIiHQFBvosVjmW5A.png" style="margin: 0.1em;" alt="Curves of Leaky ReLU & Generalized ReLU functions" title="Curves of Leaky ReLU & Generalized ReLU functions" height=140><br/>
    <img src="https://miro.medium.com/max/875/1*XZQ-Op5RiB2gwXQqOlCvkA.png" style="margin: 0.1em;" alt="Curves of Maxout function" title="Curves of Maxout function" height=150>
    <img src="https://miro.medium.com/max/1250/1*2c9kIQBN0gV-fk4cmr2sAQ.png" style="margin: 0.1em;" alt="Curves of swish functions" title="Curves of swish functions" height=150>
  </a>
</div>


## Lost/Cost Function and Gradient Descent

### Overview of Lost Function

+ [Loss function/cost function](../ML/MLNN-Hinton/a02-IntermediateNN.md#loss-functions)
  + NN trained using an optimization process that requires a loss function to calculate the model error
  + many functions used to estimate the error of a set of weights in a neural network
  + prefer a function where the space of candidate solutions maps onto a smooth (but high-dimensional) landscape that the optimization algorithm can reasonably navigate via iterative updates to the model wights
  + maximum likelihood: a framework for choosing a loss function when training neural networks and machine models in general
  + what loss function to use depends on the output data distribution and is closely coupled to the output unit
  + main types of loss functions: cross-entropy and mean squared error
  + cross-entropy loss function > mean squared error: classification that use a sigmoid or softmax activation function in the output layer learn faster and more robustly
  + The use of cross-entropy looses greatly improved the performance of models with sigmoid and softmax outputs, which had previously suffered from saturation and slow learning when using the mean squared error loss. - Deep Learning, 2016

+ [Cross-entropy loss function](../ML/MLNN-Hinton/a09-SoftmaxClass.md#introduction)

  \[L_i = -\log \left( \frac{e^{f_{y_i}}}{\sum_j e^{f_j}} \right) \qquad \text{or equivalently} \qquad L_i = -f_{y_i} + \log \sum_j e^{f_j}\]

  + $f_j$: the $i$-th element of the vector of class score $f$
  + the full loss for the database: the mean of $L-i$ over all training examples together with a regularization term $R(W)$
  + softmax function: $f_j(z) = \frac{e^{z_j}}{\sum_k e^{f_j}}$; taking a vector of arbitrary real-valued scores (in $z$) and squashing it to a vector of values between zero and one that sum to one

+ [Cross-entropy vs. Mean Squared Error](../ML/MLNN-Hinton/a02-IntermediateNN.md#loss-functions)
  + form for training data and model distribution (i.e., negative log-likelihood)

    \[J(W) = - \displaystyle \mathbb{E}_{x, y \sim \hat{p}_{data}} \log(p_{\text{model}}(y|x))\]

  + example of cost functions

    <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
      <a href="https://towardsdatascience.com/comprehensive-introduction-to-neural-network-architecture-c08c6d8e5d98" ismap target="_blank">
        <img src="https://miro.medium.com/max/1250/1*ERuk0wZZw7sejFI9zwd7zQ.png" style="margin: 0.1em;" alt="an example of a sigmoid output coupled with a mean squared error loss" title="an example of a sigmoid output coupled with a mean squared error loss" height=180>
        <img src="https://miro.medium.com/max/1250/1*mJRBxNfU_mjhmi2lvZLxBg.png" style="margin: 0.1em;" alt="example using a sigmoid output and cross-entropy loss" title="example using a sigmoid output and cross-entropy loss" height=180>
      </a>
    </div>


### Gradient Descent

+ [Gradeint descent/Delta rule](../ML/MLNN-Hinton/a01-IntroNN.md#gradient-descent)
  + an iterative method for finding the minimum of a function
  + Making a step means: $w^{new} = w^{old} + \text{step}$
  + Opposite direction of the derivative means: $w^{new} = w^{old} - \lambda \frac{d\mathcal{L}}{dw}$
  + change to move conventional notation: $w^{(i+1)} = w^{(i)} - \lambda \frac{d\mathcal{L}}{dw}$
  + learning rate ($\lambda$):
    + large learning rate:
      + put more weight on the derivative
      + made larger step for each iteration of the algorithm
    + smaller learning rate
      + less weight is put on the derivative
      + smaller steps made for each iteration

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/simple-introduction-to-neural-networks-ac1d7c3d7a2c" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/1*MizSwb7-StSLiWlI2MKsxg.png" style="margin: 0.1em;" alt="Illustration of learning rate" title="Illustration of learning rate" width=200>
    </a>
  </div>

+ [Considerations for gradient descent](../ML/MLNN-Hinton/a01-IntroNN.md#gradient-descent)
  + derive the derivatives
  + know what the learning rate is or how to set it
  + avoid local minima
  + the full loss function includes summing up all individual 'errors'

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/simple-introduction-to-neural-networks-ac1d7c3d7a2c" ismap target="_blank">
      <img src="https://miro.medium.com/max/625/1*tIqU7GK--aJ-SOdOBrh37Q.png" style="margin: 0.1em;" alt="Illustration of local & global optimal" title="Illustration of local & global optimal" height=150>
      <img src="https://miro.medium.com/max/875/1*MwnXifl-uLdTrjjxiNCDJw.png" style="margin: 0.1em;" alt="Network getting stuck in local minima" title="Network getting stuck in local minima" height=150>
      <img src="https://miro.medium.com/max/875/1*K7HNhO3Fsedvx94psTpBHA.png" style="margin: 0.1em;" alt="Network reach global minima" title="Network reach global minima" height=150>
    </a>
  </div>

+ [Batch and stochastic gradient descent](../ML/MLNN-Hinton/a01-IntroNN.md#gradient-descent)
  + use a batch (a subset) of data as opposed to the whole set of data, such that the loss surface is partially morphed during each iteration
  + the loss (likelihood) function used to derive the derivatives for iteration $k$

    \[\mathcal{L}^k = - \sum_{i \in b^k} \left[ y_i \log(p_i) + (1 - p_i)\log(1 - p_i) \right]\]


### Delta Rule

+ [Delta rule for perceptrons](../ML/MLNN-Hinton/a06-DeltaRule.md#delta-rule)
  + Gradient descent learning requires that any change in a particular weight be proportional to the negative of the derivative of the error
  + The change in a given weight must be proportional to the negative of the prior equation

    \[\Delta w_{ij_x} = - \varepsilon \frac{\partial E}{\partial w_{ij}} = \varepsilon \partial a_{i_x}\]

  + $\Delta$: the difference btw the target and actual activation of the relevant output node
  + $\varepsilon$: learning rate

+ [Linear Activation function instead of a Threshold Activation function](../ML/MLNN-Hinton/a06-DeltaRule.md#delta-rule)
  + Threshold Activation function:
    + characterize both the McColloch and Pitts network and the perceptron is not differentiable at the transition between the activations of $0$ and $1$ (slope = $\infty$) 
    + derivative = 0 over the remainder of the function
  + Linear Activation function or other differentiable functions
    + allow the derivative of the error to be calculable

+ [Kronecker Delta](../ML/MLNN-Hinton/a07-DeltaFunc.md#kronecker-delta)
  + Definition

    \[\delta_{ij} = \begin{cases} 1 & i = j \\ 0 & i \neq j \end{cases} \]

  + __property__. Simplify

    \[\sum_k \delta_{ik}\delta{kj} = \delta_{ij}\]

+ [Dirac Delta](../ML/MLNN-Hinton/a07-DeltaFunc.md#dirac-delta)
  + Definition

    \[\delta(x) = \begin{cases} \infty & x = 0 \\ 0 & \text{otherwise}\end{cases} \]

    The value at which the delta function become infinite can be controlled by substituting $x - x_0$ for $x$

    \[\delta(x - x_0) = \begin{cases} \infty & x=x_0 \\ 0 & \text{otherwise} \end{cases} \]

  + Alternative definition

    \[ \int_{-\infty}^{\infty} f(x) \delta(x - x_0) dx = f(x_0) \tag*{(7)}\]

    + continuous around $x=x_0$
    + most common way used for the dirac delta function
  + __Property__.

    \[\int_{-\infty}^{\infty} f(x) \delta(x - x_0)dx = f(x_0) \\ \delta(ax) = \frac{1}{|a|} \delta(x)\]


### Mini-batch Gradient Descent

+ [Stochastic gradient descent (SGD)](../ML/MLNN-Hinton/06-MiniBatch.md#lecture-notes)
  + highly redundant dataset
    + the first half gradient $\simeq$ the second half gradient
    + update the weights using the first half gradient then get a gradient for the new weights on the second half gradient
  + online learning: update weights after each case
  + mini-batches usually better than online
    + typically 10, 100, even 1000 examples
    + advantages:
      + less computation to update the weights
      + using matrix-matrix multiplies to compute the gradient for many cases simultaneously
    + efficient matrix multiplications, especially on GPUs
  + mini-batches require to be balanced for classes
    + allocating the same class in a batch causing sloshing weights
    + random permutation for mini-atches and randomly select the mini-batches for training

+ [Two types of learning algorithm](../ML/MLNN-Hinton/06-MiniBatch.md#lecture-notes)
  + full gradient computed from all the training cases
    + ways to speed up learning, eg. non-linear conjugate gradient
    + optimization community: the general problem of optimizing smooth non-linear functions
    + multilayer neural nets: not typical of the problems; required a lot of modification to make them work
  + mini-batch learning for large neural networks w/ very large and highly redundant training sets
    + mini-batches may be quite big when adapting fancy methods
    + big mini-batches: more computationally efficient

+ [A basic mini-batch gradient descent algorithm](../ML/MLNN-Hinton/06-MiniBatch.md#lecture-notes)
  + guess an initial learning rate
    + measured on a validation set
    + each mini-batch just a rough estimate of the overall gradient
    + reducing learning rate: error getting worse or oscillated
    + increasing learning rate: error falling fairly consistent but slowly
  + write a simple program to automate this way to adjusting the learning rate
  + toward end of mini-batch learning
    + nearly always help to turn down the learning rate
    + remove fluctuations in the final weights caused by the variations btw mini-batches
  + criteria to cease the learning
    + the error stops decreasing
    + using the error on a separate validation set

### Tricks for mini-batch gradient descent

+ [Initializing the weights](../ML/MLNN-Hinton/06-MiniBatch.md#a-bag-of-tricks-for-mini-batch-descent)
  + two different units w/ exactly the same bias and exactly the same incoming and outgoing weights
    + exactly the same gradients
    + break symmetry by initializing the weights to have small random values
  + overshooting learning
    + generally smaller incoming weights when the fan-in is big
    + principle: initialize the weights to be proportional to sqrt(fan-in)
  + scale the learning rate the same way as initialization
 
+ [Shifting and scaling the inputs](../ML/MLNN-Hinton/06-MiniBatch.md#a-bag-of-tricks-for-mini-batch-descent)
  + Shifting
    + adding a constant to each of the components of the inputs
    + when using steepest descent, shifting the input values makes a big
    + help to transform each component of the input vector so that it has zero mean over the whole training set
    + considering the inputs from a hidden unit
      + the hyperbolic tangent (2*logistic - 1) produces hidden activations roughly zero mean
      + hyperbolic tangent btw $[-1, 1]$
      + faster learning in the next layer only if the inputs to the hyperbolic tangents distributed sensibly around 0
      + better than the logistic
    + Logistic performs better when
      + logistic sweeps things under
      + output = 0 no matter how small the inputs are
      + fluctuations ignore in big negative inputs
      + hyperbolic tangent requires to go out of the plateau before ignoring
  + Scaling
    + when using steepest descent, scaling the input values makes a big difference
    + help to transform each component of the input vector so that it has unit variance over the whole training set
    + each component of the input with typical variance value of 1 or -1

+ [Decorrelating the input components](../ML/MLNN-Hinton/06-MiniBatch.md#a-bag-of-tricks-for-mini-batch-descent) - a thorough method
  + guarantee to get a circle error surface at least for a linear neuron
  + decorrelate the components of the input vectors to make learning much easier
  + linear neuron: a big win by decorrelating each component of the input from the other input components
  + ways to decorrelate inputs
    + reasonable method: Principal Components Analysis (PCA)
    + drop the principal components with the smallest eigenvalues
    + achieving some dimensionality reduction
    + divide the remaining principal components by the square roots of their eigenvalues
    + linear neuron: convert an axis aligned elliptical error surface into a circular one
  + circular error surface: the gradient points straight towards the minimum

+ [Common problems occurring in multilayer networks](../ML/MLNN-Hinton/06-MiniBatch.md#a-bag-of-tricks-for-mini-batch-descent)
  + Starting w/ a very big learning rate
    + the weights of each hidden unit will all become very big and positive or very big and negative
    + driven the hidden units either firmly on or firmly off
    + state of the hidden unit no longer depends on the input
    + tiny error derivatives for the hidden units and not decreasing; the error root $\to$ 0
    + hit a plateau (zero derivatives): mistaken for a local minimum
  + Strategy w/ multilayer nets
    + classification networks: using a squared error or a cross-entropy error
    + the best guessing strategy: to make each output unit always produce an output equal to the proportion of time it should be a 1
    + quickly find the strategy and the error decrease quickly
    + multilayer nets:
      + improving over the guessing strategy requires sensible information through the whole nets
      + take a long time to improve on it by making use of the input
      + small weights result in the long learning time
    + quick learn w/ quick stop $\simeq$ local minimum $\to$ another plateau

+ [Criteria to stop the learning](../ML/MLNN-Hinton/06-MiniBatch.md#a-bag-of-tricks-for-mini-batch-descent)
  + error fluctuations caused by the different gradients on different mini-batches
  + turing down the learning rate reduces the random fluctuations in the error
    + a quicker win (red curve)
    + a slower learning (green curve)
  + Don't turn down the learning rate too soon!

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="http://www.cs.toronto.edu/~hinton/coursera/lecture6/lec6.pptx" ismap target="_blank">
      <img src="img/m06-04.png" style="margin: 0.1em;" alt="Curve of learning rate" title="Curve of learning rate" width=250>
    </a>
  </div>

+ [Methods to speed up mini-batch learning](../ML/MLNN-Hinton/06-MiniBatch.md#a-bag-of-tricks-for-mini-batch-descent)
  + use "momentum"
  + use separate adaptive learning rates for each parameter
  + rmsprop
  + take a fancy method from the optimization literature that makes use of curvature information


## Output Units

### Overview of Output Units

+ [Summary of data types, distributions, output layers and cost functions](../ML/MLNN-Hinton/a02-IntermediateNN.md#output-units)

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/comprehensive-introduction-to-neural-network-architecture-c08c6d8e5d98" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/1*s83dd-WhOgE6ZckGST-C8Q.png" style="margin: 0.1em;" alt="Summary of data types, distributions, output layers and cost functions" title="Summary of data types, distributions, output layers and cost functions" width=500>
    </a>
  </div>



## Hyperparameters

### Summary

+ __REMARK 1.__ the test/validation loss is a good indicator of the network's convergence.
  + the test/validation loss used to provide insights on the training process
  + the final test accuracy used for comparing performance

+ __REMARK 2.__ achieving the horizontal part of the test loss is the goal of hyper-parameter tuning
  + difficult with deep neural network
  + with networks becoming more powerful with greater depth (i.e., more layers), width (i.e., more neurons or filters per layer), and the addition of skip connections to its architecture
  + various forms of regularization, such as weight decay or dropout
  + important hyper-parameters
  + using a variety of optimization methods

+ __REMARK 3.__ the amount of regularization must be balanced for each dataset and architecture
  + permit general use of super-convergence
  + reducing other forms of regularization
  + regularized w/ very large learning rates makes training significantly and efficient

+ __REMARK 4.__ the practitioner's goal is obtaining the highest performance while minimizing the needed computational time
  + examined in conjunction with the execution time of the training
  + choosing the number of epochs/iterations for training should be large enough to maximize the final test performance but no larger

+ __REMARK 5.__ optimal momentum value(s) will improve network training
  + the optimal training procedure: a combination of
    + an increasing cyclical learning rate w/ an initial small learning rate permits convergence to begin
    + a decreasing cyclical momentum w/ allowing the learning rate to become larger in the early to middle parts of training
  + a constant learning rate and a decreasing cyclical momentum (0.9 ~ 0.99):
    + acting like a pseudo increasing rate
    + speeding up the training
  + too large momentum value
    + poor training results
    + visible early in the training
    + quickly tested

+ __REMARK 6.__ the amount of regularization must be balanced for each dataset and architecture
  + the value of weight decay: key knob to tune regularization against the regularization from an increasing learning rate
  + other regularization generally fixed
  + weight decay changed easily when experimenting with maximum learning rate and stepsize values

### Overview

+ [the process of setting the hyper-parameters](../ML/MLNN-Hinton/a13-HyperParam.md#1-introduction)
  + including the designing the network architecture
  + requiring expertise and extensive trial and error and time consuming

+ [no simple and easy ways to set hyper-parameters](../ML/MLNN-Hinton/a13-HyperParam.md#1-introduction)
  + learning rate, batch size, momentum and weight decay
  + grid search or random search: computationally expensive and time consuming
  + training time and final performance: highly dependent on good choice
  + choosing the standard architecture and the hyper-parameter files freely available in model zoo or from gitgub.com

+ proposed methodologies for finding optimal settings for several hyper-parameters
  
+ goal: providing practical advice that saves time and effort, yet improves performance

+ [basis of the approach](../ML/MLNN-Hinton/a13-HyperParam.md#1-introduction)
  + well-known concept of the balance between underfitting and overfitting
  + examining the training's test-/validation loss for clues of underfitting and overfitting to strive for optimal set of hyper-parameters
  + paying close attention while using cyclical learning rates and cyclical momentum

### Batch Size

+ [Small batch sizes](../ML/MLNN-Hinton/a13-HyperParam.md#42-batch-size)
  + recommended for regularization effects
  + optimal batch size on the order of 80 for Cifar-10
  + using a large batch size when using the 1cycle learning rate schedule

+ [Comparing batch sizes](../ML/MLNN-Hinton/a13-HyperParam.md#42-batch-size)
  + issue: conflicting results if one maintains a constant number of epochs vs. a constant number of iterations
  + neither appropriate for comparing different batch sizes
    + constant epochs: not account for the significant computational efficient of large batch size so it penalizes larger batch sizes
    + constant iterations: favor of larger batch sizes too much
  + larger batch sizes $\to$ the use of larger learning rate in the 1cycle learning rate schedule
  + best practice: maintaining a near constant execution time
  + people interested in minimizing training time while maintaining high performance

+ [The effects of total batch size (TBS)](../ML/MLNN-Hinton/a13-HyperParam.md#42-batch-size)
  + The effects of total batch size (TBS) on validation loss for the Cifar-10 with resnet-56 and a 1cycle learning rate schedule.
  + For a fixed computational budget, larger TBS yields higher test accuracy but smaller TBS has lower test loss.

+ [Other recommendations](../ML/MLNN-Hinton/a13-HyperParam.md#42-batch-size)
  + modifying the batch size, rather than the learning rates
  + the batch size limited by the hardware's memory, while the learning rate not
  + using a batch size that fits in the hardware's memory and enable using larger learning rates


## Linear Neurons

### Model of Linear Neurons

+ Comparisons
  + Perceptron: the weights getting closer to a good set of weights
  + Linear neurons: the output getting closer to target outputs
  + perceptron unable to generalize to hidden layers

+ [Linear neurons](../ML/MLNN-Hinton/03-Backpropagation.md#learning-the-weights-of-a-linear-neuron)
  + linear filter in EE
  + real-valued output: weighted sum of outputs

    \[y = \sum_i x_i w_i = \mathbf{W}^T \mathbf{x}\]

    + $y$: neuron's estimate the desired output
    + $\mathbf{W}$: weight vector
    + $\mathbf{x}$: input vector
  + aim of learning (objective): to minimize the error summed over all training cases
  + error (measure): the squared difference btw the desired output and the actual output


### Cost Function for Linear Neurons

+ [Definition](../ML/MLNN-Hinton/03-Backpropagation.md#learning-the-weights-of-a-linear-neuron):
  
  \[E = \frac{1}{2} \sum_{n \in training} (t^n - y^n)^2\]

  + $E$: total error
  + $t^n$: the target value of $n$-th sampling case
  + $y^n$: the actual value of $n$-th sampling case
  + $1/2$: factor to cancel the derivative constant

+ [Derivative of Error function for weights](../ML/MLNN-Hinton/03-Backpropagation.md#learning-the-weights-of-a-linear-neuron)

  \[\dfrac{\partial E}{\partial w_i} = \frac{1}{2} \sum_n \dfrac{\partial y^n}{\partial w_i} \dfrac{dE^n}{dy^n} = - \sum_n x_i^n (t^n - y^n)\]

  + applying chain rule
  + explain how the output changes as we change the weights times how the error changes as we change the output

+ [Batch delta rule](../ML/MLNN-Hinton/03-Backpropagation.md#learning-the-weights-of-a-linear-neuron)

  \[\Delta w_i = -\varepsilon \dfrac{\partial E}{\partial w_i} = \sum_n \varepsilon x_i^n (t^n - y^n)\]

+ [online delta-rule vs learning rule for perceptrons]((../ML/MLNN-Hinton/03-Backpropagation.md#learning-the-weights-of-a-linear-neuron))
  + perceptron learning
    + increment or decrement the weight vector by the input vector
    + only change the weights when making an error
  + online version of the delta-rule
    + increment or decrement the weight vector by the input vector but scaled by the residual error and the learning rate
    + choose a learning rate $\rightarrow$ annoying
      + too big $\rightarrow$ unstable
      + too small $\rightarrow$ slow


### Error Surface for Linear Neuron

+ [Error surface in extended weight space](../ML/MLNN-Hinton/03-Backpropagation.md#the-error-surface-for-a-linear-neuron)
  + Linear neuron with a squared error
    + quadratic bowl: linear neuron with a squared error
    + parabolas: vertical cross-sections
    + ellipses: horizontal cross-sections
  + multi-layer, non-linear nets: much more complicated
    + smooth curves
    + local minima
  + pictorial view of gradient descent learning using Delta rule

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="http://www.cs.toronto.edu/~hinton/coursera/lecture3/lec3.pptx" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/m03-03.png" style="margin: 0.1em;" alt="error surface" title="error surface" height=150>
    </a>
    <a href="https://math.stackexchange.com/questions/1249308/what-is-the-difference-between-an-elliptical-and-circular-paraboloid-3d/1249309#1249309" ismap target="_blank">
      <img src="https://i.stack.imgur.com/goYnm.gif" style="margin: 0.1em;" alt="An elliptical paraboloid" title="An elliptical paraboloid" height=150>
    </a>
  </div>

+ [Online vs batch learning](../ML/MLNN-Hinton/03-Backpropagation.md#the-error-surface-for-a-linear-neuron)
  + Simplest kind of batch learning (left diagram)
    + elliptical contour lines
    + steepest descent on the error surface
    + travel perpendicular to the contour lines
    + batch learning: the gradient descent summed over all training cases
  + simplest kind of online learning (right diagram)
    + online learning: update the weights in proportion to the gradient after each training case
    + zig-zag around the direction of steepest descent
  + elongated ellipse: the direction of steepest descent almost perpendicular to the direction towards the minimum

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="http://www.cs.toronto.edu/~hinton/coursera/lecture3/lec3.pptx" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/m03-04.png" style="margin: 0.1em;" alt="Contour for batch learning" title="Contour for batch learning" height=150>
      <img src="../ML/MLNN-Hinton/img/m03-05.png" style="margin: 0.1em;" alt="Contour for online learning" title="Contour for online learning" height=150>
      <img src="../ML/MLNN-Hinton/img/m03-06.png" style="margin: 0.1em;" alt="enlongated ellipse with slow learning" title="enlongated ellipse with slow learning" height=150>
    </a>
  </div>


### Backpropagation

+ [Backpropagation](../ML/MLNN-Hinton/a01-IntroNN.md#backpropagation)
  + the central mechanism by which neural networks learn
  + During prediction, a neural network propagates signal forward through the nodes of the network until it reaches the output layer where a decision is made.
  + A neural network propagates signal forward through the nodes of the network until it reaches the output layer where a decision is made.
  + The network then backpropagates information about this error backward through the network such that it can alter each of the parameters.
  + Backpropagation performed first in order to gain the information necessary to perform gradient descent.

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/simple-introduction-to-neural-networks-ac1d7c3d7a2c" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/1*q1M7LGiDTirwU-4LcFq7_Q.png" style="margin: 0.1em;" alt="The forward pass on the left calculates z as a function f(x,y) using the input variables x and y. The right side of the figures shows the backward pass. Receiving dL/dz, the gradient of the loss function with respect to z from above, the gradients of x and y on the loss function can be calculate by applying the chain rule, as shown in the figure." title="Forward propagation and Back propagation" width=550>
    </a>
  </div>

+ [Automatic differentiation](../ML/MLNN-Hinton/a01-IntroNN.md#backpropagation)

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/simple-introduction-to-neural-networks-ac1d7c3d7a2c" ismap target="_blank">
      <img src="https://miro.medium.com/max/1250/1*fdYrXF6IGhS0nitxkoHJcA.png" style="margin: 0.1em;" alt="Derivative of Loss function with differentiation" title="Derivative of Loss function with differentiation" width=450>
    <a href="https://towardsdatascience.com/simple-introduction-to-neural-networks-ac1d7c3d7a2c" ismap target="_blank">
      <img src="https://miro.medium.com/max/1250/1*fdYrXF6IGhS0nitxkoHJcA.png" style="margin: 0.1em;" alt="function library to the architecture such that the procedure is abstracted and update automatically as the network architecture" title="Function library" width=450>
    </a>
    </a>
  </div>

  + a function library that is inherently linked to the architecture such that the procedure is abstracted and updates automatically as the network architecture is updated

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/simple-introduction-to-neural-networks-ac1d7c3d7a2c" ismap target="_blank">
      <img src="https://miro.medium.com/max/1250/1*fdYrXF6IGhS0nitxkoHJcA.png" style="margin: 0.1em;" alt="function library to the architecture such that the procedure is abstracted and update automatically as the network architecture" title="Function library" width=650>
    </a>
  </div>




## Logistic Neurons

### Model for Logistic Neurons

+ [Definition](../ML/MLNN-Hinton/03-Backpropagation.md#learning-the-weights-of-a-logistic-output-neuron)

  \[z = b + \sum_i x_i w_i \qquad y = \frac{1}{1 + e^{-z}}\]

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://www.bo-song.com/coursera-neural-networks-for-machine-learning/" ismap target="_blank">
      <img src="https://www.bo-song.com/wp-content/uploads/2015/12/Untitled-5.png" style="margin: 0.1em;" alt="Logistic function" title="Logistic function" width=200>
    </a>
  </div>

+ [Derivative of the output w.r.t. the logit](../ML/MLNN-Hinton/03-Backpropagation.md#learning-the-weights-of-a-logistic-output-neuron)

  \[y = \frac{1}{1 + e^{-z}} \quad \implies \quad \frac{dy}{dz} = y(1-y)\]

+ [Logistic regression](../ML/MLNN-Hinton/a01-IntroNN.md#the-motivation-for-neural-networks)
  + the problem of estimating a probability that someone has heart disease, P(y=1), given an input value X.
  + the logistic function, to model P(y=1):

    \[P(Y=1) = \frac{e^{\beta_0+\beta_1 X}}{1 + e^{\beta_0+\beta_1 X}} = \frac{1}{1 + e^{-(\beta_0 + \beta_1 X)}}\]

  + general shape: the model will predict P(y=1) with an S-shaped curve
  + $\beta_0$ shifts the curve right or left by $c = − \beta_0 / \beta_1$, whereas $\beta_1$ controls the steepness of the S-shaped curve.
  + change of the $beta_0$ value to move offset
  + change of the $beta_1$ value to distort gradient

  <div style="display:flex;justify-content:center;align-items:center;flex-flow:row wrap;margin: 0.5em;">
    <a href="https://towardsdatascience.com/simple-introduction-to-neural-networks-ac1d7c3d7a2c" ismap target="_blank">
      <img src="https://miro.medium.com/max/875/1*PD7DZlFWkYCxrg5Y1-OOXQ.png" style="margin: 0.1em;" alt="Diagram of logistic regression" title="Diagram of logistic regression" width=250>
      <img src="https://miro.medium.com/max/875/1*B0W_JthGRm6NFEvtD3ZxIA.png" style="margin: 0.1em;" alt="Diagram of logistic regression with beta_0" title="Diagram of logistic regression with beta_0=80" width=250>
      <img src="https://miro.medium.com/max/875/1*YpPeJSaOwD0Pv83KQgj3Iw.png" style="margin: 0.1em;" alt="Diagram of logistic regression with beta_1 = 1.0" title="Diagram of logistic regression with beta_1 = 1.0" width=250>
    </a>
  </div>


### Backpropagation for Logistic Neurons

+ [Idea Behind](../ML/MLNN-Hinton/03-Backpropagation.md#the-backpropagation-algorithm)
  + knowing what actions in the hidden units
  + efficiently computing error derivatives

+ Error derivatives w.r.t activities to get error derivatives w.r.t. the incoming weights on a sampling case

  \[E = \frac{1}{2} \sum_{j \in output} (t_j - y_j)^2 \quad \implies \quad \frac{\partial E}{\partial y_j} = - (t_j - y_j)\]

+ [Total error derivatives w.r.t. various factors](../ML/MLNN-Hinton/03-Backpropagation.md#the-backpropagation-algorithm)

  \[\begin{array}{rcl} \dfrac{\partial E}{\partial z_j} & = & \dfrac{dy_j}{dz_j} \dfrac{\partial E}{\partial y_j} = y_j(1- y_j)\dfrac{\partial E}{\partial y_j} \\\\ \dfrac{\partial E}{\partial y_j} &=& \displaystyle \sum_j \dfrac{dz_j}{dy_i} \dfrac{\partial E}{\partial z_j} = \sum_j w_{ij} \dfrac{\partial E}{\partial z_j} \\\\ \dfrac{\partial E}{\partial w_{ij}} &=& \dfrac{\partial z_j}{\partial w_{ij}} \dfrac{\partial E}{\partial z_j} = y_i \dfrac{\partial E}{\partial z_j} \end{array}\]

+ [Optimization of Logistic Regression](../ML/MLNN-Hinton/a01-IntroNN.md#the-motivation-for-neural-networks)
  + using a loss function in order to quantify the level of error that belongs to our current parameters
  + find the coefficients that minimize this loss function
  + the parameters of the neural network have a relationship with the error the net produces
  + gradient descent:
    + changing the parameters using an optimization algorithm
    + useful for finding the minimum of a function

  + the loss function or the objective function

    \]\mathcal{L}(\beta_0, \beta_1) = - \sum_i \left[ y_i \log(p_i) + ( 1- y_i) \log(1 - p_i)\right]\]


### Lost Function for Softmax Function

+ The [cost function](../ML/MLNN-Hinton/a08-SoftmaxReg.md#cost-function) with weight decay for Softmax Regression

  \[J(\theta) = -\frac{1}{m} \left[ \sum_{i=1}^m \sum_{j=1}^k \mathbf{1}\{y^{(i)}=j\} \log\left( \frac{e^{\theta_j^T x^{(i)}}}{\sum_{l=1}^k} e^{\theta_i^T x{(i)}} \right) \right] + \frac{2}{\lambda} \sum_{i=1}^k \sum_{j=0}^n \theta_{ij}^2 \]

  + $\mathbf{1}\{y^{(i)} = j\}$: an indicator function; only the output of the classifier corresponding to the correct class label
  + $log(x) \in (-\infty, 0] \text{ when } x \in [0, 1]$
  + if the classifier outputs 1 for the training example, then the cos is zero.


### Gradient Descent for Softmax Function

+ [The gradient descent function](../ML/MLNN-Hinton/a08-SoftmaxReg.md#gradients)

  \[\Delta_{\theta_j}J(\theta) = -\frac{1}{m} \sum_{i=1}^m \left[ x^{(i)} \left(\mathbf{1}\{y^{(i)} = j\} - p(y^{(i)} = j | x^{(i)}; \theta)\right) \right] + \lambda \theta_j \]

  + the function computes the gradients for a single class $j$

  + $\left(\mathbf{1}\{y^{(i)} = j\} - p(y^{(i)} = j | x^{(i)}; \theta)\right)$: evaluate a single value btw 0 and 1

  + multiplied by a vector $x^{(i)}$ to get the weight updates for a single training example $i$ and a single class $j$

+ [Vectorization and dimensional analysis](../ML/MLNN-Hinton/a08-SoftmaxReg.md#gradients)
  + $M$: outputs for all classes and all training examples; dimensions: [numClass x numExamples]
  + $grad$: gradient matrix; dimension: [numClass x input Size]
  + $data$: data matrix; dimension: [inputSize x numExamples]

  \[grad = M * data\]


## Overfitting and Underfitting

### Overview

+ [Overfitting in deep neural networks](../ML/MLNN-Hinton/a14-Advanced.md#4-how-to-address-overfitting)
  + never truly believe that the results from a trained network are optimal
  + very common

+ [Generalization Concern - Overfitting](../ML/MLNN-Hinton/03-Backpropagation.md#how-to-use-the-derivatives-computed-by-the-backpropagation-algorithm)
  + Unable to identify which regularities causing errors
  + Possible solutions:
    + Weight-decay
    + Weight-sharing
    + Early stopping
    + Model averaging
    + Bayesian fitting on neural nets
    + Dropout
    + Generative pre-training

+ [Underfitting](../ML/MLNN-Hinton/a13-HyperParam.md#31-a-review-of-the-underfitting-and-overfitting-trade-off)
  + unable to reduce the error for either the test or training set
  + cause: an under capacity of the machine learning model
  + not powerful enough to fit the underlying complexities of the data distribution

+ [Overfitting](/ML/MLNN-Hinton/a13-HyperParam.md#31-a-review-of-the-underfitting-and-overfitting-trade-off): model so powerful as to fit the training set too well and the generalization error increases

+ Pictorial explanation of the tradeoff between underfitting and overfitting (Fig. 2)
  + model complexity (the x axis) refers to the capacity or powerfulness of the machine learning model
  + the optimal capacity falls between underfitting and overfitting
  + achieving a horizontal test loss during the training of a network can also point to the optimal balance of the hyper-parameter

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://www.arxiv-vanity.com/papers/1803.09820/" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/a13-under-overfitting.png" style="margin: 0.1em;" alt="Pictorial explanation of the tradeoff between underfitting and overfitting." title="Pictorial explanation of the tradeoff between underfitting and overfitting." height=200>
    </a>
  </div>

+ [Insight of underfitting and overfitting](../ML/MLNN-Hinton/a13-HyperParam.md#31-a-review-of-the-underfitting-and-overfitting-trade-off)
  + signs of the underfitting and overfitting of the test or validation loss early in the training process useful for tuning the hyper-parameters
  + Fig. 1a: some overfitting within the black square indicates a suboptimal choice of hyper-parameters
  + well set initial values for hyper-parameters results in performing well through the entire training process
  + the test loss during the training process used to find the optimal network architecture and hyper-parameters w/o performing a full training to compare the final performance results


### Underfitting

+ [Underfitting visible during the training](../ML/MLNN-Hinton/a13-HyperParam.md#32-underfitting)
  + Underfitting is characterized by a continuously decreasing test loss, rather than a horizontal plateau.
  + Test loss for the Cifar-10 dataset with a shallow 3 layer network (left diagram)
    + red curve
      + decreasing test loss w/ a learning rate ($LR = 0.001$)
      + Underfitting: continue to decrease
    + blue curve
      + decreasing more rapidly during the initial iterations and then is horizontal
      + __a positive clue__: the configuration producing a better final accuracy than other configuration
  + Test loss for Imagenet with two networks; resnet-50 and inception-resnet-v2 (right diagram)
    + underfitting: underlying complexities of the data distributions
    + the test loss continues decreasing over the 100,000 iterations (about 3 epochs)
    + the inception-resnet-v2 decreasing more and becoming more horizontal
    + the inception-resnet-v2 less underfitting

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://www.arxiv-vanity.com/papers/1803.09820/" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/a13-3layerLoss.png" style="margin: 0.1em;" alt="(a) Test loss for the Cifar-10 dataset with a shallow 3 layer network." title="Test loss for the Cifar-10 dataset with a shallow 3 layer network." height=150>
      <img src="../ML/MLNN-Hinton/img/a13-imagenetTestLoss3.png" style="margin: 0.1em;" alt="(b) Test loss for Imagenet with two networks; resnet-50 and inception-resnet-v2." title="Test loss for Imagenet with two networks; resnet-50 and inception-resnet-v2." height=150>
    </a>
  </div>


### Overfitting

+ [Examples of overfitting](../ML/MLNN-Hinton/a13-HyperParam.md#33-overfitting)
  + increasing validation/test loss indicates overfitting
  + Cifar-10 dataset with a shallow 3 layer network (left diagram)
    + $WD = 10^{-4}$ (blue curve): minimizing near at $LR = 0.002$, then increasing (overfitting)
    + $WD = 4 \times 10^{-3}$: (red curve)
      + stable at a larger LR range
      + attain a lower loss value
      + better than the previous one
      + diverging at $LR = 0.008$
    + $WD = 10^{-2}$ (yellow curve): sharp increasing at $LR = 0.005$
      + not a sign of overfitting
      + caused by instabilities in the training due to the large learning rate
  + Imagenet dataset with resnet-50 architecture (right diagram)
    + blue curve: underfitting w/ $LR = 0.1$ and $WD = 10^{-4}$
    + red curve: overfittign w/ a ver small $WD = 10^{-7}$

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://www.arxiv-vanity.com/papers/1803.09820/" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/a13-overfitting3.png" style="margin: 0.1em;" alt="(a) Cifar-10 dataset with a shallow 3 layer network." title="Cifar-10 dataset with a shallow 3 layer network." height=150>
      <img src="../ML/MLNN-Hinton/img/a13-imagenetResnetOverfitting.png" style="margin: 0.1em;" alt="(b) Imagenet dataset with resnet-50 architecture." title="Imagenet dataset with resnet-50 architecture." height=150>
    </a>
  </div>

+ [Overfitting](../ML/MLNN-Hinton/09-Overfitting.md#91-overview-of-ways-to-improve-generalization)
  + true and accidental regularities: training data in the mapping from input to output
  + unable to identify the regularities real or caused by sampling error
  + variance
    + fit the model w/ another training set drawn from the same distribution over cases
    + making different predictions on the test data

+ [Preventing overfitting](../ML/MLNN-Hinton/09-Overfitting.md#91-overview-of-ways-to-improve-generalization)
  + Approach 1: get more data!
  + Approach 2: using a model w/ the right capacity
  + Approach 3: average many different models
  + Approach 4: Bayesian

+ [Ways to limit the cpacity of a neural network](../ML/MLNN-Hinton/09-Overfitting.md#91-overview-of-ways-to-improve-generalization)
  + controlling capacity w/
    + <span style="color: blue;">architecture</span>: limit the number of hidden layers and the number of units per layer
    + <span style="color: blue;">early stopping</span>: start w/ small weights and stop the learning before it overfits
    + <span style="color: blue;">weight-decay</span>:
      + given model a number of hidden layers or units per layer which is a little too large
      + penalize large weights using penalties or constrains on their squared values (L2 penalty) or absolute values (L1 penalty)
    + <span style="color: blue;">noise</span>: add to the weights of the activities
  + typically, using a combinaition of several of these methods

+ [Overfitting: a frequentist illusion?](../ML/MLNN-Hinton/10-CombineDropout.md#103-the-idea-of-full-bayesian-learning)
  + overfitting: fit a complicated model to a small amount of data
  + result of not bothering to get the full posterior distribution over the parameters
  + not much data
    + using simple model than complex one to prevent overfitting
    + only if assume that fitting a model means choosing a single best setting of the parameters
    + using full posterior distribution over parameter setting $\implies$ overfitting disappear
  + little data
    + very vague predictions
    + many different parameter settings have significant posterior probabilities
  + more and more data:
    + posterior probability will get more and more focused on a few settings of parameters
    + posterior prediction will get much shaper


### Meta Parameters

+ [Meta parameters to control capacity](..(../ML/MLNN-Hinton/09-Overfitting.md#91-overview-of-ways-to-improve-generalization))
  + meta parameters: the number of hidden units, the number of layers, or the size of the weight penalty
  + wrong: trying lots of alternatives and choosing the one w/ the best performance on the test set

+ [Cross-validation](../ML/MLNN-Hinton/09-Overfitting.md#91-overview-of-ways-to-improve-generalization)
  + a better way to choose meta parameters
  + divide the total dataset into 3 subsets
    + <span style="color: red;">training data</span>: used for learning the parameters of the model
    + <span style="color: red;">validation data</span>: not for learning but for deciding what settings of the meta parameters work best
    + <span style="color: red;">test data</span>: used to get a final, unbiased estimate of how well the network works
  + N-fold cross-validation
    + divide the total dataset into one final test set and $N$ other subsets
    + train on all but one of those subsets to get $N$ different estimates of the validation error rate
    + the $N$ estimates not independent


### Combined Models

+ [Combining networks: the bias-variance trade-off](../ML/MLNN-Hinton/10-CombineDropout.md#101-why-it-helps-to-combine-models)
  + limited amount of training data $\implies$ overfitting
  + regression: squared error = "bias" term + "variance" term
    + high bias: model w/ too little capacity to fit the data
    + big variance: so much capacity that it is good at fitting the sampling error in each particular training set
  + using high variance and high capacity (typically w/ low bias) models to average out the variance

+ [Combined predictor vs individual predictors](../ML/MLNN-Hinton/10-CombineDropout.md#101-why-it-helps-to-combine-models)
  + on any one test case, some individual predictors may be better than the combined predictor
  + individual predictors <span style="color: red;">disagree</span> significantly
    + combined predictor typically better than all of the individual predictors when averaging over test cases
    + usage: trying to make the individual predictors disagree but w/o making them much worse individually

+ [Combining network reduces variance](../ML/MLNN-Hinton/10-CombineDropout.md#101-why-it-helps-to-combine-models)
  + compare two expected squared errors
    + randomly pick a predictor to make prediction
    + average all the predictors: $i$ as an index over the $N$ models, $<\;>$ as expection

      \[ \overline{y} = \;<y_i>_i \;=\; \frac{1}{N} \sum_{i=1}^{N} y_i \]

  + expected squared errors

    \[<(t-y_i)^2>_i =  (t - \overline{y})^2 + \underbrace{<(y_i - \overline{y})^2>_i}_{\text{variance of }y_i} -2 \; (t - \overline{y}) \underbrace{\;<(y_i - \overline{y})_i>_i}_{=0} \]

+ [Discrete distributions over class labels](../ML/MLNN-Hinton/10-CombineDropout.md#101-why-it-helps-to-combine-models)
  + Assumption:
    + one model gives the correct label probability $p_i$
    + the other model gives the correct probability $p_j$
  + which better way: randomly pick one model or averaging two probabilities?

    \[ \log \left( \frac{p_i + p_j}{2} \right) \geq \frac{\log p_i + \log p_j}{2} \]

  + the average of $p_i$ and $p_j$ (middle point of gold line) below the blue dot due to log probability

+ [Overview of ways to make predictors differ](../ML/MLNN-Hinton/10-CombineDropout.md#101-why-it-helps-to-combine-models)
  + rely on the learning algorithm getting stuck in different local optima $\implies$ a dubious hack (but worth to try)
  + using different non-neural network models
Backpro    + decision trees
    + Gaussian process models
    + support vector machines
    + others
  + neural network models
    + different numbers of hidden layers
    + different numbers of units per layer
    + different types of unit, e.g., rectified linear units and logistic units
    + different types or strengths of weight penalty; e.g., early stopping, L2 penalty, and L1 penalty
    + different learning algorithms; e.g., full bach and mini-batch

+ [Making models different by changing the training data](../ML/MLNN-Hinton/10-CombineDropout.md#101-why-it-helps-to-combine-models)
  + Bagging
    + train different models on different subsets of the data
    + get different training sets by using sampling w/ replacement; e.g., $a, b, c, d, e \to a \, c \, c \, d \, d$
    + random forest: using lots of different decision trees trained using bagging (better result)
    + able to use w/ neural networks but very expensive; e.g., 20 neural nets $\implies$ 20 training and 20 testing
  + Boosting
    + train a sequence of low capacity models w/ the whole training set
    + weight the training cases differently for each model in the sequence
      + boosting up-weights cases w/ previous models got wrong
      + boosting down-weight cases w/ previous cases got right
    + use resources to try and deal w/ wrong models


### Mixture of Experts

+ [Purpose of mixtures of experts](../ML/MLNN-Hinton/10-CombineDropout.md#102-mixtures-of-experts)
  + Better way than just averaging models
    + possible: looking at the input data for a particular case to help decide which model to rely on
    + allowing particular models to specialize in a subset of the training cases
    + not learn on cases for which they are not picked $\implies$ ignore stuff not good at modeling
    + individual model might be very good at something and very bad at other things
  + key idea
    + make each model or expert focus on predicting the right answer
    + the cases w/ right answer where it is already doing better than the other experts
    + causing specialization

+ [A spectrum of models](../ML/MLNN-Hinton/10-CombineDropout.md#102-mixtures-of-experts)
  + Very local model: predict $y$ from $x$ $\implies$ simply find the stored value of $x$ closest to the test value of $x$ to predict the $y$
  + Fully global models
    + may be slow to fit and also unstable
    + small changes to data can cause big changes to the fit
    + each parameter depends on all the data

+ [Multiple local models](../ML/MLNN-Hinton/10-CombineDropout.md#102-mixtures-of-experts)
  + in between the very local & fully global models
  + using several models of intermediate complexity than using a single global model or lots of very local models
  + how to partition the dataset into different regimes?

+ [Datset partitioning](../ML/MLNN-Hinton/10-CombineDropout.md#102-mixtures-of-experts)
  + ways: based on input vs. based on the input-output relationship
  + cluster the training cases into subsets
  + one for each local model
  + aim of the clustering:
    + Not to find clusters of similar input vectors
    + each cluster to have a relationship btw input and output that can be well-modeled by one local model

+ [Cooperation and Specialization](../ML/MLNN-Hinton/10-CombineDropout.md#102-mixtures-of-experts)
  + error function encouraging cooperation
    + compare the average to all the predictors w/ the target
    + train all the predictors together to reduce the discrepancy btw the target and the average
    + overfit badly: making the model much more powerful than training each predictor separately

      \[ E = (t - \underbrace{<y_i>_i}_{\text{average of all}\\ \text{the predictor}})^2 \]

  + error function encouraging specialization
    + compare each predictor separately w/ the target
    + use a "manager" to determine the probability of picking each expert
    + most experts end up ignoring most targets

      \[ E = <p_i \cdot (t-y_i)^2> \]

      + $p_i$: probability of the manager picking expert $i$ for this case
  
+ [The mixture of experts architecture (almost)](../ML/MLNN-Hinton/10-CombineDropout.md#102-mixtures-of-experts)
  + different experts (the right hand side) making their own predictions based on the input
  + the manager (the left hand side)
    + multiple layers
    + the last layer: softmax
    + output: probabilities for the experts
  + using output of manager and experts to compute the value of the error function

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="http://www.cs.toronto.edu/~hinton/coursera/lecture10/lec10.pptx" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/m10-07.png" style="margin: 0.1em;" alt="Architecture for mixture of experts" title="Architecture for mixture of experts" width=350>
    </a>
  </div>

+ [The derivatives of the simple cost function](../ML/MLNN-Hinton/10-CombineDropout.md#102-mixtures-of-experts)
  + differentiate w.r.t. the outputs of the experts: a signal for training each expert
  + differentiate w.r.t. the outputs of the gating network
    + a signal for training the gating network
    + as differentiate w.r.t. the quantity entering the softmax
    + raise $p$ for all experts that give less than the average squared error of all the experts (weighted by $p$)
  + math representation

    \[ p_i = \frac{e^{x_i}}{\sum_j e^{x_j}}, \qquad\qquad E = \sum_i p_i \cdot (t-y_i)^2 \]

    \[ \frac{\partial E}{\partial y_i} = p_i \cdot (t-y_i) \qquad\qquad \frac{\partial E}{\partial x_i} = p_i \cdot \left( (t-y_i)^2 - E \right) \]

+ [A better cost function for mixtures of experts](../ML/MLNN-Hinton/10-CombineDropout.md#102-mixtures-of-experts)
  + each expert making a prediction w/ a Gaussian distribution around its output (w/ variance 1)
  + the manager:
    + deciding on a scale for each of these Gaussian
    + the scale called a "mixing proportion"
    + predictive distribution of mixture of expert: no longer Gaussian after summing of scaled down read Gaussian and scaled down green Gaussian
  + maximize the log probability of the target value under this mixture of Gaussian model; i.e., the sum of the two scaled Gaussian

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="http://www.cs.toronto.edu/~hinton/coursera/lecture10/lec10.pptx" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/m10-08.png" style="margin: 0.1em;" alt="Gaussian distributions of two models" title="Gaussian distributions of two models" width=350>
    </a>
  </div>

  + the probability of the target under a mixture of Gaussian

    \[ p(t^c | MoE) = \sum_i p_i^c \cdot \frac{1}{\sqrt{2\pi}} \exp \left(-\frac{1}{2} (t^c - y_i^c)^2 \right) \]

    + $p(t^c | MoE)$: prob. of target value on case $c$ given the mixture
    + $p_i^c$: mixing proportion assigned to expert $i$ for case $c$ by the gating network
    + $y_i^c$: output of expert $i$
    + $1/\sqrt{2 \pi}$: normoralization term for a Gaussian w/ $\sigma^2 = 1$


### Early Stopping

+ [Early stopping](../ML/MLNN-Hinton/09-Overfitting.md#91-overview-of-ways-to-improve-generalization)
  + goal: preventing overfitting
  + expensive: training w/ different sized penalities on the weights of different architectures
  + Procedure:
    + start w/ very small weights
    + grow the weights until the performance on the validation set starts getting worse
  + issues:
    + hard to decide when the performance getting worse
    + limited capacity of the model

+ [Why early stopping works](../ML/MLNN-Hinton/09-Overfitting.md#91-overview-of-ways-to-improve-generalization)
  + very small weights
    + every hidden unit in its linear range
    + even w/ a large layer of hidden units
    + no more capacity than a linear net (inputs directly connected to outputs)
  + as weights grow
    + hidden units start using the non-linear ranges
    + capacity grows


### Weight Decay

+ [Weight decay](../ML/MLNN-Hinton/a13-HyperParam.md#44-weight-decay)
  + a form of regularization
  + balancing the various forms of regularization to obtain good performance
  + best practice: remaining constant through the training
  + generally applied for regularization
  + network performance: proper weight decay value
  + the validation loss early in the training: sufficient for determining a good value
  + reasonable procedure: combined CLR and CM runs at a few values of the weight decay to simultaneously determine the best learning rates, momentum and weight decay

+ [Weight decay values](../ML/MLNN-Hinton/a13-HyperParam.md#44-weight-decay)
  + reasonable values: $10^{-3}, 10^{-4}, 10^{-5}$ and $0$
  + smaller datasets and architectures: larger values for weight decay
  + larger datasets and deeper architectures: smaller values
  + hypothesis: complex data provides its own regularization and other regularization should be reduced
  + experience: $10^{-4}$ about right w/ initial runs at $3 \times 10^{-5}, 10^{-4}, 3 \times 10^{-4}$
  + bisection of the exponent rather than bisecting the value ($10^{-3.5} = 3.16 \times 10^{-4}$)
  + make a follow up run that bisects the exponent of the best two of these if none seem best, extrapolate toward an improved value

+ Examples of weight decay search using a 3-layer network on the Cifar-10 dataset
  + Training used a constant learning rate (0.005) and constant momentum (0.95).
  + The best value for weight decay is easier to interpret from the loss than from the accuracy.

+ More examples of weight decay search using a 3-layer network on the Cifar-10 dataset
  + Training used cyclical learning rates (0.001 - 0.01) and cyclical momentum (0.98 - 0.9).
  + The best value of weight decay is smaller when using CLR because the larger learning rates help with regularization.

+ [Grid search for weight decay (WD) on Cifar-10 with resnet-56 and a constant momentum=0.95 and TBS = 1,030](../ML/MLNN-Hinton/a13-HyperParam.md#44-weight-decay)
  + The optimal weight decay is different if you search with a constant learning rate (left) versus using a learning rate range (right) due to the regularization by large learning rates.
  + different optimal weight decay: a constat learning rate vs. a learning rate range
  + the larger learning rates provide regularization so a smaller weight decay value is optimal

+ [Grid search for the optimal WD restarting from a snapshot](../ML/MLNN-Hinton/a13-HyperParam.md#44-weight-decay)
  + a grid search for a weight decay to make a single run at a middle value for weight decay and save a snapshot after the loss plateau
  + using the snapshot to restart runs w/ different WD values

+ [Weight decay](../ML/MLNN-Hinton/09-Overfitting.md#92-limiting-size-of-the-weights)
  + the standard L2 weight penalty
    + the derivative of the penalty acts as a force pulling weight towards to zero
    + adding an extra term to the cost function that penalizes the squared weights
  + cost function: optimize by reducing the normal error

    \[\begin{align*} 
      C &= E + \frac{\lambda}{2} \sum_i w_i^2 \\
      \frac{\partial C}{\partial w_i} &= \frac{\partial E}{\partial w_i} + \lambda w_i
    \end{align*}\]

    + $\frac{\partial C}{\partial w_i} = 0 \implies w_i = - \frac{1}{\lambda} \frac{\partial E}{\partial w_i}$
    + big weights $\impliedby$ minimum of the cost function $\iff$ maximum error derivatives

+ [The effect of L2 weight cost](../ML/MLNN-Hinton/09-Overfitting.md#92-limiting-size-of-the-weights)
  + prevent the network from using weights not needed
  + prefer to equally divide the weight on each branch

+ [Weight penalities vs weight constraints](../ML/MLNN-Hinton/09-Overfitting.md#92-limiting-size-of-the-weights)
  + penalities: usually penalize the squared value of each weight separately
  + constraint on the maximum squared length of the incoming weight vector of each hidden or output unit
  + advantages of weight constraints over weight penalities
    + easier to set a sensible value
    + preventing hidden units getting stuck near zero
    + prevent weights exploding
  + the effectiveness of weight penalty determined by the big gradients
    + more effective than a fixed penalty at pushing irrelevant weights towards zero
    + the penalty just the Lagrange multipliers required to keep the constraints satisfied


### Adding Noise

+ [L2 weight-decay via noisy input](../ML/MLNN-Hinton/09-Overfitting.md#93-using-noise-as-a-regularizer)
  + Adding Gaussian noise to the inputs
  + linear network $\implies$ amplified noise simply adds to the output
  + minimizing the squared error tends to minimize the squared weights when the inputs are noisy
  + expected squared difference between $y^{noise}$ and target value $t$

    \[E[(y^{noise} - t)^2] = (y-t)^2 + \sum_i w_i^2 \sigma_i^2 \]

    $\therefore \sigma_i^2 \equiv$ an L2 penalty

+ [Noisy weights in complex nets](../ML/MLNN-Hinton/09-Overfitting.md#93-using-noise-as-a-regularizer)
  + adding Gaussian noise to the weights of a multilayer non-linear architecture
  + not exactly equivalent to using an L2 weight penalty

+ [Using noise in the activities as a regularizer](../ML/MLNN-Hinton/09-Overfitting.md#93-using-noise-as-a-regularizer)
  + using backpropagation to train a multilayer NN composed of logistic units
  + logistic function
    + treat a logistic unit in the forward pass as if a stochastic binary neuron
    + the forward pass makes a random decision wether to "1" or "0" using the probability
    + for backward pass, using the real value $p$ for backpropagating derivatives through the hidden unit
  + Characteristics:
    + worse on the training set
    + considerably slower
    + significantly better on the test set


### Dropout

+ [Dropout](../ML/MLNN-Hinton/a14-Advanced.md#5-dropout)
  + easy to implement but more difficult to grasp its underlying philosophy
  + a regularization technique for deep neural networks
  + employed at training time
    + eliminated the dropout od some units randomly
    + preventing the network from relying on individual neurons too much
    + preventing from overfitting
  + testing time
    + all neurons presented
    + firing probability scaled
    + more neurons than previously present at training time

+ [Dropout technique](../ML/MLNN-Hinton/a14-Advanced.md#5-dropout)
  + used in combination with other regularization techniques (such as L2, batch normalization, etc.)
  + Purpose: prevent the co-adaption of feature detectors for a set of neurons, and avoid overfitting
    + enforcing the neurons to develop an individual role on their own given an overall population behavior
    + training weights encouraged to be spread across the neural network because no neuron is permanent
  + Interpretation: training examples provide gradients from different, randomly sampled architectures
  + direct implementation
    + at training time: eliminate the output of some units randomly
    + at test time: all units are present

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://towardsdatascience.com/advanced-topics-in-neural-networks-f27fbcc638ae" ismap target="_blank">
      <img src="https://miro.medium.com/max/1375/1*J_l09l2Fo4k5EHwUSRenQA.png" style="margin: 0.1em;" alt="Example of applying dropout" title="Example of applying dropout" height=150>
      <img src="https://miro.medium.com/max/1395/1*pBncBWIkmogWIQ_6AhWCeQ.png" style="margin: 0.1em;" alt="Implement of dropout at training and test times" title="Implement of dropout at training and test times" height=100>
    </a>
  </div>

+ [Two ways to average models](../ML/MLNN-Hinton/10-CombineDropout.md#105-dropout-an-efficient-way-to-combine-neural-nets)
  + Mixture: combine models by averaging their output probabilities
  + Product: combine models by taking geometric means of their output probabilities

+ [Dropout](../ML/MLNN-Hinton/10-CombineDropout.md#105-dropout-an-efficient-way-to-combine-neural-nets)
  + an efficient way to average many large neural nets
  + consider a neural net w/ one hidden layer
  + randomly omit each hidden unit w/ probability $0.5$ for a training example
  + randomly sampling from $2^H$ different architectures where $H$ as the number of hidden units
  + all architectures share weights: a hidden unit uses the same weights as it has in other architectures
  + a form of model averaging
    + sample from $2^H$ models
      + only a few of the models ever get trained
      + only get one training example when selected
      + as extreme form of bagging
    + sharing weights with other models
      + every model is very strongly regularized by the others
      + much better than L2 and L1 penalities that pull the weights towards zero
      + regularized by something that tends to pull the weights towards the correct value

+ [Testing](../ML/MLNN-Hinton/10-CombineDropout.md#105-dropout-an-efficient-way-to-combine-neural-nets)
  + naive method:
    + sample many different architectures
    + take the geometric mean of their output distribution
  + efficient method
    + use all of the hidden units but to halve their outgoing weights $\implies$ the same expected effect as they did when we were sampling
    + using all of the hidden units w/ half of their outgoing weights
    + exactly compute the geometric mean of the predictions of all $2^H$ models
    + using a softmax output group

+ [Multiple hidden layers](../ML/MLNN-Hinton/10-CombineDropout.md#105-dropout-an-efficient-way-to-combine-neural-nets)
  + use dropout of $0.5$ in every layer
  + testing: use the "mean net" that has all the outgoing weights halved
  + stochastic model w/ dropout:
    + run the stochastic model several times on the same input
    + average across those stochastic models
    + provide an idea of the uncertainty in the answer

+ [Input layer](../ML/MLNN-Hinton/10-CombineDropout.md#105-dropout-an-efficient-way-to-combine-neural-nets)
  + use dropout too but w/ a higher probability of keeping an input unit
  + used by the "denoising autoencoders"

+ [How well dropout work](../ML/MLNN-Hinton/10-CombineDropout.md#105-dropout-an-efficient-way-to-combine-neural-nets)
  + usually reduce the number of errors significantly w/ significantly overfitting deep neural net
    + "early dropping" do better than "dropout"
    + cost: longer training time and might be more hidden units
  + deep neural net w/o overfitting:
    + using a bigger one
    + using dropout that's assuming enough computational power

+ [Viewpoint of Cooperation and Specialization](../ML/MLNN-Hinton/10-CombineDropout.md#105-dropout-an-efficient-way-to-combine-neural-nets)
  + related to mixtures of experts
  + a hidden unit knows which other hidden units present
    + co-adapt to them on the training data
    + big, complex conspiracies not robust
    + better w/ conspiracies to have lots of little conspiracies
  + a hidden unit work well w/ combinatorially many sets of co-works


### Inverted Dropout

+ [Dropout usage](../ML/MLNN-Hinton/a14-Advanced.md#51-inverted-dropout)
  + normal dropout
    + scale activations by dropout rate $p$ at test time
    + not dropping out any of the neurons
    + required to match expected value at training
  + inverted dropout
    + scaling applied at training time, but inversely
    + dropout all activations by dropout factor $p$
    + scaling by inverse dropout factor $1/p$

+ [Inverted dropout](../ML/MLNN-Hinton/a14-Advanced.md#51-inverted-dropout)
  + advantage: don't have to do anything at test time to make inference faster
  + most current implementations
    + weighting performed during training
    + no re-weighting at test time required
  + for layer $l$

    \[\begin{align*}
      z^{[l]} &= \frac{1}{p_l} W^{[l]} D^{[l]} a^{[a-1]} + b^{[l]} \\
      a^{[l]} &= g(z^{[l]}) 
    \end{align*}\]

    + $p_l$: retention probability
    + $D^{[l]}$: dropout activations
    + $a^{[l-1]}$: output from previous layer
    + $W^{[l]}$: layer weights
    + $b^{[l]}$: offset weights
    + $z^{[l]}$: linear output
    + $g(\cdot)$: nonlinear activation function

    <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
      <a href="https://towardsdatascience.com/advanced-topics-in-neural-networks-f27fbcc638ae" ismap target="_blank">
        <img src="https://miro.medium.com/max/618/1*CAcPwIHBS_-8Ms4ZqlnbFA.png" style="margin: 0.1em;" alt="Inverted dropout — weights are scaled at training time as opposed to testing time, the opposite of traditional dropout." title="Inverted dropout" width=150>
      </a>
    </div>


## Applications

### Family Tree - Multiclass Learning

+ [Family tree](../ML/MLNN-Hinton/04-Multiclasses.md#learning-to-predict-the-next-word)
  + Q: Figuring out the regularities from given family trees
  + Block - local encoding of person 1: 24 people: 12 British & 12 Italian
  + Block - local encoding of relationship: 12 relationships
  + Block - Distributed encoding of person 1: 6 big gray boxes
  + Observe the patterns from the right diagram
    + top right unit (big grey block): nationality
    + 2nd right block: generation
    + left bottom block: branches of family tree
  + features: only useful if the other bottlenecks use similar representations
  + Generalization: able to complete those triples correctly?
    + trained with 108 triples instead of 112 triples
    + Validate on the 4 held-out cases
  + (A r B): A has a relationship r with B
    + predict 3rd term (B) from the first two terms (A & r)
    + using the trained net to find very unlikely triples

<div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
  <a href="http://www.cs.toronto.edu/~hinton/coursera/lecture4/lec4.pptx" ismap target="_blank">
    <img src="../ML/MLNN-Hinton/img/m04-01.png" style="margin: 0.1em;" alt="Example of family trees" title="Example of family trees" height=130>
    <img src="../ML/MLNN-Hinton/img/m04-02.png" style="margin: 0.1em;" alt="The structure of neural network to search symbolic rules" title="The structure of neural network to search symbolic rules" height=130>
    <img src="../ML/MLNN-Hinton/img/m04-03.png" style="margin: 0.1em;" alt="The example to search symbolic rules" title="The example to search symbolic rules" height=130>
  </a>
</div>


### Speech Recognition

+ A basic problem in speech recognition
  + Not able to identify phonemes perfectly in noisy speech
  + Ambiguous acoustic input: several different words fitting the acoustic signal equally well
  + Human using their understanding of the meaning of the utterance to hear the right words
  + knowing which words are likely to come next and which are not in speech recognition

+ [The standard Trigram method](../ML/MLNN-Hinton/04-Multiclasses.md#neuro-probabilistic-language-models)
  + Gather a huge amount of text and count the frequencies of all triples or words
  + Use the formula to bet the relative probabilities of words with the two previous words

    \[\frac{p(w_3 = c | w_2 = b, w_1 = a)}{p(w_3 = d | w_2 =b, w_1 = a)} = \frac{\text{count}(abc)}{\text{count}(abd)}\]

  + The state-of-the-art methodology recently
  + drawback: not understand similarity btw words

+ [Bengio's neural net](../ML/MLNN-Hinton/04-Multiclasses.md#neuro-probabilistic-language-models)

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="url" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/m04-04.png" style="margin: 0.1em;" alt="Bengio's neural net for predicting the next word" title="Bengio's neural net for predicting the next word" width=350>
    </a>
  </div>

  + similar to family tree problem but larger scale
  + Typical 5 previous words used but shown 2 in the diagram
  + Using distributed representations via hidden layers to predict via huge softmax to get probabilities for all various words might coming next
  + refinement:
    + skip layer connection to skip from input to output
    + input words individually informative about what the word might be
  + A problem w/ a very large vector of weights
    + unnecessary duplicates: plural of a word and tenses of verbs
    + each unit in the last hidden layer w/ 100,000 outgoing weights

+ [A serial architecture](../ML/MLNN-Hinton/04-Multiclasses.md#dealing-with-large-number-of-possible-outputs)

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="http://www.cs.toronto.edu/~hinton/coursera/lecture4/lec4.pptx" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/m04-05.png" style="margin: 0.1em;" alt="A serial architecture for speech recognition" title="A serial architecture for speech recognition" width=350>
    </a>
  </div>

  + adding an extra input as candidate for the next word same as the context word
  + output: score for how good the candidate in the context
  + execute the net many times but most of them only one required

+ [Structure words as a tree](../ML/MLNN-Hinton/04-Multiclasses.md#dealing-with-large-number-of-possible-outputs) (Minih and Hinton, 2009)
  + predicting a path through a binary tree
  + arranging all the words in a binary tree with words as the leaves
  + using the previous context to generate a __prediction vector__, $v$

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="url" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/m04-07.png" style="margin: 0.1em;" alt="Neural network architecture for speech recognition" title="Neural network architecture for speech recognition" height=150>
      <img src="../ML/MLNN-Hinton/img/m04-08.png" style="margin: 0.1em;" alt="The path for word searching with computed probabilities" title="The path for word searching with computed probabilities" height=150>
    </a>
  </div>

  + $\sigma$: the logistic function
  + using contexts to learn a prediction vector with the neural net
  + the prediction vector compared with the vectors learned for all the nodes on the path to the correct next word
  + take the path with high sum of their log probabilities: take the higher probability on each node

  + A convenient decomposition
    + maximizing the log probability of picking the target word: $\mathcal{O}(\log(N))$
    + Still slow at test time though a few hundred times faster


### A Unified Architecture for Natural Language Processing

+ Collobert and Weston, [A unified architecture for natural language processing: deep neural networks with multitask learning](https://ronan.collobert.com/pub/matos/2008_nlp_icml.pdf), ICML'08, 2008
  + learned feature vectors for words
  + applied to many different natural language processing tasks well
  + not try to predict the next word but good feature vectors for words
  + use both the past and future contexts
  + observe a window with 11 words, 5 in the past and 5 in the future
  + the middle word either the correct word actually occurred in the text or a random word
  + train the neural net to produce the output
    + high probability: correct word
    + low probability: random word
  + map the individual words to feature vectors
  + use the feature vectors in the neural net (possible many hidden layers) to predict whether the word correct or not

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="http://www.cs.toronto.edu/~hinton/coursera/lecture4/lec4.pptx" ismap target="_blank">
      <img src="../ML/MLNN-Hinton/img/m04-09.png" style="margin: 0.1em;" alt="Neural network architecture for feature vectors learning (Collobert & Weston, 2008)" title="Neural network architecture for feature vectors learning (Collobert & Weston, 2008)" height=150>
    </a>
  </div>

+ [2D map to display the learned feature vectors](../ML/MLNN-Hinton/04-Multiclasses.md#dealing-with-large-number-of-possible-outputs)
  + get idea of the quality of the learned feature vectors
  + display similar vectors close to each other
  + T-SNE: a multi-scale method to display similarity at different scale

+ [Checking strings of words](../ML/MLNN-Hinton/04-Multiclasses.md#dealing-with-large-number-of-possible-outputs)
  + learned feature vectors capturing lots of subtle semantic distinctions
  + no extra supervision required
  + information of all words in the context

