# Basic Data Processing with Pandas

## Introduction

+ Pandas
    + Created in 2008 by Wes McKinney
    + Open source New BSD license
    + 100+ different contributors
+ References
    + Stack Overflow
        + http://stackoverflow.com
        + Massive knowledge forum of python and pandas related content
        + Free to join and participate in
        + Heavily used by pandas developers instead of a mailing list
    + Books
        + Wes McKinney, 'Python for Data Analysis', O'Reilly
        + Matt Harrison, 'Learning the Pandas Library'
    + Planet Python
        + http://planetpython.org/
        + Excellent blog aggregator for python related news
        + Significant number of data science and python tutorials as posted
        + Great blend of applied beginner and higher level python postings


<a href="https://d3c33hcgiwev3.cloudfront.net/ThPPKZeOEeaK1Q4gRyvE8A.processed/full/540p/index.mp4?Expires=1525478400&Signature=NYPazMrxmZWOy9hKKwMPe8J2PYvD8l7oWRsWCpNaCe30bNglWeval5sYOl6KWmHf8~C3PWCsRyAMhTMfPhe0UaHLSax9lUbIRd2rFWOPgL9ryQ0RPM2lgP5cQ9lKOYJrRE9AEfMemDma~wUeENMyrCExe8tb0HxEhf88hAJPhL4_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" style="width:60px;height:60px;border:0;"> 
</a>

## Week 2 Lectures Jupyter Notebook

To download notebooks and datafiles, as well as get help on Jupyter notebooks in the Coursera platform, visit the [Jupyter Notebook FAQ](https://www.coursera.org/learn/python-data-analysis/resources/0dhYG) course resource.

[Web Notebook](https://hub.coursera-notebooks.org/hub/coursera_login?token=YARyOKhmToCEcjioZl6AkA&next=%2Fnotebooks%2FWeek%25202.ipynb)

[Local Notebook](./notebooks/Week02.ipynb)

## The Series Data Structure

![diagram](https://www.kdnuggets.com/wp-content/uploads/pandas-02.png)

+ The Series
    + Name: label of a column
    + Index: the index of a row
    + Value: the element
+ Class `Series`
    + Syntax: `pd.Series(data, index, dtype=None, copy=False)`
    + One-dimensional ndarray with axis labels (including time series)
    + `data`: array-like, dict, or scalar value; Contains data stored in Series
    + `index`: array-like or Index (1d); Values must be hashable and have the same length as `data`. 
    + `dtype`: numpy.dtype or None
    + `copy`: boolean, default False; Copy input data
+ `np.isnan` func:
    + Syntax: `isnan(x, out=None)`
    + Test element-wise for NaN and return result as a boolean array
    + `x`: array_like; input array
    + `out`: ndarray, None, or tuple of ndarray and None; A location into which the result is stored

+ Demo
    ```python
    import pandas as pd
    pd.Series?

    animals = ['Tiger', 'Bear', 'Moose']
    pd.Series(animals)

    numbers = [1, 2, 3]
    pd.Series(numbers)

    animals = ['Tiger', 'Bear', None]
    pd.Series(animals)      # None --> None; dtype: object

    numbers = [1, 2, None]
    pd.Series(numbers)      # None --> NaN; dtype: float64

    import numpy as np
    np.nan == None          # False

    np.nan == np.nan        # False

    np.isnan(np.nan)

    sports = {'Archery': 'Bhutan',
            'Golf': 'Scotland',
            'Sumo': 'Japan',
            'Taekwondo': 'South Korea'}
    s = pd.Series(sports)

    s.index         # Index(['Archery', 'Golf', 'Sumo', 'Taekwondo'], dtype='object')

    s = pd.Series(['Tiger', 'Bear', 'Moose'], index=['India', 'America', 'Canada'])

    sports = {'Archery': 'Bhutan',
            'Golf': 'Scotland',
            'Sumo': 'Japan',
            'Taekwondo': 'South Korea'}
    s = pd.Series(sports, index=['Golf', 'Sumo', 'Hockey']) # only last three taken
    ```

<a href="https://d3c33hcgiwev3.cloudfront.net/deR9JZmEEeaToA55AQb91A.processed/full/540p/index.mp4?Expires=1525478400&Signature=KsI8ZLjCILliqC04ox1NQDk76fV-CCnCsJA3FeP~J55DpQR6dRMcvN6ffqUJ6Prk00ecOnm8TUMudKNsbiR6A2e7pC0XV1wAArn6rNh~rGyoICswJLp2MHSPUKTWuimK2gNzPpXbH06ucv0T~2s9S-QCQwGqyY7QGsAY-EuJO2w_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" style="width:60px;height:60px;border:0;"> 
</a>

## Querying a Series

+ `df.loc` property:
    + Purely label-location based indexer for selection by label.
    + `df.loc[]` is primarily label based, but may also be used with a boolean array.
    + Allowed inputs are:
        + A single label, e.g. `5` or `'a'`, (note that `5` is interpreted as a *label* of the index, and **never** as an integer position along the index).
        + A list or array of labels, e.g. `['a', 'b', 'c']`.
        + A slice object with labels, e.g. `'a':'f'` (note that contrary to usual python slices, **both** the start and the stop are included!).
        + A boolean array.
        + A `callable` function with one argument (the calling Series, DataFrame or Panel) and that returns valid output for indexing (one of the above)

+ `df.iloc` property:
    + Purely integer-location based indexing for selection by position.
    + `df.iloc[]` is primarily integer position based (from `0` to `length-1` of the axis), but may also be used with a boolean array.
    + Allowed inputs are:
        + An integer, e.g. `5`. 
        + A list or array of integers, e.g. `[4, 3, 0]`.
        + A slice object with ints, e.g. `1:7`.
        + A boolean array.
        + A `callable` function with one argument (the calling Series, DataFrame or Panel) and that returns valid output for indexing (one of the above)

+ Demo
    ```python
    sports = {'Archery': 'Bhutan',
            'Golf': 'Scotland',
            'Sumo': 'Japan',
            'Taekwondo': 'South Korea'}
    s = pd.Series(sports)

    s.iloc[3]       # index location
    s.loc['Golf']   # value location
    s[3]            # index location
    s['Golf']       # value location

    sports = {99: 'Bhutan',
            100: 'Scotland',
            101: 'Japan',
            102: 'South Korea'}
    s = pd.Series(sports)

    s[0] #This won't call s.iloc[0] as one might expect, it generates an error instead

    s = pd.Series([100.00, 120.00, 101.00, 3.00])   # auto index w/ number sequence from 0

    # np.sum and iteration
    total = 0
    for item in s:
        total+=item
    print(total)

    total = np.sum(s)
    print(total)

    #this creates a big series of random numbers
    s = pd.Series(np.random.randint(0,1000,10000))
    s.head()

    len(s)

    # run to times and get the average time to execute the code
    %%timeit -n 100
    summary = 0
    for item in s:
        summary += item
    # 1.07 ms ± 95.2 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)

    # get_ipython().run_cell_magic('timeit', '-n 100', 'summary = 0\nfor item in s:\n    summary+=item')

    # generate random series for 10 times
    %%timeit -n 100
    summary = np.sum(s)
    # 144 µs ± 24.1 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)

    # get_ipython().run_cell_magic('timeit', '-n 100', 'summary = np.sum(s)')

    s+=2 #adds two to each item in s using broadcasting
    s.head()

    for label, value in s.iteritems():
        s.set_value(label, value+2)
    s.head()

    %%timeit -n 10
    s = pd.Series(np.random.randint(0,1000,10000))
    for label, value in s.iteritems():
        s.loc[label]= value+2

    # get_ipython().run_cell_magic('timeit', '-n 10', 's = pd.Series(np.random.randint(0,1000,10000))\nfor label, value in s.iteritems():\n    s.loc[label]= value+2')

    %%timeit -n 10
    s = pd.Series(np.random.randint(0,1000,10000))
    s+=2

    # get_ipython().run_cell_magic('timeit', '-n 10', 's = pd.Series(np.random.randint(0,1000,10000))\ns+=2')

    s = pd.Series([1, 2, 3])
    s.loc['Animal'] = 'Bears'

    original_sports = pd.Series({'Archery': 'Bhutan',
                                'Golf': 'Scotland',
                                'Sumo': 'Japan',
                                'Taekwondo': 'South Korea'})
    cricket_loving_countries = pd.Series(['Australia',
                                        'Barbados',
                                        'Pakistan',
                                        'England'], 
                                    index=['Cricket',
                                            'Cricket',
                                            'Cricket',
                                            'Cricket'])
    all_countries = original_sports.append(cricket_loving_countries)

    original_sports
    cricket_loving_countries
    all_countries
    all_countries.loc['Cricket']
    ```

<a href="https://d3c33hcgiwev3.cloudfront.net/nE8CiJePEea_cQqzDLeQwg.processed/full/540p/index.mp4?Expires=1525564800&Signature=eml1y2DEZSD3DW4FUnrzfUiypGLnp8kIOTr43m7-sobpf4sXW80ltXDAyktfSfoZuuNMaifteEJuEvFBtf52LUwKIoug-CwAYNIy-eJxzSeQzKCpQvFRcj1DRU~q~il6LL4R31z3WtjZSeOZZM6T~q--KijBe-0ksPF7ftnH2Ko_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" style="width:60px;height:60px;border:0;"> 
</a>

## The DataFrame Data Structure

<img src="./diagrams/dataframe.png" width="450" alt="DataFrame anotomy">

+ `df.copy` method:
    + Syntax: `df.copy(deep=True)`
    + Make a copy of this objects data
    + `deep`: boolean or string; 
        + True: Make a deep copy, including a copy of the data and the indices.
        + False: neither the indices or the data are copied.
+ `df.drop` method:
    + Syntax: `df.drop(labels=None, axis=0, index=None, columns=None, level=None, inplace=False, errors='raise')`
    + Return new object with labels in requested axis removed
    + `labels`: single label or list-like; Index or column labels to drop.
    + `axis`: int or axis name; Whether to drop labels from the index (0/'index') or columns (1/'columns').
    + `index`, `columns`: single label or list-like; Alternative to specifying `axis` (`labels, axis=1` is equivalent to `columns=labels`).
    + `level`: int or level name; For MultiIndex 
    + `inplace`: bool; True: do operation inplace and return None.
    + `errors`: {'ignore', 'raise'}

    <img src="https://cdn-images-1.medium.com/max/1250/1*ZSehcrMtBWN7_qCWq_HiSg.png" width="600" alt="Anatomy of Pandas DataFrame">

+ Demo
    ```python
    purchase_1 = pd.Series({'Name': 'Chris',
                            'Item Purchased': 'Dog Food',
                            'Cost': 22.50})
    purchase_2 = pd.Series({'Name': 'Kevyn',
                            'Item Purchased': 'Kitty Litter',
                            'Cost': 2.50})
    purchase_3 = pd.Series({'Name': 'Vinod',
                            'Item Purchased': 'Bird Seed',
                            'Cost': 5.00})
    df = pd.DataFrame([purchase_1, purchase_2, purchase_3], index=['Store 1', 'Store 1', 'Store 2'])
    df.head()

    df.loc['Store 2']           # 'Store 2' row
    type(df.loc['Store 2'])     # pandas.core.series.Series
    df.loc['Store 1']           # 'Store 1' row
    df.loc['Store 1', 'Cost']   # ('Store 1', Cost) element
    df.T.loc['Cost']            # Cost column
    df['Cost']                  # Cost column
    df.loc['Store 1']['Cost']   # ('Store 1', Cost) element
    df.loc[:,['Name', 'Cost']]  # 
    df.drop('Store 1')

    copy_df = df.copy()
    copy_df = copy_df.drop('Store 1')
    copy_df

    help(opy_df.drop)

    del copy_df['Name']
    copy_df

    df['Location'] = None
    ```

+ Quiz
    + For the purchase records from the pet store, how would you get a list of all items which had been purchased (regardless of where they might have been purchased, or by whom)?
        ```python
        purchase_1 = pd.Series({'Name': 'Chris',
                                'Item Purchased': 'Dog Food',
                                'Cost': 22.50})
        purchase_2 = pd.Series({'Name': 'Kevyn',
                                'Item Purchased': 'Kitty Litter',
                                'Cost': 2.50})
        purchase_3 = pd.Series({'Name': 'Vinod',
                                'Item Purchased': 'Bird Seed',
                                'Cost': 5.00})

        df = pd.DataFrame([purchase_1, purchase_2, purchase_3], index=['Store 1', 'Store 1', 'Store 2'])

        # Your code here
        ```
    + Answer: 
        ```python
        df['Item Purchased']
        ```
    + For the purchase records from the pet store, how would you update the DataFrame, applying a discount of 20% across all the values in the 'Cost' column?
        ```python
        purchase_1 = pd.Series({'Name': 'Chris',
                                'Item Purchased': 'Dog Food',
                                'Cost': 22.50})
        purchase_2 = pd.Series({'Name': 'Kevyn',
                                'Item Purchased': 'Kitty Litter',
                                'Cost': 2.50})
        purchase_3 = pd.Series({'Name': 'Vinod',
                                'Item Purchased': 'Bird Seed',
                                'Cost': 5.00})

        df = pd.DataFrame([purchase_1, purchase_2, purchase_3], index=['Store 1', 'Store 1', 'Store 2'])

        # Your code here
        ```
    + Answer:
        ```python
        df['Cost'] *= 0.8
        ptint(df)
        ```

    <img src="http://pbpython.com/images/pandas-dataframe-shadow.png" width="600" alt="Creating DataFrame">

<a href="https://d3c33hcgiwev3.cloudfront.net/w6PVAZmGEeaagxL7xdFKxA.processed/full/540p/index.mp4?Expires=1525564800&Signature=cI~uPCjTpOVibCfdgKjXSUO2fSV5tMmHRPm578h5Gfms2Dd08CDs8xYtFW~5uDiS9PwP6SUWTp03wT2h3Ks0OeLf4FmmRAcb9OiFU3x-nkBQv2WjJw7iD13EiRJoRQNN04RMpFTmh5xkALYvwUsoTaweFMTBo9zF2WbtKJnQgwQ_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" style="width:60px;height:60px;border:0;"> 
</a>

## DataFrame Indexing and Loading

+ `rename` method
    + Syntax: `rename(mapper=None, index=None, columns=None, axis=None, copy=True, inplace=False, level=None)`
    + Alter axes labels.
    + `mapper`, `index`, `columns`: dict-like or function; dict-like or functions transformations to apply to that axis' values. Use either `mapper` and `axis` to specify the axis to target with `mapper`, or `index` and `columns`.
    + `axis`: int or str; Axis to target with `mapper`. Can be either the axis name `('index', 'columns')` or number `(0, 1)`. The default is 'index'.
    + `inplace`: boolean
    + `level`: int or level name; In case of a MultiIndex, only rename labels in the specified level.

+ `pd.read_csv` method
    + Signature: `pd.read_csv(filepath_or_buffer, sep=',', delimiter=None, header='infer', names=None, index_col=None, usecols=None, squeeze=False, prefix=None, mangle_dupe_cols=True, dtype=None, engine=None, converters=None, true_values=None, false_values=None, skipinitialspace=False, skiprows=None, nrows=None, na_values=None, keep_default_na=True, na_filter=True, verbose=False, skip_blank_lines=True, parse_dates=False, infer_datetime_format=False, keep_date_col=False, date_parser=None, dayfirst=False, iterator=False, chunksize=None, compression='infer', thousands=None, decimal=b'.', lineterminator=None, quotechar='"', quoting=0, escapechar=None, comment=None, encoding=None, dialect=None, tupleize_cols=False, error_bad_lines=True, warn_bad_lines=True, skipfooter=0, skip_footer=0, doublequote=True, delim_whitespace=False, as_recarray=False, compact_ints=False, use_unsigned=False, low_memory=True, buffer_lines=None, memory_map=False, float_precision=None)`
    + Docstring: Read CSV (comma-separated) file into DataFrame. Also supports optionally iterating or breaking of the file into chunks.
    + Parameters
        + `filepath_or_buffer` (str, pathlib.Path, py._path.local.LocalPath or any object with a `read()` method (such as a file handle or StringIO)): The string could be a URL. Valid URL schemes include http, ftp, s3, and file. For file URLs, a host is expected. For instance, a local file could be `file ://localhost/path/to/table.csv`
        + `sep` (str, default ','): Delimiter to use. If `sep` is None, the `C` engine cannot automatically detect the separator, but the Python parsing engine can, meaning the latter will be used automatically. In addition, separators longer than 1 character and different from `'\s+'` will be interpreted as regular expressions and will also force the use of the Python parsing engine. Note that regex delimiters are prone to ignoring quoted data. Regex example: `'\r\t'`
        + `delimiter` (str, default ``None``): Alternative argument name for `sep`.
        + `delim_whitespace` (boolean, default False): Specifies whether or not whitespace (e.g. `' '` or `'    '`) will be used as the `sep`. Equivalent to setting `sep='\s+'`. If this option is set to True, nothing should be passed in for the `delimiter` parameter.
        + `header` (int or list of ints, default 'infer'): Row number(s) to use as the column names, and the start of the data. Default behavior is as if set to 0 if no `names` passed, otherwise `None`. Explicitly pass `header=0` to be able to replace existing names. The header can be a list of integers that specify row locations for a multi-index on the columns e.g. [0,1,3]. Intervening rows that are not specified will be skipped (e.g. 2 in this example is skipped). Note that this parameter ignores commented lines and empty lines if `skip_blank_lines=True`, so header=0 denotes the first line of data rather than the first line of the file.
        + `names` (array-like, default None): List of column names to use. If file contains no header row, then you should explicitly pass header=None. Duplicates in this list are not allowed unless mangle_dupe_cols=True, which is the default.
        + `index_col` (int or sequence or False, default None): Column to use as the row labels of the DataFrame. If a sequence is given, a MultiIndex is used. If you have a malformed file with delimiters at the end of each line, you might consider index_col=False to force pandas to _not_ use the first column as the index (row names)
        + `usecols` (array-like or callable, default None): Return a subset of the columns. 
            + If array-like, all elements must either be positional (i.e. integer indices into the document columns) or strings that correspond to column names provided either by the user in `names` or inferred from the document header row(s). For example, a valid array-like `usecols` parameter would be [0, 1, 2] or ['foo', 'bar', 'baz'].
            + If callable, the callable function will be evaluated against the column names, returning names where the callable function evaluates to True. An example of a valid callable argument would be `lambda x: x.upper() in ['AAA', 'BBB', 'DDD']`. Using this parameter results in much faster parsing time and lower memory usage.
        + `squeeze` (boolean, default False): If the parsed data only contains one column then return a Series
        + `prefix` (str, default None): Prefix to add to column numbers when no header, e.g. 'X' for X0, X1, ...
        + `mangle_dupe_cols` (boolean, default True): Duplicate columns will be specified as 'X.0'...'X.N', rather than 'X'...'X'. Passing in False will cause data to be overwritten if there are duplicate names in the columns.
        + `dtype` (Type name or dict of column -> type, default None): Data type for data or columns. E.g. {'a': np.float64, 'b': np.int32} Use `str` or `object` to preserve and not interpret dtype. If converters are specified, they will be applied INSTEAD of dtype conversion.
        + `engine` ({'c', 'python'}, optional): Parser engine to use. The C engine is faster while the python engine is currently more feature-complete.
        + `converters` (dict, default None): Dict of functions for converting values in certain columns. Keys can either be integers or column labels
        + `true_values` (list, default None): Values to consider as True
        + `false_values` (list, default None): Values to consider as False
        + `skipinitialspace` (boolean, default False): Skip spaces after delimiter.
        + `skiprows` (list-like or integer or callable, default None):  Line numbers to skip (0-indexed) or number of lines to skip (int) at the start of the file.  If callable, the callable function will be evaluated against the row indices, returning True if the row should be skipped and False otherwise. An example of a valid callable argument would be `lambda x: x in [0, 2]`.
        + `skipfooter` (int, default 0): Number of lines at bottom of file to skip (Unsupported with engine='c')
        + `skip_footer` (int, default 0): DEPRECATED: use the `skipfooter` parameter instead, as they are identical
        + `nrows` (int, default None): Number of rows of file to read. Useful for reading pieces of large files
        + `na_values` (scalar, str, list-like, or dict, default None): Additional strings to recognize as NA/NaN. If dict passed, specific per-column NA values.  By default the following values are interpreted as NaN: '', '#N/A', '#N/A N/A', '#NA', '-1.#IND', '-1.#QNAN', '-NaN', '-nan', '1.#IND', '1.#QNAN', 'N/A', 'NA', 'NULL', 'NaN', 'nan'`.
        + `keep_default_na` (bool, default True): If na_values are specified and keep_default_na is False the default NaN values are overridden, otherwise they're appended to.
        + `na_filter` (boolean, default True): Detect missing value markers (empty strings and the value of na_values). In data without any NAs, passing na_filter=False can improve the performance of reading a large file
        + `verbose` )(boolean, default False): Indicate number of NA values placed in non-numeric columns
        + `skip_blank_lines` (boolean, default True): If True, skip over blank lines rather than interpreting as NaN values
        + `parse_dates` (boolean or list of ints or names or list of lists or dict, default False)
            + boolean: If True -> try parsing the index.
            + list of ints or names: e.g. If [1, 2, 3] -> try parsing columns 1, 2, 3 each as a separate date column.
            + list of lists: e.g.  If [[1, 3]] -> combine columns 1 and 3 and parse as a single date column.
            + dict: e.g. {'foo' : [1, 3]} -> parse columns 1, 3 as date and call result 'foo'

            If a column or index contains an unparseable date, the entire column or index will be returned unaltered as an object data type. For non-standard datetime parsing, use ``pd.to_datetime`` after ``pd.read_csv``

            Note: A fast-path exists for iso8601-formatted dates.
        + `infer_datetime_format` (boolean, default False):  If True and parse_dates is enabled, pandas will attempt to infer the format of the datetime strings in the columns, and if it can be inferred, switch to a faster method of parsing them. In some cases this can increase the parsing speed by 5-10x.
        + `keep_date_col` (boolean, default False): If True and parse_dates specifies combining multiple columns then keep the original columns.
        + `date_parser` (function, default None): Function to use for converting a sequence of string columns to an array of datetime instances. The default uses `dateutil.parser.parser` to do the conversion. Pandas will try to call date_parser in three different ways, advancing to the next if an exception occurs: 1) Pass one or more arrays (as defined by parse_dates) as arguments; 2) concatenate (row-wise) the string values from the columns defined by parse_dates into a single array and pass that; and 3) call date_parser once for each row using one or more strings (corresponding to the columns defined by parse_dates) as arguments.
        + `dayfirst` (boolean, default False):  DD/MM format dates, international and European format
        + `iterator` (boolean, default False): Return TextFileReader object for iteration or getting chunks with `get_chunk()`.
        + `chunksize` (int, default None): Return TextFileReader object for iteration.
        + `compression` ({'infer', 'gzip', 'bz2', 'zip', 'xz', None}, default 'infer'): For on-the-fly decompression of on-disk data. If 'infer', then use gzip, bz2, zip or xz if filepath_or_buffer is a string ending in '.gz', '.bz2', '.zip', or 'xz', respectively, and no decompression otherwise. If using 'zip', the ZIP file must contain only one data file to be read in. Set to None for no decompression.
        + `thousands` (str, default None): Thousands separator
        + `decimal` (str, default '.'): Character to recognize as decimal point (e.g. use ',' for European data).
        + `float_precision` (string, default None): Specifies which converter the C engine should use for floating-point values. The options are `None` for the ordinary converter, `high` for the high-precision converter, and `round_trip` for the round-trip converter.
        + `lineterminator` (str (length 1), default None): Character to break file into lines. Only valid with C parser.
        + `quotechar` (str (length 1), optional):  The character used to denote the start and end of a quoted item. Quoted items can include the delimiter and it will be ignored.
        + `quoting` (int or csv.QUOTE_* instance, default 0): Control field quoting behavior per ``csv.QUOTE_*`` constants. Use one of QUOTE_MINIMAL (0), QUOTE_ALL (1), QUOTE_NONNUMERIC (2) or QUOTE_NONE (3).
        + `doublequote` (boolean, default `True`): When quotechar is specified and quoting is not `QUOTE_NONE`, indicate whether or not to interpret two consecutive quotechar elements INSIDE a field as a single `quotechar` element.
        + `escapechar` (str (length 1), default None): One-character string used to escape delimiter when quoting is QUOTE_NONE.
        + `comment` (str, default None): Indicates remainder of line should not be parsed. If found at the beginning of a line, the line will be ignored altogether. This parameter must be a single character. Like empty lines (as long as `skip_blank_lines=True`), fully commented lines are ignored by the parameter `header` but not by `skiprows`. For example, if comment='#', parsing '#empty\na,b,c\n1,2,3' with `header=0` will result in 'a,b,c' being treated as the header.
        + `encoding` (str, default None): Encoding to use for UTF when reading/writing (ex. 'utf-8'). [List of Python standard encodings](https://docs.python.org/3/library/codecs.html#standard-encodings)
        + `dialect` (str or csv.Dialect instance, default None): If provided, this parameter will override values (default or not) for the following parameters: `delimiter`, `doublequote`, `escapechar`, `skipinitialspace`, `quotechar`, and `quoting`. If it is necessary to override values, a ParserWarning will be issued. See csv.Dialect documentation for more details.
        + `tupleize_cols` (boolean, default False): Leave a list of tuples on columns as is (default is to convert to a Multi Index on the columns)
        + `error_bad_lines` (boolean, default True): Lines with too many fields (e.g. a csv line with too many commas) will by default cause an exception to be raised, and no DataFrame will be returned. If False, then these "bad lines" will dropped from the DataFrame that is returned.
        + `warn_bad_lines` (boolean, default True): If error_bad_lines is False, and warn_bad_lines is True, a warning for each "bad line" will be output.
        + `low_memory` (boolean, default True): Internally process the file in chunks, resulting in lower memory use while parsing, but possibly mixed type inference.  To ensure no mixed types either set False, or specify the type with the `dtype` parameter. Note that the entire file is read into a single DataFrame regardless, use the `chunksize` or `iterator` parameter to return the data in chunks. (Only valid with C parser)
        + `buffer_lines` (int, default None):  DEPRECATED: this argument will be removed in a future version because its value is not respected by the parser
        + `memory_map` (boolean, default False): If a filepath is provided for `filepath_or_buffer`, map the file object directly onto memory and access the data directly from there. Using this option can improve performance because there is no longer any I/O overhead.
    + Returns: `result` (DataFrame or TextParser)


+ Demo
    ```python

    !cat olympics.csv # shell cmd execution

    # CSV file loading
    df = pd.read_csv('olympics.csv')
    df.head()

    # CSV file loading w/ index and row skipping
    df = pd.read_csv('olympics.csv', index_col = 0, skiprows=1)
    df.head()

    df.columns

    for col in df.columns:
        if col[:2]=='01':
            df.rename(columns={col:'Gold' + col[4:]}, inplace=True)
        if col[:2]=='02':
            df.rename(columns={col:'Silver' + col[4:]}, inplace=True)
        if col[:2]=='03':
            df.rename(columns={col:'Bronze' + col[4:]}, inplace=True)
        if col[:1]=='№':
            df.rename(columns={col:'#' + col[1:]}, inplace=True) 

    df.head()
    ```

+ Quiz
    + Suppose we have a CSV file exercise.csv that looks like this:

        Exercise CSV  
        Week 1 Exercises  
        
        | Activity ID | Activity Type | Activity Duration | Calories | 
        |-------------|---------------|-------------------|----------|
        | 125 | Running | 65 | 450 | 
        | 126 | Biking | 40 | 280 | 
        | 127 | Running | 90 | 850 | 
        | 128 | Walking | 30 | 160 | 

        Which of the following would return a DataFrame with the columns = ['Activity Type', 'Activity Duration', 'Calories'] and index = [125, 126, 127, 128] with the name 'Activity ID'?
        
        a. `pd.read_csv('exercise.csv', skiprows=2, index_col=0)`<br/>
        b. `pd.read_excel('exercise.csv', skiprows=2, index_col=0)`<br/>
        c. `pd.read_excel('exercise.csv', skiprows=2, sep='\t')`<br/>
        d. `pd.read_csv('exercise.csv', skiprows=2, sep=',')`<br/>

    + Answer:  a


<a href="https://d3c33hcgiwev3.cloudfront.net/zFPMm5ePEea2tg7d5YqbXg.processed/full/540p/index.mp4?Expires=1525564800&Signature=BW85AthCkYtHJ9xLHWM4xnWm9yoYWWVy1WEu1J4mVtFugzdS76x49rkoaL0JJP3xhAaTVuACmjbxmbnUQyMsp0B8-7Uf2PqaJ6xNy5PHdK-kJepTL48FKWd8C5N-JHo6lkDp6cGhKgm~pC79NPt~OTu9cBzjHPPmT1PZFZtn2Sk_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" style="width:60px;height:60px;border:0;"> 
</a>

## Querying a DataFrame

+ Boolean Masking
    + conceptually efficient and cornerstone of efficient NumPy
    + an array or dataframe  w/ `True` or `False` on each element
    <a href="url"> <br/>
        <img src="./diagrams/booleanMasking.png" alt="The example illustrated hwo booklean masking works" title= "Boolean Masking Example" height="200">
    </a>

+ `df.where` method:
    + Syntax: `df.where(cond, other=nan, inplace=False, axis=None, level=None, errors='raise', try_cast=False, raise_on_error=None)`
    + Return an object of same shape as self and whose corresponding entries are from self where `cond` is True and otherwise are from `other`.
    + `cond`: boolean NDFrame, array-like, or callable; 
        + Where `cond` is True, keep the original value. Where False, replace with corresponding value from `other`.
        + If `cond` is callable, it is computed on the NDFrame and should return boolean NDFrame or array. The callable must not change input NDFrame (though pandas doesn't check it).
    + `other`: scalar, NDFrame, or callable
        + Entries where `cond` is False are replaced with corresponding value from `other`.
        + If other is callable, it is computed on the NDFrame and should return scalar or NDFrame. The callable must not change input NDFrame (though pandas doesn't check it).
    + `inplace`: boolean; Whether to perform the operation in place on the data
    + `axis`: alignment axis if needed
    + `level`: alignment level if needed
    + `errors`: str, {'raise', 'ignore'}, default 'raise'
        + `raise` : allow exceptions to be raised
        + `ignore` : suppress exceptions. On error return original object
+ `df.dropna` method:
    + Syntax: `df.dropna(axis=0, how='any', thresh=None, subset=None, inplace=False)`
    + Return object with labels on given axis omitted where alternately any or all of the data are missing
    + `axis`: {0 or 'index', 1 or 'columns'}, or tuple/list thereof; Pass tuple or list to drop on multiple axes
    + `how`: {'any', 'all'}
        + any : if any NA values are present, drop that label
        + all : if all values are NA, drop that label
    + `thresh`: int; int value : require that many non-NA values
    + `subset`: array-like; Labels along other axis to consider, e.g. if you are dropping rows these would be a list of columns to include 
    + `inplace`: boolean
+ `df.count` method:
    + Syntax: `df.count(axis=0, level=None, numeric_only=False)`
    + Return Series with number of non-NA/null observations over requested axis. Works with non-floating point data as well (detects NaN and None)
    + `axis`: {0 or 'index', 1 or 'columns'}
    + `level`: int or level name; If the axis is a MultiIndex (hierarchical), count along a particular level, collapsing into a DataFrame
    + `numeric_only`: boolean; Include only float, int, boolean data

+ Demo
    ```python
    df['Gold'] > 0      # create boolean mask

    # apply boolean mask to dataframe w/ where function
    only_gold = df.where(df['Gold'] > 0)
    only_gold.head()

    # some countries do not have gold medal
    only_gold['Gold'].count()
    df['Gold'].count()

    # drop rows w/ NaN
    only_gold = only_gold.dropna()
    only_gold.head()

    only_gold = df[df['Gold'] > 0]
    only_gold.head()

    # countries won gold medals in summer or winter
    len(df[(df['Gold'] > 0) | (df['Gold.1'] > 0)])

    # counties won golf medal only in winter
    df[(df['Gold.1'] > 0) & (df['Gold'] == 0)]
    ```
+ Quiz
    + Write a query to return all of the names of people who bought products worth more than $3.00
        ```python
        purchase_1 = pd.Series({'Name': 'Chris',
                                'Item Purchased': 'Dog Food',
                                'Cost': 22.50})
        purchase_2 = pd.Series({'Name': 'Kevyn',
                                'Item Purchased': 'Kitty Litter',
                                'Cost': 2.50})
        purchase_3 = pd.Series({'Name': 'Vinod',
                                'Item Purchased': 'Bird Seed',
                                'Cost': 5.00})

        df = pd.DataFrame([purchase_1, purchase_2, purchase_3], index=['Store 1', 'Store 1', 'Store 2'])

        # Your code here
        ```
    + Answer: `df['Name'][df['Cost']>3]`

<a href="https://d3c33hcgiwev3.cloudfront.net/LHzOC5mHEeaqggpsvkGGZA.processed/full/540p/index.mp4?Expires=1525564800&Signature=BflZUCj82jZiMQn4jQihd5IuGFo8ZCcK6HwJ9CGkISeYIMzYGnAf91Lo44uTmeUPlxfKhRlHV8GNCs2RPu1iO1lw0V7fzk3fTXeybs3qq8QckukBBhaIyoEZt6SZi3OzXK7zARHJOueBkLSYow1m2LY0fBxlROJUKOXl~YtKqdQ_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" style="width:60px;height:60px;border:0;"> 
</a>

## Indexing DataFrames

+ Indexing
    + `index`: row level label
    + `set_index` method: 
        + destructive operation
        + copy the column and set its index to preserve the original index
        + index column offset with original dataframe
        + new 1st row w/ empty value
    + `reset_index` method: remove original indices and create a default numerical indices

+ `df.set_index` method:
    + Syntax: `df.set_index(keys, drop=True, append=False, inplace=False, verify_integrity=False)`
    + Set the DataFrame index (row labels) using one or more existing columns. By default yields a new object.
    + `keys`: column label or list of column labels / arrays
    + `drop`: boolean; Delete columns to be used as the new index
    + `append`: boolean; Whether to append columns to existing index
    + `inplace`: boolean; Modify the DataFrame in place (do not create a new object)
    + `verify_integrity`: boolean; Check the new index for duplicates. Otherwise defer the check until necessary. Setting to False will improve the performance of this method

+ `df.reset_index` method:
    + Syntax: `df.reset_index(level=None, drop=False, inplace=False, col_level=0, col_fill='')`
    + For DataFrame with multi-level index, return new DataFrame with labeling information in the columns under the index names, defaulting to 'level_0', 'level_1', etc. if any are None. For a standard index, the index name will be used (if set), otherwise a default 'index' or 'level_0' (if 'index' is already taken) will be used.
    + `level`: int, str, tuple, or list; Only remove the given levels from the index. Removes all levels by default
    + `drop`: boolean; Do not try to insert index into dataframe columns. This resets the index to the default integer index.
    + `inplace`: boolean; Modify the DataFrame in place (do not create a new object)
    + `col_level`: int or str; If the columns have multiple levels, determines which level the labels are inserted into. By default it is inserted into the first level.
    + `col_fill`: object; If the columns have multiple levels, determines how the other levels are named. If None then the index name is repeated.

+ `df.unique` function
    + Syntax: `df.unique(values)`
    + Hash table-based unique. Uniques are returned in order of appearance. This does NOT sort.
    + `values`: 1d array-like

+ Demo
    ```python
    df['country'] = df.index    # preserve index as column 'country'
    df = df.set_index('Gold')   # set 'Gold' column as index and move to front
    df.head()

    df = df.reset_index()
    df.head()

    df = pd.read_csv('census.csv')
    df.head()                       # only display first 5 rows

    # distinct values in 'SUMLEV' column
    df['SUMLEV'].unique()

    df=df[df['SUMLEV'] == 50]   # reserve rows with SUMLEV=50

    # set of columns to keep
    columns_to_keep = ['STNAME', 'CTYNAME', 'BIRTHS2010',
                    'BIRTHS2011', 'BIRTHS2012', 'BIRTHS2013',
                    'BIRTHS2014', 'BIRTHS2015', 'POPESTIMATE2010',
                    'POPESTIMATE2011', 'POPESTIMATE2012', 'POPESTIMATE2013',
                    'POPESTIMATE2014', 'POPESTIMATE2015']
    
    df = df[columns_to_keep]

    df = df.set_index(['STNAME', 'CTYNAME'])    # dual indices
    df.loc['Michigan', 'Washtenaw County']      # single set of values
    df.loc[ [('Michigan', 'Washtenaw County'),  # multi-sets of values
            ('Michigan', 'Wayne County')] ]
    ```

+ Quiz
    + Reindex the purchase records DataFrame to be indexed hierarchically, first by store, then by person. Name these indexes 'Location' and 'Name'. Then add a new entry to it with the value of:

        Name: 'Kevyn', Item Purchased: 'Kitty Food', Cost: 3.00 Location: 'Store 2'.
        ```python
        purchase_1 = pd.Series({'Name': 'Chris',
                                'Item Purchased': 'Dog Food',
                                'Cost': 22.50})
        purchase_2 = pd.Series({'Name': 'Kevyn',
                                'Item Purchased': 'Kitty Litter',
                                'Cost': 2.50})
        purchase_3 = pd.Series({'Name': 'Vinod',
                                'Item Purchased': 'Bird Seed',
                                'Cost': 5.00})

        df = pd.DataFrame([purchase_1, purchase_2, purchase_3], index=['Store 1', 'Store 1', 'Store 2'])

        # Your answer here  
        ```
    + Answer:
        ```python
        df = df.set_index([df.index, 'Name'])
        df.index.names = ['Location', 'Name']
        df = df.append(pd.Series(data={'Cost': 3.00, 'Item Purchased': 'Kitty Food'}, name=('Store 2', 'Kevyn')))
        df
        ```

<a href="https://d3c33hcgiwev3.cloudfront.net/60unRpePEeaK1Q4gRyvE8A.processed/full/540p/index.mp4?Expires=1525564800&Signature=D2XAgk~woURtyknKbi4bx-12FPNB~42JHGHlKi54CzwLUrc8dqLdXNiswpwRvoxmkQoK7MsMbTM-o2ASqaNPSgX2Na3yUrv6iLjvvcmM4~lZlbwegcKYGRSm~ZBLHMGw~Tm23r8HPKpIyUquWvQrDKg6FDsYsKQ5LrVacGB4SyQ_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" style="width:60px;height:60px;border:0;"> 
</a>

## Missing Values

+ `fillna` method: 
    + Signature: `df.fillna(value=None, method=None, axis=None, inplace=False, limit=None, downcast=None, **kwargs)`
    + Docstring: Fill NA/NaN values using the specified method
    + Parameters
        + `value`: scalar, dict, Series, or DataFrame; Value to use to fill holes (e.g. 0), alternately a dict/Series/DataFrame of values specifying which value to use for each index (for a Series) or column (for a DataFrame). (values not in the dict/Series/DataFrame will not be filled). This value cannot be a list.
        + `method`: {'backfill', 'bfill', 'pad', 'ffill', None}; Method to use for filling holes in reindexed Series, `pad`/`ffill`: propagate last valid observation forward to next valid, `backfill`/`bfill`: use NEXT valid observation to fill gap
        + `axis`: {0 or 'index', 1 or 'columns'}  
        + `inplace`: boolean; If True, fill in place. Note: this will modify any other views on this object, (e.g. a no-copy slice for a column in a DataFrame).
        + `limit`: int; If method is specified, this is the maximum number of consecutive NaN values to forward/backward fill. In other words, if there is a gap with more than this number of consecutive NaNs, it will only be partially filled. If method is not specified, this is the maximum number of entries along the entire axis where NaNs will be filled. Must be greater than 0 if not None.
        + `downcast`: dict; a dict of item->dtype of what to downcast if possible, or the string 'infer' which will try to downcast to an appropriate equal type (e.g. float64 to int64 if possible)

+ `df.sort_index` method:
    + Syntax: `df.sort_index(axis=0, level=None, ascending=True, inplace=False, kind='quicksort', na_position='last', sort_remaining=True, by=None)`
    + Sort object by labels (along an axis)
    + Parameters:
        + `axis`: index, columns to direct sorting
        + `level`: int or level name or list of ints or list of level names
            if not None, sort on values in specified index level(s) 
        + `ascending`: boolean; Sort ascending vs. descending
        + `inplace`: bool; if True, perform operation in-place
        + `kind`: {'quicksort', 'mergesort', 'heapsort'}, default 'quicksort'
        + `na_position`: {'first', 'last'}; `first` puts NaNs at the beginning, `last` puts NaNs at the end. Not implemented for MultiIndex.
        + `sort_remaining`: bool; if true and sorting by level and index is multilevel, sort by other levels too (in order) after sorting by specified level

+ Demo
    ```python
    df = pd.read_csv('log.csv')

    help(pd.DataFrame.fillna)

    df = df.set_index('time')
    df = df.sort_index()

    df = df.reset_index()
    df = df.set_index(['time', 'user'])

    df = df.fillna(method='ffill')
    df.head()
    ```


<a href="https://d3c33hcgiwev3.cloudfront.net/99DDF5ePEeaK1Q4gRyvE8A.processed/full/540p/index.mp4?Expires=1525564800&Signature=BvPVy7JSz-QfzQJawmWgz-jCCdOctkjwFMoV5gw0K4l0A4YSsBnrMrdpZN3iN0O11mh~Ai30CIhpT2v42JDuZ1thRA~i73TxBhU4dfVHsm3T6iF21U3qCp2lRXUksOAslNc5Mz2vs~gQiTQ5JQhIcoK7SzXWrvAkJlFydWmcDhE_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A" target="_blank">
  <img src="http://files.softicons.com/download/system-icons/windows-8-metro-invert-icons-by-dakirby309/png/64x64/Folders%20&%20OS/My%20Videos.png" alt="Video" style="width:60px;height:60px;border:0;"> 
</a>


## Hacked Data

This course uses a third-party tool, Hacked Data, to enhance your learning experience. The tool will reference basic information like your name, email, and Coursera ID.

[Open Tool](https://nzh13lxjj0.execute-api.us-east-1.amazonaws.com/prod/response/2/new/)


## Opinion:

Nathaniel Poor and Roei Davidson from the Data and Society Research Institute were faced with an ethical dilemma when the data they wanted to use for research but couldn't (because of logistics issues) was released by hackers. The data they were interested in was publicly available, but difficult to get at requiring an expensive manual process. The hacked dataset included this public data as well as private messages which they were not interested in. 

Read the case study [here](http://bdes.datasociety.net/wp-content/uploads/2016/10/Patreon-Case-Study.pdf). 

Do you agree with the author's decision to not use the hacked data, and state any arguments they haven't considered for or against the use of this data?



> Agree

> I agree authors's decision not to use the data set.  Yes, the data is available in public domain now.  However, the way and origin of the data is illegal.  The root of the data is malicious.   
>
> According to the Fruit of the poisonous tree theory, the fruit is poisonous no matter how great  it is.   Similarly, the use of the data might come out fruitful results due to the accuracy and completeness of the data set.  However, The ethic issues, in particular, privacy, makes the data improper.  The results are also improper.  Though someone might said the data used was filtered and scanned before use and published.  To get such results based on the rotten root makes the results arguable.  
> 
> Alternatively,  why not contact the data source again and ask their permission for using the data they provide or crawled by authors themselves.  The authors still can get similar results with the proper way.  The results are more respectful and appreciate by others.

### Peer Feedback : Peer Feedback 

A student from Ethiopia agrees with you.  
> I totally agree with the author's decision not to use the hacked data because it would intrude the privacy of many users even though the data was to be used for a research. Furthermore, the research could be done using other means and medium of data which would have been legal whereas using this data would set an example that might lead to increase hacking of personal data in the name of research. The research might just be very biased rather than generalizable because no one can confirm the validity of hacked data.


My Opinion: convincing

> I agree the opinion and found the author provided a  good point.  The use of the data set will implicitly encourage more hackers doing similar activities.  In this case, the data uses for research.  The result seems not too bad.  However, many other usage might cause big damage on other issues, such as trusty between people and the Internet service provider.  That will eventually tear down the trust and hinder the development  and use of technology. 

This activity is a new one, and we would like your feedback on the value of peer review in peer review in Coursera courses like this one. Please share your thoughts to the following:

A student from India agrees with you.  
> I strongly agree with the author's decision to not use the hacked data. The advent of internet has had far reaching effects on humanity. While it can be argued that a vast majority of them are progressive, there has been considerable wrong doing as well. This has left a great degree of skepticism about the internet in the minds of humans . As a progressive species we must try to avoid and eradicate the evil effects of internet to foster faith in skeptics. With that intention, we must not only avoid the use of data that was gathered illegally but actively discourage the very act of hacking data.

My Opinion: convincing

> The opinion remind me  on of the value in Google, Don't be evil.  This is a great part of Internet.  So many people, even county, such as China, manipulate the publicity and freedom of the Internet.  That will block the progressive of the technology eventually.


A student from United Kingdom agrees with you.
> 1. Researchers have a limited capability to distinguish between public and private information within the hacked data. 
> 2. May see private data when cleaning the data. 
> 3. Perhaps legitimizing criminal activity. 
> 4. Violating users’ expectation of privacy. 
> 5. Using people’s data without consent. 
> 6. We want this data, but we don’t need it.  
> Other data can be ethically collected and used. These arguments against using the data, we feel, are much stronger than the arguments for using the data. Thus, in the end, we did not use the data copied and released by the hackers. Considering other cases and academic guidelines, we felt it would not be appropriate. Altogether, despite our hoping to do some good with the data and despite our hope to only use parts of it that were originally public, we felt the negatives outweighed the positives, especially when we could gather all or most of the same data in a more legal and more accepted manner. Some cases of using data (or not) will be clear, other cases will not be. In the spirit of making lemonade out of lemons, we hope our case highlights some of the difficulties and considerations academics may encounter when contemplating the use of data.

My Opinion: convincing

> I agree the comments.  However, the opinion just states some facts not provide consequence of using the data significantly.   The consequence of using such illegal  data will make the opinion much stronger.


