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

Pandas provides a number of reader functions that process files and return a Pandas object (i.e. `DataFrame`). Multiple different file types can be read, like `csv`, `txt`, `xls`, `dta`, and `json`. The `read_table()` function parses the tabular data contained in the files and returns a formatted and indexed `DataFrame`. A number of additional arguments can be specified, allowing us to specify the separator used in delimited text files, which column to use as an index, etc. Additional information on file types and specifications (and lots of other useful info on Pandas!) can be found [here](http://pandas.pydata.org/pandas-docs/stable/api.html).

To start us off, let's look at 311 calls from three NYC zip codes (10010, 10011, 10001)!

This data is in the data folder in the intro_resource folder in our GitHub repo. The file should be called `NYC311_3zips.csv`. Since it is a `csv` file, we will read it in using the pandas `read_csv` function and store it in a new pandas DataFrame that we call `df` (we could, of course, call it anything).

```python
# Make sure the Python path below matched the working directory that you are currently working in (or the one that you launched Atom in). One way to shortcut this, is to use the `os` library that allows you to set your working directory within a folder nested in the folder in which you're already working.

# read in csv with 311 data
import os
os.chdir('intro_resources')

df = pd.read_csv('data/NYC311_3zips.csv', sep=',')

# We can print the first 5 rows of the dataframe
df.head()
```

Notice we have a table! A spreadsheet! And it indexed the rows. Pandas (borrowing from R) calls it a DataFrame. Lets see the types of the columns.

`df`, in Python context, is an instance of the `pd.DataFrame` class, created by calling the `pd.read_table` function, which calls the DataFrame constructor inside of it. `df` is a dataframe object.

## DataFrame Methods
The df object, for example, has methods, or functions belonging to it, which allow it to do things. Above, we ran `df.head()` which is a method that shows the first 5 rows of the dataframe. `df.dtypes` returns the data types of each of the columns. Additional documentation can be found [here](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.html).


```python
df.dtypes
```

We can determine the shape (i.e., the number of rows and columns) of our dataframe by accessing its `shape` property.

```python
df.shape
```

7498 rows times 52 columns! Not exactly *big* data, but pandas can handle *much* bigger data than this. `df.shape` returns a `tuple`, so we can access members of this `tuple` like we do with a `list`:

```python
# Number of rows
df.shape[0]
# Number of columns
df.shape[1]
```

Let's retrieve the DataFrame's column names. We do this by accessing its columns property. While we're at it, let's look into the data type of the object returned by `df.columns`.

```python
df.columns
type(df.columns)
```

The `df.columns` returns an `Index` object, which is a series. This object is built on top of Python `lists`, and has similar methods and attributes.

We can access an individual column using a simple syntax:

```python
df.AgencyName
```
We can also use a more explicit syntax to retrieve a column that can't be so easily misinterpreted.

```python
df['AgencyName']
```

This is useful if we have column names that might also be the names of pandas functions. For example, if we had a column named `count` since `count` is also a built-in pandas function. `count` refers to a specific pandas function that counts the number of non-null observations over a given axis.

We can use the `unique()` method to find the unique values in each column. Let's find the unique values in the `AgencyName` column.

```python
df.AgencyName.unique()
```

If we want to take a subset of our dataframe and turn that into a new dataframe, we can easily select specific columns.

```python
df_someColumns = df[['CreatedDate', 'ClosedDate', 'ComplaintType']]
df_someColumns.head()
```

## Querying

Pandas dataframes have built-in methods for performing queries using a style similar to SQL. This allows us to slice and dice our dataframes with ease. We can apply queries to parts of the `df`, and based on this query select subsets of the whole `df`. Let's do some filtering and querying.

The output of this is a series containing the truth of falsehood of our query - we call this a **mask**.

```python
df['ComplaintType'] == 'Water System'
```

To print out the table with only the rows we want, we can apply what is called a filter. Our query above returned a **mask**---a series containing the Boolean result of evaluating each value in our column against a specified criteria. Let's take a look at all complaints about Asbestos. We can use the `df` mask to "index" into the dataframe to get the rows we want.

```python
water_complaints = df[df['ComplaintType'] == 'Water System']
water_complaints.head()
water_complaints.shape
```

We see that we now have a DataFrame containing observations in which the 311 complaint was about the water system. Using `.shape`, we can see that it contains 1,478 rows.

We can query based on multiple criteria using boolean operators (`&` for `and`, `|` for `or`). All we need to do is add `()` brackets around each condition. The query uses a boolean `&` and each condition creates a mask containing `True` and `False` values.

```python
df[(df['ComplaintType'] == 'Water System') & (df['IncidentZip'] == 10010)]
```

We've now filtered our dataset: we've limited our results to only reflect complaints about water in only one zip code, 10010.

Pandas gives us a simple way to generate summary statistics. The `.describe()` method can be used to return a table that includes the count of non-null rows, their mean, standard deviation, etc.

Say that we want to generate summary statistics for each agency. We can use the `.groupby()` method to collapse a DataFrame on the values stored in a given column. Then, for each unique value stored in the date column, we're executing two given methods: first, we are counting the number of non-null unique keys for each Agency using `.count()`; and second, we are getting summary statistics of those counts using `.describe()`.

The output of this operation produces a summary table of the number of individual 311 calls by agency.

```python
df.groupby('AgencyName')['UniqueKey'].count().describe()
```

We can group by multiple columns as well. Let's calculate summary statistics for the count of individual calls to a given agency in one zip code!

```python
df.groupby(['AgencyName', 'IncidentZip'])['UniqueKey'].count().describe()
```

We can also use built-in pandas methods to calculate individual summary statistics---for example, `.max()`, `.min()`, and `.mean()`! First, we will make a new df for the counts of calls per complaint type. (This is only helpful because our data does not have a count column already.)

```python
ComplaintCount = df.groupby('ComplaintType')['UniqueKey'].count()
ComplaintCount.head()

ComplaintCount.max()
ComplaintCount.min()
ComplaintCount.mean()
ComplaintCount.std()
ComplaintCount.count()
```

You can save these as variables and cast them to strings.

```python
# create min, max, and mean
max_count = ComplaintCount.max()
min_count = ComplaintCount.min()
mean_count = ComplaintCount.mean()

# print out some results
print(f"Maximum number of 311 Calls by Complaint Type: {max_count}")
print(f"Minimum number of 311 Calls by Complaint Type: {min_count}")
print(f"Average number of 311 Calls by Complaint Type: {mean_count}")
```

Say we want to know which complaint has the most calls associated with it.

```python
ComplaintCount[ComplaintCount == ComplaintCount.max()]
```

There is a single complaint row that contains the maximum number of calls. This is not the case for the minimum---the following query returns a table with a large number of complaint rows with only a single 311 call.

```python
ComplaintCount[ComplaintCount == ComplaintCount.min()]
```

##### More to be added here on cleaning data in Pandas and exporting data from Pandas. Check back later for updates!

## Cleaning

One of the most common tasks while working with big data is data cleaning. As we know all too well, datasets are inherently heterogeneous and unstructured. The lack of structure can cause functions to throw errors. We can clean data sets through various methods; if the discrepancies follow a structured pattern, it is possible to use built-in functions, or write our own functions. However, if the errors cannot be structured, we might have to do it manually!
