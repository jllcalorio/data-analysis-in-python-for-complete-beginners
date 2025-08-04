---
section: Data Analysis with Python
nav_order: 2
title: Introduction to Pandas
topics: pandas, data frame, data, structured data
---

**Pandas** is the cornerstone of data analysis in Python. It provides powerful data structures and tools for working with structured data.

# Key Data Structures
## Series - One-dimensional data

```python
import pandas as pd

# Creating a Series
ages = pd.Series([25, 30, 35, 28, 32], 
                 index=['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'])
print(ages)
print(f"Data type: {ages.dtype}")
print(f"Shape: {ages.shape}")

# Basic operations
print(f"Mean age: {ages.mean()}")
print(f"Oldest person: {ages.idxmax()}")
```

## DataFrame - Two-dimensional data

```python
# Creating a DataFrame
data = {
    'Name': ['Alice', 'Bob', 'Charlie', 'Diana', 'Eve'],
    'Age': [25, 30, 35, 28, 32],
    'City': ['New York', 'London', 'Tokyo', 'Paris', 'Sydney'],
    'Salary': [70000, 80000, 90000, 75000, 85000],
    'Department': ['IT', 'Finance', 'IT', 'HR', 'Finance']
}

df = pd.DataFrame(data)
print(df)
print(f"\nDataFrame shape: {df.shape}")
print(f"Column names: {list(df.columns)}")
print(f"Data types:\n{df.dtypes}")
```

## DataFrame Inspection Methods

```python
# Essential DataFrame methods
print("First 3 rows:")
print(df.head(3))

print("\nLast 2 rows:")
print(df.tail(2))

print("\nDataFrame info:")
print(df.info())

print("\nDescriptive statistics:")
print(df.describe())

print("\nColumn-specific info:")
print(f"Unique cities: {df['City'].nunique()}")
print(f"Value counts for Department:\n{df['Department'].value_counts()}")
```
