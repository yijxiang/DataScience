# Section 8a: A/B Testing (Lec 8.1 - Lec 8.3)

[Web Notebook](https://hub.data8x.berkeley.edu/user/59d217c894d11dbd21d2d37ef6ae9675/notebooks/materials-x18/lec/x18/2/lec8.ipynb)

[Local Notebook](./notebooks/lec8.ipynb)

[Local Python Code](./notebooks/lec8.py)

## Lec 8.1 Introduction

### Notes

+ Comparing Two Samples
    + Compare values of sampled individuals in Group A with values of sampled individuals in Group B.
    + Question: Do the two sets of values come from the same underlying distribution?
    + Answering this question by performing a statistical test is called __A/B testing.__
+ Two Population Proportions
    + Parameters: $p_1 - p_2$
        + $p_1$: population proportion for the first population
        + $p_2$: population proportion for the second population
    + Statistic/Estimate: $\hat{p}_1 - \hat{p}_2$
    + Standard Error: $\text{s.e.}(\hat{p}_1 - \hat{p}_2) = \sqrt{\frac{\hat{p}_1 (1-\hat{p}_1)}{n_1} + \frac{\hat{p}_2 (1-\hat{p}_2)}{n_2}}$
    + Confidence interval: $(\hat{p}_1 - \hat{p}_2) = z^* \text{s.e.}(\hat{p}_1 - \hat{p}_2)$
    + Large Sample $z$-Test: $z = \frac{\hat{p}_1 - \hat{p}_2}{\sqrt{\hat{p}(1-\hat{p}(\frac{1}{n_1} + \frac{1}{n_2}))}}$, where $\hat{p} = \frac{N-1\hat{p}_1 + n_2\hat{p}_2}{n_1 + n_2}$
    + Constraints: $n_1 \times p_1 \geq 10$ and $n_2 \times p_2 \geq 10$

+ SD Module 2:  Sampling Distributions for the Difference in Two Sample Proprotions
    + Independent samples
    + Ways that independent samples can occur:
        + Random sample are taken separately from _two populations_ and same response variable is recorded for each individual
        + One random sample is taken and a variable recorded for each individual, but then units are categorized as _belonging to one population or other_ (e.g. M/F)
        + Participants randomly assigned to one of _two treatment conditions_, same response variable recorded for each unit.
    + Categorical response variable
    + Difference between the two population proportion: $p_1 - p_2$
    + General description: Estimating the _difference_ between two populations w.r.t. the proportion failing into a category of categorical variable.

+ Example: HT2
    + Q: Sample of college students asked if would return money if found a wallet on the street
        + 83/93 women said they would
        + 53/73 men said they would
    + Assume these represent all college students
    + Test hypothesis that equal proportions of college men and women would return money vs. alternative hypothesis that a higher proportion of women would do so.
    + Using $5\%$ significance level: <br/>
        Let $1 = \text{women}$ and $2 = \text{man}$, then <br/>&nbsp;&nbsp;&nbsp;&nbsp;
        $n_1 = 93$ (83 Yes, 10 No); $n_2 = 73$ (53 Yes, 22 No). <br/>
        Therefore, <br/>&nbsp;&nbsp;&nbsp;&nbsp;
        $\hat{p}_1 = \frac{83}{93} =  0.8925$ and $\hat{p}_2 = \frac{53}{75}$ <br/>&nbsp;&nbsp;&nbsp;&nbsp;
        $H_0 = p_1 - p_2 = 0$ vs. $H_a: p_1 - P_2 > 0$
    + Perform the $z$-test of $H_0: p_1 = p_2$ vs. $H_a: p_1 > p_2$ at $5\%$ level: <br/>&nbsp;&nbsp;&nbsp;&nbsp;
        $p= \frac{83+53}{93+75} = 0.8095$, $z = \frac{\hat{p}_1 - \hat{p_2}}{\sqrt{\hat{p}(1-\hat{p})({\frac{1}{n_1}+\frac{1}{N_2}})}} =  \frac{(0.8925 - 0.7067)}{0.8095 (1 - 0.8095)(\frac{1}{93} + \frac{1}{75})}$ <br/>&nbsp;&nbsp;&nbsp;&nbsp;
        $\text{p-value} = P\{z \geq 3.05 \text{ under the } N(0, 1) \text{ distribution}\} = 0.011$
    + Conclusion: 
        + Reject $H_0$: $\text{p-value} \leq 0.05$
        + In the populations represented by these samples, there is evidence to say that a higher proportion of women than men would return the money.


+ Demo
    ```python
    from datascience import *
    import numpy as np

    import matplotlib.pyplot as plots
    plots.style.use('fivethirtyeight')
    %matplotlib inline

    baby = Table.read_table('baby.csv')

    smoking_and_birthweight = baby.select('Maternal Smoker', 'Birth Weight')

    smoking_and_birthweight.group('Maternal Smoker')
    # Maternal Smoker   count
    #          False    715
    #          True     459

    smoking_and_birthweight.hist('Birth Weight', group='Maternal Smoker')

    means_tbl = smoking_and_birthweight.group('Maternal Smoker', np.average)
    # Maternal Smoker   Birth Weight average
    #           False   123.085
    #           True    113.819

    means = means_tbl.column(1)
    observed_difference = means.item(0) - means.item(1)
    # 9.266142572024918
    ```

### Video

<a href="https://edx-video.net/BERD82FD2018-V002600_DTH.mp4" alt="Lec 8.1 Introduction" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>


## Lec 8.2 Hypotheses and Statistic

### Notes

+ The Groups and the Question
    + Random sample of mothers of newborns. Compare:
        + (A) Birth weights of babies of mothers who smoked during pregnancy
        + (B) Birth weights of babies of mothers who didn’t smoke
    + Question: Could the difference be due to chance alone?
+ Comparing Two Samples
    + Compare values of sampled individuals in Group A with values of sampled individuals in Group B.
    + Question: Do the two sets of values come from the same underlying distribution?
    + Answering this question by performing a statistical test is called A/B testing.

+ The Groups and the Question
    + Random sample of mothers of newborns. Compare:
        + (A) Birth weights of babies of mothers who smoked during pregnancy
        + (B) Birth weights of babies of mothers who didn’t smoke
    + Question: Could the difference be due to chance alone?

+ Hypotheses
    + __Null__: <br/>
        In the population, the distributions of the birth weights of the babies in the two groups are the same. (They are different in the sample just due to chance.)
    + __Alternative__: <br/>
        In the population, the babies of the mothers who didn’t smoke were heavier, on average, than the babies of the smokers.

+ Test Statistic
    + Group A: smokers
    + Group B: non-smokers
    + Statistic: Difference between average weights <br/> $\text{Group B average} - \text{Group A average}$
    + Large values of this statistic favor the alternative

+ Simulating Under the Null

    + If the null is true, all rearrangements of the birth weights among the two groups are equally likely - __permutation test__
    + Plan:
        + Shuffle all the birth weights
        + Assign some to “Group A” and the rest to “Group B”, maintaining the two sample sizes
        + Find the difference between the averages of the two shuffled groups
        + Repeat



### Video

<a href="https://edx-video.net/BERD82FD2018-V002500_DTH.mp4" alt="Lec 8.2 Hypotheses and Statistic" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>


## Lec 8.3 Performing the Test

### Notes

+ Demo
    ```python
    weights = smoking_and_birthweight.select('Birth Weight')
    weights

    weights.sample(with_replacement=False)

    shuffled_weights = weights.sample(with_replacement=False).column(0)

    original_and_shuffled = smoking_and_birthweight.with_column(
        'Shuffled Birth Weight', shuffled_weights
    )

    original_and_shuffled.group('Maternal Smoker', np.average)

    group_labels = baby.select('Maternal Smoker')

    # Procedure: 
    # 1. array of shuffled weights
    # 2. table with shuffled weights assigned to group labels
    # 3. array of means of the two groups
    # 4. difference between means of the two groups
    shuffled_weights = weights.sample(with_replacement=False).column(0)
    shuffled_tbl = group_labels.with_column('Shuffled Weight', shuffled_weights)
    means = shuffled_tbl.group('Maternal Smoker', np.average).column(1)
    new_difference = means.item(0) - means.item(1)
    # -1.1400795283148284 -> randomly

    differences = make_array()

    for i in np.arange(5000):
        shuffled_weights = weights.sample(with_replacement = False).column(0)
        shuffled_tbl = group_labels.with_column('Shuffled Weight', shuffled_weights)
        means = shuffled_tbl.group('Maternal Smoker', np.average).column(1)
        new_difference = means.item(0) - means.item(1)
        differences = np.append(differences, new_difference)

    Table().with_column('Difference Between Means', differences).hist(bins=20, ec='w')

    observed_difference
    # 9.266142572024918
    ```

### Video

<a href="https://edx-video.net/BERD82FD2018-V002800_DTH.mp4" alt="Lec 8.3 Performing the Test" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>


## Reading and Practice for Section 8a

### Reading

This guide assumes that you have watched the videos for Section 8a.

This corresponds to textbook section:

[Chapter 12: Comparing Two Samples](https://www.inferentialthinking.com/chapters/12/comparing-two-samples.html)

In section 8a, we developed a way of comparing two random samples and answer questions about the similarities and differences between them. So far, we have seen several examples of assessing whether a single sample looks like random draws from a specified chance model. A/B testing refers to deciding whether two numerical samples come from the same underlying distribution.

Try the following practice problems.

### Practice

Suppose we want to write a function to preform A/B testing for the difference between averages. Let us define a function that generates the array of simulated differences. The function `difference_of_ab_sample_means` takes four arguments:

+ the data table
+ the label of the column containing the variable whose average is of interest
+ the label of the column containing group labels (e.g., A and B)
+ the number of repetitions

It returns and array of simulated differences in group means, each computed by first randomly permuting the data and assigning random values to each group. The length of the array is equal to the number of repetitions. 

Try to fill in the missing blanks of the `difference_of_ab_sample_means` without looking at examples. 

```python
def difference_of_ab_sample_means(table, label, group_label, repetitions):
      
      tbl = table.select(group_label, label)
      
      differences = ____A____.
      
      for i in np.arange(repetitions):
            shuffled = tbl.sample(____B____).column(1)
            original_and_shuffled = tbl.with_column('Shuffled Data', shuffled)
      
            shuffled_means = ____C____.____D____(____E____, np.average).column(2)
            simulated_difference = ____F____.item(1) - ____G____.item(0)
      
            differences = np.append(differences, simulated_difference)
      
      return differences
```

    Ans:
    A: make_array()
    B: with_replacement = False
    C: original_and_shuffled
    D: group
    E. group_label
    F. shuffled_means
    G. shuffled_means


# Section 8b: Deflategate Example (Lec 8.4 - Lec 8.5)

## Lec 8.4 Deflategate Introduction

### Notes

+ Deflategate <br/>
    + 2015 AFC Championship Game
    + Wikipedia: 
        > The 2015 AFC Championship Game football tampering scandal, commonly referred to as Deflategate, or Ballghazi

+ Demo
    ```python
    football = Table.read_table('deflategate.csv')
    football.show()

    football = football.drop(1, 2).with_column(
        'Combined', (football.column(1) + football.column(2)) / 2
    )
    football.show()

    start = np.append(12.5 * np.ones(11), 13 * np.ones(4))
    # array([12.5, 12.5, 12.5, 12.5, 12.5, 12.5, 12.5, 12.5, 12.5, 12.5, 12.5, 13. , 13. , 13. , 13. ])
    drops = start - football.column(1)
    # array([0.85 , 1.475, 1.175, 1.65 , 1.225, 0.725, 0.425, 1.175, 1.35, 1.8  , 1.375, 0.475, 0.475, 0.275, 0.65 ])

    football = football.select('Team').with_column(
        'Drop', drops
    )
    means_tbl = football.group('Team', np.average)
    #   Team        Drop average
    #   Colts       0.46875
    #   Patriots    1.20227

    means = means_tbl.column(1)
    observed_difference = means.item(0) - means.item(1)
    # -0.733522727272728
    ```

### Video

<a href="https://edx-video.net/BERD82FD2018-V002700_DTH.mp4" alt="Lec 8.4 Deflategate Introduction
" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>


## Lec 8.5 Deflategate Testing

### Notes

+ Null hypothesis <br/>
    The 4 Colts footballs are like a sample drawn at random without replacement from all 15 balls. <br/>
    + To test this hypothesis, repeat this process:
        + Randomly permute all 15 balls
        + Label 11 of them “Patriots” and the remaining 4 “Colts”
        + Compare the averages of the two groups

+ Demo
    ```python
    group_labels = football.select('Team')
    drop_tbl = football.select('Drop')

    shuffled_drops = drop_tbl.sample(with_replacement=False).column(0)
    shuffled_tbl = group_labels.with_column('Shuffled Drop', shuffled_drops)
    means = shuffled_tbl.group('Team', np.average).column(1)
    new_difference = means.item(0) - means.item(1)
    #0.12727272727272665 -> random results

    differences = make_array()
    for i in np.arange(20000):
        shuffled_drops = drop_tbl.sample(with_replacement=False).column(0)
        shuffled_tbl = group_labels.with_column('Shuffled Drop', shuffled_drops)
        means = shuffled_tbl.group('Team', np.average).column(1)
        new_difference = means.item(0) - means.item(1)
        differences = np.append(differences, new_difference)

    Table().with_column('Difference Between Means', differences).hist(ec='w')
    plots.scatter(observed_difference, 0, color='red', s=40);

    np.count_nonzero(differences <= observed_difference) / 20000
    # 0.00225 -> p-value
    ```

### Video

<a href="https://edx-video.net/BERD82FD2018-V002900_DTH.mp4" alt="Lec 8.5 Deflategate Testing
" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>



