# Section 5a: Strings (Lec 5.1 - Lec 5.4)

## Lec 5.1 Creating Tables

### Notes

+ Ways to create a table

    + Read a table from a spreadsheet: `Table.read_table(filename)`
    + An empty table: `Table()`
    + and ...
+ Array --> Tables

    + Create a table with a single column w/ `data` as an array: `Table().with_column(label, data)`
    + Create a table w/ an array of data for each column: `Table().with_columns(label1, data1, ...)`
+ Table Methods:

    + Create and extending tables: `Table().with_columns` and `Table.read_table(filename)`
    + Finding the size: `num_rows` and `num_columns`
    + Referring to columns: labels, relabeling, and indices; column indices start from 0: `labels` and `relabeled`
    + Accessing data in a column: `column` takes a label or index and returns an array
    + Using array methods to work with data in columns: `item`, `sum`, `min`, `max`, and so on
    + Creating new tables containing some of the original columns: `select` and `drop`
+ Examples

    The table `students` has columns `Name`, `ID`, and `Score`. Write one line code that evaluates to:  
    a) A table consisting of only the column labeled `Name`: `students.select('Name')`  
    b) The largest score: `students.column('Score').max()` or `max(students.column('Score'))`

### Video

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/Obg7GqjxZ-Q)

## Lec 5.2 Strings

### Notes

+ Text and Strings
    + A Sstring value is a snippet of text of any length
        + 'a'
        + 'We can do it'
        + "there can be 2 sentences. Here's the second!"
    + Strings that contain numbers can be converted to numbers
        + `int('12)`
        + `float('1.2')`
    + Any value can be converted to a string
        + `str(5)`
+ Demo
    ```python
    '2.3' + 4                   # typeError
    '2.3' * 4                   # '2.32.32.32.3' repeats 4 times
    int('23') + float('2.3')
    x = 12; int(str(x) + '0')   # 120
    ```

### Video

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/NJQr6a-j8b0)

## Lec 5.3 String Exercise

### Notes

+ Discussion Question

    + Assume you have run tthe following statements
        1. `x = 3`
        2. `y = '4'`
        3. `z= '5.6'`
    + What's the source of the error in each example?

        a. `x + y`  
        b. `x + int(y + z)`  
        c. `str(x) + int(y)`  
        d. `str(x, y) + z`

### Video

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/rMIcCFnloiE)

## Lec 5.4 Exercise Answer

### Notes

+ Answers:

    a. TypeError: add int and string  
    b. ValueError: int('45.6') not integer  
    c. TypeError: add string and int  
    d. TypeError: str takes only one argument and must be string

### Video

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/L_UtEQX7QpY)

## Reading and Practice for Section 5a

### Readings

This guide assumes that you have watched section 5a (video lecture segments Lec 5.1, Lec 5.2, Lec 5.3, Lec 5.4) in Courseware.

This corresponds to textbook sections:

+ [Chapter 4.2: Strings](https://www.inferentialthinking.com/chapters/04/2/strings.html)
+ [Chapter 6: Tables](https://www.inferentialthinking.com/chapters/06/tables.html)

In section 5a, we learned a little more about building tables, and we were introduced to text representations in Python, otherwise known as strings.  Just like floats and ints that represent numbers, strings are a very powerful data type for text.  It's important to understand the different behaviors of strings, ints, floats, and other data types in Python.

Here are the table methods we learned.  These will be important later on in the course!

`Table.read_table(filename)` create a table with data from a file

`Table()` create an empty table

`Table().with_columns(name, values, ...)` creates a table with an array of values for each column name

`tbl.with_columns(name, values, ...)` appends a column name with an array of values to an existing table

`tbl.num_rows` returns the number of rows in a table

`tbl.num_columns`  returns the number of columns in a table

`tbl.labels` returns a list of column labels of a table

`tbl.relabeled(old_label, new_label)` returns a new table with a changed label column

`tbl.drop(col1, col2, …)` returns a table without the dropped columns

Here is some more practice with strings and types.

### Practices

Assume you have run the following statements
```python
a = 2
b = '3'
c = '4.5'
d = 10
```

What is the output for each of these code statements? Fill in your exact answer. If your answer is a string, please use SINGLE quotations (i.e. '10'). If the code results in an error message, write `Error`. Make sure to include quotations if your answer is a string (i.e. '1').

Q1. `int(b)`

    Ans: 3

Q2. `str(a)`

    Ans: '2'

Q3. `int(c)`

    Ans: Error

Q4. `a * b`

    Ans: '33'

Q5. `int(str(d) + b)`

    Ans: 103

Q6. `int(str(a) * c)`

    Ans: Error

# Section 5b: Minrad's Map (Lec 5.5 - Lec 5.6)

## Lec 5.5 Minard's Map

### Notes

+ Charles Joseph Minard, 1781-1870

    + French civil engineer who create one of the greatest graph of all time
    + Visualized Napoleon's 1812 invasion of Russia, including

        + the number of soldiers
        + the direction of the march
        + the latitude and longitude of each city
        + the temperature on the return journey
        + Dates in November and December

![Minard's Map](https://media1.britannica.com/eb-media/87/75087-004-046911B2.jpg)

+ Different types of data

    | Longitude | Latitude | City | Direction | Survivors |
    |-----------|----------|------|-----------|-----------|
    | 32   | 54.8 | Smolensk | Advance | 145000 |
    | 33.2 | 54.9 | Dorogobouge | Advance | 140000|
    | 34.4 | 55.5 | Chjat | Advance | 127100 |
    | 37.6 | 55.8 | Moscou | Advance | 100000 |
    | 34.3 | 55.2 | Wixma | Retreat | 55000 |
    | 32   | 54.6 | Smolensk | Retreat | 24000 |
    | 40.4 | 54.4 | Orscha | Retreat | 20000 |
    | 26.8 | 54.3 | Moiodexno | Retreat | 12000 |

    + float - decimal number: longitude, latitude
    + string - text: City
    + int - integer - Survivors

### Video

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/dcuI0D9gXdQ)

## Lec 5.6 Minard's Map Code

### Notes

+ Demo

    ```python
    # load data
    minard = Table.read_table('https://www.inferentialthinking.com/notebooks/minard.csv')
    
    # class attributes
    minard.num_columns
    minard.num_rows
    minard.labels

    # label and index manipulation
    minard.column('Survivors')
    minard.column(4)

    # calculate surviving percentage
    initial_size = minard.column('Survivors').item(0)
    percentage_surviving = minard.column('Survivors')/initial_size

    # Adding column into table and reformat
    with_percentages = minard.with_column('Percent Surviving', percentage_surviving)
    with_percentages.set_format('Percent Surviving', PercentFormatter)
    ```

### Video

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/AtlV0r24uy4)


# Section 5c: Building Tables (Lec 5.7 - Lec 5.9)

## Lec 5.7 Lists

### Notes

+ Lists are generic sequences
    + A list is a sequence of values (just like an array), but the values can all have different types
        ```python
        [2+3, 'four', Table().with_column('K', [3, 4])]
        ```
    + If you create a table column from a list, it will be converted to an array automatically
+ Demo

    ```python
    make_array(2, 3.0)
    make_array(2, 3.0).item(0)
    make_array(2, 'three')
    make_array(2, 'three').item(0)

    type([2, 'three'])

    flowers = Table.read_table('flowers.csv')
    my_favorite_flower = [5, 'morning glory', 'purple']
    flowers.with_row(my_favorite_flower)
    ```

### Video

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/KOcIKkXQvl0)

## Lec 5.8 Take

### Notes

+ `Take` Rows, `Select` Columns

    + The `select` method returns a table w/ only some columns
    + The `take` method returns a table w/ only some rows
        + Rows are unmbered, starting at 0
        + Taking a single number returns a one-row table
        + Taking a list of numbers returns a table as well
+ Demo

    ```python
    # load data
    minard = Table.read_table('https://www.inferentialthinking.com/notebooks/minard.csv')

    # take operation
    minard.take(0)
    minard.take([0, 1, 2, 3])   # row 0, 1, 2, 3
    minard.take(np.arange(0,4)) # consecutive rows
    ```
### Video

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/TlHeF21OSAc)

## Lec 5.9 Where

### Notes

+ The `where` Method

    + Constructs a new table with just the rows that match the condition: `t.where(label, condition)`
+ Manipulating Rows

    + sort the rows in increasing order: `t.sort(column)`
    + keep the numbered rows, index starting at 0: `t.take(row_number)`
    + keep all rows for which a column's value satisfies a condition: `t.where(column, are.condition)`
    + keep all rows containing a certain value in a column: `t.where(column, value)`
+ Demo
    ```python
    # load data
    nba = Table.read_table('nba_salaries.csv')

    # basic operations
    nba.sort('2015-2016 SALARY')
    nba = nba.relabeled('2015-2016 SALARY', 'SALARY')

    # where operation
    nba.sort('SALARY')
    nba.where('SALARY', are.above(10))
    nba.where('SALARY', are.above(10)).sort('SALARY')
    nba.where('SALARY', are.between(10, 11))
    nba.where('TEAM', are.equal_to('Toronto Raptors'))
    nba.where('TEAM', 'Toronto Raptors')
    nba.where('TEAM', are.containing('Raptors'))
    nba.where('TEAM', are.equal_to('Golden State Warriors')).sort('SALARY', descending=True)
    nba.where('SALARY', are.between(10, 12))
    ```

### Video

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg)](https://youtu.be/xCk4CxHL2ec)

## Reading and Practice for Section 5c

### Readings

This guide assumes that you have watched section 5c (video lecture segments Lec 5.7, Lec 5.8, Lec 5.9) in Courseware.

This corresponds to textbook sections:

+ [Chapter 6: Tabl](https://www.inferentialthinking.com/chapters/06/tables.html)
+ [Chapter 6.2: Selecting Rows](https://www.inferentialthinking.com/chapters/06/2/selecting-rows.html)

In section 5c, we learned more about building tables. It started with lists, another type of sequence in Python.  Make sure you understand the difference between lists and arrays. Remember that sequences in Python are "0-indexed."  We also learned more table operators, which are defined below.

`tbl.take(row_indices)` returns a table with only the rows at the given indices.  row_indices is an array

`tbl.where(label, condition)` constructs a new table with just the rows that match a given condition

Test your understanding with these practice questions.

### Practice

Q1. Lists can contain values of different types (ints, strings, floats, etc).

    Ans: True

Q2. Arrays can contain values of different types (ints, strings, floats, etc).

    Ans: False

Q3. This list `my_listis ['cat', 'dog', 4, 'three', True]` What is the index of `'cat'` in `my_list`?

    Ans: 0

Q4. What is the index of `True` in the above list?

    Ans: 4, -1


Suppose I have a table called `students` with one row per student and with columns `first_name`, `last_name`, and `grade`. You can assume that the grade is a numerical `score`.

Q5. I want to find all the students with a grade above 95. What table operation should I use? (ignore the arguments). Your answer should be the name of a method, like select or sort.

    a. students.take('grade', are.above(95))
    b. students.where('grade', are.above(95))
    c. students.where('grade', are_above(95))
    d. students.select('grade', are.above(95))

    Ans: b

Q6. Now I want to find all the students with the first name 'Wilton'. I decide to use the where method. Complete the blank in the code. 
students.where('first_name', _______)

    Ans: 'Wilton'
