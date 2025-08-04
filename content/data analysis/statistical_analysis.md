---
section: Data Analysis with Python
nav_order: 7
title: Statistical Analysis
topics: statistics, t-test, anova, chi-square, correlation, regression
---

Now let's perform various statistical tests to extract meaningful insights from our data.

# Descriptive Statistics

```python
from scipy import stats
import numpy as np

# Comprehensive descriptive statistics
def describe_data(data, column_name):
    """Generate comprehensive descriptive statistics."""
    print(f"\n=== Descriptive Statistics for {column_name} ===")
    print(f"Count: {len(data)}")
    print(f"Mean: {np.mean(data):.2f}")
    print(f"Median: {np.median(data):.2f}")
    print(f"Mode: {stats.mode(data, keepdims=True)[0][0]:.2f}")
    print(f"Standard Deviation: {np.std(data, ddof=1):.2f}")
    print(f"Variance: {np.var(data, ddof=1):.2f}")
    print(f"Skewness: {stats.skew(data):.2f}")
    print(f"Kurtosis: {stats.kurtosis(data):.2f}")
    print(f"Range: {np.max(data) - np.min(data):.2f}")
    print(f"IQR: {np.percentile(data, 75) - np.percentile(data, 25):.2f}")

# Analyze salary and age
describe_data(df['salary'], 'Salary')
describe_data(df['age'], 'Age')
```

# T-Tests

```python
# One-sample t-test
# Test if average salary differs significantly from $70,000
population_mean = 70000
t_stat, p_value = stats.ttest_1samp(df['salary'], population_mean)

print(f"\n=== One-Sample T-Test ===")
print(f"Testing if mean salary differs from ${population_mean:,}")
print(f"Sample mean: ${df['salary'].mean():,.2f}")
print(f"T-statistic: {t_stat:.4f}")
print(f"P-value: {p_value:.4f}")
print(f"Significant at α=0.05: {'Yes' if p_value < 0.05 else 'No'}")

# Two-sample t-test
# Compare salaries between IT and Finance departments
it_salaries = df[df['department'] == 'IT']['salary']
finance_salaries = df[df['department'] == 'Finance']['salary']

t_stat, p_value = stats.ttest_ind(it_salaries, finance_salaries)

print(f"\n=== Two-Sample T-Test ===")
print(f"Comparing IT vs Finance salaries")
print(f"IT mean salary: ${it_salaries.mean():,.2f}")
print(f"Finance mean salary: ${finance_salaries.mean():,.2f}")
print(f"T-statistic: {t_stat:.4f}")
print(f"P-value: {p_value:.4f}")
print(f"Significant difference at α=0.05: {'Yes' if p_value < 0.05 else 'No'}")

# Paired t-test example (if we had before/after data)
# Simulate salary increases
np.random.seed(42)
salary_before = df['salary'].sample(30).values
salary_after = salary_before + np.random.normal(5000, 2000, 30)

t_stat, p_value = stats.ttest_rel(salary_before, salary_after)

print(f"\n=== Paired T-Test ===")
print(f"Testing salary increase effectiveness")
print(f"Mean before: ${np.mean(salary_before):,.2f}")
print(f"Mean after: ${np.mean(salary_after):,.2f}")
print(f"T-statistic: {t_stat:.4f}")
print(f"P-value: {p_value:.4f}")
print(f"Significant improvement at α=0.05: {'Yes' if p_value < 0.05 else 'No'}")
```

# ANOVA (Analysis of Variance)

```python
# One-way ANOVA - Compare salaries across all departments
department_groups = [group['salary'].values for name, group in df.groupby('department')]

f_stat, p_value = stats.f_oneway(*department_groups)

print(f"\n=== One-Way ANOVA ===")
print(f"Testing salary differences across all departments")
print(f"F-statistic: {f_stat:.4f}")
print(f"P-value: {p_value:.4f}")
print(f"Significant differences at α=0.05: {'Yes' if p_value < 0.05 else 'No'}")

# Post-hoc analysis if ANOVA is significant
if p_value < 0.05:
    print("\nPost-hoc pairwise comparisons:")
    departments = df['department'].unique()
    for i, dept1 in enumerate(departments):
        for dept2 in departments[i+1:]:
            group1 = df[df['department'] == dept1]['salary']
            group2 = df[df['department'] == dept2]['salary']
            t_stat, p_val = stats.ttest_ind(group1, group2)
            print(f"{dept1} vs {dept2}: p = {p_val:.4f} {'*' if p_val < 0.05 else ''}")

# Two-way ANOVA example (salary by department and age group)
# Create a more balanced dataset for demonstration
balanced_data = []
for dept in df['department'].unique():
    for age_grp in df['age_group'].unique():
        subset = df[(df['department'] == dept) & (df['age_group'] == age_grp)]
        if len(subset) > 0:
            balanced_data.extend(subset[['salary', 'department', 'age_group']].values)

if len(balanced_data) > 0:
    balanced_df = pd.DataFrame(balanced_data, columns=['salary', 'department', 'age_group'])
    
    # Note: For true two-way ANOVA, you'd typically use statsmodels
    print(f"\nTwo-way ANOVA data prepared with {len(balanced_df)} observations")
```

# Chi-Square Tests

```python
# Chi-square test of independence
# Test if department and age group are independent
contingency_table = pd.crosstab(df['department'], df['age_group'])
print(f"\n=== Chi-Square Test of Independence ===")
print("Contingency Table:")
print(contingency_table)

chi2, p_value, dof, expected = stats.chi2_contingency(contingency_table)

print(f"\nChi-square statistic: {chi2:.4f}")
print(f"P-value: {p_value:.4f}")
print(f"Degrees of freedom: {dof}")
print(f"Significant association at α=0.05: {'Yes' if p_value < 0.05 else 'No'}")

# Chi-square goodness of fit test
# Test if department distribution follows expected proportions
observed_freq = df['department'].value_counts().sort_index()
expected_proportions = [0.3, 0.25, 0.25, 0.2]  # Expected proportions
expected_freq = np.array(expected_proportions) * len(df)

chi2, p_value = stats.chisquare(observed_freq, expected_freq)

print(f"\n=== Chi-Square Goodness of Fit Test ===")
print(f"Testing if department distribution matches expected proportions")
print(f"Observed frequencies: {observed_freq.values}")
print(f"Expected frequencies: {expected_freq}")
print(f"Chi-square statistic: {chi2:.4f}")
print(f"P-value: {p_value:.4f}")
print(f"Significant deviation at α=0.05: {'Yes' if p_value < 0.05 else 'No'}")
```

# Correlation and Regression Analysis

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import classification_report, confusion_matrix
```

## Correlation analysis

```python
print(f"\n=== Correlation Analysis ===")
numeric_columns = ['age', 'salary', 'years_employed']
correlation_matrix = df[numeric_columns].corr()
print("Correlation Matrix:")
print(correlation_matrix.round(3))

# Test significance of correlations
def correlation_significance(x, y):
    r, p = stats.pearsonr(x, y)
    return r, p

for i, col1 in enumerate(numeric_columns):
    for col2 in numeric_columns[i+1:]:
        r, p = correlation_significance(df[col1], df[col2])
        print(f"{col1} vs {col2}: r = {r:.3f}, p = {p:.4f} {'*' if p < 0.05 else ''}")
```

## Simple Linear Regression (using scipy)

```python
slope, intercept, r_value, p_value, std_err = stats.linregress(df['age'], df['salary'])

print(f"\n=== Linear Regression: Age predicting Salary ===")
print(f"Slope: {slope:.2f} (salary increase per year of age)")
print(f"Intercept: {intercept:.2f}")
print(f"R-squared: {r_value**2:.4f}")
print(f"P-value: {p_value:.4f}")
print(f"Standard error: {std_err:.2f}")
```

## Logistic Regression

```python
# Predict high salary (above median) based on age and years employed
median_salary = df['salary'].median()
df['high_salary'] = (df['salary'] > median_salary).astype(int)

# Prepare features
X = df[['age', 'years_employed']].values
y = df['high_salary'].values

# Split data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Fit logistic regression
log_reg = LogisticRegression()
log_reg.fit(X_train, y_train)

# Make predictions
y_pred = log_reg.predict(X_test)
y_pred_proba = log_reg.predict_proba(X_test)[:, 1]

print(f"\n=== Logistic Regression: Predicting High Salary ===")
print(f"Model coefficients: {log_reg.coef_[0]}")
print(f"Model intercept: {log_reg.intercept_[0]:.4f}")
print(f"Model accuracy: {log_reg.score(X_test, y_test):.3f}")

print("\nClassification Report:")
print(classification_report(y_test, y_pred))

print("\nConfusion Matrix:")
print(confusion_matrix(y_test, y_pred))
```
