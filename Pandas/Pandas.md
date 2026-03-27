<div align="center">

# <span style="color:#0A2FA8">Pandas</span>


</div>

---

## <span style="color:#1565C0">1. Introduction to Pandas</span>

> **Definition:** Pandas is a powerful open-source Python library for data manipulation and analysis. It provides fast, flexible, and expressive data structures designed to make working with structured (tabular, multidimensional, potentially heterogeneous) and time series data both easy and intuitive.

```
Raw Data → Pandas (Series / DataFrame) → Clean, Analyze, Transform → Insights
```

**Two core data structures:**

| Structure | Dimensions | Think of it as |
|:---:|:---:|:---:|
| `Series` | 1D | A single column |
| `DataFrame` | 2D | A full spreadsheet / table |

**Standard import convention:**
```python
import numpy as np
import pandas as pd
```

---

## <span style="color:#1565C0">2. Pandas Series</span>

### <span style="color:#2E86AB">2.1 What is a Series?</span>

> **Definition:** A Series is a one-dimensional labeled array capable of holding any data type (integers, strings, floats, Python objects, etc.). The axis labels are collectively referred to as the **index**.

### <span style="color:#2E86AB">2.2 Creating a Series</span>

**From a list (default integer index):**
```python
my_data = [10, 20, 30]
pd.Series(my_data)
# 0    10
# 1    20
# 2    30
```

**From a list with custom index:**
```python
labels = ['a', 'b', 'c']
pd.Series(data=my_data, index=labels)
# a    10
# b    20
# c    30
```

**From a NumPy array:**
```python
arr = np.array([10, 20, 30])
pd.Series(arr)
```

**From a dictionary (keys become index):**
```python
d = {'a': 10, 'b': 20, 'c': 30}
pd.Series(d)
# a    10
# b    20
# c    30
```

### <span style="color:#2E86AB">2.3 Series Key Properties</span>

| Property | Description | Example |
|---|---|---|
| `.values` | Returns underlying data as NumPy array | `s.values` |
| `.index` | Returns the index labels | `s.index` |
| `.dtype` | Data type of the series | `s.dtype` |
| `.shape` | Tuple of dimensions | `s.shape` |
| `.name` | Name of the series | `s.name = 'Sales'` |

---

## <span style="color:#1565C0">3. Pandas DataFrame</span>

### <span style="color:#2E86AB">3.1 What is a DataFrame?</span>

> **Definition:** A DataFrame is a 2-dimensional labeled data structure with columns of potentially different data types. It is the most commonly used pandas object - like a spreadsheet or SQL table.

### <span style="color:#2E86AB">3.2 Creating a DataFrame</span>

**From a dictionary (most common):**
```python
data = {
    'name':   ['Alice', 'Bob', 'Charlie', 'David', 'Eve'],
    'age':    [25, 30, 35, 40, 45],
    'city':   ['New York', 'Los Angeles', 'Chicago', 'Houston', 'Phoenix'],
    'Salary': [50000, 60000, 70000, 80000, 90000]
}
df = pd.DataFrame(data)
```

**From a list of lists (then assign column names):**
```python
data_list = [
    ['Alice', 25, 'New York', 50000],
    ['Bob',   30, 'Los Angeles', 60000],
]
df2 = pd.DataFrame(data_list)
df2.columns = ['name', 'age', 'city', 'Salary']
```

**From a CSV / Excel file:**
```python
df = pd.read_csv('file.csv')
df = pd.read_excel('file.xlsx')
```

---

## <span style="color:#1565C0">4. Basic DataFrame Operations</span>

### <span style="color:#2E86AB">4.1 Inspection Methods</span>

| Method | What it returns |
|---|---|
| `df.shape` | Tuple (rows, columns) |
| `df.columns` | Column names |
| `df.index` | Row index |
| `df.dtypes` | Data type of each column |
| `df.info()` | Full summary (nulls, types, memory) |
| `df.describe()` | Statistical summary (count, mean, std, min, max, quartiles) |
| `df.head(n)` | First n rows (default 5) |
| `df.tail(n)` | Last n rows (default 5) |

```python
df.shape       # (5, 4)
df.columns     # Index(['name', 'age', 'city', 'Salary'])
df.info()      # Prints full column info
df.describe()  # Stats for numerical columns
```

### <span style="color:#2E86AB">4.2 Column Operations</span>

**Access a single column (returns Series):**
```python
df['age']
```

**Access multiple columns (returns DataFrame):**
```python
df[['name', 'city']]
```

**Add a new column:**
```python
df['designation'] = ['Data Scientist', 'Data Analyst', 'Data Engineer', 'ML Engineer', 'AI Researcher']
```

**Drop a column:**
```python
df.drop('designation', axis=1, inplace=True)
# axis=1 → drop column | inplace=True → modifies original df
```

**Drop a row:**
```python
df.drop(0, axis=0, inplace=True)
# axis=0 → drop row
```

### <span style="color:#2E86AB">4.3 Arithmetic Operations on Columns</span>

```python
df['Salary'] + 10000   # Add 10000 to all values
df['Salary'] - 5000    # Subtract
df['Salary'] * 1.1     # Multiply (e.g., 10% raise)
df['Salary'] / 12      # Divide (e.g., monthly salary)
```

> **Key Rule:** Arithmetic operations return a new Series - they do **not** modify the original DataFrame unless you reassign.

---

## <span style="color:#1565C0">5. Selecting & Filtering Data</span>

### <span style="color:#2E86AB">5.1 loc vs iloc</span>

| Accessor | Based on | Syntax |
|:---:|:---:|:---|
| `.loc` | **Label** (index name) | `df.loc[row_label, col_label]` |
| `.iloc` | **Integer position** | `df.iloc[row_int, col_int]` |

```python
# Select row by label
df.loc[1]              # Row with index label 1
df.loc[[1, 2]]         # Rows with index labels 1 and 2

# Select rows and specific columns by label
df.loc[0:3, ['name', 'age']]

# Select by integer position
df.iloc[0]             # First row
df.iloc[0:3, 0:2]      # First 3 rows, first 2 columns
```

### <span style="color:#2E86AB">5.2 Conditional / Boolean Filtering</span>

**Single condition:**
```python
df[df['age'] > 32]
```

**Multiple conditions (use `&` for AND, `|` for OR):**
```python
df[(df['age'] > 30) & (df['Salary'] > 80000)]
df[(df['age'] < 30) | (df['city'] == 'Chicago')]
```

**Using `.isin()`:**
```python
df[df['city'].isin(['New York', 'Chicago'])]
```

**Using `.str` methods:**
```python
df[df['name'].str.startswith('A')]
df[df['city'].str.contains('Los')]
```

---

## <span style="color:#1565C0">6. Applying Functions</span>

### <span style="color:#2E86AB">6.1 .apply() - Column-wise or Row-wise</span>

> **Definition:** `.apply()` lets you apply any function along an axis of the DataFrame or to a Series element-by-element.

```python
# Define a custom function
def square(x):
    return x ** 2

# Apply to a single column
df['B'].apply(square)

# Apply lambda function
df['Salary'].apply(lambda x: x * 1.1)

# Apply across rows (axis=1)
df.apply(lambda row: row['age'] + row['Salary'] / 1000, axis=1)
```

**Save the result back into a new column:**
```python
df['Salary_Squared'] = df['Salary'].apply(square)
```

### <span style="color:#2E86AB">6.2 .map() - Element-wise on Series</span>

```python
# Replace values using a dictionary
df['city'].map({'New York': 'NY', 'Chicago': 'CHI'})
```

### <span style="color:#2E86AB">6.3 .applymap() / .map() - Element-wise on DataFrame</span>

```python
# Pandas 2.x: use .map() on DataFrame
df[['age', 'Salary']].map(lambda x: x * 2)
```

---

## <span style="color:#1565C0">7. Handling Missing Data</span>

### <span style="color:#2E86AB">7.1 Detecting Missing Values</span>

> **Definition:** Missing data in pandas is represented as `NaN` (Not a Number) for numeric data, or `None` for object types.

```python
df.isna()          # Boolean mask: True where value is missing
df.isnull()        # Same as isna()
df.isna().sum()    # Count of NaN per column
df.isna().any()    # True/False per column - does it have any NaN?
df.isna().all()    # True if entire column is NaN
```

### <span style="color:#2E86AB">7.2 Removing Missing Values</span>

```python
df.dropna()              # Drop ALL rows with any NaN
df.dropna(axis=1)        # Drop columns with any NaN
df.dropna(thresh=4)      # Keep rows with at least 4 non-NaN values
df.dropna(how='all')     # Drop rows only if ALL values are NaN
```

### <span style="color:#2E86AB">7.3 Filling Missing Values</span>

```python
df.fillna(0)                          # Fill all NaN with 0
df.fillna({'a': 10, 'b': 20})         # Fill per column
df.fillna(df.mean())                  # Fill with column mean
df.fillna(df.median())                # Fill with column median
df.fillna(method='ffill')             # Forward fill (propagate last valid)
df.fillna(method='bfill')             # Backward fill
```

> **Remember:** `fillna()` / `dropna()` do NOT modify the original DataFrame unless you use `inplace=True` or reassign: `df = df.fillna(0)`.

### <span style="color:#2E86AB">7.4 Missing Data Decision Table</span>

| Situation | Recommended Action |
|---|---|
| Very few missing values | `dropna()` |
| Many rows affected | `fillna(mean/median)` |
| Time-series data | `fillna(method='ffill')` |
| Categorical data | `fillna(mode()[0])` |
| Domain-specific default | `fillna(specific_value)` |

---

## <span style="color:#1565C0">8. GroupBy & Aggregation</span>

### <span style="color:#2E86AB">8.1 GroupBy - Split-Apply-Combine</span>

> **Definition:** `groupby()` splits data into groups based on criteria, applies a function to each group independently, and combines the results into a data structure.

```
Split → Apply → Combine
```

```python
data = {
    'category': ['A', 'A', 'B', 'B', 'C', 'C'],
    'store':    ['X', 'Y', 'X', 'Y', 'X', 'Y'],
    'sales':    [100, 150, 200, 250, 300, 350],
    'Quantity': [10,   15,  20,  25,  30,  35],
}
df = pd.DataFrame(data)

grouped = df.groupby('category')
```

**Iterate through groups:**
```python
for name, group_df in grouped:
    print(name)
    print(group_df)
```

### <span style="color:#2E86AB">8.2 Aggregation Functions</span>

**Single aggregation:**
```python
grouped[['sales', 'Quantity']].sum()
grouped['sales'].mean()
grouped['sales'].count()
grouped['sales'].max()
grouped['sales'].min()
```

**Multiple aggregations with `.agg()`:**
```python
df['sales'].agg(['mean', 'sum', 'max', 'min'])
# Returns all four stats at once
```

**Different aggregations per column:**
```python
df.groupby('category').agg({
    'sales':    ['sum', 'mean'],
    'Quantity': ['sum', 'max']
})
```

### <span style="color:#2E86AB">8.3 Multi-column GroupBy</span>

```python
grouped_multi = df.groupby(['category', 'store'])
grouped_multi[['sales', 'Quantity']].sum()
# Returns MultiIndex DataFrame
```

### <span style="color:#2E86AB">8.4 Common Aggregation Reference</span>

| Function | Description |
|:---:|---|
| `.sum()` | Total sum |
| `.mean()` | Average |
| `.median()` | Middle value |
| `.std()` | Standard deviation |
| `.var()` | Variance |
| `.count()` | Non-null count |
| `.min()` / `.max()` | Minimum / Maximum |
| `.first()` / `.last()` | First / Last value in group |
| `.nunique()` | Count unique values |

---

## <span style="color:#1565C0">9. Merging, Joining & Concatenation</span>

### <span style="color:#2E86AB">9.1 pd.merge() - SQL-style Joins</span>

> **Definition:** `merge()` combines two DataFrames based on a common key column, similar to SQL JOIN operations.

```python
df1 = pd.DataFrame({
    'EmployeeID': [1, 2, 3, 4],
    'Name':       ['Alice', 'Bob', 'Charlie', 'David'],
    'Department': ['HR', 'IT', 'Finance', 'IT']
})
df2 = pd.DataFrame({
    'EmployeeID': [1, 2, 3, 5],
    'Salary':     [50000, 60000, 55000, 70000],
    'bonus':      [5000,  6000,  5500,  7000]
})
```

**Inner Join - only matching keys:**
```python
pd.merge(df1, df2, on='EmployeeID', how='inner')
# Returns: EmployeeID 1, 2, 3 (common to both)
```

**Outer Join - all records, NaN for no match:**
```python
pd.merge(df1, df2, on='EmployeeID', how='outer')
# Returns: all IDs (1, 2, 3, 4, 5); NaN where missing
```

**Left Join - all from left, match from right:**
```python
pd.merge(df1, df2, on='EmployeeID', how='left')
# Returns: all from df1; NaN for ID 4 salary
```

**Right Join - all from right, match from left:**
```python
pd.merge(df1, df2, on='EmployeeID', how='right')
# Returns: all from df2; NaN for ID 5 name/dept
```

### <span style="color:#2E86AB">9.2 Join Types Visual</span>

| Join Type | Keeps | Missing Values |
|:---:|:---:|:---:|
| `inner` | Only matching rows | None |
| `outer` | All rows from both | NaN for non-matches |
| `left` | All rows from left df | NaN from right |
| `right` | All rows from right df | NaN from left |

### <span style="color:#2E86AB">9.3 pd.concat() - Stacking DataFrames</span>

> **Definition:** `concat()` stacks DataFrames either vertically (row-wise) or horizontally (column-wise).

```python
df1 = pd.DataFrame({'a': ['a1','a2','a3'], 'b': ['b1','b2','b3']})
df2 = pd.DataFrame({'a': ['a4','a5','a6'], 'b': ['b4','b5','b6']})

# Vertical stack (add rows) - axis=0 (default)
pd.concat([df1, df2])

# Horizontal stack (add columns) - axis=1
pd.concat([df1, df2], axis=1)

# Reset index after concat
pd.concat([df1, df2], ignore_index=True)
```

### <span style="color:#2E86AB">9.4 df.join() - Index-based Join</span>

> **Definition:** `join()` combines DataFrames on their **index** rather than on a column.

```python
df1 = pd.DataFrame({'name': ['Alice', 'Bob'], 'age': [25, 30]})
df2 = pd.DataFrame({'city': ['New York', 'Los Angeles']})

df1.join(df2)
# Joins on shared index (0, 1)

df1.join(df2, lsuffix='_left', rsuffix='_right')
# Add suffixes when column names overlap
```

### <span style="color:#2E86AB">9.5 merge vs join vs concat</span>

| Method | Key Basis | Best For |
|:---:|:---:|---|
| `pd.merge()` | Column key | SQL-style joins on a common column |
| `df.join()` | Index | Quick join when indices align |
| `pd.concat()` | Positional | Stacking multiple DataFrames |

---

## <span style="color:#1565C0">10. Pivot Tables</span>

### <span style="color:#2E86AB">10.1 What is a Pivot Table?</span>

> **Definition:** A pivot table summarizes data by grouping rows and columns and applying an aggregation function - transforming long-format data into a wide, cross-tabulated view.

```python
pd.pivot_table(df,
               values='sales',      # column to aggregate
               index='Region',      # becomes row labels
               columns='product')   # becomes column headers
```

**With explicit aggregation function:**
```python
pd.pivot_table(df,
               values='Revenue',
               index='Month',
               columns='Quarter',
               aggfunc='sum')
```

**Multiple aggregation functions:**
```python
pd.pivot_table(df,
               values='sales',
               index='Region',
               columns='product',
               aggfunc=['sum', 'mean'])
```

### <span style="color:#2E86AB">10.2 pd.crosstab() - Frequency Table</span>

> **Definition:** `crosstab()` creates a frequency table counting how many times combinations of two categorical variables appear.

```python
pd.crosstab(df['Region'], df['product'])
# Shows count of records for each Region × product combination
```

### <span style="color:#2E86AB">10.3 Pivot Table Parameters</span>

| Parameter | Description |
|---|---|
| `values` | Column to aggregate |
| `index` | Rows of the pivot table |
| `columns` | Columns of the pivot table |
| `aggfunc` | Function(s): `'sum'`, `'mean'`, `['sum','mean']` |
| `fill_value` | Replace NaN in the result |
| `margins` | Add row/column totals (`margins=True`) |

---

## <span style="color:#1565C0">11. Sorting & Ranking</span>

### <span style="color:#2E86AB">11.1 Sorting</span>

```python
df.sort_values('Salary')                         # Ascending (default)
df.sort_values('Salary', ascending=False)        # Descending
df.sort_values(['age', 'Salary'], ascending=[True, False])  # Multi-column
df.sort_index()                                  # Sort by index
```

### <span style="color:#2E86AB">11.2 Ranking</span>

```python
df['Salary'].rank()                        # Default: average for ties
df['Salary'].rank(method='min')            # Lowest rank for ties
df['Salary'].rank(ascending=False)         # Rank largest as 1
```

---

## <span style="color:#1565C0">12. String Operations (.str accessor)</span>

> **Definition:** The `.str` accessor provides vectorized string functions on Series, allowing you to apply string methods element-wise.

```python
df['name'].str.upper()           # Convert to uppercase
df['name'].str.lower()           # Convert to lowercase
df['name'].str.len()             # Length of each string
df['name'].str.strip()           # Remove leading/trailing whitespace
df['name'].str.replace('a', 'A') # Replace characters
df['name'].str.contains('Ali')   # Boolean: does it contain substring?
df['name'].str.startswith('A')   # Boolean: starts with?
df['name'].str.split(' ')        # Split into list
df['city'].str[:3]               # Slice - first 3 characters
```

---

## <span style="color:#1565C0">13. DateTime Operations</span>

> **Definition:** Pandas provides `pd.Timestamp`, `pd.DatetimeIndex`, and the `.dt` accessor for powerful date and time manipulation.

**Creating date ranges:**
```python
pd.date_range('2023-01-01', periods=6, freq='D')  # Daily
pd.date_range('2023-01-01', periods=4, freq='M')  # Monthly
```

**Extracting date components with `.dt`:**
```python
df['date'].dt.year
df['date'].dt.month
df['date'].dt.month_name()        # 'January', 'February', ...
df['date'].dt.day
df['date'].dt.day_name()          # 'Monday', 'Tuesday', ...
df['date'].dt.quarter             # 1, 2, 3, or 4
df['date'].dt.week                # Week number
```

**Useful date operations:**
```python
df['date'] + pd.Timedelta(days=7)       # Add 7 days
(df['end_date'] - df['start_date']).dt.days  # Difference in days
pd.to_datetime(df['date_string'])       # Convert string to datetime
```

---

## <span style="color:#1565C0">14. Data Cleaning Techniques</span>

### <span style="color:#2E86AB">14.1 Renaming Columns</span>

```python
df.rename(columns={'old_name': 'new_name'}, inplace=True)
df.columns = ['col1', 'col2', 'col3']   # Rename all at once
```

### <span style="color:#2E86AB">14.2 Changing Data Types</span>

```python
df['age'].astype(float)
df['date'].astype('datetime64[ns]')
df['category'].astype('category')       # Memory efficient for categoricals
pd.to_numeric(df['col'], errors='coerce')  # Convert, set errors to NaN
```

### <span style="color:#2E86AB">14.3 Removing Duplicates</span>

```python
df.duplicated()                         # Boolean mask
df.duplicated().sum()                   # Count duplicates
df.drop_duplicates()                    # Remove all duplicate rows
df.drop_duplicates(subset=['name'])     # Remove duplicates by column
df.drop_duplicates(keep='last')         # Keep last occurrence
```

### <span style="color:#2E86AB">14.4 Replacing Values</span>

```python
df.replace(0, np.nan)                              # Replace 0 with NaN
df['city'].replace('NY', 'New York')               # Replace in a column
df.replace({'a': 1, 'b': 2})                       # Replace using dict
```

### <span style="color:#2E86AB">14.5 Resetting Index</span>

```python
df.reset_index()                # Adds old index as column
df.reset_index(drop=True)       # Discards old index entirely
df.set_index('name')            # Set column as index
```

---

## <span style="color:#1565C0">15. Reading & Writing Data</span>

### <span style="color:#2E86AB">15.1 Reading Data</span>

| Format | Function | Common Parameters |
|---|---|---|
| CSV | `pd.read_csv('file.csv')` | `sep`, `header`, `index_col`, `usecols`, `nrows` |
| Excel | `pd.read_excel('file.xlsx')` | `sheet_name`, `header` |
| JSON | `pd.read_json('file.json')` | `orient` |
| SQL | `pd.read_sql(query, conn)` | `con` |
| Parquet | `pd.read_parquet('file.parquet')` | - |

```python
df = pd.read_csv('data.csv', index_col=0, parse_dates=['date'])
```

### <span style="color:#2E86AB">15.2 Writing Data</span>

```python
df.to_csv('output.csv', index=False)
df.to_excel('output.xlsx', index=False, sheet_name='Sheet1')
df.to_json('output.json', orient='records')
```

---

## <span style="color:#1565C0">16. Important Parameters to Remember</span>

### <span style="color:#2E86AB">16.1 inplace Parameter</span>

> **Definition:** When `inplace=True`, the operation modifies the DataFrame directly. When `inplace=False` (default), it returns a new DataFrame leaving the original unchanged.

<div align="center" style="border: 2px solid #D4A017; border-radius: 8px; padding: 14px 24px; margin: 12px auto; max-width: 540px;">

### <span style="color:#D4A017">df.drop(..., inplace=True) → modifies original</span>
### <span style="color:#D4A017">df = df.drop(...) → also modifies original (via reassignment)</span>

</div>

### <span style="color:#2E86AB">16.2 axis Parameter</span>

<div align="center" style="border: 2px solid #D4A017; border-radius: 8px; padding: 14px 24px; margin: 12px auto; max-width: 400px;">

### <span style="color:#D4A017">axis=0 → Rows (default) | axis=1 → Columns</span>

</div>

```python
df.drop('col_name', axis=1)   # Drop a column
df.drop(0, axis=0)            # Drop row with label 0
df.sum(axis=0)                # Sum down each column
df.sum(axis=1)                # Sum across each row
```

---

## <span style="color:#1565C0">17. Quick Reference Cheat Sheet</span>

### <span style="color:#2E86AB">DataFrame Creation</span>

```python
pd.DataFrame(dict)                    # From dict
pd.DataFrame(list_of_lists)           # From list
pd.read_csv('file.csv')               # From CSV
```

### <span style="color:#2E86AB">Inspection</span>

```python
df.shape / df.columns / df.dtypes    # Structure
df.head() / df.tail()                # Preview
df.info() / df.describe()            # Summary
```

### <span style="color:#2E86AB">Selection</span>

```python
df['col']                            # One column
df[['col1', 'col2']]                 # Multiple columns
df.loc[label]                        # Row by label
df.iloc[position]                    # Row by position
df[df['col'] > val]                  # Conditional filter
```

### <span style="color:#2E86AB">Missing Data</span>

```python
df.isna().sum()                      # Count NaN
df.dropna()                          # Remove NaN rows
df.fillna(value)                     # Fill NaN
```

### <span style="color:#2E86AB">GroupBy & Aggregation</span>

```python
df.groupby('col').sum()
df.groupby('col').agg(['mean','sum'])
pd.pivot_table(df, values, index, columns, aggfunc)
```

### <span style="color:#2E86AB">Merging</span>

```python
pd.merge(df1, df2, on='key', how='inner/outer/left/right')
pd.concat([df1, df2], axis=0/1)
df1.join(df2)
```

### <span style="color:#2E86AB">Transformation</span>

```python
df['col'].apply(func)                # Apply function
df['col'].map(dict)                  # Map values
df.sort_values('col')                # Sort
df.drop_duplicates()                 # Remove dups
df.rename(columns={'old':'new'})     # Rename
```

---

## <span style="color:#1565C0">18. Things to Always Remember</span>

| # | Rule |
|:---:|---|
| 1 | Operations on DataFrames return **new objects** unless `inplace=True` |
| 2 | `axis=0` = rows, `axis=1` = columns - memorize this |
| 3 | `.loc` uses labels; `.iloc` uses integer positions |
| 4 | `&` and `\|` for multiple conditions - wrap each condition in `()` |
| 5 | `groupby()` without aggregation returns a GroupBy object - you must call `.sum()`, `.mean()`, etc. |
| 6 | `pd.merge()` is for key-column joins; `pd.concat()` is for stacking |
| 7 | `.apply()` doesn't change the original - reassign or use a new column |
| 8 | `fillna()` / `dropna()` are not in-place by default |
| 9 | Always `parse_dates=True` or `parse_dates=['col']` when reading time data |
| 10 | Use `.copy()` when slicing to avoid `SettingWithCopyWarning` |

---

<div align="center">



**Compiled from hands-on practice notebooks covering Series, DataFrames, Operations, GroupBy, Aggregation, Missing Data, Merging, Joining, Concatenation, and Pivot Tables**

</div>

---

<div align="center">

<sub>These notes were written and compiled by</sub>

### **Sagar Bhadra**

<sub>Connect with me on</sub>

<br>

[![GitHub](https://img.shields.io/badge/GitHub-SagarBhadra01-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/SagarBhadra01)&nbsp;
[![X (Twitter)](https://img.shields.io/badge/Twitter-SagarBhadra01-000000?style=for-the-badge&logo=x&logoColor=white)](https://x.com/SagarBhadra01)&nbsp;
[![LinkedIn](https://img.shields.io/badge/LinkedIn-sagarbhadra01-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/sagarbhadra01)&nbsp;
[![Gmail](https://img.shields.io/badge/Gmail-sagarbhadra404@gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:sagarbhadra404@gmail.com)

</div>