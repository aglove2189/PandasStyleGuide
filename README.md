# Pandas Style Guide

#### Most of these points were graciously taken from Ted Petrou's [Minimally Sufficient Pandas](https://medium.com/dunder-data/minimally-sufficient-pandas-a8e67f2a2428) article
 
* Use brackets for selecting a column of data over dot notation. This avoids name collisions and column names with spaces and/or reserved characters.

  ```python
  df['count'] # good
  df.count    # ambiguous
  ```

* Use loc and iloc, ix is deprecated.
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
* Use reset_index to avoid a MultiIndex after a groupby call.

  ```python
  df.groupby('column_name').agg({'other_column': 'max'}).reset_index()
  ```

* Use pivot_table over pivot, unstack, or crosstab.
  * Use crosstab if you need to find relative frequency.
* Use melt over stack since it allows you to rename columns and avoids a MultiIndex.
* Avoid iterating over a DataFrame, Pandas is built around vectorization.
  * From fastest to slowest: NumPy array > Pandas vectorized operation > apply > iterrows > Python loop.
  * [Sofia Heisler's article](https://engineering.upside.com/a-beginners-guide-to-optimizing-pandas-code-for-speed-c09ef2c6a4d6) has more detail.
* Use NumPy arrays if your application relies on performance.