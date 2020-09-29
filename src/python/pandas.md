---
eleventyNavigation:
  key: Pandas
  order: 4
  parent: Python
layout: topic-layout.njk
---

## Outstanding Questions

Is a DataFrame a collection of Series objects?
Do DataFrame methods always return a new DataFrame?
Do the new DataFrame objects share Series and cells
with ones they were created from?

Pandas DataFrames use Numpy arrays.

## Overview

{% aTargetBlank "https://pandas.pydata.org/", "pandas" %}
is a Python library for data analysis.
For details, see the
{% aTargetBlank "https://pandas.pydata.org/docs/reference/", "API Reference" %}.

To install pandas, enter `pip install pandas`.

To import the pandas library, use `import pandas as pd`.
By convention, "pd" is the name used to refer to the library in code.

Pandas provides two primary data structures.
The `Series` class is used to represent a series of data values
and can be thought of as a single-column spreadsheet.
The `DataFrame` class is used to represent a table of data values
and can be thought of as a multi-column spreadsheet.
It is used more frequently than `Series`.

## Loading Data

A `DataFrame` can be created from many sources.

To create a `DataFrame` from a Python list of dict objects:

```python
dogs_df = pd.DataFrame([
    {'name': 'Maisey', 'breed': 'Treeing Walker Coonhound'},
    {'name': 'Oscar', 'breed': 'German Shorthaired Pointer'},
    {'name': 'Ramsay', 'breed': 'Native American Indian Dog'},
    {'name': 'Comet', 'breed': 'Whippet'}
])
```

To create a `DataFrame` from a CSV file

```python
# If the first line contains column names ...
df = pd.read_csv('file-name.csv') # from comma-separated
df = pd.read_csv('file-name.csv', delimiter='\t') # for tab-separate

# If the first line contains data rather than column names ...
df = pd.read_csv('file-name.csv', names=['colName1', 'colName2', ...])
```

To create a `DataFrame` from an Excel spreadsheet:

```python
df = pd.read_excel('file-name.xlsx', sheet_name='name')
```

To create a `DataFrame` from a NumPy array:

```python
df = pd.DataFrame(data=numpy_array)
```

## Data Types

When pandas creates `Series` and `DataFrame` objects from Python data
it converts Python string and number types to its own types.

| Python type | pandas type |
| ----------- | ----------- |
| str         | object      |
| int         | int64       |
| float       | float64     |

For more detail, see {% aTargetBlank "https://pbpython.com/pandas_dtypes.html",
"Overview of Pandas Data Types" %}.

## Getting Data

Note that these just return data.
To print it, pass the result to the `print` function.

Start indexes (`si`) are inclusive and default to zero.
End indexes (`ei`) are exclusive and default to length.
Column name values below are abbreviated as `cn`.
Row index values below are abbreviated as `ri`.
Column index values below are abbreviated as `ci`.

| Operation                                                                     | Code                                 |
| ----------------------------------------------------------------------------- | ------------------------------------ |
| get column names                                                              | `df.columns`                         |
| get column names as a list                                                    | `list(df.columns)`                   |
| get column data types                                                         | `df.dtypes`                          |
| get cell value                                                                | `df.at[ri, cn]` or `df.iloc[ri, ci]` |
| get all rows <sub>[1](#fn1)</sub>                                             | `df`                                 |
| get first n rows                                                              | `df.head(n)` where n defaults to 5   |
| get last n rows                                                               | `df.tail(n)` where n defaults to 5   |
| get one row                                                                   | `df.iloc[ri]`                        |
| get row range                                                                 | `df.iloc[si:ei]`                     |
| get row index values                                                          | `df.index`                           |
| get one column as a `Series` object                                           | `df.cn` or `df[cn]`                  |
| get one column of specified rows                                              | `df[col_name][si:ei]`                |
| get multiple columns in specified order                                       | `df[[cn1, cn2, ...]]`                |
| get rows matching criteria                                                    | `df.loc(criteria)`                   |
| get statistics of numeric columns<br>including count, min, max, mean, and std | `df.describe()`                      |

<a name="fn1">1</a>: By default the number of rows displayed is limited.
To remove the limit `pd.set_option('display.max_rows', None)`.

Criteria use logical operators like `==`, `!=`, `<`, `<=`, `>=`, and `>`.
Criteria can also use bitwise operators for and (`&`), or (`|`), and not (`~`).

The example below gets all rows where the `name` column contains the letter "a"
and the `breed` column consists of three words.

```python
df.loc[df.name.str.contains('a') & (df.breed.str.split(' ').apply(len) == 3)]
```

The example below gets all rows where the `breed` column
does not contain the word "Dog".

```python
df.loc[~df.breed.str.contains('Dog')]
```

The example below uses a regular expression to get rows
where the breed starts with "w" or "W" (case insensitive).

```python
import re
df.loc[df.breed.str.contains('^W', regex=True, flags=re.I)]
```

To treat `Series` values as strings, add `.str`.
For example, `df.name.str`.

To iterate over all rows:

```python
for index, row in df.iterrows():
    # Use index and row (a Series object) here.
```

## Modifying Data

| Operation                                             | Code                                                         |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| set cell value                                        | `df.at[ri, cn] = value`                                      |
| conditionally set cell value                          | `df.loc[criteria, cn] = value`                               |
| conditionally set multiple cell values                | `df.loc[criteria, [cn1, cn2]] = [value1, value2]`            |
| add column computed from others                       | `df['new_cn'] = expression`                                  |
| add column that is sum of others <sub>[2](#fn2)</sub> | `df['my sum'] = df.iloc[:, si:ei].sum(axis=1)`               |
| delete columns                                        | `df = df.drop(columns=['cn1', 'cn2', ...])`                  |
| delete columns and ignore errors if not present       | `df = df.drop(columns=['cn1', 'cn2', ...], errors='ignore')` |
| reorder and remove columns                            | `df = df[['cn1', 'cn2', ...]]`                               |
| change column names (must specify all)                | `df.columns = cn1, cn2, ...`                                 |

<a name="fn2">2</a>: The first slice (colon) with no number on either side means "all rows".
The second slice specifies a column range.
Specifying `axis=1` means horizontal and `axis=0` means vertical.

Suppose we want to change the "name" column value to be uppercase
for all rows where the "breed" column value is "Whippet".

```python
df.loc[df.breed == 'Whippet', 'name'] = df.name.str.upper()
```

Suppose we want to add a column named "name length"
that holds the length of each "name" value.

```python
df['name length'] = df['name'].apply(len)
```

Suppose we have the columns `width`, `depth`, and `height`
that represent refrigerator dimensions and we want to
add a new `volume` column.

```python
df['volume'] = df.width * df.depth * df.height
```

## Creating New DataFrames

When a new `DataFrame` is created from an existing one
the new one shares memory with original.
So changes to the underlying data affect both `DataFrame`s.

By default new `DataFrame`s retain the same index values at the original.
To reset the index values,
`new_df = new_df.reset_index(drop=True)`
or
`new_df.reset_index(drop=True, inplace=True)`.
Including `drop=True` removes the original index column.

| Operation                | Code                                                       |
| ------------------------ | ---------------------------------------------------------- |
| sort on one column       | `df.sort_values('cn', ascending=Bool)`                     |
| sort on multiple columns | `df.sort_values(['cn1', 'cn2'], ascending=[Bool1, Bool2])` |
| transpose                | `df.T`                                                     |

To sort in place, add `inplace=True`.

## Aggregating Data

The `DataFrame` `groupby` method is used to aggregate data.
It automatically sorts groups alphabetically.
Statistics are often computed from the aggregated data
using the methods `count`, `sum`, and `mean`.

For example, suppose we have a `DataFrame` where each row represents a dog
and the columns are "name", "breed", and "weight".
We can find the number of dogs from each breed
and the average weight of each breed as follows.

```python
# Group data by breed and compute the
# mean of every numeric column within each breed.
df.groupby(['breed']).mean()

# Group data by breed and compute the
# mean of only the "weight" column within each breed.
df.groupby(['breed'])['weight'].mean()

df['count'] = 0 # create new column to hold counts
# Group data by breed and compute the count of each breed.
df.groupby(['breed']).count()['count']
```

We can aggregate across multiple columns. For example:

```python
players = pd.DataFrame([
    {'sport': 'hockey', 'team': 'Oilers', 'name': 'Wayne Gretzky'},
    {'sport': 'hockey', 'team': 'Oilers', 'name': 'Marty McSorley'},
    {'sport': 'hockey', 'team': 'Oilers', 'name': 'Grant Fuhr'},
    {'sport': 'hockey', 'team': 'Bruins', 'name': 'Phil Esposito'},
    {'sport': 'hockey', 'team': 'Bruins', 'name': 'Bobby Orr'},
    {'sport': 'baseball', 'team': 'Cardinals', 'name': 'Bob Gibson'}
])
players.groupby(['sport', 'team']).count()
```

The output is:

```text
   sport      team
baseball Cardinals    1
hockey   Bruins       2
         Oilers       3
```

## Creating Other Representations

| Operation          | Code            |
| ------------------ | --------------- |
| create NumPy array | `df.to_numpy()` |

## Writing Data

To create a CSV file from a `DataFrame`:

```python
df.to_csv(file_path) # comma-separated
df.to_csv(file_path, index=False) # to omit index column
df.to_csv(file_path, sep='\t') # tab-separated
```

To create an Excel file from a `DataFrame`:

```python
df.to_excel(file_path)
df.to_excel(file_path, index=False) # to omit index column
```

## Processing Large Datasets

Some datasets are too large to fit in memory.
One way to work around this limitation is to process the data in chunks of rows.
To demonstrate this, we will use data from the
{% aTargetBlank "https://www.kaggle.com/tmdb/tmdb-movie-metadata",
"TMBD 5000 Movie Dataset" %}.
This is found at the {% aTargetBlank "https://www.kaggle.com/datasets",
"Kaggle" %} website which is a good source for public datasets.

For example:

```python
# Create a new, empty DataFrame.
subset_df = pd.DataFrame()

# Process a large CSV file this many rows at a time.
row_count = 100
for df in pd.read_csv('./movies/tmdb_5000_movies.csv', chunksize=row_count):
    # Only keep rows for movies with a high "vote_average".
    filtered_df = df[df['vote_average'] >= 8]
    subset_df = pd.concat([subset_df, filtered_df])

# Now only the retained rows are available in subset_df
# and we can operate on that.
```