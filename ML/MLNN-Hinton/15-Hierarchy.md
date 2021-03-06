# 15. Hierarchical Structure with Neural Networks

## 15.1 From principal components analysis to autoencoders

### Lecture Notes

+ Principal Components Analysis (PCA) -Intro
  + widely used technique in signal processing
  + higher dimensional data represented by a much lower dimensional code
  + situation: a data lying a linear manifold in the high dimensional space
  + task: finding a data manifold and projecting the data onto the manifold = representation on the manifold $\to$ orthogonal directions not variation much in the data $\implies$ not losing much information
  + operation:
    + standard principal components methods: efficient
    + neural network w/ one linear hidden layer and linear output layer: inefficient
  + advantage of using neural networks:
    + generalizing the technique by using deep neural networks where the code is a nonlinear function of the input
    + reconstructing the data from the code as a nonlinear function of the input vector
    + able to deal w/ curved manifold in the input space

+ Principal Components Analysis
  + finding the $M$ orthogonal directions
    + $\exists\; N$-dimensional data, representing the data w/ less than $N$ numbers, said $M$
    + the direction where data w/ the most variance
    + ignoring the directions where the data not varying much
    + $M$ principal directions forming a lower-dimensional subspace
    + representing an $N$-dimensional datapoint by its projections onto the $M$ principal directions
    + losing all information about where the datapoint located in the remaining orthogonal directions but not much
  + reconstructing by using the mean value (over all the data)
    + the mean value w/ $N-M$ directions not represented w/ $M$ orthogonal directions
    + reconstruction error = sum over all these unrepresented directions of the squared differences of the datapoint from the mean
  + example: PCA w/ $N=2$ and $M=1$ (see diagram)
    + 2-dimensional data distributed according to an elongated Gaussian
    + the ellipse: a kind of one standard deviation contour of the Gaussian
    + the green point on PC directions representing the data on the red point
      + using PCA w/ a single component
      + the component as the direction in the data w/ greatest variance
      + representing the red point = representing how far along that direction
      + $\therefore$ representing the projection of the red point onto that line; i.e., the green point
    + reconstruction of the red point: an error equal to the squared difference btw red and green points
      + using all the mean values of the data points ignored
      + representing a point on the black line
      + the loss on the construction = the squared difference btw the red point and the green point
      + the loss = the difference btw the data point and the mean values of all the data in the direction ignored
      + minimizing the loss = choosing to ignore the directions w/ less variance

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://bit.ly/39K9qaJ" ismap target="_blank">
      <img src="img/m15-01.png" style="margin: 0.1em;" alt="PCA example w/ N=2 and M=1" title="PCA example w/ N=2 and M=1" width=350>
    </a>
  </div>

+ Implementing PCA w/ backpropagation
  + inefficient implementation
  + task: making output = the input in a network w/ a central bottleneck
    + making a network in which the output of the network as the reconstruction of input
    + trying to minimize the squared error in the reconstruction
    + the network w/ a central bottleneck
    + $\exists\; M$ hidden units corresponding to the principal components
    + input vector projected to the code vector
    + from code vector to construct the output vector
    + goal: making the output vector as similar as the input vector

    <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
      <a href="https://bit.ly/39K9qaJ" ismap target="_blank">
        <img src="img/m15-02.png" style="margin: 0.1em;" alt="PCA example w/ N=2 and M=1" title="PCA example w/ N=2 and M=1" width=200>
      </a>
    </div>

  + efficient code = the activities of the hidden units $\to$ the bottleneck
    + the activities of the hidden unit forming a bottleneck
    + the code vector = a compressed representation of the input vector
  + linear hidden and output layers $\implies$ autoencoder
    + autoencoder
      + learning hidden units w/ a linear function of the data
      + minimizing the squared reconstruction error
    + exactly what PCA does
      + exact the same reconstruction error as PCA does
      + not necessary w/ hiddent units corresponding exactly to the principal components
  + $M$ hidden units
    + spanning the same space at the first $M$ components found by PCA
    + weight vectors probably not orthogonal
    + tending to have equal variances
    + probably rotating and skewing of those axes
    + the incoming vectors of code units $\neq$ the directions of the components $\implies$ orthogonal
    + the space spanned by the incoming weight vectors of those code units = the space spanned by the $M$ principal components
    + $\therefore\;$ the networks $\equiv$ principal components
    + performance: the stochastic gradient descent learning for the network < PCA algorithm

+ Generalizing PCA w/ backpropagation
  + purpose: generalizing PCA
    + able to represent data w/ a curved manifold rather than a linear manifold in a high dimensional space
  + adding nonlinear layers before and after the code: encoding and decoding weights
    + encoder: converting coordinates in the input space to coordinates on the manifold
    + decoder: inverting the mapping of encoder
    + nonlinear layers: possibly efficiently representing data that lies on or near a nonlinear manifold
  + learned $\to$ mapping on both directions  
  + network architecture (see diagram)
    + adding one ore more layers of nonlinear hidden units, typically using logistic units
    + the code layer: linear units
    + following a one or more layers of nonlinear units
    + output layer trained as similar as possible to the input vector
    + using supervisor learning algorithm to do unsupervised learning

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://bit.ly/39K9qaJ" ismap target="_blank">
      <img src="img/m15-03.png" style="margin: 0.1em;" alt="PCA example w/ N=2 and M=1" title="PCA example w/ N=2 and M=1" width=200>
    </a>
  </div>


### Lecture Video

<a href="https://bit.ly/2UOSCv3" target="_BLANK">
  <img style="margin-left: 2em;" src="https://bit.ly/2JtB40Q" width=100/>
</a><br/>


## 15.2 Deep Autoencoders

### Lecture Notes

+ Prior works
  + developed in 1980s
  + unable to train them significantly better than PCA
  + various publications w/o good demonstrations of impressive performance
  + applying pre-training deep networks layer-by-layer to pre-training deep autoencoders

+ Deep autoencoders
  + always looking like a nice way to do nonlinear dimensional reduction
    + providing flexible mapping both ways
    + mapping able to be nonlinear
    + linear (or better) learning time in the number of training cases
    + final encoding model: fairly compact and fast $\impliedby$ multiplication of matrices for each layer
  + difficulties
    + very difficult to optimize deep autoencoders using backpropagation
    + small initial weights $\to$ backpropagation gradient vanished
  + Solutions
    + unspervised layer-by-layer pre-training
    + initializing the weights carefully as in Echo-state nets

+ Deep autoencoders on MNIST digits
  + G. E. Hinton*, R. R. Salakhutdinov, [Reducing the Dimensionality of Data with Neural Networks](https://bit.ly/2xbMHXZ), Science, 28 Jul 2006
  + network architecture: (see diagram)
    + starting w/ images w/ 784 pixels
    + encoding the pixels via 3 hidden layers into 30 real-value activities in a central code layer
    + decoding those 30 real-valued activities back to 784 reconstructed pixels
    + using a stack of RBMs to initialize the weights used for encoding ($W_1, W_2, W_3, W_4$)
    + taking the transpose over those weights to initialize the decoding network ($W_4^T, W_3^T, W_2^T, W_1^T$)
    + training a stack of 4 RBM's and then unrolling them
    + fine-tuning w/ gentle backpropagation to minimize the reconstruction error
    + using cross-entropy error due to logistic units
  + comparisons of methods for compressing digit images to 30 real numbers
    + real data
    + 30-D deep autoencoder
    + 30D PCA

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://bit.ly/39K9qaJ" ismap target="_blank">
      <img src="img/m15-04.png" style="margin: 0.1em;" alt="Autoencoder example w/ 4 RBMs" title="Autoencoder example w/ 4 RBMs" width=350>
      <img src="img/m15-05.png" style="margin: 0.1em;" alt="Comparison of autoencoder results" title="Comparison of autoencoder results" width=350>
    </a>
  </div>


### Lecture Video

<a href="https://bit.ly/3b04kbG" target="_BLANK">
  <img style="margin-left: 2em;" src="https://bit.ly/2JtB40Q" width=100/>
</a><br/>


## 15.3 Deep autoencoders for document retrieval and visualization

### Lecture Notes

+ Introduction
  + applying deep autoencoders to document retrieval
  + method: latent semantic analysis (LSA) - a technique in natural language processing, in particular, distributional semantics, of analyzing relationship btw a set of documents and the terms they contains by producing a set of concepts related to the document and terms
  + applying PCA to vector of word counts extracted from the documents
  + the codes
    + produced by latent semantic analysis
    + used for judging similarity btw documents
  + $\therefore\;$ used for document retrival
  + expecting much better codes using a deep autoencorder than using latent semantic analysis
  + results:
    + 10 components extracted w/ a deep autoencoders > 50 components extracted w/ linear method like latent semantic analysis
    + 2 components to visualize documents as a point in a 2D map > the first two principal components

+ Modeling similarity of documents
  + converting each documents into a "bag of words"
    + a vector of word counts ignoring order
      + throwing away a lot of information
      + retaining a lot of information about the topic of the document
    + ignoring stop words (like "the" or "over") $\impliedby$ not containing much information about the topic
    + example: counting for various words (see diagram)
      + the counts for the document on the bottom
      + nonzero counts for the words telling the information about the document
  + comparison the word counts of the query document and millions of other documents
    + issue: too slow $\impliedby$ involving big vectors
    + solution: reducing each query vector to a much smaller vector
    + the vector still containing most of the information about the content of the document

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://bit.ly/39K9qaJ" ismap target="_blank">
      <img src="img/m15-06.png" style="margin: 0.1em;" alt="Architecture of compressing word count" title="Architecture of compressing word count" height=100>
    </a>
  </div>

+ Mechanism to compress the count vector
  + deep autoencoder architecture
    + compressing 2000 word counts $\to$ 10 real numbers
    + reconstructing the 2000 words w/ the 10 numbers
  + training the neural network to reproduce its input vector as its output
  + forcing the net to compress as much information as possible into the 10 numbers in the central bottleneck
  + comparing documents w/ these 10 numbers

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://bit.ly/39K9qaJ" ismap target="_blank">
      <img src="img/m15-07.png" style="margin: 0.1em;" alt="Architecture of compressing word count" title="Architecture of compressing word count" height=250>
    </a>
  </div>

+ Reconstructing bag of words w/ non-linearity
  + word counts not the same as pixels or real values
  + word frequency in the document
    + dividing the counts in a bag of words vector by $N$
    + $N$ = the total number of non-stop words in the document
    + result: <span style="color: blue;">probability vector</span> = the probability of getting a particular word if picking a non-stop word at random from the document
  + using softmax at the output of the autoencoder
    + probability vector $:=$ the desired outputs of the softmax
  + training the first RBM in the stack by using the same trick
    + $N$ observations from the probability distribution
    + treating the word counts as probabilities
    + the visible to hidden weights = $N \times$ the hidden to visible weights
    + input in probabilities $\implies$ very small activities for the 1st hidden layer

+ Performance of the autoencoder at document retrieval
  + autoencoder settings:
    + bags of words: 2000
    + training cases: 400,000
    + type: business documents
    + label: $\sim$ 100 categories
    + output: softmax w/ 2000 ways
  + training procedure
    + first train a stack of RBMs
    + fine-tune w/ backpropagation
  + testing on a separate 400,000 documents
    + picking a document as query
    + ranking order all the other test documents by using the cosine of the angle btw codes
    + repeating the process for the 400,000 documents $\to$ requiring 0.16 trillion comparisons
  + plotting the number of retrieved documents against the proportion
    + the proportion in the same hand-labeled class as the query document
    + comparing w/ LSA (a version of PCA)
      + not a very good measure of the quality of the retrieval
  + Performance plottings
    + left diagram: accuracy retrieval as a function of the number of retrieval documents
      + Retrieval performance on 400,000 Reuter new stories
      + The fraction of retrieved documents in the same class as the query when a query document from the test set is used to retrieve other test set documents, averaged over all 402,207 possible queries.
      + accuracy: autoencoders using a code w/ 10 real numbers > LSA w/ 50 real numbers > LSA w/ 10 real numbers
      + computational: Autoencoder $\approx$ LSA-50D / 5
    + middle diagram: distribution of classes
      + compressing all documents to 2 numbers using PCA on $\log(1+count)$ by the class of the document
      + using different colors for different categories
      + logarithm to suppress counts w/ big numbers $\to$ PCA work better
      + green classes in one place while the red class in slightly different place
      + classes mixed
    + right diagram: 
      + compressing all documents to 2 numbers using deep auto
      + using different colors for different document categories
      + much better layout for the structure of the data set
      + classes separated w/ different colors
      + documents in the middle = not many words in them $\to$ difficult to distinguish them
  + visualization: very useful for judgment

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://bit.ly/39K9qaJ" ismap target="_blank">
      <img src="img/m15-08.png" style="margin: 0.1em;" alt="The fraction of retrieved documents in the same class as the query when a query document from the test set is used to retrieve other test set documents, averaged over all 402,207 possible queries." title="Retrieval performance on 400,000 Reuter new stories" height=200>
      <img src="img/m15-09.png" style="margin: 0.1em;" alt="First compress all documents to 2 numbers using PCA on log(1+count). Then use different colors for different categories." title="The codes produced by two-dimensional LSA." height=200>
      <img src="img/m15-10.png" style="margin: 0.1em;" alt="First compress all documents to 2 numbers using deep auto. Then use different colors for different document categories" title="The codes produced by a 2000-500-250-125-2 autoencoder" height=200>
    </a>
  </div>



### Lecture Video

<a href="https://bit.ly/2wZfoHG" target="_BLANK">
  <img style="margin-left: 2em;" src="https://bit.ly/2JtB40Q" width=100/>
</a><br/>


## 15.4 Semantic hashing

### Lecture Notes

+ Introduction to semantic hashing
  + providing an extremely efficient way of finding a documents similar to a query document
  + idea:
    + converting the document into a memory address
    + organizing semantic in the memory
    + looking at the nearby addresses for a particular address $\to$ finding documents very similar
  + analogy: similar products located nearby in a supermarket

+ Finding binary codes for documents
  + binary descriptors of images $\to$ a good way of retrieving images quickly
    + some binary descriptor easily to get; e.g., indoor or outdoor scene, color or black-and-white image
    + difficult to get a list of binary descriptors, said 30 $\to$ more or less orthogonal to one another
    + solved by machine learning
  + training an autoencoder using 30 logistic units for the code layer
    + instead of getting real values for documents
    + getting binary code from word count documents
    + implementing logistic units in code layer $\to$ inefficient
    + logistic unit used real value in their middle range $\to$ conveying as much information as possible about the 2000 word counts
  + procedure
    + first, training w/ a stack of RBMs
    + then unrolling these RBMs by using the transposes of the weight matrices for the decoder
    + last, fine-tuning w/ backpropagation
  + fine-tuning stage
    + adding noise to the inputs to the code units
    + noise forcing their activities to become bimodal in order to resist the effects of the noise
      + code units either firmly on or firmly off
      + noise encouraging the learning to avoid the middle region of the logistic
      + the range conveying a lot of information but very sensitive to noise in its inputs
    + simply threshold the activities of the 30 code units to get a binary code
      + tested w/ simple threshold in logistic units to get binary values
      + training w/ autoencoder able to convert the kind of a bag of words into small number of binary values
      + learning a set of binary features good for reconstructing the bag of words
  + easier to just use binary stochastic units in the code layer during training - Krizhevsky
    + adding Gaussian noise to the inputs to the 30 code units not required
    + just making the 30 code units as stochastic binary units
      + forward pass: picking a binary value using the output of the logistic
      + backward pass: pretending to transmit the real value of probability from the logistic $\to$ smooth gradient for backpropagation
    + doing sequential search on the obtained short binary code
    + storing a code for each known document
    + a query document
      + extracting the binary code of the document
      + comparing the code w/ the codes of all stored documents
    + using special bit operations to do fast comparison $\to$ parallel operations in CPU
    + issue: probably a long list of documents
    + solution: treating the code as if a memory address

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://bit.ly/39K9qaJ" ismap target="_blank">
      <img src="img/m15-11.png" style="margin: 0.1em;" alt="Deep autoencoder architecture w/ 30 real-valued numbers" title="Deep autoencoder architecture w/ 30 real-valued numbers" height=200>
    </a>
  </div>

+ Semantic hashing
  + deep autoencoder as hash-function
    + task: finding approximate matches
    + using autoencoder as a hash function to convert a document into a 30 bit address
    + a memory w/ 30 bit addresses and each bit of the memory pointing back to the document
    + collision: a list to store same address
    + similar documents $\implies$ similar addresses
    + query document $\to$ binary code $\to$ memory address
    + looking at nearby addresses $\to$ flipping bits in the address to access nearby addresses
    + a little Hamming ball of nearby addresses = small difference in bit flipping counts
    + nearby address $\implies$ semantically similar document
    + advantage: avoiding searching a big list but flipping a few bits in memory addresses
    + a.k.a. supermarket search (see diagram)
  + fast retrieval methods
    + working by intersecting stored lists that are associated w/ cues extracted from the query
    + example: Google search
      + a list of all documents w/ some particular rare word
      + a query w/ the rare word $\to$ immediately accessing to the list
      + intersecting the list w/ other lists to satisfy all the terms in the query
  + memory bus in computer hardware
    + intersecting 32 very long lists in one instruction
    + each bit in a 32-bit binary code specifying a list of half the addresses in the memory
    + forming a binary search
  + using machine learning to map the retrieval problem onto the type of list intersection the computer is good at

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://bit.ly/39K9qaJ" ismap target="_blank">
      <img src="img/m15-12.png" style="margin: 0.1em;" alt="Approximation match w/ a hash-function" title="Approximation match w/ a hash-function" height=150>
    </a>
  </div>



### Lecture Video

<a href="https://youtu.be/swjncYpcLsk?list=PLoRl3Ht4JOcdU872GhiYWf6jwrk_SNhz9" target="_BLANK">
  <img style="margin-left: 2em;" src="https://bit.ly/2JtB40Q" width=100/>
</a><br/>


## 15.5 Learning binary codes for image retrieval

### Lecture Notes

+ Binary codes for image retrieval
  + typically done by using the captions
  + task: retrieval images by objects in images
    + pixels not like words
    + individual pixels not telling much about the content
    + recognizing objects in the images $\to$ searching similar to words
    + hard to extract object classes from images
    + solved by deep neural network
  + extracting a real-valued vector w/ information about the content
    + matching real-valued vectors: big database and slow
    + requiring a lot of storage
  + storing short codes $\to$ easy to store and match

+ A two-stage method
  + procedure
    + using semantic hashing w/ 28-bit binary code to get a long "shortlist" of promising images
      + applying short binary code as used w/ semantic hashing $\to$ very rapidly to get a shortlist of promising images
      + taking the short binary code and flipping a few bits $\to$ candid images
    + using 256-binary codes to do a serial search for good matches
      + only requiring a few words of storage per image
      + the serial search done by using fast bit-operation
      + the candid images able to match by using 256-bit binary codes stored for each known images
      + much better matching than finding w/ a 28-bit binary code
      + only 4-word memory per image
      + fast searching $\to$ a few operations to compare 256-bit binary codes
  + 256-bit binary code
    + is good enough?
    + how to judge similarity?

+ Krizhevsky's deep autoencoder
  + architecture (top left diagram)
    + input: 32x32 pixels of images
    + taking input via red, green and blue channels $\to \approx$ 3000 inputs
    + expanding w/ a larger number of hidden units: real-valued inputs to logistic hidden units w/ less capacity
    + progressively decreasing the half number of units each layer $\to$ 256-bit binary code at the last layer
  + the encoder $\approx$ 67,000,000 parameters
  + taking a few days on a GTX 285 GPU to train on two million images
  + no theory to justify this architecture
    + guess: architecture half number of units each layer
    + presumably some other architecture working better
  + examples
    + top right: how well the autoencoder
      + reconstructions of 32x32 color images from 256-bit codes
      + each left sub-image as the origin
      + the right sub-image as the reconstructed images
    + starting w/ a picture of Michael Jackson in red box
      + middle left: retrieved using 256 bit codes
        + Alex net retrieving objects from images
        + extracting the most similar images and indicating the bit distance on top of each subimages
        + distance = 61: extraordinarily unlikely to happen by chance
        + similar images; only a few bits
      + middle right: retrieved using Euclidean distance in pixel intensity space
    + image of a party scene and retrieving other images
      + bottom left: retrieved using 256 bit codes
        + half of the retried images fairly similar
        + origin party scene: bright in the middle
        + most bad matches: bright in the middle
        + sensitive to the image structure and brighter patches
      + bottom left: retrieved using Euclidean distance in pixel intensity space
        + much worse results: only one other images w/ a group of people
        + Euclidean distance: not very smooth images
          + unable to match the high frequency variation in the images
          + better to match the average of the high frequency variation of other stuff $\to$ out of phase
        + Euclidean distance usually finding smooth images to match $\because$ minimizing squared error in pixel space

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://bit.ly/39K9qaJ" ismap target="_blank">
      <img src="img/m15-13.png" style="margin: 0.1em;" alt="Network architecture for image encoding" title="Network architecture for image encoding" height=150>
      <img src="img/m15-14.png" style="margin: 0.1em;" alt="Reconstructions of 32x32 color images from 256-bit codes" title="Reconstructions of 32x32 color images from 256-bit codes" width=350>
    </a>
    <a href="https://bit.ly/39K9qaJ" ismap target="_blank">
      <img src="img/m15-15a.png" style="margin: 0.1em;" alt="Retrieved using 256 bit codes" title="Retrieved using 256 bit codes" width=350>
      <img src="img/m15-15b.png" style="margin: 0.1em;" alt="Retrieved using Euclidean distance in pixel intensity space" title="Retrieved using Euclidean distance in pixel intensity space" width=350>
    </a>
    <a href="https://bit.ly/39K9qaJ" ismap target="_blank">
      <img src="img/m15-16a.png" style="margin: 0.1em;" alt="Retrieved using 256 bit codes" title="Retrieved using 256 bit codes" width=350>
      <img src="img/m15-16b.png" style="margin: 0.1em;" alt="Retrieved using Euclidean distance in pixel intensity space" title="Retrieved using Euclidean distance in pixel intensity space" width=350>
    </a>
  </div>

+ Improvement of deep autoencoder
  + task: making image retrieval more sensitive to object and less sensitive to pixel intensities
  + procedure
    + training a big net to recognize lots of different types of object in real image (Mod05)
    + using the activity vector in the last hidden layer as the representation of the image
      + much better representation to match than the pixel intensities
  + verify w/ the net described in Mod 05, won the ImageNet competition
  + only using the Euclidean distance btw the activity vector in the last hidden layer
    + taking those activity vectors and building an autoencoder on them to get down to binary codes $\to$ working really well
    + working w/ binary code?
  + examples (see diagram)
    + leftmost column: the search image
    + other columns: the most similar feature activities in the last hidden layer
    + elephant image:
      + retrieving elephant images w/ different poses
      + images w/o good overlap in pixel space
    + Halloween pumpkins:
      + good for all retrieved images
      + some of images w/ pretty bad overlap in pixel space
  + expectation: reducing these activity vector to short binary codes $\to$ a fast and effective way of retrieving similar images just by the contents of the image

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="https://bit.ly/39K9qaJ" ismap target="_blank">
      <img src="img/m15-17.png" style="margin: 0.1em;" alt="Query images and various matching images" title="Query images and various matching images" width=350>
    </a>
  </div>


### Lecture Video

<a href="https://youtu.be/MSYmyJgYOnU?list=PLoRl3Ht4JOcdU872GhiYWf6jwrk_SNhz9" target="_BLANK">
  <img style="margin-left: 2em;" src="https://bit.ly/2JtB40Q" width=100/>
</a><br/>


## 15.6 Shallow autoencoders for pre-training

### Lecture Notes

+ RBM as autoencoder 
  + one hidden layer RBM = shallow autoencoder
  + training an RBM w/ one-step contrastive divergence
    + RBM trying to make the reconstructions look like input data
    + autoencoder view: strongly regularized by using binary activities in the hidden layer
  + RBMs $\neq$ autoencoders when trained w/ maximum likelihood
    + e.g., pixel as pure noise
      + autoencoder: trying to reconstruct whatever noise value it had
      + RBM: training w/ maximum likelihood and using the bias for that input
  + applying pre-training on autoencoders
    + Question: replacing the stack of RBMs used for pre-training by a stack of shallow autoencoders
    + the shallow autoencoders regularized by penalizing the squared weights $\implies$ pre-training not effective (for subsequent discrimination)
    + stacking autoencoders not working as well as stacking RBMs

+ Denoising autencoders
  + adding noise to input vector setting many of its components to zero
    + different components for different input vectors
    + like dropout but for input than hidden units
    + still required to reconstruct these components
    + extracting features to capture correlations btw inputs
    + not just copying input $\impliedby$ denoising
    + N.B.: shallow autoencoder w/ enough hidden units $\to$ copying each pixel to one hidden unit $\to$  reconstruct that pixel from that hidden unit $\implies$ not applied for a denoising autoencoder
    + using hidden units to capture correlation btw the inputs
    + using the value of some inputs to help reconstructing the inputs that have been zeroed out
  + pre-training working well w/ a stack of denoising autoencoders
    + performance: $\geq$ RBM w/ pre-training
    + simpler to evaluate the pre-training $\gets$ easily computing the value of the objective function
      + pre-training RBM w/ contrastive divergence unable to compute the value of real objective function to minimize
      + squared reconstruction error not what been minimized
    + lacking the nice variational bound as w/ RBMs $\to$ only of theoretical interest
  + P. Vincent, H. Larochelle, Y. Bengio, and P. Manzagol, [Extracting and composing robust features with denoising autoencoders](https://bit.ly/2USqMy4), ICML '08: Proceedings of the 25th international conference on Machine learning, 2008

+ Contractive autencoders
  + alternative way to regularize an autoencoder
    + trying to make the activities of the hidden units as intensities as possible to the inputs
    + reconstruction $\to$ unable to ignore the inputs
  + achieved by penalizing the squared gradient of each hidden activity w.r.t. the inputs
  + working well w/ pre-training
    + property of the codes: only a small subset of the hidden units sensitive to changes in the input
      + different parts of the input space = different subset in an active set acting like a sparse code
      + other hidden units all saturated and insensitive
    + RBMs behaving similar
      + after trained, many units saturated
      + the working set of unsaturated one $\neq$ training cases
  + S. Rifai, P. Vincent, X. Muller, X. Glorot, and Y. Bengio, [Contractive Auto-Encoders: Explicit Invariance During Feature Extraction](https://bit.ly/2K2WXVr), ICML 2011

+ Conclusion about pre-training
  + many different ways to do layer-by-layer pre-training to discover good features
    + discovering features before using the labels
    + helpful for subsequent discriminative learning as database w/o huge numbers of labeled cases
    + useful for discovering features w/o using the information in the labels
    + information in the labels used for fine-tuning the decision boundaries btw classes
  + initializing weights not required
    + situation
      + applied for very large, labeled datasets
      + executing supervised learning by using unsupervised pre-training
    + pre-training used to be a good way to initialize the weights for deep nets
    + other ways available now
  + large network $\implies$ pre-training required


### Lecture Video

<a href="https://bit.ly/2RnWYHi" target="_BLANK">
  <img style="margin-left: 2em;" src="https://bit.ly/2JtB40Q" width=100/>
</a><br/>

