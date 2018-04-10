# Section 4: Expressions (Lec 4.1 - Lec 4.5)

## Lec 4.1 Arithmetic

### Notes

+ Arithmetic Operators
    | Operation | Operator | Example | Value |
    |-----------|:----------:|---------|-------|
    | Addition | `+` | `2 + 3` | 5 |
    | Subtraction | `-` | `2 - 3` | -1 |
    | Multiplication | `*` | `2 * 3` | 6 |
    | Division | `/` | `8 / 3` | 2.6666666666666665 |
    | Remainder | `%` | `8 % 3` | 2 |
    | Exponentiation | `**` | `2 ** 0.5` | 1.4142135623730951 |
+ Ints and Floats
    + Python has two real number types:
        + `int`: an integer of any size
        + `float`: a number with a fractional aprt that may be wero
    + An `int` never has a decimal point; a `float` alwaus does
    + A `float` might be printed using scientific notation.
    + Three limitations of float values:
        + limited size (but the limit is huge)
        + limited precision of 15-16 decimal places
        + after arithmetic, the final few decimal places can be wrong
+ Demo
    + Programming environment
        ```python
        from datascience import *
        import numpy as np

        %matplotlib inline
        import matplotlib.pyplot as plots
        plots.style.use('fivethirtyeight')
        ```
    + precision: 15 or 16 significant digits
        ```python
        (2 ** 0.5) * (2 ** 0.5)         # != 2
        (2 ** 0.5) * (2 ** 0.5) - 2     # != 0
        ```

### Video

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/hWY_LGmzwkU)

## Lec 4.2 Arithmetic Question

### Notes

+ Rank the results of the following expression in order from least to greatest

    a. 3 * 10 ** 10  
    b. 10 * 3 ** 10  
    c. (10 * 3) ** 10  
    d. 10 / 3 / 10  
    e. 10 / (3 / 10)  

    Ans: c (4904900000000) > a (30000000000) > b (590490) > e (0.33333333333333337) > d (33.333333333333336)

### Video

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/F3KVaWfrwn0)

## Lec 4.3 Exponential Growth

### Notes

+ Ebola Epidemic, Sept. 2014
+ Growth Rate
    + The _growth rate_ is the rate of increase per unit time
    + After one time unit, a quantity x growing at rate `g` will be  
        $x * (1 + g)$
    + After `t` time units, a quantity `x` growing at rate `g` will be  
        $x * (1 + g) * t$
    + If `after` and `before` are measurements of the same quantity taken `t` time units apart, then the _growth rate_ is  
        $(after/before)^{(1/t)} - 1$
+ Demo
    ```python
    sept_7 = 4366
    aug_7 = 1830
    growth_per_month = (sept_7 / aug_7) - 1

    sept_7 * (1 + growth_per_month) ** 12

    fed_budget_2002 = 2370000000000
    fed_budget_2012 = 3380000000000
    fed_budget_2012 - fed_budget_2002

    g = (fed_budget_2012 / fed_budget_2002) ** (1/10) - 1

    fed_budget_2002 * (1 + g) ** 16 # Actual 2018 budget: $4.1 trillion
    ```

### Video

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/MHRQ1UGKRyI)

## Lec 4.4 Arrays

### Notes

+ Arrays - containing a sequence if values
    + all elements of an array should have the same type
    + arithmetic is applied to each element individually
    + when two arrays are added, they must have the same size; corresponding elements are added in the result
_ Demo
    ```python
    make_array(1, 2, 3)
    make_array(1, 2, 3) * 2

    a = make_array(1, 2, 3)
    a + make_array(10, 100, 1000)
    sum(a); max(a); min(a)
    fed_budget_2002 * (1 + g) ** a
    ```

### Video

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/q6cQBGP9wsQ)

## Lec 4.5 Columns

### Notes

+ Columns of Tables - a column of a table is an array
    + Access a column of a table `t` using its label or index: `movies.column('Year')` or `movies.column(4)` [index starts at 0]
    + A column expression evaluates to an array
    + Arithmetic doesn't change the array or table
    + Make a table with a column using `with_column` method
+ Demo
    ```python
    movies = Table.read_table('top_movies_2017.csv')
    movies.column('Gross')

    movies.set_format('Gross', NumberFormatter) # adding , for numbers

    adjustment = movies.column('Gross (Adjusted)') / movies.column('Gross')

    movies.with_column('Adjustment', adjustment)
    movies.with_column('Adjustment', adjustment).scatter('Year', 'Adjustment')

    movies.column('Year')

    age = 2017 - movies.column('Year')
    movies = movies.with_column('Age', age)
    movies = movies.with_column('Growth rate', adjustment ** (1 / age) - 1)

    movies.scatter('Year', 'Growth rate')
    movies.sort('Age').show(20)
    movies.sort('Year').show(20)
    ```

### Video

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/n8R4pZQDl_8)

