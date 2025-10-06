---
section: Data Analysis with Python
nav_order: 2
title: Introduction to Pandas
topics: pandas, data frame, data, structured data
---

**Pandas** is the cornerstone of data analysis in Python. It provides powerful data structures and tools for working with structured data.

## Key Data Structures

{% include question.html header="Series - One-dimensional data" text="

```python
import pandas as pd
```

Creating a Series

```python
ages = pd.Series([25, 30, 35, 28, 32],
                 index=['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'])

print(ages)
print(f\"Data type: {ages.dtype}\")
print(f\"Shape: {ages.shape}\")
```

Basic operations

```python
print(f\"Mean age: {ages.mean()}\")
print(f\"Oldest person: {ages.idxmax()}\")
```
" %}

{% include question.html header="DataFrame - Two-dimensional data" text="

Creating a DataFrame

```python
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Age': [25, 30, 35, 28, 32],
    'City': ['New York', 'London', 'Tokyo', 'Paris', 'Sydney'],
    'Salary': [70000, 80000, 90000, 75000, 85000],
    'Department': ['IT', 'Finance', 'IT', 'HR', 'Finance']
}

df = pd.DataFrame(data)
print(df)
print(f\"\nDataFrame shape: {df.shape}\")
print(f\"Column names: {list(df.columns)}\")
print(f\"Data types:\n{df.dtypes}\")
```
" %}

{% include question.html header="DataFrame Inspection Methods" text="

Below are some essential DataFrame methods.

This code prints the 1st 3 rows of the DataFrame.

```python
print(df.head(3))
```

This code prints the last 2 rows of the DataFrame.

```python
print(df.tail(2))
```

This code prints the some information about the DataFrame.

```python
print(df.info())
```

This code prints quick and simple descriptive statistics for the DataFrame.

```python
print(df.describe())
```

This code prints column-specific information from a DataFrame.

```python
print(f\"Unique cities: {df['City'].nunique()}\")
print(f\"Value counts for Department:\n{df['Department'].value_counts()}\")
```
" %}
