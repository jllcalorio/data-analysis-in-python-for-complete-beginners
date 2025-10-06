---
section: Data Analysis with Python
nav_order: 4
title: Data Querying and Selection
topics: query, select, filter
---

Learning to extract specific data is crucial for analysis.

{% include question.html header="Selecting Columns" text="

```python
# Single column selection
names = df['name']
print(f\"Names (Series): {type(names)}\")
```



```python
# Multiple column selection
basic_info = df[['name', 'age', 'department']]
print(f\"Basic info (DataFrame): {type(basic_info)}\")
```



```python
# Column selection with conditions
numeric_columns = df.select_dtypes(include=[np.number])
print(f\"Numeric columns: {list(numeric_columns.columns)}\")
```
" %}

# Selecting Rows

```python
# Row selection by index
first_employee = df.iloc[0]  # First row
first_five = df.iloc[0:5]    # First 5 rows

# Row selection by condition
high_earners = df[df['salary'] > 80000]
it_employees = df[df['department'] == 'IT']

print(f\"High earners: {len(high_earners)} employees\")
print(f\"IT employees: {len(it_employees)} employees\")

# Multiple conditions
senior_it = df[(df['age'] > 40) & (df['department'] == 'IT')]
young_high_earners = df[(df['age'] < 30) & (df['salary'] > 70000)]

print(f\"Senior IT employees: {len(senior_it)}\")
print(f\"Young high earners: {len(young_high_earners)}\")
```

# Advanced Querying

```python
# Using query method (more readable for complex conditions)
experienced_workers = df.query('age > 35 and salary > 60000')
recent_hires = df.query('hire_date > \"2022-01-01\"')

print(f\"Experienced workers: {len(experienced_workers)}\")
print(f\"Recent hires: {len(recent_hires)}\")

# Using isin for multiple values
target_departments = df[df['department'].isin(['IT', 'Finance'])]
print(f\"IT and Finance employees: {len(target_departments)}\")

# String operations
employees_with_a = df[df['name'].str.contains('a', case=False)]
print(f\"Employees with 'a' in name: {len(employees_with_a)}\")
```
