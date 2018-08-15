# Section 2: Normal Curve (Lec 2.1 - Lec 2.4)

+ [Launching Notebook Web Page](https://courses.edx.org/courses/course-v1:BerkeleyX+Data8.3x+2T2018/courseware/7bba8d29a20946e5be64e508fd3481b2/f9a06e52a1c448049e646a8101021f26/1?activate_block_id=block-v1%3ABerkeleyX%2BData8.3x%2B2T2018%2Btype%40vertical%2Bblock%406f23e54059604575bf51e75383dfe293)
+ [Notebook Web Page](https://hub.data8x.berkeley.edu/user/37b80bfacc52ea5dfdad124579807188/notebooks/materials-x18/lec/x18/3/lec2.ipynb#)
+ [Local Notebook](./notebook/lec2.ipynb)
+ [Local Python code](./notebook/lec2.py)

## Lec 2.1 Standard Units

### Notes

+ Goals
    + Describe what is meant by "bell shaped curve"
    + Explain how bell shaped curves arise in inference

+ Standard Units
    + How many SDs above average?
    + $z = (\text{value} - \text{average})/SD$
        + Negative z: value below average
        + Positive z: value above average
        + z = 0: value equal to average
    + When values are in standard units: average = 0, SD = 1
    + Chebyshev: At least 96% of the values of z are between -5 and 5

+ Discussion Question - `both` table in Demo <br/>
    Find whole numbers that are close to: <br/> &nbsp;&nbsp;&nbsp;&nbsp;
    a.  the average age <br/> &nbsp;&nbsp;&nbsp;&nbsp;
    b.  the SD of the ages

    + Ans: 
      + The average is about 27 (about 0 standard units)
      + The SD is abut 6 (33 is about 1 SD above the average)


+ Demo
    ```python
    def standard_units(x):
        """Convert the array x to standard units"""
        return (x - np.average(x)) / np.std(x)

    births = Table.read_table('baby.csv')
    births.labels
    # ('Birth Weight', 'Gestational Days', 'Maternal Age', 'Maternal Height',
    #  'Maternal Pregnancy Weight', 'Maternal Smoker')

    ages = births.column('Maternal Age')
    ages_in_standard_units = standard_units(ages)
    np.average(ages_in_standard_units), np.std(ages_in_standard_units)
    # (-7.868020072300939e-17, 1.0)

    both = Table().with_column(
        'Age in Years', ages,
        'Age in Standard Units', ages_in_standard_units
    )
    # Age in Years	Age in Standard Units
    # 27            -0.0392546
    # 33            0.992496
    # 28            0.132704
    # ... (rows omitted)

    np.mean(ages), np.std(ages)   # (27.228279386712096, 5.815360404190897)

    both.hist('Age in Years', bins = np.arange(15, 46, 2))

    both.hist('Age in Standard Units', bins = np.arange(-2.2, 3.4, 0.35))
    plots.xlim(-2, 3.1);
    ```

### Video


<a href="https://edx-video.net/BERD83FD2018-V000700_DTH.mp4" alt="Lec 2.1 Standard Units" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>

## Lec 2.2 SD and Bell Curves

### Notes


+ Demo
    ```python

    ```

### Video


<a href="https://edx-video.net/BERD83FD2018-V000600_DTH.mp4" alt="Lec 2.2 SD and Bell Curves" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>

## Lec 2.3 Normal Distribution

### Notes


+ Demo
    ```python

    ```

### Video


<a href="https://edx-video.net/BERD83FD2018-V000500_DTH.mp4" alt="Lec 2.3 Normal Distribution" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>

## Lec 2.4 Central Limit Theorem

### Notes


+ Demo
    ```python

    ```

### Video


<a href="https://edx-video.net/BERD83FD2018-V000800_DTH.mp4" alt="Lec 2.4 Central Limit Theorem" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" width="60px"> 
</a>

## Reading and Practice

### Reading


### Practice

