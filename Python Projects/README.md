# HR Employee Retention and Attrition Analysis

## Project Overview
Employee turnover is a critical issue for modern organizations, directly affecting productivity, morale, and recruitment costs. This project analyzes the Salifort Motors HR dataset to identify likely risk factors associated with employee attrition and build a model that predicts which employees are at higher risk of leaving.

Rather than relying only on predictive modeling, the analysis uses applied statistical inference to test observed relationships before moving into machine learning.

## Business Problem
The HR department wants to understand:
1. Which employee attributes are associated with attrition?
2. Which employees are most likely to leave next?
3. Which practical retention actions should management prioritize?

## The Data
The dataset (`HR_capstone_dataset.csv`) contains 14,999 employee records with fields such as:
* `satisfaction_level`: Employee-reported job satisfaction
* `last_evaluation`: Score of the most recent performance review
* `number_project`: Number of projects handled
* `average_montly_hours`: Average hours worked per month
* `tenure`: Years spent at the company
* `salary`: Categorical salary level (low, medium, high)
* `left`: Binary target variable indicating turnover (1 = left, 0 = stayed)

After removing duplicate rows for the statistical inference section, the analysis uses 11,991 employee records.

## Methodology: Applied Statistics and Machine Learning

### 1. Exploratory Data Analysis
* Identified two notable attrition profiles: employees with low satisfaction and lower activity, and highly evaluated employees working very long hours.
* Found that employees with high evaluation scores and longer tenure often had no recent promotion, making promotion history a practical risk signal to investigate.

### 2. Statistical Inference
The hypothesis tests show statistically significant relationships, but they should be interpreted as association evidence, not causal proof.

* **Chi-Square Test of Independence:** Salary level and attrition are statistically associated (`p = 8.98e-39`, Cramer's V = `0.121`). The effect size suggests a real but modest relationship.
* **Welch's Two-Sample T-test:** Employees who left worked about 9.2 more hours per month on average than employees who stayed (`p = 2.27e-10`, Cohen's d = `0.190`). The difference is statistically significant, but the effect size is small.
* **One-Way ANOVA:** Satisfaction differs across project-count groups (`p < 0.001`, eta squared = `0.257`). The clearest practical drop appears at 6-7 projects, where average satisfaction is much lower.

### 3. Feature Engineering and Target Leakage Prevention
* **Preventing target leakage:** `satisfaction_level` is strongly correlated with turnover, but it is also close to the outcome HR wants to prevent. For a more actionable model, the final model excludes `satisfaction_level`.
* **Creating business-relevant features:** A binary `overworked` feature was engineered to flag employees working more than 180 hours per month.

### 4. Machine Learning Modeling
* **Logistic Regression:** Used as a baseline model to establish linear relationships.
* **XGBoost Classifier:** Selected as the final model because it captures non-linear interactions such as high evaluation, long hours, tenure, and no recent promotion.
* **Performance:** The final XGBoost model achieved precision of **91.5%**, recall of **89.3%**, and overall accuracy of **96.8%**.

## Results and Business Recommendations
The evidence points to workload/project load, overtime patterns, salary level, and career progression as practical attrition risk signals.

**Actionable recommendations for management:**
1. **Cap workloads:** Set a practical limit on simultaneous projects and review employees approaching 300 monthly hours.
2. **Review promotion pathways:** Employees with high evaluation scores and longer tenure should have clear advancement options.
3. **Improve evaluation incentives:** Reward impact and efficiency, not only long hours, so the performance system does not encourage burnout.

## Limitations
* The hypothesis tests and model results show association, not causation.
* The `left` target may combine different exit types, such as voluntary resignation and termination.
* The analysis depends on historical HR records and may not capture manager quality, team culture, commute, compensation changes, or external job-market conditions.

## Tools Used
* **Languages:** Python (pandas, numpy)
* **Statistics:** SciPy (`scipy.stats`)
* **Machine Learning:** scikit-learn, XGBoost
* **Data Visualization:** Matplotlib, Seaborn
