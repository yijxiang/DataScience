# Neural Networks for Machine Learning

## 01. Introduction to Machine Learning

+ [Why do we need machine learning](01-IntroML.md#why-do-we-need-machine-learning)
+ [What are neural networks](01-IntroML.md#what-are-neural-networks)
+ [Some simple models of neurons](01-IntroML.md#some-simple-models-of-neurons)
+ [A simple example of learning](01-IntroML.md#a-simple-example-of-learning)
+ [Three types of learning](01-IntroML.md#three-types-of-learning)

## 02. Perceptron Learning Procedure

+ [An overview of the main types of network architecture](02-Perceprtons.md#an-overview-of-the-main-types-of-network-architecture)
+ [Perceptrons](02-Perceprtons.md#perceptrons-the-first-generation-of-neural-networks)
+ [A geometrical view of perceptrons](02-Perceprtons.md#a-geometrical-view-of-perceptrons)
+ [Why the learning works](02-Perceprtons.md#why-the-learning-works)
+ [What perceptrons can not do](02-Perceprtons.md#what-perceptrons-can-not-do)


## 03. Backpropagation Learning Procedure
  
+ [Learning the weights of a linear neuron](03-Backpropagation.md#learning-the-weights-of-a-linear-neuron)
+ [The error surface for a linear neuron](03-Backpropagation.md#the-error-surface-for-a-linear-neuron)
+ [Learning the weights of a logistic output neuron](03-Backpropagation.md#learning-the-weights-of-a-logistic-output-neuron)
+ [The backpropagation algorithm](03-Backpropagation.md#the-backpropagation-algorithm)
+ [How to use the derivatives computed by the backpropagation algorithm](03-Backpropagation.md#how-to-use-the-derivatives-computed-by-the-backpropagation-algorithm)


## 04. Multiclasses Machine Learning

+ [Learning to predict the next word](04-Multiclasses.md#learning-to-predict-the-next-word)
+ [A brief diversion into cognitive science](04-Multiclasses.md#a-brief-diversion-into-cognitive-science)
+ [Another diversion_The softmax output function](04-Multiclasses.md#another-diversion-the-softmax-output-function)
+ [Neuro-probabilistic language models](04-Multiclasses.md#neuro-probabilistic-language-models)
+ [ways to deal with large number of possible outputs](04-Multiclasses.md#dealing-with-large-number-of-possible-outputs)


## 05. Convolutional Neural Networks

+ [Why object recognition is difficult](05-CNN.md#why-object-recognition-is-difficult)
+ [Ways to achieve viewpoint invariance](05-CNN.md#ways-to-achieve-viewpoint-invariance)
+ [Convolutional neural networks for hand-written digit recognition](05-CNN.md#convolutional-neural-networks-for-hand-written-digit-recognition)
+ [Convolutional neural networks for object recognition](05-CNN.md#convolutional-neural-networks-for-object-recognition)


## 06. Mini-batch Gradient Descent

+ [Overview of mini-batch gradient descent](06-MiniBatch.md#overview-of-mini-batch-gradient-descent)
+ [A bag of tricks for mini-batch descent](06-MiniBatch.md#a-bag-of-tricks-for-mini-batch-descent)
+ [The momentum method](06-MiniBatch.md#the-momentum-methodadaptive-learning-rate-for-each-connection)
+ [Adaptive learning rate for each connection](06-MiniBatch.md#)
+ [rmsprop: Normalized the gradient](06-MiniBatch.md#rmsprop-normalized-the-gradient)


## 07. Recurrent Neural Networks

+ [Modeling sequences: A brief overview](07-RNN.md#71-modeling-sequences-a-brief-overview)
+ [Training RNNs with backpropagation](07-RNN.md#72-training-rnns-with-backpropagation)
+ [A toy example of training an RNN](07-RNN.md#73-a-toy-example-of-training-an-rnn)
+ [Why it is difficult to train an RNN](07-RNN.md#74-why-it-is-difficult-to-train-an-rnn)
+ [Long term short term memory](07-RNN.md#75-long-short-term-memory)


## 08. Multicaptive Connections
  
+ [A brief overview of Hessian-free optimization](08-RNN2.md#81-a-brief-overview-of-hessian-free-optimization)
+ [Modeling character strings with multiplicative connections](08-RNN2.md#82-modeling-character-strings-with-multiplicative-connections)
+ [Learning to predict the next character using HF](08-RNN2.md#83-learning-to-predict-the-next-character-using-hf)
+ [Echo state networks](08-RNN2.md#84-echo-state-networks)


## 09. Overfitting
  
+ [Overview of ways to improve generalization](09-Overfitting.md#91-overview-of-ways-to-improve-generalization)
+ [Limiting size of the weights](09-Overfitting.md#92-limiting-size-of-the-weights)
+ [Using noise as a regularizer](09-Overfitting.md#93-using-noise-as-a-regularizer)
+ [Introduction to the Bayesian approach](09-Overfitting.md#94-introduction-to-the-bayesian-approach)
+ [The Bayesian interpretation of weight decay](09-Overfitting.md#95-the-bayesian-interpretation-of-weight-decay)
+ [MacKays quick and dirty method of fixing weight costs](09-Overfitting.md#96-mackays-quick-and-dirty-method-of-fixing-weight-costs)


## 10. Model Combination and Dropouts
  
+ [Why it helps to combine models](10-CombineDropout.md#101-why-it-helps-to-combine-models)
+ [Mixtures of experts](10-CombineDropout.md#102-mixtures-of-experts)
+ [The idea of full bayesian learning](10-CombineDropout.md#103-the-idea-of-full-bayesian-learning)
+ [Making full bayesian learning practical](10-CombineDropout.md#104-making-full-bayesian-learning-practical)
+ [Dropout an efficient way to combine neural nets](10-CombineDropout.md#105-dropout-an-efficient-way-to-combine-neural-nets)


## 11. Hopfield Nets and Boltzmann Machines

+ [Hopfield Nets](11-Hopfield.md#111-hopfield-nets)
+ [Dealing with spurious minima in Hopfield nets](11-Hopfield.md#112-dealing-with-spurious-minima-in-hopfield-nets)
+ [Hopfields Nets with hidden units](11-Hopfield.md#113-hopfields-nets-with-hidden-units)
+ [Using stochastic units to improve search](11-Hopfield.md#114-using-stochastic-units-to-improve-search)
+ [How a Boltzmann machine models data](11-Hopfield.md#115-how-a-boltzmann-machine-models-data)


## 12. Restricted Boltzmann Machine (RBMs)

+ [The Boltzmann machine learning algorithm](12-Boltzmann.md#121-the-boltzmann-machine-learning-algorithm)
+ [More efficient ways to get the statistics](12-Boltzmann.md#122-more-efficient-ways-to-get-the-statistics)
+ [Restricted Boltzmann machines](12-Boltzmann.md#123-restricted-boltzmann-machines)
+ [An example of contrastive divergence learning](12-Boltzmann.md#124-an-example-of-contrastive-divergence-learning)
+ [RBMs for collaborative filtering](12-Boltzmann.md#125-rbms-for-collaborative-filtering)


## 13. Deep Belief Nets

+ [The ups and downs of backpropagation](13-BeliefNets.md#131-the-ups-and-downs-of-backpropagation)
+ [Belief nets](13-BeliefNets.md#132-belief-networks)
+ [Learning Sigmoid Belief Nets](13-BeliefNets.md#133-learning-sigmoid-belief-nets)
+ [The wake-sleep algorithm](13-BeliefNets.md#134-the-wake-sleep-algorithm)


## 14. Deep Belief Networks and Restricted Boltzmann Machine
  
+ [Learning layers of features by stacking RBMs](14-DBNsRBM.md#141-learning-layers-of-features-by-stacking-rbms)
+ [Discriminative fine-tuning for DBNs](14-DBNsRBM.md#142-discriminative-fine-tuning-for-dbns)
+ [What happens during discriminative fine-tuning?](14-DBNsRBM.md#143-what-happens-during-discriminative-fine-tuning)
+ [Modeling real-valued data with an RBM](14-DBNsRBM.md#144-modeling-real-valued-data-with-an-rbm)
+ [RBMs are infinite sigmoid belief nets](14-DBNsRBM.md#145-rbms-are-infinite-sigmoid-belief-nets)


## 15. Hierarchical Structure with Neural Networks

+ [From principal components analysis to autoencoders](15-Hierarchy.md#151-from-principal-components-analysis-to-autoencoders)
+ [Deep Autoencoders](15-Hierarchy.md#152-deep-autoencoders)
+ [Deep autoencoders for document retrieval and visualization](15-Hierarchy.md#153-deep-autoencoders-for-document-retrieval-and-visualization)
+ [Semantic hashing](15-Hierarchy.md#154-semantic-hashing)
+ [Learning binary codes for image retrieval](15-Hierarchy.md#155-learning-binary-codes-for-image-retrieval)
+ [Shallow autoencoders for pre-training](15-Hierarchy.md#156-shallow-autoencoders-for-pre-training)


## 16. Deep Neural Networks
  
+ [Learning a joint model of images and captions](16-DeepNN.md#161-learning-a-joint-model-of-images-and-captions)
+ [Hierarchical coordinate frames](16-DeepNN.md#162-hierarchical-coordinate-frames)
+ [Bayesian optimization of neural network hyperparameters](16-DeepNN.md#163-bayesian-optimization-of-neural-network-hyperparameters)
+ [The fog of progress](16-DeepNN.md#164-the-fog-of-progress)


## Related Articles

+ Matthew Stewart, [Introduction to Neural Networks](a01-IntroNN.md)
+ Matthew Stewart, [Intermediate Topics in Neural networks](a02-IntermediateNN.md)
+ Matthew Stewart, [Neural Network Optimization](a03-Optimization.md)
+ Matthew Stewart, [Simple Guide to Hyperparameter Tuning in Neural Networks](a04-Hyperparameter.md)
+ Matthew Stewart, [Neural Style Transfer and Visualization of Convolutional Networks](a05-VisualCNN.md)
+ Random Nerd, [Delta Learning Rule & Gradient Descent | Neural Networks](a06-DeltaRule.md)
+ Drew Rollins, [Delta Function](a07-DeltaFunc.md)
+ Chris McCormick, [Deep Learning Tutorial - Softmax Regression](a08-SoftmaxReg.md)
+ [Softmax Classifier](a09-SoftmaxClass.md) in CS231n Convolutional Neural Networks for Visual Recognition, Stanford University
+ Adit Deshpande, [A Beginner's Guide To Understanding Convolutional Neural Networks](a10-CNNsGuide.md)
+ Adit Deshpande, [The 9 Deep Learning Papers You Need to Know About](a11-9Papers.md)


## References

+ [Introduction to Neural Networks and Machine Learning - CSC321 Winter 2014](http://www.cs.toronto.edu/~tijmen/csc321/)
  + [Lecture Notes](http://www.cs.toronto.edu/~tijmen/csc321/lecture_notes.shtml)
  + [Assignmenets](http://www.cs.toronto.edu/~tijmen/csc321/assignments.shtml)
  + [Optional Readings](http://www.cs.toronto.edu/~tijmen/csc321/texts.shtml)
  + [Computing](http://www.cs.toronto.edu/~tijmen/csc321/computing.shtml)
  + [Exam](http://www.cs.toronto.edu/~tijmen/csc321/tests.shtml)
+ [2012 COURSERA COURSE LECTURES: Neural Networks for Machine Learning](http://www.cs.toronto.edu/~hinton/nntut.html)
  + [Lecture Videos](http://www.cs.toronto.edu/~hinton/coursera_lectures.html)
  + [Lecture Slides](http://www.cs.toronto.edu/~hinton/coursera_slides.html)
+ [CS231n: Convolutional Neural Networks for Visual Recognition](http://cs231n.stanford.edu/)
  + [Course Notes](http://cs231n.github.io/)
  + [Course Video](https://www.youtube.com/playlist?list=PL3FW7Lu3i5JvHM8ljYj-zLfQRF3EO8sYv)
+ Github Related Links
  + [Fuyang Liu](https://github.com/liufuyang/course-Neural-Networks-for-Machine-Learning)
  + [Chinmay Das](https://github.com/chinmaydas96/Neural-Networks-for-Machine-Learning)
  + [Chouffe](https://github.com/Chouffe/hinton-coursera)
  + [khanhnamle1994](https://github.com/khanhnamle1994/neural-nets)
+ Harry Wechsler, [Neural Networks for Perception. Computation, Learning, and Architectures](https://bit.ly/2RcSCTs), AP, 1992



