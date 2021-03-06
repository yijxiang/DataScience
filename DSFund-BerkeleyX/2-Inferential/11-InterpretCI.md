# Section 11: Interpreting Confidence (Lec 11.1 - Lec 11.3)

+ [Launch Web Page](https://courses.edx.org/courses/course-v1:BerkeleyX+Data8.2x+1T2018/courseware/95ee24be1f714d51bb48d73712c71aba/c1392ee86ecc4e6ca55908f2d3f9242c/1?activate_block_id=block-v1%3ABerkeleyX%2BData8.2x%2B1T2018%2Btype%40vertical%2Bblock%40ece536653f1143a78cbee4c9858ef8cb)
+ [Web Notebook](https://hub.data8x.berkeley.edu/user/59d217c894d11dbd21d2d37ef6ae9675/notebooks/materials-x18/lec/x18/2/lec11.ipynb#)
+ [Local Notebook](./notebooks/lec11.ipynb)
+ [Local Python](./notebooks/lec11.py)

## Lec 11.1 Applying the Bootstrap

### Notes

+ When to Find a Confidence Interval
    + You wan to guess a parameter of a population.
    + You have a random sample from the population.
    + You want to quantify your uncertainty.
    + A statistic is a reasonable estimate of the parameter.

+ Demo
    ```python
    births = Table.read_table('baby.csv')
    births.show(3)
    # Birth     Gestational     Maternal    Maternal    Maternal            Maternal 
    # Weight    Days            Age         Height      Pregnancy Weight    Smoker
    # 120       284             27          62          100                 False
    # 113       282             33          64          135                 False
    # 128       279             28          64          115                 True

    babies = births.select('Birth Weight', 'Gestational Days')
    # Birth Weight    Gestational Days
    # 120             284
    # 113             282
    # ...

    babies.scatter(1, 0)

    ratios = babies.with_column(
        'Ratio BW/GD', babies.column(0)/babies.column(1)
    )
    # Birth Weight    Gestational Days    Ratio BW/GD
    # 120             284                 0.422535
    # 113             282                 0.400709
    # ...

    ratios.hist('Ratio BW/GD')

    np.median(ratios.column('Ratio BW/GD'))     # 0.42907801418439717

    resampled_medians = []
    for i in np.arange(1000):
        resample = ratios.sample()
        median = np.median(resample.column('Ratio BW/GD'))
        resampled_medians.append(median)

    interval_99 = [percentile(0.5, resampled_medians),
                percentile(99.5, resampled_medians)]
    print(interval_99)      # [0.4243514279485503, 0.43416370106761565]

    Table().with_column('Resampled median', resampled_medians).hist(0)
    plots.plot(interval_99, [0, 0], color='gold', lw=10);
    ```

### Video

<a href="https://edx-video.net/BERD82FD2018-V003800_DTH.mp4" alt="Lec 11.1 Applying the Bootstrap" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>


## Lec 11.2 Confidence Interval Pitfalls

### Notes

+ When Not to Use The Bootstrap
    + If you’re trying to estimate very high or very low percentiles, or min and max
    + If you’re trying to estimate any parameter that’s greatly affected by rare elements of the population
    + If the probability distribution of your statistic is not roughly bell shaped (the shape of the empirical distribution will be a clue)
    + If the original sample is very small (fewer than 20)

+ Can You Use a CI Like This?
    + By our calculation, an approximate $95\%$ confidence interval for the average age of the mothers in the population is $(26.9, 27.6)$ years.
    + True or False: <br/> About $95\%$ of the mothers in the population were between 26.9 years and 27.6 years old.
    + Answer: False. We’re estimating that their average age is in this interval.

+ Is This What a CI Means?
    + True or False: There is a 0.95 probability that the average age of mothers in the population is in the range $26.9$ to $27.6$ years.
    + Answer: False. <br/> The average age of the mothers in the population is unknown but it’s a constant. It’s not random. No chances involved.
    + An approximate $95\%$ confidence interval for the average age of the mothers in the population is $(26.9, 27.6)$ years.

### Video

<a href="https://edx-video.net/BERD82FD2018-V004000_DTH.mp4" alt="Lec 11.2 Confidence Interval Pitfalls" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>


## Lec 11.3 Confidence Interval Tests

### Notes

+ Using a CI for Testing
    + Null hypothesis: __Population average = x__
    + Alternative hypothesis: __Population average ≠ x__
    + Cutoff for P-value: $p\%$
    + Method:
        + Construct a $(100-p)\%$ confidence interval for the population average
        + If x is not in the interval, reject the null
        + If x is in the interval, can’t reject the null

### Video

<a href="https://edx-video.net/BERD82FD2018-V003700_DTH.mp4" alt="Lec 11.3 Confidence Interval Tests" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>


## Reading and Practice

### Reading

This guide assumes that you have watched the videos for Section 11.

This corresponds to textbook section:

[Chapter 13.3: Confidence Intervals](https://www.inferentialthinking.com/chapters/13/3/confidence-intervals.html)

[Chapter 13.4: Using Confidence Intervals](https://www.inferentialthinking.com/chapters/13/4/using-confidence-intervals.html)

In section 11, we learned more about confidence intervals. We use confidence intervals to estimate some unknown parameter.  Confidence intervals account for chance variability in our original random sample by producing an interval of estimates.  A common misconception is that the 95% confidence interval contains the parameter 95% of the time. It does not. Rather, "95% confidence" describes the method we used to create the interval.  About 95% of the time, our method creates a good intervals (one that contains the parameter). 

Test your conceptual understanding of confidence intervals with the following practice questions.

### Practice

You sample 100 dogs at random from all dogs in Berkeley and compute a 95% confidence interval of their average height. For each of the statements below, state whether they are Always True, Typically True, Not Expected to be True, or False.

Q1. The chance that the average height of all dogs in Berkeley is in this interval is 95%.

    a. Always True
    b. Typically True
    c. Not Expected to be True
    d. False

    Ans: d

Q2. If you had repeated the process of sampling 100 dogs many times and computed a confidence interval from each sample, approximately 95% of the intervals would contain the average height of all dogs in Berkeley.

    a. Always True
    b. Typically True
    c. Not Expected to be True
    d. False

    Ans: b

Q3. If you had repeated the process of sampling 100 dogs many times and computed a confidence interval from each sample, 95% of the intervals would contain the heights of all dogs in Berkeley.

    a. Always True
    b. Typically True
    c. Not Expected to be True
    d. False

    Ans: c

Q4. If you had sampled another 100 dogs from the population and computed a second confidence interval, it would be the same as the first.

    a. Always True
    b. Typically True
    c. Not Expected to be True
    d. False

    Ans: c

Q5. If you had sampled 100 dogs a second time and computed a new confidence interval, it would overlap with your original confidence interval.

    a. Always True
    b. Typically True
    c. Not Expected to be True
    d. False

    Ans: b

Q6. If you had sampled 100 dogs a second time and computed a second confidence interval, it would be approximately the same size as the first, but have a different center.

    a. Always True
    b. Typically True
    c. Not Expected to be True
    d. False

    Ans: b

Q7. If you had sampled 1000 dogs instead of 100 dogs, your confidence interval would have been smaller.

    a. Always True
    b. Typically True
    c. Not Expected to be True
    d. False

    Ans: b






