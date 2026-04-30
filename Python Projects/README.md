# 📊 HR Employee Retention & Attrition Analysis

## 📖 Project Overview
Employee turnover is a critical issue for modern organizations, directly impacting productivity, morale, and recruitment costs. This project aims to analyze a dataset from Salifort Motors to identify the root causes of employee attrition and predict which employees are at high risk of leaving. 

Rather than relying purely on predictive models, this project utilizes **Applied Statistical Inference** to mathematically validate the underlying causes of turnover before building machine learning models.

## 🎯 Business Problem
The HR department wants to know:
1. **Why** are employees leaving? (Root cause analysis)
2. **Who** is likely to leave next? (Predictive modeling)
3. **What** actionable steps can be taken to retain top talent?

## 📂 The Data
The dataset (`HR_capstone_dataset.csv`) contains 14,999 records of employee data, featuring:
* `satisfaction_level`: Employee-reported job satisfaction
* `last_evaluation`: Score of the most recent performance review
* `number_project`: Number of projects handled
* `average_montly_hours`: Average hours worked per month
* `tenure`: Years spent at the company
* `salary`: Categorical salary level (low, medium, high)
* `left`: Binary target variable indicating turnover (1 = left, 0 = stayed)

## 🔬 Methodology: Applied Statistics & Machine Learning

### 1. Exploratory Data Analysis (EDA)
* Identified that departing employees typically exhibit two distinct profiles: either underperforming with low hours, or highly evaluated but severely overworked (working near 300 hours/month).
* Discovered a significant lack of promotions over the last 5 years, even among top performers.

### 2. Statistical Inference (Hypothesis Testing)
To ensure the business insights are mathematically rigorous, several statistical tests were conducted:
* **Chi-Square Test of Independence:** Proved a statistically significant relationship between an employee's salary level and their likelihood of leaving ($p < 0.05$).
* **Two-Sample Independent T-test:** Validated that the difference in average monthly working hours between employees who stayed and those who left is statistically significant, confirming overwork as a systematic issue.
* **One-Way ANOVA (F-test):** Demonstrated that job satisfaction levels vary significantly depending on the number of projects assigned.

### 3. Feature Engineering & Target Leakage Prevention
* **Preventing Target Leakage:** The `satisfaction_level` feature was highly correlated with turnover. However, dissatisfaction is a *symptom* of leaving, not a fixable root cause. To build an actionable model, `satisfaction_level` was dropped.
* **Creating Business-Relevant Features:** A new binary feature, `overworked`, was engineered (defined as working $>180$ hours/month) to capture the threshold of burnout.

### 4. Machine Learning Modeling
* **Logistic Regression:** Served as a baseline model to establish linear relationships.
* **XGBoost Classifier:** Selected as the final champion model due to its ability to capture complex, non-linear interactions (e.g., high evaluation + long hours + no promotion).
* **Performance:** The final XGBoost model achieved a Precision of **91.5%**, Recall of **89.3%**, and an overall Accuracy of **96.8%**.

## 💡 Results & Business Recommendations
Based on the feature importance and statistical analysis, the primary drivers of employee turnover are excessive workloads and stagnant career progression. 

**Actionable Recommendations for Management:**
1. **Cap Workloads:** Implement a hard limit on the number of projects an employee can handle simultaneously. Employees should not be working 300+ hours a month.
2. **Revamp Promotion Criteria:** Employees with high evaluation scores and over 4 years of tenure are leaving due to lack of advancement. Establish a clear promotion pathway for senior individual contributors.
3. **Restructure Evaluation Metrics:** Ensure performance evaluations are based on impact and efficiency, rather than purely rewarding long hours, which actively incentivizes burnout.

## 🛠️ Tools Used
* **Languages:** Python (pandas, numpy)
* **Statistics:** SciPy (`scipy.stats`), statsmodels
* **Machine Learning:** scikit-learn, XGBoost
* **Data Visualization:** Matplotlib, Seaborn
