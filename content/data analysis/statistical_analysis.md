---
section: Data Analysis with Python
nav_order: 7
title: Statistical Analysis
topics: statistics, t-test, anova, chi-square, correlation, regression
---

Now let's perform various ```statistical tests``` to extract meaningful insights from our data.

{% include question.html header="Descriptive Statistics" text="

**Descriptive statistics** are tools used to **summarize and describe the main features of a dataset**. In medicine, they help you make sense of patient data, lab results, or clinical trial outcomes **without making predictions or testing hypotheses**.

Think of them as the **vital signs of your data** — they give you a quick snapshot of what’s going on.

🧪 **Key Components You’ll Often Use:**
- Measures of central tendency:
  - Mean (e.g., average blood pressure)
  - Median (e.g., middle value of patient age)
  - Mode (e.g., most common diagnosis)
- Measures of variability:
  - Range (e.g., youngest to oldest patient)
  - Standard deviation (e.g., how spread out glucose levels are)
- Frequencies and proportions:
  - Counts and percentages (e.g., 60% of patients are female)
- Visual summaries (although this belongs to the 'Data Visualization' part, but still are descriptive in nature):
  - Tables, histograms, pie charts — like those in journal articles or case reports


**To start**, let's import the stuff that we need to use.

```python
from scipy import stats
import numpy as np
```

**Let's define a comprehensive descriptive statistics function.**

```python
def describe_data(data, column_name):
    \"\"\"Generate comprehensive descriptive statistics.\"\"\"
    print(f\"\n=== Descriptive Statistics for {column_name} ===\")
    print(f\"Count: {len(data)}\")
    print(f\"Mean: {np.mean(data):.2f}\")
    print(f\"Median: {np.median(data):.2f}\")
    print(f\"Mode: {stats.mode(data, keepdims=True)[0][0]:.2f}\")
    print(f\"Standard Deviation: {np.std(data, ddof=1):.2f}\")
    print(f\"Variance: {np.var(data, ddof=1):.2f}\")
    print(f\"Skewness: {stats.skew(data):.2f}\")
    print(f\"Kurtosis: {stats.kurtosis(data):.2f}\")
    print(f\"Range: {np.max(data) - np.min(data):.2f}\")
    print(f\"IQR: {np.percentile(data, 75) - np.percentile(data, 25):.2f}\")
```

**Analyze salary and age**

```python
describe_data(df['salary'], 'Salary')
describe_data(df['age'], 'Age')
```
" %}

## Univariate tests

{% include question.html header="t-tests" text="

One-sample t-test

Let's check if average salary differs significantly from Php 70,000

```python
population_mean = 70000
t_stat, p_value = stats.ttest_1samp(df['salary'], population_mean)

print(f\"\n=== One-Sample T-Test ===\")
print(f\"Testing if mean salary differs from ${population_mean:,}\")
print(f\"Sample mean: ${df['salary'].mean():,.2f}\")
print(f\"T-statistic: {t_stat:.4f}\")
print(f\"P-value: {p_value:.4f}\")
print(f\"Significant at α=0.05: {'Yes' if p_value < 0.05 else 'No'}\")
```

Two-sample t-test

Let's compare the salaries between IT and Finance departments

```python
it_salaries = df[df['department'] == 'IT']['salary']
finance_salaries = df[df['department'] == 'Finance']['salary']

t_stat, p_value = stats.ttest_ind(it_salaries, finance_salaries)

print(f\"\n=== Two-Sample T-Test ===\")
print(f\"Comparing IT vs Finance salaries\")
print(f\"IT mean salary: ${it_salaries.mean():,.2f}\")
print(f\"Finance mean salary: ${finance_salaries.mean():,.2f}\")
print(f\"T-statistic: {t_stat:.4f}\")
print(f\"P-value: {p_value:.4f}\")
print(f\"Significant difference at α=0.05: {'Yes' if p_value < 0.05 else 'No'}\")
```

Paired t-test example (if we had before/after data)

Let's simulate salary increases

```python
np.random.seed(42)
salary_before = df['salary'].sample(30).values
salary_after = salary_before + np.random.normal(5000, 2000, 30)

t_stat, p_value = stats.ttest_rel(salary_before, salary_after)

print(f\"\n=== Paired T-Test ===\")
print(f\"Testing salary increase effectiveness\")
print(f\"Mean before: ${np.mean(salary_before):,.2f}\")
print(f\"Mean after: ${np.mean(salary_after):,.2f}\")
print(f\"T-statistic: {t_stat:.4f}\")
print(f\"P-value: {p_value:.4f}\")
print(f\"Significant improvement at α=0.05: {'Yes' if p_value < 0.05 else 'No'}\")
```
" %}

{% include question.html header="ANOVA (Analysis of Variance)" text="

One-way Analysis of Variance (ANOVA)

ANOVA is an extension to t-test, where there can be more than 2 groups being compared. In this case, we would like to compare salaries across all departments.

```python
department_groups = [group['salary'].values for name, group in df.groupby('department')]

f_stat, p_value = stats.f_oneway(*department_groups)

print(f\"\n=== One-Way ANOVA ===\")
print(f\"Testing salary differences across all departments\")
print(f\"F-statistic: {f_stat:.4f}\")
print(f\"P-value: {p_value:.4f}\")
print(f\"Significant differences at α=0.05: {'Yes' if p_value < 0.05 else 'No'}\")
```

Post-hoc analysis is required to be implemented if ANOVA is significant, i.e., the p-value < 0.05. This threshold is the usual threshold for significant p-values. You can be very strict and go down to 0.01, or maybe less strict by going up to 0.10. However, the latter is not very recommended because studies with these thresholds

- have results that are considered to have **weak evidence** and increases the risk of **Type I errors**—falsely rejecting a true null hypothesis
- are less likely to replicate in future studies
- Journals and reviewers may view such results as tentative or inconclusive, reducing their impact
- can lead to overstated claims or misleading conclusions in public-facing research

```python
if p_value < 0.05:
    print(\"\nPost-hoc pairwise comparisons:\")
    departments = df['department'].unique()
    for i, dept1 in enumerate(departments):
        for dept2 in departments[i+1:]:
            group1 = df[df['department'] == dept1]['salary']
            group2 = df[df['department'] == dept2]['salary']
            t_stat, p_val = stats.ttest_ind(group1, group2)
            print(f\"{dept1} vs {dept2}: p = {p_val:.4f} {'*' if p_val < 0.05 else ''}\")
            ```



            ```python
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
    print(f\"\nTwo-way ANOVA data prepared with {len(balanced_df)} observations\")
```
" %}

{% include question.html header="Chi-Square Tests" text="

```python
# Chi-square test of independence
# Test if department and age group are independent
contingency_table = pd.crosstab(df['department'], df['age_group'])
print(f\"\n=== Chi-Square Test of Independence ===\")
print(\"Contingency Table:\")
print(contingency_table)

chi2, p_value, dof, expected = stats.chi2_contingency(contingency_table)

print(f\"\nChi-square statistic: {chi2:.4f}\")
print(f\"P-value: {p_value:.4f}\")
print(f\"Degrees of freedom: {dof}\")
print(f\"Significant association at α=0.05: {'Yes' if p_value < 0.05 else 'No'}\")
```



```python
# Chi-square goodness of fit test
# Test if department distribution follows expected proportions
observed_freq = df['department'].value_counts().sort_index()
expected_proportions = [0.3, 0.25, 0.25, 0.2]  # Expected proportions
expected_freq = np.array(expected_proportions) * len(df)

chi2, p_value = stats.chisquare(observed_freq, expected_freq)

print(f\"\n=== Chi-Square Goodness of Fit Test ===\")
print(f\"Testing if department distribution matches expected proportions\")
print(f\"Observed frequencies: {observed_freq.values}\")
print(f\"Expected frequencies: {expected_freq}\")
print(f\"Chi-square statistic: {chi2:.4f}\")
print(f\"P-value: {p_value:.4f}\")
print(f\"Significant deviation at α=0.05: {'Yes' if p_value < 0.05 else 'No'}\")
```
" %}

## Correlation and Regression Analysis

```python
from sklearn.linear_model import LogisticRegression
from sklearn.model_selection import train_test_split
from sklearn.metrics import classification_report, confusion_matrix
```

{% include question.html header="Correlation analysis" text="

```python
print(f\"\n=== Correlation Analysis ===\")
numeric_columns = ['age', 'salary', 'years_employed']
correlation_matrix = df[numeric_columns].corr()
print(\"Correlation Matrix:\")
print(correlation_matrix.round(3))

# Test significance of correlations
def correlation_significance(x, y):
    r, p = stats.pearsonr(x, y)
    return r, p

for i, col1 in enumerate(numeric_columns):
    for col2 in numeric_columns[i+1:]:
        r, p = correlation_significance(df[col1], df[col2])
        print(f\"{col1} vs {col2}: r = {r:.3f}, p = {p:.4f} {'*' if p < 0.05 else ''}\")
```
" %}

{% include question.html header="Simple Linear Regression (using scipy)" text="

```python
slope, intercept, r_value, p_value, std_err = stats.linregress(df['age'], df['salary'])

print(f\"\n=== Linear Regression: Age predicting Salary ===\")
print(f\"Slope: {slope:.2f} (salary increase per year of age)\")
print(f\"Intercept: {intercept:.2f}\")
print(f\"R-squared: {r_value**2:.4f}\")
print(f\"P-value: {p_value:.4f}\")
print(f\"Standard error: {std_err:.2f}\")
```
" %}

{% include question.html header="Logistic Regression" text="

```python
# Predict high salary (above median) based on age and years employed
median_salary = df['salary'].median()
df['high_salary'] = (df['salary'] > median_salary).astype(int)
```



```python
# Prepare features
X = df[['age', 'years_employed']].values
y = df['high_salary'].values
```



```python
# Split data
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)
```



```python
# Fit logistic regression
log_reg = LogisticRegression()
log_reg.fit(X_train, y_train)
```



```python
# Make predictions
y_pred = log_reg.predict(X_test)
y_pred_proba = log_reg.predict_proba(X_test)[:, 1]
```



```python
print(f\"\n=== Logistic Regression: Predicting High Salary ===\")
print(f\"Model coefficients: {log_reg.coef_[0]}\")
print(f\"Model intercept: {log_reg.intercept_[0]:.4f}\")
print(f\"Model accuracy: {log_reg.score(X_test, y_test):.3f}\")

print(\"\nClassification Report:\")
print(classification_report(y_test, y_pred))

print(\"\nConfusion Matrix:\")
print(confusion_matrix(y_test, y_pred))
```
" %}
