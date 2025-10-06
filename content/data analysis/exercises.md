---
section: Data Analysis with Python
nav_order: 8
title: Exercises with Solutions
topics: exercises
---

{% include question.html header="Exercise 1: Sales Data Analysis" text="

Analyze a sales dataset to extract business insights.

" solution="

```python
# Create sample sales data
np.random.seed(42)
n_records = 1000

sales_data = pd.DataFrame({
    'date': pd.date_range('2023-01-01', periods=n_records, freq='D'),
    'product_category': np.random.choice(['Electronics', 'Clothing', 'Books', 'Home'], n_records),
    'sales_amount': np.random.exponential(100, n_records) + 50,
    'quantity': np.random.poisson(3, n_records) + 1,
    'customer_type': np.random.choice(['New', 'Returning'], n_records, p=[0.3, 0.7]),
    'region': np.random.choice(['North', 'South', 'East', 'West'], n_records),
    'discount_applied': np.random.choice([True, False], n_records, p=[0.4, 0.6])
})

# Add some derived columns
sales_data['month'] = sales_data['date'].dt.month
sales_data['quarter'] = sales_data['date'].dt.quarter
sales_data['day_of_week'] = sales_data['date'].dt.day_name()

print(\"Sales Data Analysis\")
print(\"=\" * 50)

# 1. Basic descriptive statistics
print(\"1. Descriptive Statistics:\")
print(sales_data.describe())

# 2. Monthly sales trends
monthly_sales = sales_data.groupby('month').agg({
    'sales_amount': ['sum', 'mean', 'count'],
    'quantity': 'sum'
}).round(2)

print(f\"\n2. Monthly Sales Summary:\")
print(monthly_sales)

# 3. Category performance analysis
category_performance = sales_data.groupby('product_category').agg({
    'sales_amount': ['sum', 'mean'],
    'quantity': 'sum',
    'date': 'count'  # Number of transactions
}).round(2)

print(f\"\n3. Category Performance:\")
print(category_performance)

# 4. Statistical tests
print(f\"\n4. Statistical Analysis:\")

# Test if sales differ significantly between customer types
new_customer_sales = sales_data[sales_data['customer_type'] == 'New']['sales_amount']
returning_customer_sales = sales_data[sales_data['customer_type'] == 'Returning']['sales_amount']

t_stat, p_value = stats.ttest_ind(new_customer_sales, returning_customer_sales)
print(f\"New vs Returning Customer Sales:\")
print(f\"New customers mean: ${new_customer_sales.mean():.2f}\")
print(f\"Returning customers mean: ${returning_customer_sales.mean():.2f}\")
print(f\"T-test p-value: {p_value:.4f}\")
print(f\"Significant difference: {'Yes' if p_value < 0.05 else 'No'}\")

# ANOVA for sales across regions
region_groups = [group['sales_amount'].values for name, group in sales_data.groupby('region')]
f_stat, p_value = stats.f_oneway(*region_groups)
print(f\"\nANOVA for sales across regions:\")
print(f\"F-statistic: {f_stat:.4f}, p-value: {p_value:.4f}\")

# 5. Visualization
fig, axes = plt.subplots(2, 2, figsize=(15, 12))

# Monthly trend
monthly_trend = sales_data.groupby('month')['sales_amount'].sum()
axes[0, 0].plot(monthly_trend.index, monthly_trend.values, marker='o')
axes[0, 0].set_title('Monthly Sales Trend')
axes[0, 0].set_xlabel('Month')
axes[0, 0].set_ylabel('Total Sales ($)')

# Category comparison
category_sales = sales_data.groupby('product_category')['sales_amount'].sum()
axes[0, 1].bar(category_sales.index, category_sales.values)
axes[0, 1].set_title('Sales by Product Category')
axes[0, 1].set_xlabel('Category')
axes[0, 1].set_ylabel('Total Sales ($)')
axes[0, 1].tick_params(axis='x', rotation=45)

# Customer type comparison
customer_comparison = sales_data.groupby('customer_type')['sales_amount'].mean()
axes[1, 0].bar(customer_comparison.index, customer_comparison.values, color=['skyblue', 'lightcoral'])
axes[1, 0].set_title('Average Sales by Customer Type')
axes[1, 0].set_xlabel('Customer Type')
axes[1, 0].set_ylabel('Average Sales ($)')

# Sales distribution
axes[1, 1].hist(sales_data['sales_amount'], bins=30, edgecolor='black', alpha=0.7)
axes[1, 1].set_title('Distribution of Sales Amounts')
axes[1, 1].set_xlabel('Sales Amount ($)')
axes[1, 1].set_ylabel('Frequency')

plt.tight_layout()
plt.show()

print(\"\n\" + \"=\"*50)
print(\"Exercise 1 Complete: Sales data analyzed successfully!\")
```
" %}

{% include question.html header="Exercise 2: Customer Segmentation Analysis" text="

Perform customer segmentation using statistical methods.

" solution="

```python
# Create customer data
np.random.seed(123)
n_customers = 500

customer_data = pd.DataFrame({
    'customer_id': range(1, n_customers + 1),
    'age': np.random.normal(40, 12, n_customers).astype(int),
    'annual_income': np.random.normal(60000, 20000, n_customers),
    'spending_score': np.random.normal(50, 25, n_customers),
    'years_as_customer': np.random.exponential(3, n_customers),
    'total_purchases': np.random.poisson(10, n_customers),
    'avg_order_value': np.random.gamma(2, 50, n_customers),
    'customer_service_calls': np.random.poisson(2, n_customers),
    'email_opens': np.random.binomial(20, 0.3, n_customers),
    'region': np.random.choice(['Urban', 'Suburban', 'Rural'], n_customers)
})

# Clean unrealistic values
customer_data['age'] = customer_data['age'].clip(18, 80)
customer_data['annual_income'] = customer_data['annual_income'].clip(20000, 200000)
customer_data['spending_score'] = customer_data['spending_score'].clip(0, 100)

print(\"Customer Segmentation Analysis\")
print(\"=\" * 50)

# 1. Exploratory Data Analysis
print(\"1. Customer Data Overview:\")
print(customer_data.describe())

# 2. Customer segmentation based on spending patterns
def create_customer_segments(df):
    \"\"\"Create customer segments based on income and spending score.\"\"\"
    # Create quartiles for income and spending
    df['income_quartile'] = pd.qcut(df['annual_income'], 4, labels=['Low', 'Medium', 'High', 'Premium'])
    df['spending_quartile'] = pd.qcut(df['spending_score'], 4, labels=['Low', 'Medium', 'High', 'Very High'])

    # Create combined segments
    segment_map = {
        ('Low', 'Low'): 'Budget Conscious',
        ('Low', 'Medium'): 'Budget Conscious',
        ('Low', 'High'): 'Aspirational',
        ('Low', 'Very High'): 'Aspirational',
        ('Medium', 'Low'): 'Conservative',
        ('Medium', 'Medium'): 'Mainstream',
        ('Medium', 'High'): 'Mainstream',
        ('Medium', 'Very High'): 'High Value',
        ('High', 'Low'): 'Conservative',
        ('High', 'Medium'): 'Conservative',
        ('High', 'High'): 'High Value',
        ('High', 'Very High'): 'Premium',
        ('Premium', 'Low'): 'Conservative',
        ('Premium', 'Medium'): 'High Value',
        ('Premium', 'High'): 'Premium',
        ('Premium', 'Very High'): 'Premium'
    }

    df['customer_segment'] = df.apply(
        lambda row: segment_map.get((row['income_quartile'], row['spending_quartile']), 'Other'),
        axis=1
    )

    return df

customer_data = create_customer_segments(customer_data)

# 3. Segment analysis
segment_analysis = customer_data.groupby('customer_segment').agg({
    'annual_income': ['mean', 'median'],
    'spending_score': ['mean', 'median'],
    'total_purchases': ['mean', 'sum'],
    'avg_order_value': 'mean',
    'customer_service_calls': 'mean',
    'customer_id': 'count'
}).round(2)

print(f\"\n2. Customer Segment Analysis:\")
print(segment_analysis)

# 4. Statistical tests across segments
print(f\"\n3. Statistical Tests Across Segments:\")

# ANOVA for spending score across segments
segment_groups = [group['spending_score'].values for name, group in customer_data.groupby('customer_segment')]
f_stat, p_value = stats.f_oneway(*segment_groups)
print(f\"ANOVA for spending score across segments:\")
print(f\"F-statistic: {f_stat:.4f}, p-value: {p_value:.4f}\")

# Chi-square test for segment distribution across regions
contingency_table = pd.crosstab(customer_data['customer_segment'], customer_data['region'])
chi2, p_value, dof, expected = stats.chi2_contingency(contingency_table)
print(f\"\nChi-square test for segment vs region independence:\")
print(f\"Chi-square: {chi2:.4f}, p-value: {p_value:.4f}\")

# 5. Customer lifetime value estimation
def calculate_clv(df):
    \"\"\"Simple CLV calculation.\"\"\"
    df['estimated_clv'] = (
        df['avg_order_value'] *
        df['total_purchases'] *
        (1 + df['years_as_customer']) *
        (1 - df['customer_service_calls'] * 0.1)  # Penalty for service calls
    )
    return df

customer_data = calculate_clv(customer_data)

clv_by_segment = customer_data.groupby('customer_segment')['estimated_clv'].agg(['mean', 'median', 'std']).round(2)
print(f\"\n4. Customer Lifetime Value by Segment:\")
print(clv_by_segment)

# 6. Visualization
fig, axes = plt.subplots(2, 3, figsize=(18, 12))

# Segment distribution
segment_counts = customer_data['customer_segment'].value_counts()
axes[0, 0].pie(segment_counts.values, labels=segment_counts.index, autopct='%1.1f%%')
axes[0, 0].set_title('Customer Segment Distribution')

# Income vs Spending Score scatter
segments = customer_data['customer_segment'].unique()
colors = plt.cm.Set3(np.linspace(0, 1, len(segments)))
for segment, color in zip(segments, colors):
    segment_data = customer_data[customer_data['customer_segment'] == segment]
    axes[0, 1].scatter(segment_data['annual_income'], segment_data['spending_score'],
                      label=segment, alpha=0.6, c=[color])
axes[0, 1].set_xlabel('Annual Income ($)')
axes[0, 1].set_ylabel('Spending Score')
axes[0, 1].set_title('Income vs Spending Score by Segment')
axes[0, 1].legend()

# CLV by segment
clv_means = customer_data.groupby('customer_segment')['estimated_clv'].mean().sort_values(ascending=False)
axes[0, 2].bar(range(len(clv_means)), clv_means.values)
axes[0, 2].set_xticks(range(len(clv_means)))
axes[0, 2].set_xticklabels(clv_means.index, rotation=45)
axes[0, 2].set_title('Average CLV by Segment')
axes[0, 2].set_ylabel('Estimated CLV ($)')

# Age distribution by segment
for segment in segments:
    segment_ages = customer_data[customer_data['customer_segment'] == segment]['age']
    axes[1, 0].hist(segment_ages, alpha=0.5, label=segment, bins=15)
axes[1, 0].set_xlabel('Age')
axes[1, 0].set_ylabel('Frequency')
axes[1, 0].set_title('Age Distribution by Segment')
axes[1, 0].legend()

# Purchase behavior
purchase_by_segment = customer_data.groupby('customer_segment')['total_purchases'].mean().sort_values(ascending=False)
axes[1, 1].bar(range(len(purchase_by_segment)), purchase_by_segment.values, color='lightgreen')
axes[1, 1].set_xticks(range(len(purchase_by_segment)))
axes[1, 1].set_xticklabels(purchase_by_segment.index, rotation=45)
axes[1, 1].set_title('Average Total Purchases by Segment')
axes[1, 1].set_ylabel('Total Purchases')

# Service calls analysis
service_calls_by_segment = customer_data.groupby('customer_segment')['customer_service_calls'].mean()
axes[1, 2].bar(range(len(service_calls_by_segment)), service_calls_by_segment.values, color='salmon')
axes[1, 2].set_xticks(range(len(service_calls_by_segment)))
axes[1, 2].set_xticklabels(service_calls_by_segment.index, rotation=45)
axes[1, 2].set_title('Average Service Calls by Segment')
axes[1, 2].set_ylabel('Average Service Calls')

plt.tight_layout()
plt.show()

print(\"\n\" + \"=\"*50)
print(\"Exercise 2 Complete: Customer segmentation analysis finished!\")
```
" %}

{% include question.html header="Exercise 3: A/B Testing Analysis" text="

Analyze the results of an A/B test to determine statistical significance.

" solution="

```python
# Create A/B test data
np.random.seed(456)

# Control group (A) - current website design
n_control = 1000
control_conversion_rate = 0.12  # 12% baseline conversion rate
control_conversions = np.random.binomial(1, control_conversion_rate, n_control)

# Treatment group (B) - new website design
n_treatment = 1000
treatment_conversion_rate = 0.15  # 15% conversion rate (3% improvement)
treatment_conversions = np.random.binomial(1, treatment_conversion_rate, n_treatment)

# Create combined dataset
ab_test_data = pd.DataFrame({
    'user_id': range(1, n_control + n_treatment + 1),
    'group': ['A'] * n_control + ['B'] * n_treatment,
    'converted': np.concatenate([control_conversions, treatment_conversions]),
    'session_duration': np.concatenate([
        np.random.exponential(120, n_control),  # Control: average 2 minutes
        np.random.exponential(140, n_treatment)  # Treatment: slightly longer
    ]),
    'page_views': np.concatenate([
        np.random.poisson(3, n_control),     # Control: average 3 pages
        np.random.poisson(4, n_treatment)    # Treatment: average 4 pages
    ])
})

print(\"A/B Testing Analysis\")
print(\"=\" * 50)

# 1. Basic summary statistics
print(\"1. A/B Test Summary:\")
summary_stats = ab_test_data.groupby('group').agg({
    'user_id': 'count',
    'converted': ['sum', 'mean'],
    'session_duration': 'mean',
    'page_views': 'mean'
}).round(4)

print(summary_stats)

# 2. Conversion rate analysis
control_group = ab_test_data[ab_test_data['group'] == 'A']
treatment_group = ab_test_data[ab_test_data['group'] == 'B']

control_conversion_rate = control_group['converted'].mean()
treatment_conversion_rate = treatment_group['converted'].mean()
lift = (treatment_conversion_rate - control_conversion_rate) / control_conversion_rate * 100

print(f\"\n2. Conversion Rate Analysis:\")
print(f\"Control (A) conversion rate: {control_conversion_rate:.4f} ({control_conversion_rate*100:.2f}%)\")
print(f\"Treatment (B) conversion rate: {treatment_conversion_rate:.4f} ({treatment_conversion_rate*100:.2f}%)\")
print(f\"Absolute lift: {treatment_conversion_rate - control_conversion_rate:.4f}\")
print(f\"Relative lift: {lift:.2f}%\")

# 3. Statistical significance testing
# Two-proportion z-test
def two_proportion_z_test(x1, n1, x2, n2):
    \"\"\"Perform two-proportion z-test.\"\"\"
    p1 = x1 / n1
    p2 = x2 / n2
    p_pool = (x1 + x2) / (n1 + n2)

    se = np.sqrt(p_pool * (1 - p_pool) * (1/n1 + 1/n2))
    z = (p2 - p1) / se
    p_value = 2 * (1 - stats.norm.cdf(abs(z)))

    return z, p_value

control_conversions = control_group['converted'].sum()
treatment_conversions = treatment_group['converted'].sum()

z_stat, p_value = two_proportion_z_test(
    control_conversions, len(control_group),
    treatment_conversions, len(treatment_group)
)

print(f\"\n3. Statistical Significance Test:\")
print(f\"Z-statistic: {z_stat:.4f}\")
print(f\"P-value: {p_value:.4f}\")
print(f\"Significant at α=0.05: {'Yes' if p_value < 0.05 else 'No'}\")

# 4. Confidence interval for the difference
def confidence_interval_diff_proportions(x1, n1, x2, n2, confidence=0.95):
    \"\"\"Calculate confidence interval for difference in proportions.\"\"\"
    p1 = x1 / n1
    p2 = x2 / n2
    diff = p2 - p1

    se = np.sqrt((p1 * (1 - p1) / n1) + (p2 * (1 - p2) / n2))
    z_critical = stats.norm.ppf(1 - (1 - confidence) / 2)

    margin_error = z_critical * se
    ci_lower = diff - margin_error
    ci_upper = diff + margin_error

    return ci_lower, ci_upper, diff

ci_lower, ci_upper, diff = confidence_interval_diff_proportions(
    control_conversions, len(control_group),
    treatment_conversions, len(treatment_group)
)

print(f\"\n4. 95% Confidence Interval for Difference:\")
print(f\"Difference in conversion rates: {diff:.4f}\")
print(f\"95% CI: [{ci_lower:.4f}, {ci_upper:.4f}]\")
print(f\"95% CI (percentage): [{ci_lower*100:.2f}%, {ci_upper*100:.2f}%]\")

# 5. Power analysis and sample size calculation
def sample_size_two_proportions(p1, p2, alpha=0.05, power=0.8):
    \"\"\"Calculate required sample size for two-proportion test.\"\"\"
    from scipy.stats import norm

    z_alpha = norm.ppf(1 - alpha/2)
    z_beta = norm.ppf(power)

    p_avg = (p1 + p2) / 2

    n = ((z_alpha * np.sqrt(2 * p_avg * (1 - p_avg)) +
          z_beta * np.sqrt(p1 * (1 - p1) + p2 * (1 - p2))) / (p2 - p1)) ** 2

    return int(np.ceil(n))

required_sample_size = sample_size_two_proportions(0.12, 0.15)
print(f\"\n5. Power Analysis:\")
print(f\"Required sample size per group (80% power, 5% significance): {required_sample_size}\")
print(f\"Actual sample size per group: {len(control_group)}\")
print(f\"Study was {'adequately' if len(control_group) >= required_sample_size else 'under'} powered\")

# 6. Secondary metrics analysis
print(f\"\n6. Secondary Metrics Analysis:\")

# Session duration comparison
session_t_stat, session_p_value = stats.ttest_ind(
    control_group['session_duration'],
    treatment_group['session_duration']
)

print(f\"Session Duration:\")
print(f\"Control mean: {control_group['session_duration'].mean():.2f} seconds\")
print(f\"Treatment mean: {treatment_group['session_duration'].mean():.2f} seconds\")
print(f\"T-test p-value: {session_p_value:.4f}\")

# Page views comparison
pageview_t_stat, pageview_p_value = stats.ttest_ind(
    control_group['page_views'],
    treatment_group['page_views']
)

print(f\"\nPage Views:\")
print(f\"Control mean: {control_group['page_views'].mean():.2f}\")
print(f\"Treatment mean: {treatment_group['page_views'].mean():.2f}\")
print(f\"T-test p-value: {pageview_p_value:.4f}\")

# 7. Visualization
fig, axes = plt.subplots(2, 2, figsize=(15, 10))

# Conversion rates comparison
conversion_rates = [control_conversion_rate, treatment_conversion_rate]
group_names = ['Control (A)', 'Treatment (B)']
colors = ['lightblue', 'lightgreen']

bars = axes[0, 0].bar(group_names, conversion_rates, color=colors)
axes[0, 0].set_title('Conversion Rates by Group')
axes[0, 0].set_ylabel('Conversion Rate')
axes[0, 0].set_ylim(0, max(conversion_rates) * 1.2)

# Add value labels on bars
for bar, rate in zip(bars, conversion_rates):
    axes[0, 0].text(bar.get_x() + bar.get_width()/2, bar.get_height() + 0.001,
                    f'{rate:.3f}', ha='center', va='bottom')

# Session duration distribution
axes[0, 1].hist(control_group['session_duration'], alpha=0.7, label='Control', bins=30, color='lightblue')
axes[0, 1].hist(treatment_group['session_duration'], alpha=0.7, label='Treatment', bins=30, color='lightgreen')
axes[0, 1].set_title('Session Duration Distribution')
axes[0, 1].set_xlabel('Session Duration (seconds)')
axes[0, 1].set_ylabel('Frequency')
axes[0, 1].legend()

# Page views comparison
pageview_comparison = ab_test_data.groupby('group')['page_views'].mean()
axes[1, 0].bar(pageview_comparison.index, pageview_comparison.values, color=['lightblue', 'lightgreen'])
axes[1, 0].set_title('Average Page Views by Group')
axes[1, 0].set_ylabel('Average Page Views')

# Conversion funnel
funnel_data = ab_test_data.groupby('group').agg({
    'user_id': 'count',
    'converted': 'sum'
}).rename(columns={'user_id': 'visitors', 'converted': 'conversions'})

x = np.arange(len(funnel_data))
width = 0.35

axes[1, 1].bar(x - width/2, funnel_data['visitors'], width, label='Visitors', alpha=0.8)
axes[1, 1].bar(x + width/2, funnel_data['conversions'], width, label='Conversions', alpha=0.8)
axes[1, 1].set_title('Visitors vs Conversions')
axes[1, 1].set_ylabel('Count')
axes[1, 1].set_xticks(x)
axes[1, 1].set_xticklabels(funnel_data.index)
axes[1, 1].legend()

plt.tight_layout()
plt.show()

# 8. Business impact calculation
print(f\"\n7. Business Impact Analysis:\")
monthly_visitors = 10000  # Assume 10,000 monthly visitors
current_monthly_conversions = monthly_visitors * control_conversion_rate
projected_monthly_conversions = monthly_visitors * treatment_conversion_rate
additional_conversions = projected_monthly_conversions - current_monthly_conversions

average_order_value = 50  # Assume $50 average order value
monthly_revenue_increase = additional_conversions * average_order_value
annual_revenue_increase = monthly_revenue_increase * 12

print(f\"Assuming {monthly_visitors:,} monthly visitors:\")
print(f\"Current monthly conversions: {current_monthly_conversions:.0f}\")
print(f\"Projected monthly conversions: {projected_monthly_conversions:.0f}\")
print(f\"Additional monthly conversions: {additional_conversions:.0f}\")
print(f\"Monthly revenue increase: ${monthly_revenue_increase:.2f}\")
print(f\"Annual revenue increase: ${annual_revenue_increase:,.2f}\")

print(\"\n\" + \"=\"*50)
print(\"Exercise 3 Complete: A/B testing analysis finished!\")
```
" %}

{% include question.html header="Exercise 4: Time Series Analysis" text="

Analyze time-based data to identify trends and patterns.

" solution="

```python
# Create time series data
np.random.seed(789)
date_range = pd.date_range('2020-01-01', '2023-12-31', freq='D')
n_days = len(date_range)

# Create synthetic sales data with trend, seasonality, and noise
trend = np.linspace(100, 200, n_days)  # Linear upward trend
seasonal = 20 * np.sin(2 * np.pi * np.arange(n_days) / 365.25)  # Annual seasonality
weekly_pattern = 10 * np.sin(2 * np.pi * np.arange(n_days) / 7)  # Weekly pattern
noise = np.random.normal(0, 15, n_days)

sales = trend + seasonal + weekly_pattern + noise
sales = np.maximum(sales, 0)  # Ensure non-negative values

time_series_data = pd.DataFrame({
    'date': date_range,
    'sales': sales,
    'month': date_range.month,
    'year': date_range.year,
    'quarter': date_range.quarter,
    'day_of_week': date_range.dayofweek,
    'day_name': date_range.day_name(),
    'is_weekend': date_range.dayofweek >= 5
})

print(\"Time Series Analysis\")
print(\"=\" * 50)

# 1. Basic time series statistics
print(\"1. Time Series Overview:\")
print(f\"Date range: {time_series_data['date'].min()} to {time_series_data['date'].max()}\")
print(f\"Total observations: {len(time_series_data)}\")
print(f\"Average daily sales: ${time_series_data['sales'].mean():.2f}\")
print(f\"Sales standard deviation: ${time_series_data['sales'].std():.2f}\")

# 2. Trend analysis
print(f\"\n2. Trend Analysis:\")
# Linear trend
from sklearn.linear_model import LinearRegression
X = np.arange(len(time_series_data)).reshape(-1, 1)
y = time_series_data['sales'].values

trend_model = LinearRegression()
trend_model.fit(X, y)
trend_slope = trend_model.coef_[0]

print(f\"Linear trend slope: ${trend_slope:.4f} per day\")
print(f\"Annual trend: ${trend_slope * 365:.2f} per year\")

# Calculate correlation with time
time_correlation = stats.spearmanr(X.flatten(), y)[0]
print(f\"Correlation with time: {time_correlation:.4f}\")

# 3. Seasonality analysis
print(f\"\n3. Seasonality Analysis:\")

# Monthly patterns
monthly_avg = time_series_data.groupby('month')['sales'].mean()
print(\"Average sales by month:\")
for month, avg_sales in monthly_avg.items():
    month_name = pd.to_datetime(f'2023-{month:02d}-01').strftime('%B')
    print(f\"  {month_name}: ${avg_sales:.2f}\")

# Day of week patterns
dow_avg = time_series_data.groupby('day_name')['sales'].mean()
print(f\"\nAverage sales by day of week:\")
for day, avg_sales in dow_avg.items():
    print(f\"  {day}: ${avg_sales:.2f}\")

# Weekend vs weekday analysis
weekend_comparison = time_series_data.groupby('is_weekend')['sales'].mean()
print(f\"\nWeekend vs Weekday:\")
print(f\"  Weekday average: ${weekend_comparison[False]:.2f}\")
print(f\"  Weekend average: ${weekend_comparison[True]:.2f}\")

# Statistical test for weekend difference
weekday_sales = time_series_data[~time_series_data['is_weekend']]['sales']
weekend_sales = time_series_data[time_series_data['is_weekend']]['sales']
t_stat, p_value = stats.ttest_ind(weekday_sales, weekend_sales)
print(f\"  T-test p-value: {p_value:.4f}\")
print(f\"  Significant difference: {'Yes' if p_value < 0.05 else 'No'}\")

# 4. Rolling statistics
print(f\"\n4. Rolling Statistics:\")
time_series_data['sales_7day_ma'] = time_series_data['sales'].rolling(window=7).mean()
time_series_data['sales_30day_ma'] = time_series_data['sales'].rolling(window=30).mean()
time_series_data['sales_7day_std'] = time_series_data['sales'].rolling(window=7).std()

# Print some recent rolling statistics
recent_data = time_series_data.tail(30)
print(f\"Recent 7-day moving average: ${recent_data['sales_7day_ma'].iloc[-1]:.2f}\")
print(f\"Recent 30-day moving average: ${recent_data['sales_30day_ma'].iloc[-1]:.2f}\")
print(f\"Recent 7-day volatility: ${recent_data['sales_7day_std'].iloc[-1]:.2f}\")

# 5. Year-over-year analysis
print(f\"\n5. Year-over-Year Analysis:\")
yearly_stats = time_series_data.groupby('year')['sales'].agg(['sum', 'mean', 'std']).round(2)
print(\"Annual sales statistics:\")
print(yearly_stats)

# Calculate year-over-year growth
yoy_growth = yearly_stats['sum'].pct_change() * 100
print(f\"\nYear-over-year growth rates:\")
for year, growth in yoy_growth.items():
    if not np.isnan(growth):
        print(f\"  {year}: {growth:.1f}%\")

# 6. Outlier detection
print(f\"\n6. Outlier Detection:\")
Q1 = time_series_data['sales'].quantile(0.25)
Q3 = time_series_data['sales'].quantile(0.75)
IQR = Q3 - Q1
lower_bound = Q1 - 1.5 * IQR
upper_bound = Q3 + 1.5 * IQR

outliers = time_series_data[(time_series_data['sales'] < lower_bound) |
                           (time_series_data['sales'] > upper_bound)]

print(f\"Number of outliers detected: {len(outliers)}\")
print(f\"Outlier threshold: ${lower_bound:.2f} - ${upper_bound:.2f}\")

if len(outliers) > 0:
    print(\"Sample outliers:\")
    print(outliers[['date', 'sales']].head())

# 7. Visualization
fig, axes = plt.subplots(3, 2, figsize=(15, 18))

# Time series plot
axes[0, 0].plot(time_series_data['date'], time_series_data['sales'], alpha=0.7, linewidth=0.8)
axes[0, 0].plot(time_series_data['date'], time_series_data['sales_30day_ma'],
                color='red', linewidth=2, label='30-day MA')
axes[0, 0].set_title('Daily Sales Time Series')
axes[0, 0].set_xlabel('Date')
axes[0, 0].set_ylabel('Sales ($)')
axes[0, 0].legend()
axes[0, 0].grid(True, alpha=0.3)

# Monthly seasonality
monthly_avg.plot(kind='bar', ax=axes[0, 1])
axes[0, 1].set_title('Average Sales by Month')
axes[0, 1].set_xlabel('Month')
axes[0, 1].set_ylabel('Average Sales ($)')
axes[0, 1].tick_params(axis='x', rotation=45)

# Day of week pattern
dow_avg_ordered = time_series_data.groupby('day_of_week')['sales'].mean()
day_names = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
axes[1, 0].bar(day_names, dow_avg_ordered.values)
axes[1, 0].set_title('Average Sales by Day of Week')
axes[1, 0].set_xlabel('Day of Week')
axes[1, 0].set_ylabel('Average Sales ($)')

# Annual comparison
yearly_comparison = time_series_data.groupby('year')['sales'].sum()
axes[1, 1].bar(yearly_comparison.index.astype(str), yearly_comparison.values)
axes[1, 1].set_title('Annual Sales Totals')
axes[1, 1].set_xlabel('Year')
axes[1, 1].set_ylabel('Annual Sales ($)')

# Sales distribution
axes[2, 0].hist(time_series_data['sales'], bins=50, edgecolor='black', alpha=0.7)
axes[2, 0].set_title('Distribution of Daily Sales')
axes[2, 0].set_xlabel('Daily Sales ($)')
axes[2, 0].set_ylabel('Frequency')

# Box plot by quarter
quarterly_data = []
quarter_labels = []
for year in time_series_data['year'].unique():
    for quarter in [1, 2, 3, 4]:
        quarter_data = time_series_data[
            (time_series_data['year'] == year) &
            (time_series_data['quarter'] == quarter)
        ]['sales']
        if len(quarter_data) > 0:
            quarterly_data.append(quarter_data.values)
            quarter_labels.append(f'{year}Q{quarter}')

axes[2, 1].boxplot(quarterly_data)
axes[2, 1].set_title('Sales Distribution by Quarter')
axes[2, 1].set_xlabel('Quarter')
axes[2, 1].set_ylabel('Sales ($)')
axes[2, 1].set_xticklabels(quarter_labels, rotation=45)

plt.tight_layout()
plt.show()
```
" %}
