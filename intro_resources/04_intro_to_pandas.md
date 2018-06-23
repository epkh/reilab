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

One of the most common tasks while working with big data is data cleaning. As we know all too well, datasets are inherently heterogeneous and unstructured, and full of errors and gaps. Each of these problems can cause functions to throw errors, and each inform what kinds of inferences we can reasonably draw from our data. We can clean data sets through various methods. It is helpful to start by cleaning discrepancies that follow a structured pattern, because then it is possible to use built-in functions. For less standard discrepancies that still follow some pattern, we can write our own functions. However, if the errors cannot be structured, we might have to do it manually...

A common first step in cleaning is to check for duplicate rows and drop any duplicates. `.duplicated()` checks for rows that are entirely duplicated and returns a boolean, in which duplicates are marked with `True`.

```python
# in our dataset, there are no duplicates.
df.duplicated()
# if there were duplicates, we could easily run this like to drop all the duplicate rows.
df.drop_duplicates()
```
You can get fancy with selecting which duplicate records you care about and which to drop and not drop. This is one of the powerful things about pandas. See [here](https://chrisalbon.com/python/data_wrangling/pandas_delete_duplicates/) and [here](https://medium.com/@kasiarachuta/dealing-with-duplicates-in-pandas-dataframe-789894a28911) for some common tips/tricks.

Next, we check for any fields that are completely `NaN` (or null) and drop those. Having `Nan` or null fields can just clutter our dataset by making us keep track of fields that aren't going to be useful to us. It's a good habit to comment in code when you drop fields in case you want to go back later and see why those fields were dropped. To automatically drop any fields that are entirely blank, you can use the following statement:

```python
df.isnull().all()
# in our dataset, there are no columns that are entirely blank. (This is because I already removed them when cutting this data out of the entire NYC 311 database, but I'm showing you here for reference!)
```

While we don't have any columns completely blank, there are probably many columns that we either don't care about for the purposes of our analysis or columns that have so few populated rows that they won't be useful for our analysis.

There are many ways to get a sense of how many rows are blank in a given column. If you want to get a high-level sense of where there are gaps in your dataset, the python package, `missingno` [(and linked here on GitHub),](https://github.com/ResidentMario/missingno) is a neat way to visualize the gaps in your dataset.

If you just want to check the count of null values in a single column, you can use this method:

```python
df['TaxiCompanyBorough'].isnull().sum()
df['FerryTerminalName'].isnull().sum()
```
If you want to get a sense of what's missing across all the columns---which is helpful in our case because we have 52 columns---one way is to run a simple loop that prints the number of empty observations per field.

```python
# Remember, there are 7498 total rows in our dataset, so we want a count that is as close to zero and as far away from 7498 as possible.

# first we rename each empty cell as 'NaN'
df = df.fillna('NaN')
# then we write a simple function that sums the number of observations in each column that are 'NaN'
def missingcount(i):
  return sum(i == 'NaN')
#next, run these together to run the function
print ("Number of observations with no value:")
print (df.apply(missingcount, axis=0))
#axis=0 defines that function is to be applied on each row
```
Here we see that many columns are entirely populated and some have a few hundred or even a few thousand missing values. But, we will start by dropping the columns that have more than 7000 missing observations. (***Note:*** If you don't know your data well, it is often a good idea to take a look at the observations that DO have values in the columns you're about to drop in case they can tell us something about the dataset. For example, here we can see that the columns with more than 7000 missing are car and ferry related, so by dropping these columns, we are likely dropping information relevant to the few observations that are car or ferry related.)

So, let's drop the columns with more than 7000 missing observations. This is done by using the `.drop()` method and setting the results to be a new dataframe.  

```Python
df_clean = df.drop(['Landmark','VehicleType', 'TaxiCompanyBorough', 'TaxiPickUpLocation', 'BridgeHighwayName', 'BridgeHighwayDirection', 'RoadRamp', 'BridgeHighwaySegment', 'FerryTerminalName'], axis=1)
# here we set axis=1 because we want this to run on each column
#let's double check to see how many columns we just dropped
np.shape(df_clean)
# great! we just dropped 9 columns.

# now, let's take a quick look at our data again.
df_clean.head()
```
If you scroll over, you'll see that in some of the columns, 'Unspecified' seems to pop up a lot. Let's investigate this. 'Unspecified' doesn't tell us anything about the specific observation, so we may want to treat this like a null value. If there are some columns where a vast majority of the observations are 'Unspecified', we may want to drop those columns too.

So, we'll run a similar loop to the one above (again, this is just one of many ways to do this) and count the number of observations with 'Unspecified' in each column.

```Python
# write a new function that counts the observations with 'Unspecified' in each column and print column names and counts
def unspecified(x):
  return sum(x == 'Unspecified')

print ("Number of observations with unspecified:")
print (df.apply(unspecified, axis=0)) #axis=0 tells the function to be applied on each row
```
Again, let's drop the columns with more than 7000 observations that are marked as 'Unspecified' using the same method as above.
```Python
# drop the columns that are all listed as unspecified
df_cleaner = df_clean.drop(['ParkFacilityName', 'SchoolName', 'SchoolNumber', 'SchoolRegion', 'SchoolCode', 'SchoolPhoneNumber', 'SchoolAddress', 'SchoolCity', 'SchoolState', 'SchoolZip', 'SchoolNotFound'], axis=1)
np.shape(df_cleaner)
# great, now we are down to 32 columns which is more manageable than 52!
```

Another common and important step in cleaning is to make sure the dates and times are formatted correctly so that you can use them in your analysis.

```python
# let's look at our datatypes. we can see that there are some columns with 'Date' in the column name but the datatype is an object. This means that python and Pandas won't recognize these as dates.
df_cleaner.dtypes
```
Since we only have 32 columns we can see easily that there are four columns with 'Date' in it:
+ 'CreatedDate'
+ 'ClosedDate'
+ 'DueDate'
+ 'ResolutionActionUpdatedDate'
However, if we had many more columns and couldn't easily see this, we could use a regular expression (regex) to easily filter our columns for any that have the word, date, in them. Regex can be very powerful (and fast!) but we won't go into them here. To learn more about them and the specific syntax, see [here](https://docs.python.org/3.3/howto/regex.html#regex-howto) and [here](http://doc.pyschools.com/html/regex.html).

```Python
df_date = df_cleaner.filter(regex='Date')
df_date
```
So, we'll need to convert our `date` column to a `datetime` type that Python can interpret using the Pandas `pd.to_datetime()` function. Let's start by just focusing on the 'CreatedDate' to show a few things that can be done. Then, you can try to turn these into functions for all the `date` columns on your own!

We'll start by creating a new `CreatedDate_dt` column based on our `CreatedDate` column using the `.to_datetime()` method. To learn more about the many ways you can use `.to_datetime()` see [the pandas documentation](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.to_datetime.html). We do this as follows:

```python
# check to make sure that there are no null values
df_cleaner.CreatedDate.isnull().sum()
# convert to datetime and put in a new column
df_cleaner['CreatedDate_dt'] = pd.to_datetime(df_cleaner['CreatedDate'])
#check the datatype to make sure it worked
df_cleaner.dtypes

# look at our oldest and newest entries, which is only possible now that we're in datetime format
df_cleaner['CreatedDate_dt'].max()
df_cleaner['CreatedDate_dt'].min()

```
Now, let's make a column that is just the date and not the time. This can be useful if we want to look at 311 pings within a given day. Let's also make a column that shows the day of the week and not just the date. This can help us tease out any trends in 311 pings by weekday. Fortunately, Pandas has some built-in functions to do these! We start by using `.dt.normalize()` to select out the date from the full datetime but keep the date in datetime format. Info on this can be [found here](http://pandas.pydata.org/pandas-docs/version/0.23/generated/pandas.Series.dt.normalize.html).

Then, we use...

```python
# first, we make a new column that just includes the date
df_cleaner['CreatedDate_day'] = df_cleaner['CreatedDate_dt'].dt.normalize()
# and then look at it and make sure we still have a datetime datatype
df_cleaner['CreatedDate_day'].head()

#next, let's create a column for the name of the day of the week
weekday = df_cleaner['CreatedDate_day'].dt.weekday
weekday.head()
weekdayname = df_cleaner['CreatedDate_dt'].dt.day_name
pd.__version__
```

[REFERENCE]
Once we've created a new column, we can create another column which uses an internal calendar to determine which day a given calendar date lands on. The one quirk here is that, by convention, the `weekday` function returns a numeric value according to a week that runs from 0 to 6 where 0 is Monday. Our 0 hour is midnight on Sunday, so we'll need to make our weekday number match our `hours` column. We do this using the `.apply() method`.

```python
df['weekday'] = df['date_new'].apply(lambda x: x.weekday() + 1)
df['weekday'].replace(7, 0, inplace = True)
```

`lambda` sounds complicated, but really isn't. It allows us to define a function on the fly---here we're saying "do the following for every row: identify a weekday and add one to the returned value." This results in a range from 1-7 and we still want it to range from 0 to 6, so we replace 7 with 0 using the built-in Pandas `.replace` method.

## Exporting your data
The last step is to export your cleaned data so you can use it in other ways, or just to store it for your records. There are many formats that you can export data in from Pandas. See [here](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.DataFrame.to_csv.html#pandas.DataFrame.to_csv) for the `to_csv` documentation and [here](https://pandas.pydata.org/pandas-docs/stable/api.html#id12) for information on all the formats that you can export with Pandas.  

You'll notice that the statement below looks very similar to the way we read data into Pandas. Just like when we read data in, you may need to change Python's working directory so that your data is saved in the right folder. Here, we want to save it in the `data` folder.


```python
# export csv to your data folder
os.chdir('intro_resources')
df_cleaner.to_csv('data/NYC311_3zips_clean.csv')
```


## Looking at our data

We can now create some basic charts using the fabulous matplotlib.

```python
# This line lets us plot in Atom
import matplotlib
# This line allows the results of plots to be displayed inline with our code.
%matplotlib inline

##day_hours = df[df['date'] == '2017-07-02'].groupby('hour')['count'].sum()
##day_hours.plot()
```
