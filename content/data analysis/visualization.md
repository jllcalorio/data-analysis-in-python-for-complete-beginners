---
section: Data Analysis with Python
nav_order: 6
title: Data Visualization
topics: matplotlib, seaborn, visualization
---

Visualizations help us understand patterns and communicate insights effectively.

# Basic Plotting with Matplotlib

```python
import matplotlib.pyplot as plt

# Set up plotting style
plt.style.use('default')
fig_size = (12, 8)

# Histogram - Distribution of salaries
plt.figure(figsize=fig_size)
plt.hist(df['salary'], bins=20, edgecolor='black', alpha=0.7)
plt.title('Distribution of Salaries', fontsize=16)
plt.xlabel('Salary ($)', fontsize=12)
plt.ylabel('Frequency', fontsize=12)
plt.grid(True, alpha=0.3)
plt.show()

# Box plot - Salary by department
plt.figure(figsize=fig_size)
departments = df['department'].unique()
salary_by_dept = [df[df['department'] == dept]['salary'] for dept in departments]

plt.boxplot(salary_by_dept, labels=departments)
plt.title('Salary Distribution by Department', fontsize=16)
plt.xlabel('Department', fontsize=12)
plt.ylabel('Salary ($)', fontsize=12)
plt.xticks(rotation=45)
plt.grid(True, alpha=0.3)
plt.show()
```

# Advanced Plotting with Seaborn

```python
import seaborn as sns

# Set seaborn style
sns.set_style("whitegrid")
plt.figure(figsize=(15, 10))

# 1. Correlation heatmap
plt.subplot(2, 3, 1)
correlation_matrix = df[['age', 'salary', 'years_employed']].corr()
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', center=0)
plt.title('Correlation Matrix')

# 2. Scatter plot with regression line
plt.subplot(2, 3, 2)
sns.scatterplot(data=df, x='age', y='salary', hue='department', alpha=0.7)
sns.regplot(data=df, x='age', y='salary', scatter=False, color='red')
plt.title('Age vs Salary by Department')

# 3. Distribution plot
plt.subplot(2, 3, 3)
for dept in df['department'].unique():
    dept_data = df[df['department'] == dept]['salary']
    sns.distplot(dept_data, label=dept, hist=False)
plt.title('Salary Distribution by Department')
plt.legend()

# 4. Box plot
plt.subplot(2, 3, 4)
sns.boxplot(data=df, x='department', y='salary')
plt.title('Salary by Department')
plt.xticks(rotation=45)

# 5. Count plot
plt.subplot(2, 3, 5)
sns.countplot(data=df, x='salary_category', hue='department')
plt.title('Salary Categories by Department')
plt.xticks(rotation=45)

# 6. Violin plot
plt.subplot(2, 3, 6)
sns.violinplot(data=df, x='age_group', y='salary')
plt.title('Salary Distribution by Age Group')
plt.xticks(rotation=45)

plt.tight_layout()
plt.show()
```

# Interactive Plotting Concepts

```python
# Creating summary visualizations
fig, axes = plt.subplots(2, 2, figsize=(15, 12))

# Age distribution
axes[0, 0].hist(df['age'], bins=15, edgecolor='black', alpha=0.7, color='skyblue')
axes[0, 0].set_title('Age Distribution')
axes[0, 0].set_xlabel('Age')
axes[0, 0].set_ylabel('Frequency')

# Salary by department (bar plot)
dept_avg_salary = df.groupby('department')['salary'].mean().sort_values(ascending=False)
axes[0, 1].bar(dept_avg_salary.index, dept_avg_salary.values, color='lightcoral')
axes[0, 1].set_title('Average Salary by Department')
axes[0, 1].set_xlabel('Department')
axes[0, 1].set_ylabel('Average Salary ($)')
axes[0, 1].tick_params(axis='x', rotation=45)

# Years employed vs salary
axes[1, 0].scatter(df['years_employed'], df['salary'], alpha=0.6, color='green')
axes[1, 0].set_title('Years Employed vs Salary')
axes[1, 0].set_xlabel('Years Employed')
axes[1, 0].set_ylabel('Salary ($)')

# Department composition pie chart
dept_counts = df['department'].value_counts()
axes[1, 1].pie(dept_counts.values, labels=dept_counts.index, autopct='%1.1f%%')
axes[1, 1].set_title('Department Composition')

plt.tight_layout()
plt.show()
```
