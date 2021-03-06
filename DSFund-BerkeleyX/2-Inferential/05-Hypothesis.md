# Section 5: Hypothesis Testing (Lec 5.1 - Lec 5.4)

## Lec 5.1 Assessing Models

### Notes

+ Choosing One of Two Viewpoints

    + Based on data
        + “Chocolate has no effect on cardiac disease.” --> “Yes, it does.”
        + “This jury panel was selected at random from eligible jurors.” --> “No, it has too many people with college degrees.”

+ Models
    + A model is a set of assumptions aboyut the data
    + In data science, many models involve assumption about processes that involve randomnes, e.g., “Chance models”

+ Approach to Assessment

    + If we can simulate data according to the assumptions of the model, we can learn what the model predicts.
    + We can then compare the predictions to the data that were observed.
    + If the data and the model’s predictions are not consistent, that is evidence against the model.

### Video 

<a href="https://youtu.be/wJ9Eov9Mdf0" alt="Lec 5.1 Assessing Models" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>



## Lec 5.2 A Model about Random Selection

### Notes

+ Swain vs. Alabama, 1965

    + Talladega County, Alabama
    + Robert Swain, black man convicted of crime
    + Appeal: one factor was all-white jury
    + Only men 21 years or older were allowed to serve
    + 26% of this population were black
    + Swain’s jury panel consisted of 100 men
    + 8 men on the panel were black

+ Supreme Court Ruling

    + About disparities between the percentages in the eligible population and the jury panel, the Supreme Court wrote:
        > “... the overall percentage disparity has been small and reflects no studied attempt to include or exclude a specified number of Negroes”
    + The Supreme Court denied Robert Swain’s appeal

+ Sampling from a Distribution

    + Sample at random from a categorical distribution <br/>
        `sample_proportions(sample_size, pop_distribution)`
    + Samples at random from the population
    + Returns an array containing the distribution of the categories in the sample

+ `sample_porportions` function
    + Signature: `sample_proportions(sample_size, probabilities)`
    + Return the proportion of random draws for each outcome in a distribution.
    + Args: 
        + `sample_size`: The size of the sample to draw from the distribution.
        + `probabilities`: An array of probabilities that forms a distribution.
    + Ref: datascience/util.py

+ Demo 
    ````python
    # proportion of two categories
    eligible_population = make_array(0.26, 0.74)
 
    sample_proportions(100, eligible_population)

    both_counts = 100 * (sample_proportions(100, eligible_population))
 
    both_counts.item(0)

    counts = make_array()

    repetitions = 10000
    for i in np.arange(repetitions):
        sample_distribution = sample_proportions(100, eligible_population)
        sampled_count = (100 * sample_distribution).item(0)
        counts = np.append(counts, sampled_count)

    Table().with_column('Random Sample Count', counts).hist(bins = np.arange(5.5, 44.5, 1))
    ```

### Video 

<a href="https://youtu.be/OreWRDOb9fg" alt="Lec 5.2 A Model about Random Selection" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>



## Lec 5.3 A Genetic Model

### Notes

+ Steps in Assessing a Model

    + Come up with a statistic that will help you decide whether the data support the model or an alternative view of the world.
    + Simulate the statistic under the assumptions of the model.
    + Draw a histogram of the simulated values. This is the model’s prediction for how the statistic should come out.
    + Compute the observed statistic from the sample in the study.
    + Compare this value with the histogram.
    + If the two are not consistent, that’s evidence against the model.

+ Gregor Mendel, 1822-1884

    <img src="https://www.sciencelearn.org.nz/system/images/images/000/002/472/embed/Gregor_Mendel_oval.jpg" alt="text" width="123">
    <img src="https://lh3.googleusercontent.com/VXvSFXZ0srj5i4fMooyoqhcmy6T-imfcFSfBdhDSI19z_cA6brh1-Z0TBYl0V--u1mjcKyknUPqBsgy6s7FuNgfrEfP3GM3EU2BafYs=s660" alt="text" width="400">

+ A Model
    + Pea plants of a particular kind
    + Each one has either purple flowers or white flowers
    + Mendel’s model:
        + Each plant is purple-flowering with chance $75\%$,
        + regardless of the colors of the other plants
    + Question:
        + Is the model good, or not?

+ Choosing a Statistic

    + Start with percent of purple-flowering plants in sample
    + If that percent is much larger or much smaller than $75$, that is evidence against the model
    + __Distance__ from $75$ is the key
    + Statistic: $| \text{sample percent of purple-flowering plants} - 75 |$
    + If the statistic is large, that is evidence against the model


+ Demo 
    ````python
    model = make_array(0.75, 0.25)

    sample_proportions(929, model)

    percent_purple = (100 * sample_proportions(929, model)).item(0)

    abs(percent_purple - 75)

    distances = make_array()

    repetitions = 10000
    for i in np.arange(repetitions):
        one_distance = abs((100 * sample_proportions(929, model)).item(0) - 75)
        distances = np.append(distances, one_distance)

    Table().with_column('Distance from 75', distances).hist()

    abs(100 * (705 / 929) - 75)

    ```

### Video 

<a href="https://youtu.be/OI4x1i_0kPU" alt="Lec 5.3 A Genetic Model" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>



## Lec 5.4 Example

### Notes

+ Discussion Questions <br/>
    In each of (a) and (b), choose a statistic that will help you decide between the two viewpoints. <br/>
    Data: the results of 400 tosses of a coin <br/>
    (a) <br/>
        “This coin is fair.” <br/>
        “No, it’s not.” <br/>
    (b) <br/>
        “This coin is fair.” <br/>
        “No, it’s biased towards tails.”

+ “Fair”
    + For both (a) and (b),
        + The number of heads in the 400 tosses is a good starting point, but might need adjustment
        + A number of heads around 200 suggests “fair”

+ Answers <br/>
    (a) Very large or very small values of the number of heads suggest “not fair.” <br/>
        + The __distance__ between number of heads and 200 is the key
        + Statistic: $| \text{number of heads} - 200 |$
        + Large values of the statistic suggest “not fair”
    (b) Small values of the number of heads suggest “biased towards tails” <br/>
        + Statistic: number of heads


### Video 

<a href="urhttps://youtu.be/ybDvLbRR4UAl" alt="Lec 5.4 Example" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>



## Reading and Practice for Section 5

### Reading

This guide assumes that you have watched the videos for Section 5.

This corresponds to textbook sections:

[Chapter 11: Testing Hypothesis](https://www.inferentialthinking.com/chapters/11/testing-hypotheses.html)

[Chapter 11.1: Assessing Models Opens in new window](https://www.inferentialthinking.com/chapters/11/1/assessing-models.html)

In section 5, we learned how data scientists answer yes-no questions with random samples and empirical distributions. In both the U.S. Supreme Court Swain vs. Alabama example and the Mendel's Pea Flowers example, there were underlying frameworks and assumptions created that allowed for us to use chance models. We'll get more experience with designing these tests and models, choosing the right statistic, and generating conclusions from our models.

Try applying what you learned in the following practice questions.


### Practice 

Kristen Gilbert was an American nurse in the 1990’s who had established a reputation of being very good in crisis situations. When a patient went into cardiac arrest, she would stay calm, sound the code blue alarm, and administer epinephrine to restart the heart. However, other nurses at the hospital became suspicious of Gilbert because it seemed like there was an unusual number of code blue calls when she was working. Some nurses thought that Gilbert was administering fatal injections to patients to cause their cardiac arrest, but no one ever witnessed this directly. 

Here are the data. There were 1641 shifts in total. Each shift was classified according to whether or not there was at least one death and whether or not Gilbert was present.

AT LEAST ONE DEATH ON SHIFT?

| GILBERT PRESENT? | Yes | No | Total |
|------------------|-----|----|-------|
| Yes | 40 | 217 | 257 |
| No | 34 | 1350 | 1384 |
| Total | 74 | 1567 | 1641 |


In defense of Gilbert, assess whether her shifts are like random draws from all 1641 shifts in the following steps.

Q1. If you picked a shift at random, what’s the chance there’s at least one death on that shift?

    Ans: 74/1641

Q2. Suppose Gilbert's shifts were like random draws from all 1641 shifts. How many draws would there be?

    Ans: 257

Q3. If Gilbert's shifts were like random draws, in how many shifts do you expect her to have seen at least one death?

    Ans: 

Q4. In how many of Gilbert's shifts did she see at least one death?

  Ans: 40

Q5. The histogram below shows 10,000 values of the number of shifts with at least one death out of 257 randomly drawn shifts. 

![histogram](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/7748463de393cb8da912d4439ab06eb6/asset-v1:BerkeleyX+Data8.2x+1T2018+type@asset+block/gilberthistogram.png)

    Which do you conclude?

    a. Gilbert's shifts were like random draws.

    b. Gilbert had too many shifts with at least one death. Her shifts don't look like random draws.

    Ans: b




