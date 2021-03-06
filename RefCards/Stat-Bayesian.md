# Bayesian Approaches

## Overview

+ [Two competing philosophies of statistical analysis](../Notes/a05-Bayesian.md#notes)
  + the frequentist
  + the Bayesian

+ [Bayesian methods](../Notes/a05-Bayesian.md#notes)
  + based on the idea of unknown quantities w/ probability distributions
  + unknown quantities including population means and proportions
  + prior knowledge / belief
    + the probability distribution proportion
    + the knowledge from data before knowing it

+ [Frequentist vs Bayesian methods](../Notes/a05-Bayesian.md#notes)
  + frequentist methods
    + the population value: fixed, unvarying (but unknown) quantity
    + w/o a probability distribution
    + calculating confidence intervals for the quantity or significance tests of hypotheses concerning it
  + Bayesian methods
    + not allowing to widen knowledge of the problem
    + not providing what researchers seem to want
    + able to provide
      + the probability of the 95% of the population value lies within the 95% CI
      + the probability of truth of the null hypothesis less than 5% $\to p(H_0 = \text{true}) < 5\%$

+ [Issues of the Bayesian methods](../Notes/a05-Bayesian.md#notes)
  + how to decide on the prior distribution
  + intractable computational problems
  + choice of Bayesian or frequentist: unknown which existed

+ [Conclusions for computational issue](../Notes/a05-Bayesian.md#notes)
  + developing computer intensive methods of analysis
  + new approaches to very difficult statistical problems, such as the location of geographical clusters of cases of a disease
  + a change in the statistical paradigm

+ [The Bayesian approach](../Notes/p01-Bayesian.md#31-subjectivity-and-context)
  + resting on an essentially _subjective_ interpretation of probability
  + allowed to express generic _uncertainty_ or _degree of belief_ about any unknown but potentially observable quantity
  + rules of probability
    + not assumed as self-evident
    + able to derived from 'deeper' axioms of reasonable behavior of an individual
  + probabilities _for_ events rather than probabilities _of_ events
  + a reflection of personal uncertainty rather than necessarily being based on future unknown events

+ Bayesian statistics: treating subjectivity with respect by placing it in the open and under the control of the consumer of data

+ [Subjectivity](../Notes/p03-BayesianBasics.md#1-introduction)
  + Bayesian statistical methods criticized as being subjective
  + Bayesian inferential framework: a logical foundation in data analysis to accommodate
    + objective (by modeling observed data)
    + subjective (by using prior distribution for parameter)
  + classical (frequentist) statistical methods: not objective as often as claimed in practice
  + non-parametric methods: not completely objective
  + assumptions built around any scientific methods $\implies$ subjective
  + validating assumptions w/ sensitivity analysis


## School of Bayesian Approaches

+ [Four broad levels of increasing 'purity' of Bayesians](../Notes/p01-Bayesian.md#320-schools-of-bayesians)
  + the empirical Bayes approach
  + the reference Bayes approach
  + the proper Bayes approach
  + the decision-theoretic or 'full' Bayes approach

+ [Fundamental importance of concepts to distinguish Bayesian and conventional models](../Notes/p01-Bayesian.md#320-schools-of-bayesians)
  + coherence of probability statements
  + exchangeability
  + the likelihood principle




## Reporting

+ [Checklist of Bayesian assessments of health-care intervention](../Notes/p01-Bayesian.md#321-a-bayesian-checklist)
  + Background
    + the intervention
    + aim of study
  + Methods
    + study design
    + outcome measure
    + statistical model
    + prospective Bayesian analysis?
    + prior distribution
    + loss function or demand
    + computation/software
  + Results
    + evidence from study
  + Interpretation
    + Bayesian interpretation
      + clearly summarizing the posterior distribution
      + describing the formal or informal loss function and the results
      + current summary for immediate action
    + sensitivity analysis: the results of any alternative prior and/or expressions of the consequences of decisions
    + comments:  including an honest appraisal of the strengths and possible weaknesses of the analysis

+ [Example 4](../Notes/p01-Bayesian.md#37-bayesian-analysis-with-normal-distributions) -- SBP: Bayesian analysis for normal data

+ [Example 6](../Notes/p01-Bayesian.md#38-point-estimation-interval-estimation-and-interval-hypotheses) -- GREAT (continue): Bayesian analysis of a trial of early thrombolytic therapy

+ [Example 13](../Notes/p01-Bayesian.md#317-multiplicity-exchangeability-and-hierarchical-models) -- Magnesium: Meta-analysis using a skeptical prior




## Modeling for Bayesian Approaches

+ [Task, Notations and Assumptions](../Notes/p03-BayesianBasics.md#1-introduction)
  + experimental goal: to infer about plausible value(s) of the parameter vector $\theta$
  + $Y = (y_1, y_2, \dots, y_n)$: observed response data
  + making inference about such hidden cause(s), $\theta$, based on observing the effect(s), $y$
  + $p(y|\theta)$: a conditional density of the observation $y$ defined on the _sample space_ $\mathbb{Y}$; the _sampling density_ of $y$ given $\theta$
  + $p(\theta)$: the marginal density of $\theta$ to be the _prior density_ of $\theta$ defined on the _parameter space_ $\Theta$
  + actual determination of the prior density = the determination of the sampling density $p(y|\theta)$
  + $\{f(y|\theta): \theta \in \Theta\}$: the parametric class of sampling densities
  + assumption: the specific form of $p(\cdot | \theta)$ completely known once $\theta$ determined
  + assumption: $\Theta \subseteq \mathbb{R}^m$; i.e. finite-dimensional _parametric space_

+ [Bayes model](../Notes/p03-BayesianBasics.md#11-the-bayes-rule)
  + scalar form

      \[ p(\theta|y) = \frac{p(y|\theta) p(\theta)}{\int p(y|\theta)p(\theta)d\theta} = \frac{p(y|\theta)p(\theta)}{m(y)} \tag{Model.1} \]

  + vector form

      \[ p(\theta|Y) = \frac{p(Y|\theta) p(\theta)}{\int p(Y|\theta)p(\theta)d\theta} = \frac{p(Y|\theta)p(\theta)}{m(Y)} \]

  + independently and identically distributed (iid) observations
    + general: $\exists\; p_i(y_1, \dots, y_{i-1}, \theta)$ of $y_i$ given $y_1, \dots, y_{i-1}$ and $\theta$ for $i=2, 3, \dots, n \implies f(Y|\theta) = p_1(y_1|\theta) \prod_{i=1}^n p(y_i|\theta)$
    + vector form: replacing $p(y|\theta)$ by $p(Y|\theta)$ for (Eq.Model.1)
  + summary

    \[\begin{array}{ll}
      \text{prior density for } \theta: & p(\theta) \\
      \text{sampling density of } y \text{ given } \theta: & p(y|\theta) \\
      \text{marginal density of } y: & m(y) = \int p(y|\theta)p(\theta) d\theta \\
      \text{posterior density of } \theta \text{ given } y: & p(\theta | y) = p(y|\theta)/m(y)
    \end{array}\]

+ [Kernel functions](../Notes/p03-BayesianBasics.md#11-the-bayes-rule)
  + prior kernel function

    \[ p(\theta) = C \cdot k(\theta \]

  + likelihood function

    \[ p(Y|\theta) =  C(Y)\mathcal{L}(\theta; Y) \]

  + posterior kernel function

    \[ K(\theta; Y) = \mathcal{L}(\theta; Y) k(\theta) \tag{2} \]

+ [Example: vitamin C cure within a week (cont.)](../Notes/p03-BayesianBasics.md#6-examples)





## Prior Distribution

+ [The prior distribution](../Notes/p01-Bayesian.md#31-subjectivity-and-context)
  + the prior probability of a random event or an uncertain proposition: the unconditional probability assigned before any relevant evidence is taken into account
  + methods to create prior
    + determined from past information, such as previous experiments
    + elicited from the purely subjective assessment of an experienced expert
    + (uninformative) created to reflect a balance among outcomes when no information is available
    + chosen according to some principle, such as symmetry or maximizing entropy given constraints
    + (conjugate) chosen a prior from a family simplifies calculation of the posterior distribution

+ [Characteristics of prior](../Notes/p01-Bayesian.md#39-the-prior-distribution)
  + not necessarily specified beforehand
  + not necessarily unique
  + not necessarily completely specified
  + not necessarily important





## Improper Prior

+ [Improper prior](../Notes/p03-BayesianBasics.md#11-the-bayes-rule)
  + def: prior kernel function $k(\theta) \geq 0$ for which $\int C \cdot k(\theta) d\theta  = \infty$
  + using improper prior $p(\theta) = C \cdot k(\theta) \implies$ verifying the posterior kernel finitely integrable $\int K(\theta; Y) d\theta < \infty$ for almost all $Y$
  + Applying Fubini's theorem (on interchanging order of integration)
  + __Lemma__: If the likelihood function is bounded below, i.e., $\inf_\theta \mathcal{L}(\theta; Y) \geq \mathcal{L}_0(Y)$ for some $\mathcal{L}_0(Y) >0 \implies$ any improper prior leads to an improper posterior
  + the posterior distribution not necessary proper if the prior improper
  + improper priors not true probability distributions



## Prior with Conjugate Family

+ [Prior conjugate family](../Notes/p03-BayesianBasics.md#11-the-bayes-rule)
  + conjugate family: prior densities and their leading posterior densities belonging to the same family
  + the choice of conjugate family not unique
  + exponential family of densities: sampling density w/ a sufficient statistic of constant dimension always finds a conjugate family of prior densities
  + _natural conjugate family_:
  + _subjective prior of informative prior_: the parameters of the prior density elicited using a previously collected data or expert knowledge
  + _noninformative prior_: no such prior information available or very little knowledge available about the parameter $\theta$





## The Likelihood

+ [Likelihood function / likelihood](../Notes/p01-Bayesian.md#31-subjectivity-and-context)
  + measuring the goodness of fit of a statistical model to a sample of data for given values of the unknown parameters
  + describing a hypersurface whose peak represents the combination of model parameter values that maximize the probability of drawing the sample obtained
  + maximum likelihood estimation: a procedure for obtaining the arguments of the maximum of the likelihood function
  + Definition of a parameterized model: the likelihood function

      \[ \theta \to f(x | \theta) \implies \mathcal{L}(\theta | x) = f(x | \theta) \tag{Likelihood} \]

  + Definition for continuous distribution

    \[\text{argmax}_\theta \mathcal{L}(\theta, x_j) = \text{argmax}_\theta f(x_j | \theta) \]
  + using likelihoods to generate estimators $\to$ the maximum likelihood estimator

+ [Likelihoods](../Notes/p01-Bayesian.md#31-subjectivity-and-context)
  + statistical inference:
    + learning about the assumed underlying distribution of quantities observed
    + generally carried out by assuming that the probability distributions follow a particular _parametric_ form $p(y | \theta)$
    + the distribution of $Y$ depends on some currently unknown parameter $\theta$
  + Bayesian inference: considered as random variables but the usual convention of capital and lower-case letters is ignore, to no apparent detriment
  + likelihood $p(Y | \theta)$:
    + once data $y$ observed, a function of $\theta \to$ extend to which different values $\theta$ are supported by the data
    + summarizing all the information that the data $y$ able to provide about the parameter $\theta$
  + any function of $\theta$ proportional to $p(y|\theta)$ can be considered as the likelihood
  + likelihood function: the relative plausibility of different values of $\theta$
  + maximum likelihood estimate: with the value of $\theta$ for which the likelihood is a maximum
  + using a range of values which are _best_ supported by the data as an interval estimate for $\theta$
  + a reasonable range defined by values of the likelihood above $\exp(-1.96^2/2) = 14.7\%$ of the maximum value
  + in practice, constructing intervals in such a manner is laborious, and in general approximate likelihood functions by the normal distribution
  + example: Bernoulli



## Posterior Distribution

+ [The posterior distribution](../Notes/p01-Bayesian.md#31-subjectivity-and-context)
  + a way to summarize what we know about uncertain quantities in Bayesian analysis
  + summarizing what you know after the data has been observed

    \[ \text{Posterior Distribution} = \text{Prior Distribution} + \text{Likelihood Function (“new evidence”)} \]

  + Posterior probability: the probability that an event will happen after all evidence or background information has been taken into account

+ [The posterior density](../Notes/p03-BayesianBasics.md#11-the-bayes-rule)
  + representation w/ kernel functions

    \[ p(\theta|Y) = \frac{K(\theta; Y)}{\int K(\theta; Y) d\theta} = \frac{\mathcal{L}(\theta; Y) k(\theta)}{\int \mathcal{L}(\theta; Y) k(\theta) d\theta} \]

  + Bayesian Mantra: posterior is proportional to likelihood times prior kernel

    \[p(\theta|Y) \propto \mathcal{L}(\theta; Y) k(\theta) \]




## The Likelihood Principles

+ [The likelihood principle](../Notes/p01-Bayesian.md#31-subjectivity-and-context)
  + proposition: given a statistical model, all the evidence in a sample relevant to model parameters is contained in the likelihood function
  + all the information that the data provides about the parameter is contained in the likelihood
  + data only influence the relative plausibility of an alternative hypothesis through the relative likelihood
  + Bayesian inference automatically obeys this principle
  + example -- Stopping: The likelihood principle in action

+ [The likelihood principle](../Notes/p01-Bayesian.md#33-comparing-simple-hypotheses-likelihood-ratios-and-bayes-factors)
  + the likelihoods contains all the relevant that can be extracted from the data
  + all the information that the data provide about the parameter is contained in the likelihood

+ [Calibration of Bayes factor](../Notes/p01-Bayesian.md#33-comparing-simple-hypotheses-likelihood-ratios-and-bayes-factors) (likelihood ratio)

  <table style="font-family: arial,helvetica,sans-serif;" table-layout="auto" cellspacing="0" cellpadding="5" border="0" align="center" width=50%>
    <caption style="font-size: 1.5em; margin: 0.2em;"><a href="http://www.medicine.mcgill.ca/epidemiology/hanley/bios602/Bayes/an%20overview%20of%20the%20Bayesian%20approach.pdf">Calibration of Bayes factor (likelihood ratio)</a></caption>
    <thead>
    <tr>
      <th style="text-align: center; background-color: #3d64ff; color: #ffffff; width:20%;">Bayes factor range</th>
      <th style="text-align: center; background-color: #3d64ff; color: #ffffff; width:40%;">Strength of evidence in favour of $H_0$ and against $H_1$</th>
    </tr>
    </thead>
    <tbody>
    <tr style="text-align: center;"> <td> > 100 / < 1/100</td>       <td>Decisive</td> </tr>
    <tr style="text-align: center;"> <td>32 to 100 / 1/32 to 1/100</td>    <td>Very strong</td> </tr>
    <tr style="text-align: center;"> <td>10 to 32 / 1/10 to 1/3.2</td>     <td>Strong</td> </tr>
    <tr style="text-align: center;"> <td>3.2 to 10 1/3.2 to 1/10</td>     <td>Substantial</td> </tr>
    <tr style="text-align: center;"> <td>1 to 3.2 / 1 to 1/3.2</td>      <td>'Not worth more than a bare mention'</td> </tr>
    </tbody>
  </table>

+ Use of Bayes theorem: general statistical analysis
  + a parameter $\theta$ is an unknown quantity such as the mean benefit of a treatment on a specified patient
  + the prior distribution $p(\theta)$ needs to be specified
  + concern: a natural extension of the subjective interpretation of probability




## Odds Ratios

+ [Odds ratios](../Notes/a06-OddsRatios.md#what-is-an-odds-ratio) (OR)
  + Def: A measure of association btw an exposure and an outcome
  + the odds that an outcome will occur given a particular exposure, compared to the odds of the outcome occurring in the absence of that exposure
  + most commonly used in case control studies
  + able to be used in cross-sectional and cohort study designs
  + example: logistic regression

+ [Usage of OR](/Notes/a06-OddsRatios.md#when-is-it-used)
  + used to compare
    + the relative odds of the occurrence of the outcome of interest, eg, disease or disorder
    + given exposure to the variable of interest, eg, health characteristics, aspect of medical history
  + used to determine whether a particular exposure is a risk factor for a particular outcome, and to compare the magnitude of various risk factors for that outcome
    + $OR = 1$: exposure not affecting odds of outcomes
    + $OR > 1$: exposure associated w/ higher odds of outcome
    + $OR < 1$: exposure associated w/ lower odds of outcome

+ [confidence interval of OR](/Notes/a06-OddsRatios.md#what-about-confidence-intervals)
  + 95% confidence interval (CI): used to estimate the precision of the OR
    + large CI  $\implies$ low level of precision of the OR
    + small CI $\implies$ higher precision of the OR
  + 95% CI not measuring statistical significance
  + used as a proxy for the presence of statistical significance if not overlap the null value (eg, $OR=1$)
  + inappropriate to interpret OR w/ 95% CI that spans the null value as indicating  evidence for lack of association btw the exposure and outcome

+ [confounding](/Notes/a06-OddsRatios.md#confounding)
  + Def: non-casual association observed btw a given exposure, outcome as a result of the influence of a third variable
  + confounding variable: the third variable
    + causally associated w/ the outcome of interest
    + non-causally or causally associated w/ the exposure
    + not an intermediate variable in the causal pathway btw exposure and outcome
  + methods to address confounding
    + stratification: fixing the level of confounders and producing groups within which the confounder does not vary
    + multiple regression: adjusting for (accounting for) potentially confounding variables in the model

+ [Example: case control study](/Notes/a06-OddsRatios.md#example)





## Bayes Factor (BF)

+ [Bayes factor](../Notes/p01-Bayesian.md#33-comparing-simple-hypotheses-likelihood-ratios-and-bayes-factors) (BF)
  + measure of the relative likelihood of two hypotheses
  + small values being considered as both evidence _against_ $H_0$ and evidence _for_ $H_1$
  + transforming prior to posterior odds

+ [Bayesian factor](../Notes/p03-BayesianBasics.md#3-hypothesis-testing)
  + def: the ratio of posterior odds to prior odds
  + used to choose btw two hypotheses
  + the BF of $H_a$ to $H_0$

    \[\begin{align*}
      BF(Y) &= BF(a|0) = \frac{\Pr(\theta \in \Theta_a | Y)/\Pr(\theta \in \Theta_0 | Y)}{\Pr(\theta \in \Theta_a)/\Pr(\theta \in \Theta_0)} \\\\
       &= \frac{\int_{\Theta_a} K(\theta; Y) d\theta}{\int_{\Theta_0} K(\theta; Y) d\theta} \cdot \frac{\int_{\Theta_0} k(\theta)d\theta}{\int_{\Theta_a} k(\theta) d\theta} \tag{8}
    \end{align*}\]

  + rule to choose btw the two hypotheses

    \[\text{Reject } H_0 \iff \log\left(BF(Y)\right) > 0  \tag{9}\]

  + equal-probable prior: $\Pr(\theta \in \Theta_0) = \Pr(\theta \in \Theta_a)$ or $\int_{\Theta_0} k(\theta) d\theta = \int_{\Theta_a} k(\theta) d\theta$





## Exchangeability

+ [Exchangeability](../Notes/p01-Bayesian.md#34-exchangeability-and-parametric-modeling)
  + a formal expression of the idea that no systematic reason to distinguish the individual variables $Y_1, \dots, Y_n$ (similar but not identical)
  + exchangeable: the probability of $Y_1, \dots, Y_n$ assigned to any set of potential outcomes, $p(y_1, \dots, y_n)$, unaffected by permutations of the labels attached to the variables

+ [Judgment of exchangeability](../Notes/p01-Bayesian.md#34-exchangeability-and-parametric-modeling)
  + a set of binary variables $Y_1, \dots, Y_n$ exchangeable $\implies$ the marginal distribution

    \[ p(y_1, \dots, y_n) = \int \, \prod_{i=1}^{n} p(y_i | \theta) p(\theta) d\theta \tag{3} \]

  + exchangeable random quantities can be though of being i.i.d. variables drawn from some common distribution depending on an unknown parameter $\theta$ w/ a prior distribution $p(\theta)$
  + from a subjective judgment about observable quantities, one derives that whole apparatus of i.i.d. variables, conditional independence, parameters and prior distributions



## Bayesian Analysis

+ [Bayesian approach to make inference](../Notes/p01-Bayesian.md#36-bayesian-analysis-with-binary-data): combining the likelihood w/ initial evidence or opinion regarding $\theta$, as expressed in a prior distribution $p(\theta)$

+ [Prior to posterior analysis](../Notes/p01-Bayesian.md#32-bayes-theorem-for-two-hypotheses)
  + hypotheses $H_0$ and $H_1$: mutually exhaustive and exclusive
  + the prior probability for each of two hypotheses: $p(H_0)$ and $p(H_1)$
  + $y$: the result of a test
  + posterior probabilities:

    \[ p(H_0 | y) = \frac{p(y | H_0)}{p(y)} \times p(H_0)  \tag{1} \]

  + the overall probability of $y$ occurring:
  
    \[p(y) = p(y | H_0) p(H_0) + p(y | H_1) p(H_1) \]

  + the odds form of Bayes theorem

    \[\begin{align*}

      \frac{p(H_0 | y)}{p(H_1 | y)} &= \frac{p(y | H_0)}{p(y | H_1)} \times \frac{p(H_0)}{p(H_1)} \tag{2} \\
    \end{align*}\]

    + the prior odds: $p(H_0)/p(H_1)$
    + the posterior odds: $p(H_0 | y) / p(H_1 | y)$
    + the ratio of the likelihood: $p(y | H_0) / p(y | H_1)$

    \[\begin{align*}
      \text{posterior odds} &= \text{likelihood ratio} \times \text{prior odds} \\ \\
      \log(\text{posterior odds}) &= \log(\text{likelihood ratio}) + \log(\text{prior odds})
    \end{align*}\]

    + the weight of evidence: $\log(\text{likelihood ratio})$

+ [Bayesian approach](../Notes/p01-Bayesian.md#35-bayes-theorem-for-general-quantities)
  + Notations & Assumptions
    + $\theta$: unknown quantity
    + $p(\theta | H)$: the prior distribution of $\theta$; judgment about $\theta$ conditional on a context $H$
    + $y$: some observed evidence
  + $p(y | \theta)$: the (conditional) probability of $y$ for each possible value of $\theta$
  + $p(\theta | y)$: likelihood; to obtain the new, posterior, probability for different $\theta$, taking account of the evidence $y$
  + applying Bayesian theorem to a general quantity $\theta$

    \[ p(\theta | y) = \frac{p(y | \theta)}{p(y)} \times p(\theta)  \tag{4}\]

    + $p(y)$: a normalizing factor to ensure that $\int p(\theta|y)d\theta = 1$ and value not interested
  + the essence of Bayes theorem only concerns the terms involving $\theta$

    \[ p(\theta | y) \propto p(y | \theta) \times p(\theta) \tag{5} \]

  + the posterior distribution proportional to (i.e. has the same shape as) the product of the likelihood and the prior



## Bayesian Analysis w/ Binary Data

+ [Bernoulli distribution](../Notes/p01-Bayesian.md#361-binary-data-with-a-discrete-prior-distribution)
  + only a limited set of hypotheses concerning the true proportional $\theta$, corresponding to a finite list denoted $\theta_1, \dots, \theta_j$
  + the posterior probabilities for the $\theta_j$

    \[ p(\theta_j | y) \propto \theta_j^y (1 - \theta_j)^{1-y} \times p(\theta_j)  \tag{7} \]

    where the normalizing factor that ensures the posterior probabilities add to 1

    \[ p(y) = \sum_j \theta_j^y (1 - \theta_j)^{1-y} \times p(\theta_j) \]

  + the result w/ $r$ 'successes' out of $n$ trials, the relevant posterior

    \[ p(\theta_j | r) \propto \theta_j^r (1 - \theta_j)^{1-y} \times p(\theta_j) \tag{8} \]

+ [Uniform distribution/Notes/p01-Bayesian.md#362-conjugate-analysis-for-binary-data
  + assumption for prior distribution:
    + all possible values of $\theta$ equally likely
    + uniform distribution, $p(\theta) = 1 \, \text{ for } \,0 \leq \theta \leq 1$
  + applying Bayes theorem

    \[ p(\theta | y) \propto \theta^r (1-\theta)^{n-r} \times 1  \tag{9} \]

    + $r$: the number of events
    + $n$: the total number of individuals
  + the functional form of the posterior distribution proportional to a beta distribution: $Beta(r+1, n-r+1)$

+ [Beta distribution/Notes/p01-Bayesian.md#362-conjugate-analysis-for-binary-data): $Beta(a, b)$ for prior distribution
  
  \[\begin{align*}
    \text{Prior} &\propto \theta^{a-1} (1 - \theta)^{b-1} \\
    \text{Likelihood} &\propto \theta^r (1 - \theta)^{n-r} \\
    \text{Posterior} &\propto \theta^{a-1}(1 - \theta)^{b-1} \theta^r (1-\theta)^{n-r} \tag{10} \\
      &\propto \theta^{a+r-1}(1-\theta)^{b+n-r-1} = Beta(a+r, b+n-r)
  \end{align*}\]


+ [Beta-Binomial distribution w/ Bayesian considerations](../Notes/p01-Bayesian.md#3132-predictions-for-binary-data )
  + prior distribution: let $\mu = a/(a+b), M = a+b$

    \[\begin{align*}
      p(\theta | \mu, M) = Beta(M\mu, M(1-\mu)) &= \frac{\Gamma(M)}{\Gamma(M\mu) \Gamma(M(1-\mu))} \theta^{M\mu-1}(1-\theta)^{M(1-\mu)-1} \\\\
      E(\theta | \mu, M) = \mu \qquad & \qquad Var(\theta | \mu, M) = \frac{\mu(1-\mu)}{M-1}
    \end{align*}\]

  + posterior distribution

    \[\begin{align*}
      p(\theta | k) &\propto \underbrace{p(k | \theta)}_{\text{binomial}} \underbrace{p(\theta | \mu, M)}_{\text{beta}} = Beta(k+M\mu, n-k+M(1-\mu)) \\
        &= \frac{\Gamma(M)}{\Gamma(M\mu) \Gamma(M(1-\mu))} \begin{pmatrix} n \\ k \end{pmatrix} \theta^{k+M\mu-1} (1-\theta)^{n-k+M(1-\mu)-1} \\\\
      E(\theta | k) &= \frac{k+M\mu}{n+M}
    \end{align*}\]

  + marginal distribution

    \[\begin{align*}
      p(k | \mu, M) &= \int_0^1 p(k | \theta) p(\theta | \mu, M) d\theta \\\\
        &= \frac{\Gamma(M)}{\Gamma(M\mu)\Gamma(M(1-\mu))} \begin{pmatrix} n \\ k \end{pmatrix} \int_0^1 \theta^{k+M\mu-1}(1-\theta)^{n-k+M(1-\mu)-1} d\theta \\\\
        &= \frac{\Gamma(M)}{\Gamma(M\mu)\Gamma(M(1-\mu))} \begin{pmatrix} n \\ k \end{pmatrix} \frac{\Gamma(k+M\mu)\Gamma(n-k+M(1-\mu))}{\Gamma(n+M)} \\\\
      p(k | a, b) &= \frac{\Gamma(n+1)}{\Gamma(k+1)\Gamma(n-k+1)}\frac{\Gamma(k+a)\Gamma(n-k+b)}{\Gamma(n+a+b)}\frac{\Gamma(a+b)}{\Gamma(a)\Gamma(b)}
    \end{align*}\]



## Bayesian analysis with normal distributions

+ [Normal distribution](../Notes/p01-Bayesian.md#37-bayesian-analysis-with-normal-distributions)
  + the prior distribution $p(\theta)$

    \[ p(\theta) = N \left(\theta \left\vert \mu, \frac{\sigma^2}{n_0}\right.\right) \tag{13} \]

    + $\mu$: the prior mean
    + $\sigma$: the standard deviation for the prior and the likelihood
    + $n_0$: 'implicit' sample size that the prior based on
  + advantages of Eq.13 for prior-to-posterior analysis
    + $n_0 \to 0 \implies \sigma^2 \uparrow$ and the distribution becoming 'flatter'
    + the distribution $\to$ uniform over $(-\infty, \infty)$
    + normal prior w/ a very large variance used to represent a 'non-informative' distribution
  + posterior distribution
    + normal prior distribution: $\theta \sim N(\mu, \sigma^2/n_0)$
    + likelihood: $y_m \sim N(\theta, \sigma^2/m)$
    + posterior distribution obeys

      \[\begin{align*}
        p(\theta|y_m) &\propto p(y_m | \theta) p(\theta) \\
         &\propto \exp \left(-\frac{(y_m - \theta)^2 m}{2\sigma^2} \right) \times \exp \left(-\frac{(\theta - \mu)^2 n_o}{2\sigma^2} \right)
      \end{align*}\]

    + the term involving $\theta$ exactly that arising from a posterior distribution

      \[ p(\theta|y_m) = N \left(\theta \left\vert \frac{n_0\mu + my_m}{n_o + m}, \frac{\sigma^2}{n_0 + m}\right.\right) \tag{14}\]

    + posterior mean $(n_o \mu + m y_m)/(n_o + m)$
      + a weighted average of the prior mean $\mu$ and parameter estimate $y_m$
      + $y_m$ weighted by their precision
    + posterior variance (1/precision)
      + based on an implicit sample size equivalent to the sum of the prior 'sample size' $n_0$ and the sample size of the data $m$
      + when combining sources of evidence from the prior and the likelihood, _adding precisions_ to decrease the uncertainty

+ [General form of normal distribution](../Notes/p01-Bayesian.md#37-bayesian-analysis-with-normal-distributions)
  + general notations:
    + prior distribution: $\theta \sim N(\mu, \tau^2)$
    + likelihood: $y_m \sim N(\theta, \sigma_m^2)$
  + posterior distribution

    \[ p(\theta | y_m) = N \left( \theta \left\vert \frac{\frac{\mu}{\tau^2} + \frac{y_m}{\sigma_m^2}}{\frac{1}{\tau^2}+\frac{1}{\sigma_m^2}}, \frac{1}{\frac{1}{\tau^2}+\frac{1}{\sigma_m^2}} \right.\right) \tag{15} \]



## Point Estimation

+ [Point estimates](../Notes/p01-Bayesian.md#38-point-estimation-interval-estimation-and-interval-hypotheses)
  + traditional measures of location of distribution: mean, median, and mode
  + given a theoretical justification as a point estimate derived from a posterior distribution, by imposing a particular penalty on error in estimation
  + posterior distribution: symmetric and unimodal $\implies$ mean, median, and mode all coincide in a single value and no difficulty in making a choice
  + posterior distribution considerably skewed in some circumstances $\implies$ marked difference btw mean and median

+ [Statistical inference about $\theta$](../Notes/p03-BayesianBasics.md#2-point-estimation)
  + obtained from the posterior kernel
  + posterior density obtained via prior density w/ Bayes rule
  + prior density: $p(\theta | Y) = K(\theta; Y)/ b(Y)$ where $b(Y) = \int K(\theta; Y) d\theta$
  + the normalizing constant $b(Y)$ not required to obtain posterior estimate (via Monte Carlo method)

+ [Modeling the point estimate](../Notes/p03-BayesianBasics.md#2-point-estimation)
  + goal: estimating a special function $\eta = \eta(\theta)$
  + $\theta = (\theta_1, \theta_2, \dots, \theta_m)$: a $m$-dimensional parameter vector
  + point of estimates of $\eta$: mean, median, or mode of the posterior distribution of $\eta$ given $Y$
  + _posterior mean of $\eta$_

    \[ \hat{\eta}(Y) = E[\eta | Y] = E[\eta(\theta) | Y] = \frac{\int \eta(\theta) K(\theta; Y) d\theta}{\int K(\theta; Y) d\theta} \tag{5} \]

+ [Bayes estimator](../Notes/p03-BayesianBasics.md#2-point-estimation)
  + the optimal (Bayes) estimator of $\eta$: the posterior mean of $\eta$ w/ minimized squared error loss

    \[ E[\| \eta - \hat{\eta} \|^2] \leq E[\| \eta - T(Y)\|^2] \]

  + Bayes estimator exists for more general (convex) loss functions, such as weighted squared error loss, asymmetric loss, etc.
  + Bayes estimator expressed in close form as suitable integrals of the posterior kernel
  + advantage: obtained in a straightforward way and expressed in closed form
  + road-block in practice: high-dimensional integrals not an easy task in most situation
  + solution: advent of modern computing




## Region Estimation

+ [Interval estimates](../Notes/p01-Bayesian.md#38-point-estimation-interval-estimation-and-interval-hypotheses)
  + credible interval: any interval containing probability different from a 'Neyman-Pearson' confidence interval
  + types of intervals: assume a continuous parameter $\theta$ w/ range on $(-\infty, \infty)$ and posterior conditional on generic data $y$
    + _one-side intervals_: typical  $x = .90, .95, .99$
    + _two-sided 'equi-tail-area' intervals_: a two-sided $x \cdot 100\%$ (typical 90%, 95%, 99%) interval w/ equal probability in each tail area w/ $(\theta_L, \theta_U)$ where $p(\theta < \theta_L | y) = x/2$ and $p(\theta > \theta_U | y) = 1.0 - x/2$
    + _Highest Posterior Density (HPD) intervals_
      + adjusting: the probability ordinates at each end of the interval are identical $\implies$ the narrowest possible interval containing the required possibility
      + posterior distribution w/ more than one mode $\implies$ HPD may be a set of disjoint intervals
  + HPD interval (Fig. 4)
    + preferable but generally difficult to compute
    + normal distributions: using tables or programs giving tail areas
    + more complicated situation: generally simulating value of $\theta$ and one and two-sided intervals constructed using the empirical distribution of simulated values

    <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
      <a href="http://www.medicine.mcgill.ca/epidemiology/hanley/bios602/Bayes/an%20overview%20of%20the%20Bayesian%20approach.pdf" ismap target="_blank">
        <img src="../Notes/img/p01-04a.png" style="margin: 0.1em;" alt="(a) a symmetric unimodal distribution in which equi-tail-area and HPD intervals coincide at -1.64 to 1.64" title="Fig. 4(a) a symmetric unimodal distribution in which equi-tail-area and HPD intervals coincide at -1.64 to 1.64" height=120>
        <img src="../Notes/img/p01-04b.png" style="margin: 0.1em;" alt="(b) a skewed unimodal distribution in which the equi-tail-area interval is 0.8 to 6.3, whereas the HPD of 0.4 to 5.5 is considerably shorter" title="Fig. 4(b) a skewed unimodal distribution in which the equi-tail-area interval is 0.8 to 6.3, whereas the HPD of 0.4 to 5.5 is considerably shorter" height=120>
      </a>
      <a href="http://www.medicine.mcgill.ca/epidemiology/hanley/bios602/Bayes/an%20overview%20of%20the%20Bayesian%20approach.pdf" ismap target="_blank">
        <img src="../Notes/img/p01-04c.png" style="margin: 0.1em;" alt="(c) a bimodal distribution in which the equi-tail-area interval is -3.9 to 8.6, whereas the HPD appropriately consists of two segments" title="Fig. (c) a bimodal distribution in which the equi-tail-area interval is -3.9 to 8.6, whereas the HPD appropriately consists of two segments" height=150>
      </a>
    </div>

  + traditional confidence intervals vs. Bayesian credible intervals
    1. _interpretation_ - most important
    2. _credible interval_
    3. _care required in terminology_

+ [Interval hypotheses](../Notes/p01-Bayesian.md#38-point-estimation-interval-estimation-and-interval-hypotheses)
  + a hypothesis of interest comprises an interval $H_0: \theta_L < \theta < \theta_U$
  + posterior distribution: $p(H_0 | y) = p(\theta_L < \theta < \theta_U | y)$
  + computed w/ standard formulae or simulation methods

+ [Confidence interval of prior distribution and posterior distribution](../Notes/p01-Bayesian.md#38-point-estimation-interval-estimation-and-interval-hypotheses)
  + the (rather odd) prior belief that all values of $\theta$ were equally likely $\implies p(\theta)$ constant
  + $p(\theta | y) \propto p(y | \theta) \times p(\theta)$: the resulting posterior distribution simply proportional to the likelihood
  + $p(\theta|y_m) = N \left(\theta \left\vert \frac{n_0\mu + my_m}{n_o + m}, \frac{\sigma^2}{n_0 + m}\right.\right)$: equivalent to assuming $n_0 = 0$ in an analysis w/ normal distribution
  + traditional confidence interval: essentially equivalent to a credible interval based on the likelihood alone
  + Bayesian and classical equivalent results w/ a uniform or 'flat' prior
  + 'it is already common practice in medical statistics to interpret a frequentist confidence interval as if it did represent a Bayesian posterior probability arising from a calculation invoking a prior density that is uniform on the fundamental scale of analysis' -- P. Burton, 'Helping doctors to draw appropriate inferences from the analysis of medical studies'

+ [Region estimate](../Notes/p03-BayesianBasics.md#4-region-estimation)
  + credible set: Bayesian tests
    + a subset $R(Y)$ said a $100(1 - \alpha)\%$ _credible set_ for $\theta$ w/ a given value $\alpha \in (0, 1)$

      \[ R = R(Y) \to \Pr(\theta \in R(Y) | Y) \geq 1 - \alpha \]

    + $R = R(Y)$ guarantees that the probability that $\theta$ in $R(Y)$ is at least $1 - \alpha$
  + confidence set: traditional frequentist tests
    + a subset $C(Y)$ said a $100(1-\alpha)\%$ _confidence set_ for $\theta$

      \[ C = C(Y) = \Pr(\theta \in C(Y) | Y) \geq 1 - \alpha \;\;\forall \theta \in \Theta\]

    + $C(Y)$ merely suggests that if the method of computing the confidence set is repeated many times then at least $1 - \alpha$ proportion of those confidence sets would contain $\theta$
    + an observed data vector $Y \to$ the chance that a confidence set $C(Y)$ contains $\theta$ is either 0 or 1
  
+ [Highest Probability Density (HPD) region](../Notes/p03-BayesianBasics.md#4-region-estimation)
  + given a specific level $1-\alpha$ of credible set $R(Y)$
  + _highest probability density_ (HPD) region: the 'smallest' set or region to maintain the given level
  + $R(Y)$ as a HPD region of level $1 - \alpha$, if

    \[ R(Y) = \{\theta \in \Theta: K(\theta; Y) > K_0(Y)\} \tag{10} \]

  + in practice, not straightforward to compute the HPD region $R(Y)$, but numerical method
  + $\eta = \eta(\theta) \in \mathbb{R}$ \to$ the HPD region for $\eta$ may consist of a union of intervals
  + e.g., the posterior density as a bimodal density $\to$ the HPD may be the union of two intervals, each centered around the two modes
  + the posterior density of a real-valued parameter $\eta$ as a unimodal $\to$ the HPD region as an interval of the form

    \[ R(Y) = (a(Y), b(Y)) \subseteq \Theta, \;\; -\infty \leq a(Y) < b(Y) \leq \infty \]




## Hypothesis Testing

+ [Modeling of hypothesis testing](../Notes/p03-BayesianBasics.md#3-hypothesis-testing)
  + deciding which hypothesis w/ a larger probability: reject $H_0 \iff \Pr(\theta \in \Theta_0 | Y) < \Pr(\theta \in \Theta_a | Y)$
  + comparing the numerators to make a decision

    \[ \text{Reject } H_0 \iff \int_{\Theta_0} K(\theta; Y) d\theta < \int_{\Theta_a} K(\theta; Y) d\theta \tag{7} \]

  + a prior distribution ensuring $\Pr(\theta \in \Theta_j) > 0$ for $j=0, a$
  + using a prior distribution which assures  $\Pr(\theta \in \Theta_0) = \Pr(\theta \in \Theta_a)$ unless $\exists$ any substantial prior information about the two hypotheses
  + assume a prior w/ equal-probable hypotheses before observing any data

+ [Errors of hypothesis testing](../Notes/p03-BayesianBasics.md#3-hypothesis-testing)
  + Type I error rate: traditional frequentist methods
    + rule: reject $H_0$ if $T(Y) > T_0 \implies$ the cut-off value $T_0$ chosen $\to$ type I error rate

      \[\inf_{\theta \in \Theta_0} \Pr\left(T(Y) > T_0 | \theta\right) \leq \alpha\]

  + Type II error rate: Bayesian tests
    + type II error rate: (further check required)

      \[\inf_{\theta \in \Theta_a} \Pr(T(Y) \leq T_0 | \theta) \leq \alpha \;\;\forall \theta \in \Theta_a\]

    + alternative test statistic
      + simply report posterior probabilities $\Pr(\theta \in \Theta_j | Y)$ for $j = 0, a$
      + researcher decides a cut-off value, e.g., $p_0 \to H_0$ rejected $\iff \Pr(\theta \in \Theta_a | Y) > p_0$
  + Bayesian type I error rate

    \[ BE_1(T_0) = \Pr(T(Y) > T_0 | \theta \in \Theta_0) \]

  + Bayesian type II error rate

    \[ BE_2(T_0) = \Pr(T(Y) \leq T_0 | \theta \in \Theta_a) \]

  + controlling both types of Bayesian errors: finding a $T_0$ to minimize the the total weight error, i.e., determining

    \[\hat{T}_0 = \arg\min TWE(T_0)\]

  + sample size: $\hat{T}_0$ fixed $\implies$ optimal (minimum) sample size $\to$ $BE_1(\hat{T}_0) + BE_2(\hat{T}_0) \leq \alpha$





## Credibility Test

+ [Credibility in clinical trials](../Notes/p01-Bayesian.md#311-the-credibility-of-significant-trial-results)
  + credibility
    + the beliefability of new findings in the light of current knowledge
    + a key issue in the assessment of clinical trial outcomes
  + Bayesian methods: probability not as idealized long-run frequencies, but as degrees of belief based on all the available evidence
  + extending to ask how skeptical not to find an apparently positive treatment effective convincing
  + prior mean $y_m = 0$, reflecting initial skepticism about treatment difference, w/ the variance of the prior expressing the degree of skepticism with which we view extreme treatment effects, either positive or negative

+ [Bayesian credibility test](../Notes/p01-Bayesian.md#311-the-credibility-of-significant-trial-results)
  + critical prior distribution $\implies$ the corresponding posterior 95% interval including 0
  + observing $y_m >0$, a normal likelihood and prior w/ $\mu = 0$

    \[ \theta \sim N \left( \frac{m y_m}{n_0 + m}, \frac{\sigma^2}{n_0 + m} \right) \]

  + the upper point $u_m$ of the 95% posterior interval

    \[ u_m = \frac{m y_m}{n_0 + m} + 1.96 \frac{\sigma}{\sqrt{n_0 + m}} \]

    $\implies$ the 95% interval will overlap 0 if $u_m > 0$
  + the effective number of events in the skeptical prior leading to a 95% posterior interval including 0 (to simplify w/ equality)

    \[ n_0 > \left( \frac{m y_m}{1.96 \sigma} \right) -m = \frac{m^2}{1.96^2 \sigma^2} \left(y_m^2 - \frac{1.96^2 \sigma^2}{m} \right) \tag{16} \]

  + $l_D$, $u_D$: the lower and upper points of a 95% interval  based on the data alone, respectively

    \[\begin{align*}
      (l_D, u_D) = y_m &\pm 1.96 \sigma / \sqrt{m} \\\\
      (u_d - l_d)^2 = 4 \times 1.96^2 \sigma^2 /m \quad & \quad u_d l_D = y_m^2 - 1.96^2 \sigma^2/m
    \end{align*}\]
  
  + the critical value of $l_0$ occurs when the lower point of the 95% prior interval

    \[ l_0 = \frac{-19.6 \sigma}{\sqrt{n_0}} = - \frac{(u_D - l_D)^2}{4 \sqrt{u_D l_D}} \]

  + $l_D, u_D$ on a $\log(OR)$ scale $\to l_0 = \log(L_0), l_D = \log(L_D), u_D = \log(U_D)$

    \[ L_0 = \exp\left( \frac{-\log^2(U_D/L_D)}{4 \sqrt{\log(U_D) \log(L_D)}} \right) \tag{17} \]

  + $L_0$ and CI
    + the critical value ($L_0$) for the lower end of 95% skeptical interval $\to$ the resulting posterior distribution w/ a 95% interval including 1
    + prior belief in $(L_0, 1/L_0) \implies$ not convinced by the evidence
    + a significant trial _credible_ $\implies$ prior experience indicates that OR lying outside the critical prior interval are plausible
  
+ [Assessment of ‘credibility’ of ORs](../Notes/p01-Bayesian.md#311-the-credibility-of-significant-trial-results)
  + observing a classical 95% interval $(L_D, U_D)$ for an OR
  + $L_0$:
    + the lower end of a 95% prior interval centered on 1 expressing skepticism about large differences
    + the critical value such that the resulting posterior distribution has a 95% interval that just includes 1
    + not producing 'convincing' evidence
  + $OR >> L_0 \implies$ judged plausible based on evidence external to the study
  + the significant conclusions $\nRightarrow$ convincing

  <div style="margin: 0.5em; display: flex; justify-content: center; align-items: center; flex-flow: row wrap;">
    <a href="http://www.medicine.mcgill.ca/epidemiology/hanley/bios602/Bayes/an%20overview%20of%20the%20Bayesian%20approach.pdf" ismap target="_blank">
      <img src="../Notes/img/p01-08.png" style="margin: 0.1em;" alt="Assessment of 'credibility' of odds ratios" title="Assessment of 'credibility' of odds ratios" width=350>
    </a>
  </div>

+ [Applying assessment to GREAT study](..](../Notes/p01-Bayesian.md#311-the-credibility-of-significant-trial-results))
  + 95% classical CI for $\log(OR) = (-1.45, -0.03) \to OR = (0.24, 0.97) \implies L_D = 0.24, U_D = 0.97, L_0 = 0.10$
  + $OR >> 0.1$ as plausible $\to$ the results of the GREAT study w/ caution
  + $L_D, U_D$ and $L_0$ not plausible $\implies$ not finding GREAT result 'credible'
  + characteristic of any 'just significant' results such as those observed in the GREAT trial: just a minimal amount of prior skepticism is necessary to make the Bayesian analysis 'non-significant'

+ [Credibility: Sumartriptan trial results](../Notes/p01-Bayesian.md#311-the-credibility-of-significant-trial-results)
  + interest: the results of an early study of subcutaneous sumatriptan for migraine - Matthews, 2001
  + improvement: 79% w/ sumatriptan vs. 25% w/ placebo
  + 95% of the prior belief within critical interval $\implies$ posterior 95% interval not exclude OR = 1 $\implies$ the data not 'convincing'
  + unreasonable to rule out on prior grounds advantages of greater than 19%, and hence reject the critical prior interval as being unreasonably skeptical, and accept the results as 'credible'



## Nuisance Parameters

+ [Nuisance parameter](../Notes/p01-Bayesian.md#3181-alternative-methods-for-eliminating-nuisance-parameters)
  + a major issue in statistical modeling
  + additional unknown quantities which influence the observed data but which are not of primary interest

+ [Eliminating nuisance parameters from the likelihood](../Notes/p01-Bayesian.md#3181-alternative-methods-for-eliminating-nuisance-parameters)
  + restricting attention to an estimator of $\theta$ whose likelihood (at least approximately) does not depend on the nuisance parameters
  + estimating the nuisance parameters and 'plugging in' their maximum likelihood estimates into the likelihood for $\theta$
  + by conditioning on some aspect of the data that is taken to be uninformative about $\theta$, forming a 'conditional likelihood' which depends only on $\theta$
  + forming a 'profile likelihood' for $\theta$, obtained by maximizing over the nuisance parameters for each value of $\theta$

+ [A more 'pure' Bayesian approach](../Notes/p01-Bayesian.md#3181-alternative-methods-for-eliminating-nuisance-parameters)
  + place prior distributions over the nuisance parameters
  + form a joint posterior distribution over all the unknown quantities in the model
  + integrate out the nuisance parameters to obtain the marginal posterior distribution over $\theta$

+ [Sensitivity analysis](../Notes/p01-Bayesian.md#3181-alternative-methods-for-eliminating-nuisance-parameters)
  + importance: nuisance parameters of prior distributions
  + innocuous choices may exert unintended influence
  + hybrid strategy
    + using traditional methods to eliminate nuisance parameters before carrying out a Bayesian analysis on $\theta$ alone
    + good approximation to the full Bayesian approach





## Result Interpretation

+ [Connections btw Bayes theorem and clinical trials](../Notes/p01-Bayesian.md#310-how-to-use-bayes-theorem-to-interpret-trial-results)
  + known: the prior distribution on $\theta$ should supplement the usual information ($p$-value and CI) which summarizes the likelihood
  + consideration: huge number of clinical trials carried out and finding the few clearly beneficial interventions
  
+ [Types of error](../Notes/p01-Bayesian.md#310-how-to-use-bayes-theorem-to-interpret-trial-results)
  + Type I error ($\alpha$): false positive - the chance of claiming an ineffective treatment is effective
  + Type II error ($\beta$): false negative - the chance of claiming an effective treatment is ineffective
  + the odds of formulation of Bayes theorem, when a 'significant result' observed

    \[\begin{align*}
      \frac{p(H_0 | \text{significant result})}{p(H_1 | \text{significant result})} &= \frac{p(\text{significant result} | H_0)}{p(\text{significant result} | H_1)} \times \frac{p(H_0)}{p(H_1)} \\\\
        &= \frac{p(\text{Type I error})}{1 - p(\text{Type II error})} \times \frac{p(H_0)}{p(H_1)}
    \end{align*}\]

    + $H_0$: ineffective treatment
  + truly effective treatment relative rare $\implies$ a 'statistical significant' result stands a good chance of being a false positive
  + the precise $p$-value / 'significant' and $\alpha$
    + Lee & Zelen (2000): suggested selecting $\alpha$ that the posterior probability of an effective treatment, having observed a significant result, is sufficient high, say above 0.9
    + Simon (2000) and Bryant & Day (2000): criticized solely based on the trail is 'significant', rather than the actual observed data




## Prediction

+ [Prediction w/ Bayes theorem](../Notes/p01-Bayesian.md#3131-predictions-in-the-bayesian-framework)
  + task: predict some future observations $x$ on the basis of currently observed data $y$
  + the distribution $p(x|y)$ ex tended w/ unknown parameters $\theta$ by

    \[ p(x | y) = \int p(x | y, \theta) p(\theta | y) d\theta \]

  + the posterior distribution $p(y | \theta)$
  + $x$ and $y$ conditionally independent given $\theta \implies p(x | y, \theta) = p(x | \theta)$
  + the predictive distribution: the sampling distribution of $x$ averaged over the current beliefs regarding the unknown $\theta$

    \[ p(x | y) = \int p(x|\theta) p(\theta | y) d\theta \]

+ Predictive distribution w/ binary data
  + $\theta$ as the true response rate for a set of Bernoulli trials
  + current posterior distribution of $\theta$ with mean $\mu$
  + observing the next $n$ trials to predict $Y_n$, the number of successes

    \[ E(Y_n) = E_\theta[E(Y_n | \theta)] = E_\theta[n\theta] = n\mu \tag{20} \]

  + the probability that the next observation (n=1) is success equal to $\mu$, the posterior mean of $\theta$

+ Beta-Binomial distribution
  + $\theta$ as a conjugate $Beta(a, b)$
  + the exact predictive distribution for $Y_n$, known as the beta-binomial distribution

    \[ p(y_n) = \frac{\Gamma (a+b)}{\Gamma(a)\Gamma(b)} \begin{pmatrix} n \\ y_n \end{pmatrix} \frac{\Gamma(a+y_n) \Gamma(b+n-y_n)}{\Gamma(a+b+n)} \tag{21} \]

  + w/ $E(\theta) = a/(a+b)$, the mean and variance of the distribution

    \[ E(Y_n) = n \frac{a}{a+b} \]
    \[ Var(Y_n) = \frac{nab}{(a+b)^2} \frac{a+b+n}{(a+b+1)} \tag{22} \]

  + Special cases
    + $a = b = 1$:
      + the current posterior distribution $\sim$ uniform
      + the predictive distribution for the number of successes in the next $n$ trials $\sim$ unifrom $\forall \; n = 0, 1, 2, \dots$
    + predicting the next single observation ($n = 1$), Eq. 21 simplified to a Bernoulli distribution w/ $\mu = a/(a+b)$

+ Uniform distribution
  + a prior for $\theta$ as uniform
  + observing $m$ trials w/ positive, the posterior distribution $\sim$ Beta(m+1, 1)
  + Lapace's law of success: the probability that the event will occur at the next trial is $m/(m+1)$
  + even if an event has happened in every case so far, never completely certain that it will happen at the next opportunity

+ [Normal predictive distribution](../Notes/p01-Bayesian.md#3133-predictions-for-normal-data)
  + likelihood: $Y_n \sim N(\theta, \sigma^2/n)$
  + prior distribution: $\theta \sim N(\mu, \sigma^2/n_0)$
  + predictions on future values of $Y_n$
  + consider $Y_n$ as being the sum of two independent quantities: $(Y - \theta) \sim N(0, \sigma^2/n)$ and $\theta \sim N(\mu, \sigma^2, n_0)$
  + the predictive distribution

    \[ Y_n \sim N \left( \mu, \sigma^2 \left(\frac{1}{n} + \frac{1}{n_0}\right) \right) \tag{23} \]

  + predictions: adding variances $\implies$ increasing uncertainty
  + combining sources of evidence using Bayes theorem $\implies$ increasing precision and decreasing uncertainty
  + observed data $y_m$ and the current posterior distribution $\theta \sim N((n_0\mu+my_m)/(n_o+m), \sigma^2/(n_o+m))$, the predictive distribution

    \[ Y_n|y_m \sim N \left( \frac{n_0\mu+my_m}{n_0+m}, \sigma^2 \left( \frac{1}{n_0+m} + \frac{1}{n} \right) \right) \tag{24} \]


## Decision-Making

+ [Modeling of health-care w/ decision-making](../Notes/p01-Bayesian.md#314-decision-making)
  + the appropriate role for formal decision theory in health-care evaluation -- a subject of a long and continuing debate
  + utility $u(d, \theta)$: the consequences of taking each decision $d$ when $\theta$ is true unknown 'state of nature'
  + $p(\theta | y)$: the probability distribution for $\theta$ w/ observed some data $y$
  + $d$: expected utility of taking decision

    \[ E(d) = \int u(d, \theta) p(\theta | y) d\theta \]
  
  + $d^{opt}$: the optimal decision to maximize $E(d, \theta)$

+ [Hypotheses and decision-making](../Notes/p01-Bayesian.md#314-decision-making)
  + $H_0$ & $H_1$: two hypotheses w/ the unknown 'state of nature'
  + $p(H_0|y)$ & $p(H_1 | y)$: current posterior probabilities w/ $H_0$ and $H_1$ respectively
  + $d_0$ & $d_1$: possible decisions for $H_0$ & $H_1$ respectively, $d_0$ believing $H_0$ true while $d_1$ believing $H_1$
  + $u(d_0, H_0)$ & $u(d_1, H_1)$: the utility of taking decision $d_0$ / $d_1$ where $H_0$ / $H_1$ is true
  + maximizing expected utility by taking decision $d_0$ if $E(d_0) > E(d_1)$

    \[\frac{p(H_0|y)}{p(H_1|y)} &> \frac{u(d_1, H_1) - u(d_0, H_1)}{u(d_0, H_0) - u(d_1, H_0)} \]
  
  + intuitive explanation:
    + $u(d_1, H_1) - u(d_0, H_1)$:
      + the potential _regret_ : the potential loss in utility when erroneously deciding on $H_0$ instead of $H_1$
      + the additional utility involved in taking the correct decision when $H_1$ turns out to be the correct hypothesis
    + $u(d_0, H_0) - u(d_1, H_0)$: the potential _regret_ when $H_0$ is true
    + should only take decision $d_0$ if the posterior odds in favor of $H_0$ are sufficient to outweight any extra potential rgret associated w/ incorrectly rejecting $H_1$

+ [Decision based on future events](../Notes/p01-Bayesian.md#314-decision-making)
  + using the principle of maximizing expected utility based on future events
  + choice of action changing the probability of the events occurring
  + $c_i$: the cost taken at the decision $d_i$
  + $p_i$: the probability of taking decision $d_i$ w/ an adverse event Y = 0 or 1 occuring w/ utility $U_Y$
  + the expected utility of taking decision $i$

    \[ E(d_i) = p_i U_1 + (1-p_i) U_0 - c_i \]

  + $d_0$ preferred to $d_1$ if

    \[ p_1 - p_0 &> \frac{c_0 - c_1}{U_0 - U_1} \tag{26} \]

    + $U_0 - U_1 > 0 \impliedby$ undesirable event
  + the decision depends on the risk difference $p_1 - p_0$, rather than a relative measure such as the odds ratio
  + D. Ashby and A. Smith
    + NNT: the 'number needed to treat' to prevent one adverse event
    + $N(p_1 - p_0)$: the expected number of events prevented when treating $N$ individuals according to $d_0$ instead of $d_1$
    + preventing one event when treating $N = 1/(p_1 - p_0)$

    \[ NNT = \frac{1}{p_1 - p_0} < \frac{U_0 - U_1}{c_0 - c_1} \tag{27} \]

+ [Neural tube defects](../Notes/p01-Bayesian.md#314-decision-making): Making personal decisions about preventative treatment
  + task: a couple wishing to try and become pregnant but faced w/ the decision whether to take folic acid supplements to reduce the risk of a neural tube defect (NTD), such as spina bifida or anencephaly
  + Notations & Assumptions:
    + $d_0$ / $d_1$: the decisions not to take or to take supplementation, respectively
    + $c_0$ / $c_1$: the costs of the two decisions
    + $p_0$ / $p_1$: the probabilities of a fetus having an NTD following each of the two decisions
    + $U_0$ / $U_1$: the utilities of having a child w/o or w/ taking an NTD, respectively
    + $\rho \cdot c = c_1 - c_0$: the cost for a couple deciding whether to take the supplementation; may be in money to pay for a course of tablets
  + the couples choosing supplementation ($d_1$) if (Eq. 26)

    \[ U_0 - U_1 > \frac{c_0 - c_1}{p_1 - p_0} \tag{28} \]

+ [Decision-making and Bayesian methods](../Notes/p01-Bayesian.md#314-decision-making)
  + focused on the utility of consequences than the use of Bayesian methods to revise opinions
  + this activity blends naturally into cost-effectiveness analysis, but nevertheless the subjective interpretation of probability is essential
  + the expressions of uncertainty required for a decision analysis can rarely be based on empirical data

+ [Discussion of using Bayesian methods on decision-making](../Notes/p01-Bayesian.md#314-decision-making)
  + debate on the use of loss functions, the negative of utility, in parallel to that concerning prior distributions
  + arguing the design, monitoring and analysis of a study using the consequences of eventual decision-making w/ loss functions
  + frequentist theory of decision-making using loss functions
    + minimizing the loss whatever the true value of the parameter might be
    + thought of as assuming the most pessimistic prior distribution
    + ideological approaches employing all combinations of the use of prior distributions and/or loss  functions
  + Optimal decision-making
    + depending solely on the expected benefit
    + irrelevance: measures of uncertainty such as intervals or $p$-values




## Hierarchical Models

+ [Modeling for sequential data sets](../Notes/p01-Bayesian.md#312-sequential-use-of-bayes-theorem)
  + $\exists$ two or more segmented observed data, $y_m$ followed by $y_n$
  + the posterior distribution of $y_m$ w/ Bayes theorem (Eq. 5)

    \[ p(\theta | y_m) \propto p(y_m | \theta) \times p(\theta) \tag{18} \]

  + using the posterior distribution as the prior distribution after observing the following data segment, $y_n$
  + the posterior conditioning on all the data

    \[\begin{align*}
      p(\theta | y_n, y_m) & \propto p(y_n | \theta, y_m) p(\theta | y_m)  \tag{19} \\
        & \propto p(y_n | \theta, y_m) p(y_m | \theta) p(\theta)
    \end{align*}\]

  + factorizing the joint likelihood

    \[ p(y_m, y_n | \theta) = p(y_n | \theta, y_m) p(y_m | \theta) \]

  + most situations, $p(y_n | \theta, y_m)$ not depending on $y_m$; i.e. $Y_n$ simply conditionally independent of $Y_m$ given $\theta$
  + $\therefore p(\theta | y_m)$ simply as the prior for a standard Bayesian update using the likelihood $p(y_n | \theta)$

+ [usage of historical data](../Notes/p01-Bayesian.md#316-use-of-historical-data)
  + helping the design of experiments and pooling data in a meta-analysis
  + Bayesian reasoning gives a formal role in many aspects of evaluation
  + a brief taxonomy of ways
    + the deviation of prior distributions
    + the use of historical controls in clinical trials
    + the adjustment of observational studies for potential biases
    + the synthesis of multiple sources

+ [Relationships btw historical data and current observations](../Notes/p01-Bayesian.md#316-use-of-historical-data)
  + irrelevance: no relevant information
  + exchangeable: current and past studies similar
  + potential bias
    + past studies
      + lack of quality (internal bias)
      + setting not precisely measured (external bias)
    + appropriately adjusting historical results
  + equal but discounted
  + functional dependence
  + equal

+ [Assumptions for multiplicity](../Notes/p01-Bayesian.md#317-multiplicity-exchangeability-and-hierarchical-models)
  + different assumptions
    + _identical parameters_: all the $\theta$s identical $\implies$ pooled data w/o individual units
    + _independent parameters_: all the $\theta$s entirely unrelated $\implies$ independent analysis
    + _exchangeable parameters_
      + $\theta$s 'similar': labeling $\theta$ w/ $A, B, \dots$ w/o knowing which is which
      + prior opinion about a set of $\theta$s affected by only knowing the labels rather than the actual identities
      + $Y_1, \dots, Y_n$ random variables w/ 'exchangeable' equivalent
      + exchangeable parameters $\theta_1, \dots, \theta_K \implies$ exchangeable units mathematically equivalent to assuming the $\theta$s drawn at random from some population distribution, as a traditional random-effects model
      + considering a common prior for all units, but one unknown parameter
      + no need for any actual sampling $\impliedby$ the probability structure is a consequence of the belief in exchangability rather than a physical randomization mechanism
      + not normal distribution:
        + heavy-tailed or skewed distributions
        + partition - cluster similar or equal units into groups

+ [Hierarchical / multi-level model](../Notes/p01-Bayesian.md#317-multiplicity-exchangeability-and-hierarchical-models)
  + reasonable assumption: prior distribution w/ exchangeability
  + Bayesian approach to multiplicity $\implies$ integrating all the units into a single model
  + assumptions:
    + $\theta_1, \dots, \theta_K$ drawn from some common distribution w/ unknown parameters
    + normal distribution
  + a response $Y_k$ w/ a normal likelihood

    \[ Y_k \sim N(\theta, s_k^2) \tag{29} \]

+ [Situations of assumptions for hierarchical model](../Notes/p01-Bayesian.md#317-multiplicity-exchangeability-and-hierarchical-models)
  + identical parameters (pooled effect)
    + all the $\theta_k$ identical w/ a common treatment effect $\mu$

      \[ Y_k \sim N(\mu, s_k^2) \]

    + assuming $\mu \sim N(0, \sigma^2/n_0)$ and sequential application of Bayes theorem w/ $s_k^2 = \sigma^2/n_k$, Eq. (14) giving a 'pooled' posterior distribution for $\mu$

      \[ \mu \sim N \left(\frac{\sum_k n_k y_k}{n_0 + \sum_k n_k}, \frac{\sigma^2}{n_0 + \sum_k n_k} \right) \tag{30}\]

      + $\mu$: the posterior mean, an overall sample mean
      + $n_0$: the 'imaginary' observations of $0$, contributed by the prior
      + $n_0 \to 0 \implies$ the prior distribution on $\mu \to$ uniform
    + w/ $n_0 \to 0$ and $s_k^2 = \sigma^2/n_k$

      \[ \mu &\sim N \left( \frac{\sum_k y_k / s_k^2}{\sum_k 1/s_k^2}, \frac{1}{\sum_k 1/s_k^2} \right) \]

      + the posterior mean = the classical pooled estimate $\hat{\mu}$ = the average of the individual estimates w/ inverse variance
    + all the trials measuring the same quantity

      \[Q = \sum_k \frac{n_k}{\sigma^2} (y_k - \hat{\mu})^2 \tag{33} \]

    + absence of a significant $Q \nRightarrow$ homogeneous trials
  + independent parameters (fixed effects)
    + $\theta_k$ estimated totally w/o regard for the others
    + uniform prior for each $\theta_k$ and likelihood $Y_k \sim N(\theta, s_k^2) \implies$ the posterior distribution = the normalized likelihood

      \[ \theta_k \sim N(y_k, s_k^2) \tag{34} \]

  + exchangeable parameters (random effects)
    + $\theta_k$ assumed to be exchangeable w/ a normal distribution: 'hyperparameters', $\mu$ and $\tau^2$, for moment assumed known

      \[ \theta_k \sim N(\mu, \tau^2) \tag{35} \]

    + observing $y_k$, Bayes theorem w/ $B_k = s_k^2/(s_k^2 + \tau^2)$ (the weight given to the prior mean)

      \[ \theta_k | y_k \sim N \left(B_k \mu + (1 - B_k) y_k, (1 - B_k) s_k^2 \right) \tag{36} \]

    + $\tau^2$ value and Eq. (36)
      + $\tau^2 = 0$: a special case of the pooled result, Eq. (32)
      + $\tau^2 = \infty$: a special case of the independent result, Eq. (34)
    + exchangeable model $\implies$ inferences for each unit having narrower intervals than independent ones
    + shrunk towards the prior mean response
      + shrunk $\impliedby$ a degree of pooling depending on the variability btw studies and the precision of the individual study
      + $B_k$ controlling the 'shrinkage' of the estimate towards $\mu$
      + the reduction in the width of the interval for $\theta_k$
      + $B_k = n_0 / ((n_0 + n_k)$ as $s_k^2 = \sigma^2/n_k, \tau^2 = \sigma^2/n_0 \implies$ how the degree shrinkage increasing w/ the relative information in the prior distribution compared to the likelihood
    + empirical Bayes approach
      + unknown hyperparameters $\mu$ and $\tau$ estimated directly from the data
      + avoid specification of prior distribution for $\mu$ and $\tau$
      + not detailing the variety of techniques available as they form part of classical random-effects meta-analysis
    + the 'method-of-moments' estimator

      \[ \hat{\tau}^2 = \frac{Q - (K - 1)}{N - \sum_k n_k^2 / N} \tag{37} \]

      + $Q$: the test for heterogeneity given in Eq. (33)
      + $N = \sum_k n_k$
      + $Q < (K-1) \implies \hat{\tau}^2 = 0$ and complete homogeneity assumed
    + full Bayes approach
      + prior distribution w/ $\mu$ and $\tau^2$
      + taking particular care in the choice of a prior distribution for the between-unit variation $\tau$

+ [Profile likelihood for hierarchical model](../Notes/p01-Bayesian.md#3181-alternative-methods-for-eliminating-nuisance-parameters)
  + the hierarchical model: likelihood and prior distribution

    \[ Y_k \sim N(\theta_k, s_k^2) \qquad\qquad \theta_k \sim N(\mu, \tau^2) \]

  + the hyperparameters $\mu$ and $\tau^2$: generally unknown
  + the predictive distribution of $Y_k$, having integrated out $\theta_k$

    \[ Y_k \sim N(\mu, s_k^2 + \tau^2) \]

  + the precision $w_k = 1/(s_k^2 + \tau^2)$: the 'weight' associated w/ the $k$th study
  + the joint log(likelihood) for $\mu$ and $\tau$: an arbitrary constant plus

    \[ L(\mu, \tau) = -\frac{1}{2} \sum_k \left( (y_k - \mu)^2 w_k - \log w_k \right) \tag{38} \]

  + w/ fixed $\tau$, the conditional maximum likelihood estimator of $\mu$ and variance

    \[\begin{align*}
      \hat{\mu}(\tau) &= \sum_k y_k w_k/\sum_k w_k \tag{39} \\\\
      \hat{\sigma} &= \frac{1}{\sum_k w_k}
    \end{align*}\]

    + applied for the posterior mean and variance of $\mu$ w/ a uniform prior distribution
  + the profile log(likelihood) for $\tau$

    \[ L(\tau) = -\frac{1}{2} \sum_k \left( \left( y_k - \hat{\mu}(\tau) \right)^2 w_k - \log w_k \right) \tag{40} \]

  + plotting log(likelihood) $\implies$ maximizing numerically to obtain the maximum likelihood estimate $\hat{\tau}}$
  + the maximum likelihood estimate $\hat{\tau}$ used to obtain the maximum likelihood estimate of $\mu$ instead of Eq. (39)






