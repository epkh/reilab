# Intro to Pandas

Here we will walk through Pandas, an incredibly useful Python library for data cleaning and analysis.

###### Note
This is very closely drawn (and sometimes directly taken) from the MIT Big Data, Visualization, and Society class' Pandas Intro [linked here](https://github.com/ericmhuntley/big-data-spring2018/blob/master/week-03/WS02_pandas_intro.md).

## What is Pandas?

`Pandas` is a Python library for data manipulation and analysis. Pandas expands the data processing capacities of Python and adds a number of classes for easily importing data; in particular, it adds the ability to take numerical tables from various formats and transform them into a Pandas DataFrame object. A `DataFrame` is Panda’s basic object that allows multidimensional data processing and indexing. `DataFrames` can be easily and efficiently queried without the need of cumbersome syntax and convoluted loops. `DataFrames` can be merged with other data, they can be sliced, and they can be reshaped. In a way, we can think of Pandas as a combination of Excel and SQL. For more reading on Pandas, see the [Pandas website and documentation](https://pandas.pydata.org/).


## Resources
Pandas's syntax is a bit different from regular Python syntax. However, it is very close to functionality to `NumPy` in that objects are treated as vectors. In this tutorial, `NumPy` is generally used for math functions.

You may want to reference this fabulous [cheatsheet](http://pandas.pydata.org/Pandas_Cheat_Sheet.pdf) to ease the learning curve and learn about some of its functionality.

## Importing the Pandas Library
Remember that before you get started, you will want to make sure you're in your virtual environment and you launch Atom from within you're virtual environment (i.e. through your command line).

Now, we need to make sure the libraries are imported. If you're seeing an error that Pandas does not exist, you should install it in your command line by using `conda install pandas`.

```python
import pandas as pd
import numpy as np
```

(Note: Here we use the `as` option to allow us to invoke the library with fewer keystrokes.)

## Pandas and DataFrames

You can think of a dataframe as a manipulable, multidimensional Python array. They are based on `NumPy` arrays and can hold structured data. You can perform functions on them to manage data, such as query, select, join, group. Let's set up a really simple dataframe.

```python
# Create empty dataframe
df = pd.DataFrame()

# Create a column
df['name'] = ['Joey', 'Jeremy', 'Jenny']

# View dataframe
df
```

Say we want to add a column. Use the `assign` method.

```python
# Assign a new column to df called 'age' with a list of ages
df.assign(age = [28, 33, 27])
```

Data in this table can be manipulated, queried, sorted, and munged.

## Reading Files

It's probably rare that you'd actually load data like this, and more likely that you'd read in data from another source and then manipulate it using Pandas.

Pandas provides a number of reader functions that process files and return a Pandas object (i.e. `DataFrame`). Multiple different file types can be read, like `csv`, `txt`, `xls`, `dta`, and `json`. The `read_table()` function parses the tabular data contained in the files and returns a formatted and indexed `DataFrame`. A number of additional arguments can be specified, allowing us to specify the separator used in delimited text files, which column to use as an index, etc. Additional information on file types and specifications can be found [here](http://pandas.pydata.org/pandas-docs/stable/api.html).

To start us off, let's look at 311 calls from New York City's Block 800!

This data is in the data folder in the intro_resource folder in our GitHub repo. The file should be called `NYC311_800_clean.csv`. Since it is a `csv` file, we will read it in using the pandas `read_csv` function and store it in a new pandas DataFrame that we call `df` (we could, of course, call it anything).

```python
# Make sure the Python path below matched the working directory that you are currently working in (or the one that you launched Atom in). One way to shortcut this, is to use the `os` library that allows you to set your working directory within a folder nested in the folder in which you're already working.

# read in csv with 311 data
import os
os.chdir('reilab')

df = pd.read_csv('intro_resources/data/NYC311_800_clean.csv', sep=',')

# We can print the first 5 rows of the dataframe
df.head()
```

Notice we have a table! A spreadsheet! And it indexed the rows. Pandas (borrowing from R) calls it a DataFrame. Lets see the types of the columns.

`df`, in Python context, is an instance of the `pd.DataFrame` class, created by calling the `pd.read_table` function, which calls the DataFrame constructor inside of it. `df` is a dataframe object.

## DataFrame Methods
