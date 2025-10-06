---
section: Data Analysis with Python
nav_order: 3
title: Reading and Loading Data
topics: read, import, pandas, csv
---

Real-world data comes in various formats. Let's learn to read different file types.

{% include question.html header="Reading CSV Files" text="

Reading CSV files (most common format)

```python
df = pd.read_csv('employees.csv')
```

Common parameters for CSV reading

```python
df_csv = pd.read_csv('data.csv',
                     sep=',',                      # Separator
                     header=0,                     # Row to use as column names
                     index_col=0,                  # Column to use as row index
                     na_values=['N/A', 'NULL'],    # Values to treat as NaN
                     parse_dates=['date_column'],  # Parse dates
                     encoding='utf-8')             # File encoding
```

For demonstration, let's create and save sample data

```python
sample_data = pd.DataFrame({
    'employee_id': range(1, 101),
    'name': [f'Employee_{i}' for i in range(1, 101)],
    'age': np.random.randint(22, 65, 100),
    'salary': np.random.randint(40000, 120000, 100),
    'department': np.random.choice(['IT', 'Finance', 'HR', 'Marketing'], 100),
    'hire_date': pd.date_range('2020-01-01', periods=100, freq='W')
})
```

Save sample data

```python
sample_data.to_csv('sample_employees.csv', index=False)
print(\"Sample data created and saved!\")
```
" %}

{% include question.html header="Reading Other File Formats" text="

Reading Excel files

```python
df_excel = pd.read_excel('data.xlsx', sheet_name='Sheet1')
```

Reading JSON files

```python
df_json = pd.read_json('data.json')
```

Reading SQL databases (requires sqlalchemy)

```python
from sqlalchemy import create_engine
engine = create_engine('sqlite:///database.db')
df_sql = pd.read_sql('SELECT * FROM table_name', engine)
```

For our workshop, let's work with the CSV we created

```python
df = pd.read_csv('sample_employees.csv')
df['hire_date'] = pd.to_datetime(df['hire_date'])  # Convert to datetime

print(\"Data loaded successfully!\")
print(df.head())
```
" %}

{% include question.html header="Handling Missing Data" text="

```python
# Create some missing data for demonstration
df_with_missing = df.copy()
df_with_missing.loc[5:10, 'salary'] = np.nan
df_with_missing.loc[15:20, 'department'] = np.nan

print(\"Missing data summary:\")
print(df_with_missing.isnull().sum())
```

**Strategies for handling missing data**

1. Drop rows with missing values

```python
df_dropped = df_with_missing.dropna()
```

2. Fill missing values

```python
df_filled = df_with_missing.fillna({
    'salary': df_with_missing['salary'].median(),
    'department': 'Unknown'
})
```

3. Forward fill or backward fill

```python
df_ffill = df_with_missing.fillna(method='ffill')

print(f\"Original shape: {df_with_missing.shape}\")
print(f\"After dropping NaN: {df_dropped.shape}\")
print(f\"After filling NaN: {df_filled.shape}\")
```
" %}
