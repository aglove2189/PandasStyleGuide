# Pandas Style Guide

#### Most of these points were graciously taken from Ted Petrou's [Minimally Sufficient Pandas](https://medium.com/dunder-data/minimally-sufficient-pandas-a8e67f2a2428) article
 
* Use brackets for selecting a column of data over dot notation.
  * This avoids column names with spaces and/or reserved characters and name collisions (is df.count a column name or a count of a dataframe?).

  ```python
  df['count'] # good
  df.count    # ambiguous
  ```

* ix is deprecated, use loc and iloc instead.
* Use NumPy arrays if your application relies on performance for selecting a single cell of data.
* Use read_csv over read_table (only difference is what delimiter is being used by default).
* Use isna and notna over isnull and notnull (aliases of each other).
* Use the Pandas method over any built-in Python function with the same name.

  ```python
  df['column_name'].sum() # faster
  sum(df['column_name'])  # slower
  ```

* Use df.groupby('grouping column').agg({'aggregating column': 'aggregating function'}) as your primary syntax of choice.
  * More room for configuration
  * Easily expandable
  * Easily decomposable into separate variables if needed
* Avoid using a MultiIndex. Flatten it after a call to groupby by renaming columns and resetting the index.

  ```python
  df.groupby('column_name').agg({'other_column': 'max'}).reset_index()
  ```

* Use pivot_table over pivot, unstack, or crosstab.
  * Use crosstab when finding relative frequency.
* Use melt over stack because it allows you to rename columns and it avoids a MultiIndex
