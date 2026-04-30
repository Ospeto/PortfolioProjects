# HR Employee Retention and Attrition Analysis

## Problem

Salifort Motors wants to reduce employee turnover. The HR team needs a practical answer to one business question: what factors are most likely to make an employee leave?

This project turns the existing HR dataset into a retention analysis and predictive model that can help HR identify risk patterns before employees leave.

## Data

The project uses the HR capstone dataset from the Google Advanced Data Analytics certificate.

- Raw size: 14,999 employee records and 10 columns.
- Cleaned size used in the notebook: 11,991 records after duplicate removal.
- Target variable: `left`, where `1` means the employee left and `0` means the employee stayed.
- Key fields: satisfaction level, last evaluation score, number of projects, average monthly hours, tenure, work accident flag, promotion flag, department, and salary.

## Tools

- Python
- pandas and numpy
- matplotlib and seaborn
- scikit-learn
- XGBoost

## Method

1. Loaded and inspected the HR dataset.
2. Standardized column names into clearer snake_case names.
3. Checked for missing values, duplicate records, and outliers.
4. Explored the relationship between attrition and satisfaction, workload, project count, tenure, salary, and evaluation score.
5. Compared logistic regression with an XGBoost classifier.
6. Built a final XGBoost model with feature engineering.

The final model uses an `overworked` flag for employees working more than 180 average monthly hours. It also removes `satisfaction_level` and `average_monthly_hours` from the final feature set so the model points more directly toward operational drivers HR can act on.

## Key Findings

- Employees who left had lower satisfaction on average than employees who stayed.
- Attrition was concentrated among employees with either unusually low or unusually high monthly hours.
- High workload, project count, tenure, and evaluation score were important signals in the final model.
- The final feature importance view highlighted `last_evaluation`, `number_of_projects`, `tenure`, `overworked`, and `salary` as major predictors.
- A strong evaluation score may be partly tied to long working hours, so HR should be careful not to reward unsustainable workload patterns.

## Model Results

The final XGBoost model was selected because it performed better than logistic regression and retained strong performance after feature engineering.

| Metric | Final XGBoost result |
|---|---:|
| F1 score | 0.9046 |
| Recall | 0.8960 |
| Precision | 0.9134 |
| Accuracy | 0.9681 |

## Recommendation

HR should treat overwork and project overload as retention risks.

Recommended actions:

- Cap the number of active projects an employee can carry.
- Review overtime patterns and reduce sustained work above normal monthly hours.
- Compensate overtime clearly when high workload is unavoidable.
- Promote employees with strong evaluation scores and longer tenure instead of relying only on workload-heavy performance signals.
- Make overtime and workload expectations explicit so employees understand policy and managers apply it consistently.

## Limitations

- The dataset is a course capstone dataset, so the result should be treated as portfolio evidence, not a production HR system.
- The target variable does not cleanly separate voluntary resignation from termination.
- Evaluation scores may be biased by workload, manager behavior, or department norms.
- The model should support HR review, not automate employment decisions.
- The notebook still contains course scaffolding and exploratory work; this README is the recruiter-facing project summary.

## Files

- [Notebook](Capstone%20project%3A%20Providing%20data-driven%20suggestions%20for%20HR.ipynb)
- [Dataset](HR_capstone_dataset.csv)
- [Executive summary](Executive%20Summary%20of%20Employee_retention_project.pdf)

## How to Reproduce

1. Open the notebook in a Python environment with pandas, numpy, matplotlib, seaborn, scikit-learn, and xgboost installed.
2. Keep `HR_capstone_dataset.csv` in the same folder as the notebook.
3. Run the notebook cells from top to bottom.
4. Review the final XGBoost metrics and feature importance output.
