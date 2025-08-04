---
section: Data Analysis with Python
nav_order: 5
title: Data Filtering and Transformation
topics: filtering, transformation
---

Transform your data to extract insights and prepare for analysis.

# Grouping and Aggregation

```python
# Basic groupby operations
dept_stats = df.groupby('department').agg({
    'salary': ['mean', 'median', 'std', 'count'],
    'age': ['mean', 'min', 'max']
}).round(2)

print("Department statistics:")
print(dept_stats)

# Custom aggregation functions
def salary_range(series):
    return series.max() - series.min()

custom_stats = df.groupby('department').agg({
    'salary': [salary_range, 'mean'],
    'age': ['count']
})

print("\nCustom aggregation:")
print(custom_stats)
```

# Data Transformation

```python
# Creating new columns
df['salary_category'] = pd.cut(df['salary'], 
                              bins=[0, 50000, 75000, 100000, float('inf')],
                              labels=['Low', 'Medium', 'High', 'Very High'])

df['years_employed'] = (pd.Timestamp.now() - df['hire_date']).dt.days / 365.25
df['years_employed'] = df['years_employed'].round(1)

df['age_group'] = pd.cut(df['age'], 
                        bins=[0, 30, 45, 60, 100],
                        labels=['Young', 'Mid-career', 'Senior', 'Veteran'])

print("New columns created:")
print(df[['name', 'salary', 'salary_category', 'years_employed', 'age_group']].head())
```

# Sorting and Ranking

```python
# Sorting data
salary_sorted = df.sort_values('salary', ascending=False)
print("Top 5 earners:")
print(salary_sorted[['name', 'salary', 'department']].head())

# Multiple column sorting
multi_sorted = df.sort_values(['department', 'salary'], ascending=[True, False])
print("\nSorted by department, then salary (desc):")
print(multi_sorted[['name', 'department', 'salary']].head(10))

# Ranking
df['salary_rank'] = df['salary'].rank(ascending=False)
df['dept_salary_rank'] = df.groupby('department')['salary'].rank(ascending=False)

print("\nSalary rankings:")
print(df[['name', 'department', 'salary', 'salary_rank', 'dept_salary_rank']].head())
```
