# Handling Missing Values when Applying Classification Models

Author: Maytal Saar-Tsechansky and Foster Provost 
Publication: Journal of Machine Learning Research 8 (2007) 1625-1657

[Original document](http://jmlr.csail.mit.edu/papers/volume8/saar-tsechansky07a/saar-tsechansky07a.pdf)

## Abstract

+ Methods compared: predictive value imputation, the distribution based imputation used by C4.5, and reduced method

+ Applying calssification trees to instances with missing values and generalizing to bagged trees and to logistic regression

+ The former two preferable under difference conditions.

+ Reduced-models approach consistently outperform the other two, sometimes by a large margin.

+ Hybrid approaches scale gracefully to the amount of investment in computation/storage and outperform imputation even for small investment.

## Introduction

+ Contexts of missing values: features may be missing
    + at induction time, in the historical "training" data
    + at prediction time, in to-be-predict "test" cases

+ Classification Trees
    + Employed widely to support decision-making under uncertainty, both by 
        + practitioners (for diagnosis, for predicting customers’ preferences, etc.)
        + researchers constructing higher-level systems
    + Usage
        + Stand-alone classifiers for applications where model comprehensibility is important
        + Base classifiers in classifier ensembles
        + Components of larger intelligent systems
        + The basis of more complex models such as logistic model trees (Landwehr et al., 2005)
        + Components of or tools for the development of graphical models
            + Bayesian networks [10]
            + Dependency networks [18]
            + Probabilistic relational models [11, 24]
    + Combined into ensembles via bagging [4], produce accurate and well-calibrated probability estimates [25]

+ Imputation
    + The most common approaches for dealing with missing features [17]
    + Main idea: if an important feature is missing for a particular instance, it can be estimated from the data that are present.
    + Main families of imputation approaches: 
        + (Predictive) value imputation (PVI)
        + Distribution-based imputation (DBI)
    + Value imputation:
        + Estimate a value to be used by the model in place of the missing feature
        + More common in the statistics community
    +  Distribution-based imputation:
        + Estimate the conditional distribution of the missing value
        + Predictions based on this estimated distribution
        + The basis for the most popular treatment used by the (non-Bayesian) machine learning community, as exemplified by C4.5[31]

+ Reduced-Feature Model
    + Employ only those features known for a particular test case
    + No imputation required
    + Induced using only a subset of the features available for the training data
    + Little prior research or practice using this method
    + Treated to some extent in papers [34, 9]

+ Contributions of the paper
    + Comprehensive empirical comparison
        + Different missing-value treatments using a suite of benchmark data sets
        + A follow-up theoretical discussion
        + The inferiority of the two common imputation treatments, highlighting the underappreciated reduced-model method
        + The predictive performance of the methods is more-or-less in inverse order of their use
        + Neither of the two imputation techniques dominates cleanly
    + Hybrid models
        + Reduced-feature models: computationally expensive
        + hybrid methods: manage the tradeoff between storage/computation cost and predictive performance
        + Even a small amount of storage/computation can result in a considerable improvement in generalization performance.


## Treatments for Missing Values at Prediction Time

+ Research
    + [22]: Missing Completely At Random (MCAR) refers to the scenario where missingness of feature values is independent of the feature values
    + [14]: MCAR not hold for practical problems
    + [17]: most imputation methods rely on MCAR for their validity
    + [07]: the performance of missing-value treatments used when training classification trees seems unrelated to the Little and Rubin taxonomy, as long as missingness does not depend on the class value (in which case unique-value imputation should be used as long as the same relationship will hold in the prediction setting).

+ Alternative courses of action when features are missing in test instances
    1. Discard instances
    2. Acquire missing values
    3. Imputation
        1. (Predictive) Value Imputation (PVI)
        2. Distribution-based Imputation (DBI)
        3. Unique-value Imputation
    4. Reduced-feature Models

+ Discard instances
    + an approach often taken by researchers wanting to assess the performance of a learning method on data drawn from some population
    + appropriate if the features are missing completely at random
    + in practice, appropriate when it is plausible to decline to make a prediction on some cases at prediction time
    + maximize utility w/ the cost of inaction and prediction error

+ Acquire missing values
    + in practice, obtainable by incurring a cost, such as the cost of performing a diagnostic test or the cost of acquiring consumer data from a third party
    + Buying a missing value: only appropriate when the expected net utility from acquisition exceeds that of the alternative

+ Imputation
    + a class of methods by which an estimation of the missing value or of its distribution is used to generate predictions from a given model
    + multiple imputation [32]: a Monte Carlo approach that generates multiple simulated versions of a data set that each are analyzed and the results are combined to generate inference

+ (Predictive) Value Imputation (PVI):
    + missing values replaced with estimated values before applying a model
    + E.g., replace a missing value with the attribute’s mean or mode value (for real-valued or discrete-valued attributes, respectively) as estimated from the training data
    + alternative: impute with the average of the values of the other attributes of the test case
    + rigorous estimations: induce a relationship between the available attribute values and the missing feature
    + commercial modeling packages: offering procedures for predictive value imputation
    + surrogate splits for classification trees [5]: based on the value of another feature, assigning the instance to a subtree based on the imputed value
    + a special case of predictive value imputation [31]

+ Distribution-based Imputation (DBI)
    + Given a (estimated) distribution over the values of an attribute, one may estimate the expected distribution of the target variable (weighting the possible assignments of the missing values).
    + common for applying classification trees in AI research and practice
    + the basis for the missing value treatment implemented in the commonly used tree induction program, C4.5 [31]
    + The C4.5 algorithm: 
        1. split into multiple pseudoinstances each with a different value for the missing feature and a weight corresponding to the estimated probability for the particular missing value (based on the frequency of values at this split in the training data)
        2. Each pseudo-instance is routed down the appropriate tree branch according to its assigned value.
        3. Upon reaching a leaf node, the class-membership probability of the pseudo-instance is assigned as the frequency of the class in the training instances associated with this leaf.
        4. The overall estimated probability of class membership is calculated as the weighted average of class membership probabilities over all pseudo-instances.
        5. If there is more than one missing value, the process recurses with the weights combining multiplicatively.
    + C4.5 combines the classifications across the distribution of an attribute’s possible values, rather than merely making the classification based on its most likely value

+ Unique-value imputation
    + replace each missing value with an arbitrary unique value.
    + preferable conditions [7]
        + the fact that a value is missing depends on the value of the class variable
        + this dependence is present both in the training and in the application/test data

+ Reduced-feature Models
    + incorporates only attributes known for the test instance
    + E.g., a new classification tree could be induced after removing from the training data the features corresponding to the missing test feature
    + "lazy" classification tree [9]: potentially employ a different model for each test instance
    + Alternative: store many models corresponding to various patterns of known and unknown test features

+ Complexity of dealing missing values
    + expensive in terms of storage and/or prediction-time computation
    + exception of C4.5’s method
    + reduced-feature model requirement:
        + a model for P on-line
        + a model for P precomputed and stored
    + achieve a balance of storage and computation with a hybrid method:
        + reduced-feature models stored for the most important patterns
        + lazy learning or imputation applied for less-important patterns

+ Predictive imputation
    + model induced or precomputed to estimate the value of A based on the case’s other features
    + more than one feature missing: the imputation of A is (recursively) a problem of prediction with missing values
    + short of abandoning straightforward imputation: 
        + take a reduced-model approach for imputation itself, which begs the question: why not simply use a direct reduced-model approach? 
        + build one predictive imputation model for each attribute, using all the other features, and then use an alternative imputation method (such as mean or mode value imputation, or C4.5’s method) for any necessary secondary  [1, 30]


## Experimental Comparison of Prediction-time Treatments for Missing Values

+ The J48 algorithm: the Weka [36] implementation of C4.5 classification tree

+ Main experiments: control for various confounding factors, factors, including pattern of missingness (viz., MCAR), relevance of missing values, and induction method (including missing value treatment used for training)

+ Avoid trivial cases:
    + when a feature is not incorporated in the model: different treatments should result in the same classifications.
    + when a feature does not account for significant variance in the target variable: different treatments will not result in significantly different classifications.

+ Followup studies:
    + using different induction algorithms
    + using data sets with “naturally occurring” missing values
    + including increasing numbers missing values


### Experimental Setup

+ Values of features from the top two levels of the classification tree induced with the complete feature set are removed from test instances (cf. [1])

+ Build models using training data having no missing values, except for the natural-data experiments

+ Scenarios
    + distribution-based imputation: C4.5’s method for classifying instances with missing values
    + value imputation: 
        + estimate missing categorical features using a J48 tree, and continuous values using Weka’s linear regression
        + mean/mode imputation for the additional missing values
    + reduced model: remove all the corresponding features from the training data before the model is induced

+ Datasets
    + the average classification accuracy of a missing-value treatment over 10 independent experiments in which the data set is randomly partitioned into training and test sets
    + use 70% of the data for training and the remaining 30% as test data
    + web-usage data sets [27]
    + the UCI machine learning repository [23]

+ Hypothesis test: a sign test with the null hypothesis that the average drops in accuracy using the two treatments are equal, as compared to the complete setting


### Comparison of PVI, DBI and Reduced Modeling

+ The relative difference (improvement) w/ a treatment $T$

    $$100 \cdot \frac{AC_T - AC_K}{AC_K}$$

    + $AC_K$: the prediction accuracy obtained in the complete setting
    + $AC_T$: the accuracy obtained when a test instance includes missing values

+ Summary of Data Sets

| Data Set | Instances | Attributes | Nominal Attributes |
|----------|-----------|------------|--------------------|
| Abalone | 4177 | 8 | 1 |
| Breast Cancer | 699 | 9 | 0 |
| BMG | 2295 | 40 | 8 |
| CalHouse | 20640 | 8 | 0 |
| Car | 1728 | 6 | 6 |
| Coding | 20000 | 15 | 15 |
| Contraceptive | 1473 | 9 | 7 |
| Credit | 690 | 15 | 8 |
| Downsize | 1277 | 15 | 0 |
| Etoys | 270 | 40 | 8 |
| Expedia | 500 | 40 | 8 |
| Move | 3029 | 10 | 10 |
| PenDigits | 10992 | 16 | 0 |
| Priceline | 447 | 40 | 8 |
| QVC | 500 | 40 | 8 |

+ Reduced-feature modeling is consistently superior

    | Data Set | Predictive Imputation | Distribution-based Imputation (C4.5) |
    |----------|----------------------:|-------------------------------------:|
    | Abalone | 0.12 | 0.36 |
    | Breast Cancer | -3.45 | -26.07 |
    | BMG | -2.29 | -8.67 |
    | CalHouse | -5.32 | -4.06 |
    | Car | -13.94 | 0.00 |
    | Coding | -5.76 | -4.92 |
    | Contraceptive | -9.12 | -0.03 |
    | Credit | -23.24 | -11.61 |
    | Downsize | -10.17 | -7.49 |
    | Etoys | -4.64 | -6.38 |
    | Expedia | -0.61 | -10.03 |
    | Move | -0.47 | -13.33 |
    | PenDigits | -0.25 -| 2.70 |
    | Priceline | -0.48 | -35.32 |
    | QVC | -1.16 | -12.05 |
    | Average | -5.38 | -9.49 |

    + The differences in the relative improvements obtained with each imputation treatment from those obtained with reduced modeling.
    + A large negative value indicates that an imputation treatment resulted in a larger drop in accuracy than that exhibited by reduced modeling.

+ Reduced models
    + better performance compared to distribution-based imputation in 13/15 data sets
    + better than value imputation in 14/15 data sets

+ The average drop in accuracy:
    + reduced model: 3.76%
    + predictive value imputation: 8.73%
    + distribution-based imputation: 12.98%

+ Reduced modeling consistently yields the smallest reductions in accuracy — often performing nearly as well as having all the data. Each of the other techniques performs poorly on at least one data set, suggesting that one should choose between them carefully.


### Feature Imputability and Modeling Error

+ the two most common treatments for missing values, predictive value imputation (PVI) and C4.5’s distribution-based imputation (DBI), each has a stark advantage over
the other in some domains.

+ Feature imputability
    + Def: the fundamental ability to estimate one feature using others
    + A feature is completely imputable if it can be predicted perfectly using the other features—the feature is redundant in this sense. 
    + Affect each of the various treatments, but in different ways


#### High Feature Imputability

+ Perfect feature imputability: both the primary modeling and the imputation modeling have no intrinsic error

+ Predictive value imputation simply fills in the correct value and has no effect whatsoever on the bias and variance of the model induction.

+ Example
    + two attributes, `A` and `B`, and a class variable `C` with $A = B = C$. 
    + The “model” $A \implies C$ is a perfect classifier.
    + Given a test case with `A` missing, predictive value imputation can use the (perfect) feature imputability directly: `B` can be used to infer `A`, and this enables the use of the learned model to predict perfectly.
    + feature imputability: a direct correlate to the effectiveness of value imputation
    
+ Perfect feature imputability 
    + introduce a pathology that is fatal to C4.5’s distribution-based imputation
    + When using DBI for prediction, C4.5’s induction may have substantially increased bias, because it omits redundant features from the model.
    + features critical for prediction when the alternative features are missing

+ Not be perfect
    + high feature imputability: yield only marginal improvements given the other features—to be more likely to be omitted or pruned from classification trees
    + apply beyond decision trees to other modeling approaches that use feature selection

+ Inference procedures
    + PVI: determined (as usual) based on the class distribution of a subset Q of training examples assigned to the same leaf node
    + DBI: classification based on a superset S of Q
    + When feature imputability is high and PVI is accurate, DBI can only do as well as PVI if the weighted majority class for S is the same as that of Q.


#### Low Feature Imputation

+ Uninformed guess: when feature imputability is very low PVI must guess the missing feature value as simply the most common one

+ The class estimate obtained with DBI is based on the larger set `S` and captures the expectation over the distribution of missing feature values.

+ larger and unbiased sample, DBI’s “smoothed” estimate should lead to better predictions on average

+ Example - Fig.3:
    <a href="http://jmlr.csail.mit.edu/papers/volume8/saar-tsechansky07a/saar-tsechansky07a.pdf"> <br/>
        <img src="images/p5-01.png" alt="Assume that there is no feature imputability at all (note that A and B are marginally independent) and assume that A is missing at prediction time. Since there is no feature imputability, A cannot be inferred using B and the imputation model should predict the mode (A=2). As a result every test example is passed to the A = 2 subtree. Now, consider test instances with B = 1. Although (A = 2, B = 1) is the path chosen by PVI, it does not correspond to the majority of training examples with B = 1. Assuming that test instances follow the same distribution as training instances, on B = 1 examples PVI will have an accuracy of 38%. DBI will have an accuracy of 62%. In sum, DBI will 'marginalize' across the missing feature and always will predict the plurality class. PVI sometimes will predict a minority class. Generalizing, DBI should outperform PVI for data sets with low feature imputability." title="Classification tree example: consider an instance at prediction time for which feature A is unknown and B=1." height="250">
    </a>
    + no feature imputability
    + A and B are marginally independent
    + Assume A is missing at prediction time
    + A cannot be inferred using B and the imputation model should predict the mode (A=2).
    + Every test example is passed to the `A = 2` subtree. Now, consider test instances with B = 1.
    + `A = 2, B = 1`: the path chosen by PVI, it does not correspond to the majority of training examples with `B = 1`
    + Assuming that test instances follow the same distribution as training instances, on B = 1 examples 
        + PVI: an accuracy of $38\%$
        + DBI: an accuracy of $62\%$
    + DBI will "marginalize" across the missing feature and always will predict the plurality class. 
    + PVI sometimes will predict a minority class.
    + DBI should outperform PVI for data sets with low feature imputability.


#### Demonstration

+ PVI vs DBI
    <a href="http://jmlr.csail.mit.edu/papers/volume8/saar-tsechansky07a/saar-tsechansky07a.pdf"> <br/>
        <img src="images/p5-02.png" alt="The bars represent the differences in the entries in Table 2, between predictive value imputation and C4.5’s distribution-based imputation. A bar above the horizontal line indicates that value imputation performed better; a bar below the line indicates that DBI performed better. The relative performances follow the above argument closely, with value imputation generally preferable for high feature imputability, and C4.5’s DBI generally better for low feature imputability." title="Differences between the relative performances of PVI and DBI. Domains are ordered left-to-right by increasing feature imputability." height="250">
    </a>
    + The 15 domains of the comparative study ordered left-to-right by a proxy for increasing feature imputability.
    + A bar above the horizontal line indicates that value imputation performed better; a bar below the line indicates that DBI performed better.

#### Reduced-Feature Modeling should have Advantages all along the Imputability Spectrum

+ Reduced modeling is a lower-dimensional learning problem than the (complete) modeling to which imputation methods are applied; it will tend to have lower variance and thereby may exhibit lower generalization error.

+ Important variable: reduce the effectiveness at capturing predictive patterns involving the other variables

+ Imputation tries implicitly to approximate the full-joint distribution, similar to a graphical model such as a dependency network [18]

+ Example w/ two attributes A & B, a class C
    + reduced-feature modeling uses the feature imputability differently from predictive imputation
    + The (perfect) feature imputability ensures that there will be an alternative model ($B \rightarrow C$) that will perform well. 
    + Reduced-feature modeling may have additional advantages over value imputation when the imputation is imperfect.

+ Low feature imputation
    + problematic generally when features are missing at prediction time
    + no statistical dependency at all between the missing feature and the other features
    + Reduced modeling is likely to be better than the imputation methods

+ Reduced-feature modeling w/ Fig.3
    + no feature imputability
    + insufficient data or an inappropriate inductive bias
    + Complete model omits the important feature (B) entirely?
    + if A is missing at prediction time, no imputation technique will help us do better than merely guessing that the example belongs to the most common class (as with DBI) or guessing that the missing value is the most common one (as in PVI). 
    + may induce a partial (reduced) model (e.g., $B = 0 \rightarrow C = -$, $B = 1 \rightarrow C = +$) that will do better than guessing in expectation
    + much more robust: with only one exception (Move) reduced-feature modeling yields excellent performance until feature imputability is very low
    + Value imputation does very well only for the domains with the highest feature imputability



### Evaluation using Ensembles of Trees

+ Bagged classification trees [4]:
    + outperform simple classification trees consistently in terms of generalization performance [2, 28]
    + albeit at the cost of computation, model storage, and interpretability

+ Relative difference in prediction accuracy for bagged decision trees between imputation treatments and reduced-feature modeling

    | Data Set | Predictive Imputation | Distribution-based Imputation (C4.5) |
    |----------| ---------------------:|-------------------------------------:|
    | Abalone | -0.45 | -0.51 |
    | Breast Cancer | -1.36 | -1.28 |
    | BMG | -3.01 | -7.17 |
    | CalHouse | -5.16 | -4.41 |
    | Car | -22.58 | -9.72 |
    | Coding | -6.59 | -2.98 |
    | Contraceptive | -8.21 | 0.00 |
    | Credit | -25.96 | -5.36 |
    | Downsize | -6.95 | -4.94 |
    | Etoys | -3.83 | -8.24 |
    | Expedia | 0.20 | -8.48 |
    | Move | -0.92 v-10.61 |
    | PenDigits | -0.11 | -2.33 |
    | Priceline | 0.36 | -25.97 |
    | QVC | 0.13 | -9.99 |
    | Average | -5.47 | -6.57 |


+ Reduced Models
    + reduced modeling is better than predictive imputation in 12/15 data sets and distribution-based imputation in 14/15 data sets
    + reduced models tend to increase as the models are induced from larger training sets
    + a reduced model’s relative advantage with respect to predictive imputation is comparable to its relative advantage when a single model is used
    + given the widespread use of classification-tree induction, and of bagging as a robust and reliable method for improving classification-tree accuracy via variance reduction

+ Practitioners and researchers should not choose either C4.5-style imputation or preictive value imputation blindly. Each does extremely poorly in some domains.


### Evaluation using Logistic Regression

+ C4.5-style distribution-based imputation is not applicable for logistic regression

+ For logistic regression, reduced modeling results in higher accuracy than predictive imputation in all 15 data sets (statistically significant with $p \ll 0:01$)

+ Relative difference in prediction accuracy for logistic regression between imputation and reduced-feature modeling.

    | Data Set | Predictive Imputation |
    |----------|----------------------:|
    | Abalone | -0.20 |
    | Breast Cancer | -1.84 |
    | BMG | -0.75 |
    | CalHouse | -7.11 |
    | Car | -12.04 |
    | Coding | -1.09 |
    | Contraceptive | -1.49 |
    | Credit | -3.05 |
    | Downsize | -0.32 |
    | Etoys | -0.26 |
    | Expedia | -1.59 |
    | Move | -3.68 |
    | PenDigits | -0.34 |
    | Priceline | -5.07 |
    | QVC | -0.02 |
    | Average | -2.59 |
    + Reduced modeling never is worse, and sometimes is substantially more accurate.


### Evaluation with “Naturally Occurring” Missing Values

+ naturally occurring missing values: data sets from real classification problems

+ Missingness is unlikely to be completely at random.

+ Missing values may have little or no impact on prediction accuracy, and the corresponding attributes may not even be used by the model.

+ Summary of business data sets with “naturally occurring” missing values

    | Data Set | Instances | Attributes | Nominal Attributes | Average Number of Missing Features | 
    |:-----|---:|:---:|:---:|:---:|
    | Hospitalization | 48083 | 13 | 7 | 1.73 |
    | Insurance | 18542 | 16 | 0 | 2.32 |
    | Mortgage | 2950 | 10 | 1 | 2.76 |
    | Pricing | 15531 | 28 | 8 | 3.56 |
    + models are induced from training data using C4.5’s distribution-based imputation.

+ Reduced modeling leads to higher accuracies than both popular alternatives for all four data sets.


### Evaluation with Multiple Missing Values

+ Assess how different treatments improve performance when performance is in fact undermined by the absence of strong predictors at inference time

+ The accuracies of reduced-feature modeling and predictive value imputation as the number of missing features increases

+ The imputation methods have steeper decreases in accuracy as the number of missing values increases.

+ Reduced modeling’s decrease is convex, with considerably more robust performance even for a large number of missing values.

+ sources of imputation-modeling error
    + imputation models
        + more than one value missing $\rightarrow$ face a missing-at-prediction-time problem
        + reduced modeling for imputation
    + predictive value imputation
        + worse than reduced modeling, if the inductive bias of the resultant imputation model is “worse” than that of the reduced model
        + classification-tree modeling does a much better job with numeric variables than the linear regression we use for imputation of real-value features



## Hybrid Models for Efficient Prediction with Missing Values

+ Storing many classification models has become standard practice, e.g., for improving accuracy with classifier ensembles

+ impracticably large as soon as the possible number of (simultaneous) missing values exceeds a dozen or so

+ The strength of reduced modeling in the empirical results presented above suggests its tactical use to improve imputation.


### Likelihood-based Hybrid Solutions

+ Computational cost: induce and store models for some subset of the possible patterns of missing features

+ When a test case is encountered, the corresponding reduced model is queried. 

+ If no corresponding model has been stored, the hybrid would call on a fall-back technique:
    + incurring the expense of prediction-time reduced modeling
    + invoking an imputation method (and possibly incurring reduced accuracy)

+ the marginal likelihoods of different variables being missing are very different

+ very different (inferred) likelihoods of the many patterns of multiple missing 

+ Bayesian network induction [14]: important distinction between considering only the underlying distribution for model induction/ selection and considering the querying distribution as well

+ When comparing different Bayesian networks one should identify the network exhibiting the best expected performance over the query distribution, i.e., the distribution of tasks that the network will be used to answer, rather than the network that satisfies general measures such as maximum likelihood over the underlying event distribution.

+ [12]: precompute parts of the network that pertain to a subset of frequently encountered cases so as to increase the expected speed of inference

+ Accuracies of hybrid strategies for combining reduced modeling and imputation
    <a href="http://jmlr.csail.mit.edu/papers/volume8/saar-tsechansky07a/saar-tsechansky07a.pdf"> <br/>
        <img src="images/p5-03.png" alt="The horizontal, dashed line in Figure 11 shows the performance of pure predictive value imputation for the CalHouse data set. The lower of the two curves in Figure 11 shows the performance of a likelihood-based reduced-models/imputation hybrid. The hybrid approach allows one to choose an appropriate space-usage & accuracy tradeoff, and the figure shows that storing even a few reduced models can result in considerable improvement. The curve was generated as follows. Given enough space to store k models, the hybrid induces and stores reduced models for the top-k most likely missing-feature patterns, and uses distribution-based imputation for the rest. The Calhouse data set has eight attributes, corresponding to 256 patterns of missing features. We assigned a random probability of occurrence for each pattern as follows. The frequency of each pattern was drawn at random from the unit uniform distribution and subsequently normalized so that the frequencies added up to one. For each test instance we sampled a pattern from the resulting distribution and removed the values of features specified by the pattern." title="Accuracies of hybrid strategies for combining reduced modeling and imputation" height="250">
    </a>
    + storing even a few reduced models can result in considerable improvement
    + Given enough space to store $k$ models, the hybrid induces and stores reduced models for the top-k most likely missing-feature patterns, and uses distribution-based imputation for the rest.
    + Calhouse dataset: eight attributes $\rightarrow$ 256 patterns of missing features
    + The frequency of each pattern was drawn at random from the unit uniform distribution and subsequently normalized so that the frequencies added up to one.

+ Likelihood-based hybrid model
    + The marginal improvement in accuracy does not decrease monotonically with increasing model storage
    + The most frequent patterns are not necessarily the patterns that lead to the largest accuracy increases
    + Choosing the best set of models: a complicated optimization problem
    + Considerations:
        + the likelihood of a pattern of missing features
        + the expected improvement in accuracy that will result from including the corresponding model in the "model base"
    + Calculating the expected improvement is complicated by the fact that the patterns of missing values form a lattice [34]
    + For an optimal solution, the expected improvement for a given pattern should not be based on the improvement over using the default strategy (e.g., imputation), but should be based on using the next-best already-stored pattern.
    + Determining the next-best pattern is a non-trivial estimation problem, and, even if it weren’t, the optimization problem is hard. 
    + The optimal set of reduced models $M$ corresponds to solving the following optimization task:

        $$\begin{array}{c}
            \arg\max_M (\sum_f [p(f) \cdot U(f|M)]) \\
            \text{s.t. } \sum_{f_m \in M} t(f_m) \leq T,
        \end{array}$$
        + $M$: the subset of missing patterns for which reduced models are induced
        + $t(f)$: the (marginal) resource usage (time or space) for reduced modeling with pattern $f$
        + $T$: the maximum total resource usage allocated for reduced model induction
        + $U(f|M)$: the utility from inference for an instance with pattern $f$ given the set of reduced models in the subset $M$ (when $f \in M$ the utility is derived from inference via the respective reduced model, otherwise the utility is derived from inference using the next-best already-stored pattern)
    + estimate the marginal utility of adding a missing-feature pattern f as

        $$ u(f) = p(f) \cdot ( \hat{a}_{rm}(f) - \hat{a}_i( f ))$$,
        + $p(f)$: the likelihood of encountering pattern $f$
        + $\hat{a}_{rm}(f)$: the estimated accuracy of reduced modeling for $f$
        + $\hat{a}_i(f)$: the estimated accuracy of a predictive value imputation model for missing pattern $f$
    + Estimate $\hat{a}_{rm}(f)$ and $\hat{a}_i(f)$ based on cross-validation using the training data



### Reduced-Feature Ensembles (ReFE)

+ Notations
    + $\mathcal{R}$: a set of models each induced by excluding a single attribute
    + cardinality of $\mathcal{R}$: the number of attributes
    + Model $i$: a model $i \in \mathcal{R}$ to capture an alternative hypothesis that can be used for prediction when the value for attribute vi, perhaps among others, is unknown

+ Because the models exclude only a single attribute, a ReFE avoids the combinatorial space requirement of full-blown reduced modeling.

+ ReFE ensemble members rely on imputation for the additional missing values.

+ DBI employed for missing values in ReFE

+ ReFE classifier Procedure
    + For each attribute $v_i$ a model $m_i$ is induced with $v_i$ removed from the training data.
    + For a given test example in which the values for the set of attributes $V$ are missing, for each attribute $v_i \in V$ whose value is missing, the corresponding model $m_i$ is applied to estimate the (probability of) class membership.
    + To generate a prediction, the predictions of all models applied to a test example are averaged. 
    + When a single feature is missing, ReFE is identical to the reduced-model approach. 
    + The application of ReFE for test instances with two or more missing features results in an ensemble. 
    + To achieve variance reduction as with bagging, training data are resampled with replacement for each member of the ensemble.

+ Relative improvements in accuracy for bagging with imputation and ReFE

    | Data Sets | Bagging | ReFE | Reduced Model |
    |:----------|--------:|-----:|--------------:|
    | Abalone | 0.11 | 0.26 | 0.05 |
    | BreastCancer | 4.35 | 4.51 | 4.62 |
    | Bmg | 2.88 | 3.51 | 2.57 |
    | CalHouse | 1.25 | 6.06 | 5.45 |
    | Car | 0.10 | -0.28 | 17.55 |
    | Coding | 4.82 | 6.97 | 5.32 |
    | Contraceptive | 0.39 | 0.45 | 1.16 |
    | Credit | 2.58 | 5.54 | 8.12 |
    | Downsize | 3.09 | 3.78 | 6.51 |
    | Etoys | 0.00 | 2.28 | 1.07 |
    | Expedia | 1.76 | 2.11 | 2.73 |
    | Move | 3.26 | 5.99 | 8.97 |
    | Pendigits | 0.06 | 0.58 | 1.57 |
    | Priceline | 3.29 | 4.98 | 10.84 |
    | Qvc | 1.83 | 2.44 | 2.60 |
    | Average | 1.98 | 3.27 | 5.27 |
    + the improvements obtained by bagging alone (with imputation), and by the full-blown reduced-model approach
    + ReFE consistently improves over both a single model with imputation (positive entries in the ReFE column) and over bagging with imputation.
    + The variance reduction of bagging complements the (partial) reduced modeling.

+ ReFE > reduced-feature modeling:
    + the substantially lower computational burden of ReFE as compared to that of reduced modeling
    + $N$ attributes: 
        + Reduced-feature modesling: $(2^N -1)$
        + only $N$ models — one for each attribute



### Larger Ensembles

+ evaluate the performance of bagging with the same number of individual models for any given number of missing features

+ including a larger number of models in each ensemble results in improved performance
for all treatments, for almost all data sets

+ Percentage improvement in accuracy compared to a single model with imputation, for bagging with imputation, ReFE, and bagging with reduced models

    | Data Sets | Bagging with Imputation | Bagging with ReFE | Reduced Model |
    |:----------|----------:|-----:|-----:|
    | Abalone | 0.34 | 0.49 | 0.83 |
    | BreastCancer | 5.10 | 5.89 | 5.15 |
    | Bmg | 7.22 | 7.88 | 8.21 |
    | CalHouse | 2.66 | 7.10 | 8.47 |
    | Car | -0.10 | -0.08 | 17.55 |
    | Coding | 14.39 | 15.28 | 17.65 |
    | Contraceptive | 0.64 | 0.89 | 1.03 |
    | Credit | 4.98 | 6.77 | 9.35 |
    | Downsize | 6.91 | 7.60 | 11.13 |
    | Etoys | 2.95 | 3.35 | 3.48 |
    | Expedia | 3.41 | 4.19 | 5.27 |
    | Move | 6.48 | 9.73 | 13.78 |
    | PenDigits | 0.44 | 0.90 | 1.52 |
    | Priceline | 7.55 | 9.42 | 11.02 |
    | QVC | 4.23 | 5.88 | 7.16 |
    | Average | 4.48 | 5.69 | 8.11 |
    + All ensembles employ 30 models for prediction.


### ReFEs with Increasing Numbers of Missing Values

+ For all data sets, the accuracies of all methods decrease as more attributes are missing at prediction time. 

+ The marginal reductions in accuracy with increasing missing values are similar for ReFE and for bagging with imputation, with ReFE’s advantage diminishing slowly with increasing missing values.

+ ReFE uses imputation to handle additional missing values.

+ While using no more storage space than standard bagging, ReFE offers significantly better performance than imputation and than bagging with imputation for small numbers of missing values and hence provides another alternative for domains where full-blown reduced modeling (and especially reduced modeling with bagging) is impracticably expensive.

+ The ReFE accuracies clearly are between the extremes, trading off accuracy and storage/computation.


## Related Work

+ Theoretical analysis
    + most related work: [34] within the PAC framework [35]
    + attribute blocking process [34]: attribute values are not available at induction time
    + Strategies:
        + value imputation (simple default-value imputation in their paper)
        + distribution-based prediction
        + a reduced-feature "classifier lattice" of models for all possible patterns of missing values
    + reduced-feature modeling is the only technique that is unconditionally consistent for MCAR
    + expose the learner to the specific pattern of missing values observed in a test instance (reduced modeling), rather than to "fill in" a missing value

+ Empirical analysis
    + the challenge of induction from incomplete training data [32, 6, 33, 1, 8, 12, 13]
    + an explicit probabilistic model and a parameter estimation procedure and present a framework for handling missing values during induction when mixture models are estimated from data [13]
    + joint treatments for induction and prediction with missing nominal feature values [31]
    + two forms of imputation similar to those explored here [31]
    + classification by simply using the first tree node for which the feature is missing (treating it as a leaf) [31]
    + no solution dominates across domains [31]
    + C4.5’s DBI seems to perform best more often and hence the paper recommends its use. [31]
    + Hybrid model: Predictive value imputation often is superior to C4.5’s DBI.
    + the dominance of one form of imputation versus another depends on the statistical dependencies (and lack thereof) between the features: value imputation is likely to outperform C4.5’s DBI when feature imputability is particularly high, and vice versa.

+ Protos [29]
    + heuristic classification technique for weak-theory domains
    + Protos, ID3, and another exemplar-based program to a medical diagnosis problem where more than $50\%$ of the test feature values are missing
    + missingness depends on the feature values
    + ID3 with various imputation techniques performed poorly.

+ Lazy classification trees [9]
    + an instance of run-time reduced modeling
    + single classification-tree paths that are tailored for classifying a particular test instance w/o incorporating any missing features
    + the performance of lazy tree induction to be superior to C4.5’s technique w/ missing values
    + avoiding any tests on unknown values is the correct thing to do probabilistically, assuming the values are truly unknown...
    + C4.5’s technique particular difficulty when feature imputability is high
    + reduce the total costs of feature-value acquisitions and of misclassifications [21]

+ Co-training [3]
    + alternative predictive patterns in the training data
    + the frequent availability of such alternative predictive patterns
    + exploited to induce alternative hypotheses.
    + an induction technique based on the assumption
        + the feature set comprises two disjoint subsets such that each is sufficient to induce a classifier
        + the features in each set are not highly correlated with those of the other conditional on the class
    + E.g., a page can be represented by its content or by the words occurring in hyperlinks that point to that page
    + often successful because alternative representations are rather common [26]
    + a random partition usually produces two sets that are each sufficient for accurate classification
    + Accurate reduced models can frequently be induced in practice and offer an alternative that consistently is at least comparable to and usually superior to popular treatments.



## Limitations

+ The performance of missing-value treatments for inducing classification trees seems unrelated to the Little and Rubin taxonomy [7]

+ MCAR scenario [34]: a completely arbitrary function of an example’s values and non consistent

+ MAR scenario [22]: conditioned only on observed values

+ reduced modeling w/ MAR

+ MNAR scenario: may be useful subclasses

+ C4.5’s DBI is not based on an estimation of the full, joint distribution—the lack of which is the basis for the pathology. 

+ Full-joint methods also have practical drawbacks:
    + very expensive computationally
    + intractable for large problems
    + awkward for practitioners (and for researchers)

+ naive Bayes marginalizes simply by ignoring attributes with missing values

+ results not limited a particular imputation model


## Conclusions

+ Reduced-feature models:
    + preferable both to C4.5’s distribution-based imputation and to predictive value imputation
    + undertake a lower-variance learning task
    + not fall prey to certain pathologies
    + easily applied w/ predictive value imputation and C4.5’s DBI
    + w/ suboptimal accuracy almost always

+ Selection of imputation
    + based level of feature imputability, by theoretical arguments and by empirical results
    + A lack of feature imputability is problematic for any imputation.
    + C4.5’s weighted averaging reduces estimation variance and thereby leads to more accurate estimation.
    + High feature imputability increases the effective bias of C4.5’s technique, but of course is ideal for predictive value imputation.
    + The performance of reduced-feature modeling is indistinguishable from that of predictive value imputation.
    + Reduced-feature modeling is substantially more robust as the level of feature imputability decreases.
    + Suboptimal: the consistency and magnitude of their negative impact.

+ Reduced model & ReFE
    + reduced model: expensive either in terms of run-time computation or storage
    + ReFE: manage the tradeoff between computation and storage needs or between efficiency and accuracy
    + Storage allocation:
        + see the most use or provide the most utility
        + run-time computation applied for unlikely or less useful missing-data patterns
        + allocated to the most advantageous reduced models
    + The full accuracy of reduced modeling is maintained but both storage and run-time requirements are reduced from their extremes.
    + Accuracy is traded off for decreased storage and/or run time.
    + ReFE: ensemble methods modified to help deal with missing values


## Reference

1. Gustavo E. A. P. A. Batista and Maria Carolina Monard. An analysis of four missing data treatment methods for supervised learning. Applied Artificial Intelligence, 17(5-6):519–533, 2003.
1. E. Bauer and R. Kohavi. An empirical comparison of voting classification algorithms: Bagging, boosting and variants. Machine Learning, 36(1-2):105–139, 1999.
1. A. Blum and T. Mitchell. Combining labeled and unlabeled data with co-training. In Proc. of the 11th Annual Conf. on Computational Learning Theory, pages 92–100, Madison, WI, 1998.
1. L. Breiman. Bagging predictors. Machine Learning, 24(2):123–140, 1996.
1. L. Breiman, J. H. Friedman, R. Olshen, and C. Stone. Classification and Regression Trees. Wadsworth and Brooks, Monterey, CA, 1984.
1. A. P. Dempster, N. M. Laird, and D. B. Rubin. Maximum likelihood from incomplete data via the EM algorithm. Journal of the Royal Statistical Society B, 39:1–38, 1977.
1. Y. Ding and J. Simonoff. An investigation of missing data methods for classification trees. Working paper 2006-SOR-3, Stern School of Business, New York University, 2006.
1. A. J. Feelders. Handling missing data in trees: Surrogate splits or statistical imputation? In Principles of Data Mining and Knowledge Discovery, pages 329–334, Berlin / Heidelberg, 1999. Springer. Lecture Notes in Computer Science, Vol. 1704.
1. J. H. Friedman, R. Kohavi, and Y. Yun. Lazy decision trees. In Howard Shrobe and Ted Senator, editors, Proceedings of the Thirteenth National Conference on Artificial Intelligence and the Eighth Innovative Applications of Artificial Intelligence Conference, pages 717–724, Menlo Park, California, 1996. AAAI Press.
1. N. Friedman and M. Goldszmidt. Learning Bayesian networks with local structure. In Proc. of 12th Conference on Uncertainty in Artificial Intelligence (UAI-97), pages 252–262, 1996.
1. L. Getoor, N. Friedman, D. Koller, and B. Taskar. Learning probabilistic models of link structure. Journal of Machine Learning Research, 3:679–707, 2002.
1. Z. Ghahramani and M. I. Jordan. Supervised learning from incomplete data via the EM approach. In Advances in Neural Information Processing Systems 6, pages 120–127, 1994.
1. Z. Ghahramani and M. I. Jordan. Mixture models for learning from incomplete data. In R. Greiner, T. Petsche, and S.J. Hanson, editors, Computational Learning Theory and Natural Learning Systems, volume IV, pages 7–85. MIT Press, Cambridge, MA, 1997.
1. R. Greiner, A. J. Grove, and A. Kogan. Knowing what doesn’t matter: Exploiting the omission of irrelevant data. Artificial Intelligence, 97(1-2):345–380, 1997a.
1. R. Greiner, A. J. Grove, and D. Schuurmans. Learning Bayesian nets that perform well. In The Proceedings of The Thirteenth Conference on Uncertainty in Artificial Intelligence, pages 198–207, 1997b.
1. Herskovits E. H. and Cooper G. F. Algorithms for Bayesian belief-network precomputation. In Methods of Information in Medicine, pages 362–370. 1992.
1. T. Hastie, R. Tibshirani, and J. Friedman. The Elements of Statistical Learning. Springer Verlag, New York, August 2001.
1. D. Heckerman, D. M. Chickering, C. Meek, R. Rounthwaite, and C. M. Kadie. Dependency networks for inference, collaborative filtering, and data visualization. Journal of Machine Learning Research, 1:49–75, 2000.
1. R. Kohavi and G. H. John. Wrappers for feature subset selection. Artificial Intelligence, 97(1-2): 273–324, 1997.
1. N. Landwehr, M. Hall, and E. Frank. Logistic model trees. Machine Learning, 59(1-2):161–205, 2005.
1. C. X. Ling, Q. Yang, J. Wang, and S. Zhang. Decision trees with minimal costs. In Proc. of 21st International Conference on Machine Learning (ICML-2004), 2004.
1. R. Little and D. Rubin. Statistical Analysis with Missing Data. John Wiley & Sons, 1987.
1. C. J. Merz, P. M. Murphy, and D. W. Aha. [Repository of machine learning databases](http://www.ics.uci.edu/˜mlearn/mlrepository.html). Department of Information and Computer Science, University of California, Irvine, CA, 1996.
1. J. Neville and D. Jensen. Relational dependency networks. Journal of Machine Learning Research, 8:653–692, 2007.
1. A. Niculescu-Mizil and R. Caruana. Predicting good probabilities with supervised learning. In Proc. of 22nd International Conference on Machine Learning (ICML-2005), pages 625–632, New York, NY, USA, 2005. ACM Press. ISBN 1-59593-180-5.
1. K. Nigam and R. Ghani. Understanding the behavior of co-training. In Proc. of 6th Intl. Conf. on Knowledge Discovery and Data Mining (KDD-2000), 2000.
1. B. Padmanabhan, Z. Zheng, and S. O. Kimbrough. Personalization from incomplete data: what you don’t know can hurt. In Proc. of 7th Intl. Conf. on Knowledge Discovery and Data Mining (KDD-2001), pages 154–163, 2001.
1. C. Perlich, F. Provost, and J. S. Simonoff. Tree induction vs. logistic regression: a learning-curve analysis. Journal of Machine Learning Research, 4:211–255, 2003. ISSN 1533-7928.
1. B. W. Porter, R. Bareiss, and R. C. Holte. Concept learning and heuristic classification in weaktheory domains. Artificial Intelligence, 45:229–263, 1990.
1. J. R. Quinlan. Unknown attribute values in induction. In Proc. of 6th International Workshop on Machine Learning, pages 164–168, Ithaca, NY, June 1989.
1. J. R. Quinlan. C4.5: Programs for Machine Learning. Morgan Kaufmann, San Mateo, CA, 1993.
1. D. B. Rubin. Multiple imputation for nonresponse in surveys. JohnWiley & Sons, New York, 1987.
1. J.L. Schafer. Analysis of Incomplete Multivariate Data. Chapman & Hall, London, 1997.
1. D. Schuurmans and R. Greiner. Learning to classify incomplete examples. In Computational Learning Theory and Natural Learning Systems IV: Making Learning Systems Practical, pages 87–105. MIT Press, Cambridge MA, 1997.
1. L. G. Valiant. A theory of the learnable. Communications of the Association for Computing Machinery, 27(11):1134–1142, 1984.
1. I. H. Witten and E. Frank. Data Mining: Practical Machine Learning Tools and Techniques with Java Implementations. Morgan Kaufmann, San Francisco, 1999.
