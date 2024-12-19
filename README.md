# Healthcare Member Engagement: Practicum Project

## Project Overview

This project supports a large U.S.-based health insurance company (LHIC) in optimizing its care management team’s outreach efforts. The team engages with high-risk members to:

- Promote healthier choices.
- Encourage lower-cost healthcare interventions.
- Maintain consistent medication adherence.

The ultimate goal is to improve member health outcomes while reducing the high costs associated with emergency care, such as ER visits and surgeries. However, LHIC’s care management team struggles to connect with its high-risk population. Our task is to analyze engagement data and develop a predictive model to identify members most likely to engage, enabling focused and efficient outreach.

---

## Problem Statement

**How can we enable LHIC’s care management team to prioritize outreach to members most likely to engage?**

---

## Our Approach

### Data Exploration and Cleaning

- Analyzed data from nearly 300,000 cases, encompassing various demographic, health-related, and engagement variables.
- Cleaned and pre-processed the data by:
  - Segmenting records into pre- and post-COVID-19 periods.
  - Removing unnecessary, redundant, or overly complex fields.
  - Performing one-hot encoding for categorical variables.
  - Standardizing continuous variables.
  - Deduplicating and sorting the dataset.

### Model Development

1. **Exploratory Analysis**:
   - Investigated clusters and variable relationships linked to high engagement rates.

2. **Machine Learning Models**:
   - Tested various models to predict engagement likelihood.
   - Tuned a logistic regression model for optimal accuracy and explainability, achieving 77% accuracy.

3. **Explainability**:
   - Extracted top positive and negative predictors of engagement.

### Deliverables

- A logistic regression model capable of predicting member engagement likelihood.
- Python scripts to automate data cleaning and report generation.
- A business intelligence dashboard wireframe (Tableau) for visualizing engagement insights.

---

## Results Summary

- **Model Accuracy**: 77%.
- **Confusion Matrix**:
  - Precision: 78% for non-engagement, 72% for engagement.
  - Recall: 88% for non-engagement, 55% for engagement.
- **Key Predictors of Engagement**:
  - Positive: Conditions such as neonatal and cardiovascular issues, claims count.
  - Negative: Certain state-level demographics and eligibility indicators.

---

## Code Highlights

1. **Data Preprocessing**:
   - Handled missing data, standardized variables, and created segments based on COVID-19.
   - Example code snippet:
     ```python
     df['pre_COVID'] = np.where(df['screen_dt_deid'] < '2020-03-11', 1, 0)
     df = df.drop(columns=unnecessary_columns)
     df = pd.get_dummies(df)
     ```

2. **Logistic Regression Model**:
   - Used `GridSearchCV` to tune hyperparameters for optimal performance.
   - Example code snippet:
     ```python
     param_grid = {
         'classifier__penalty': ['l1', 'l2'],
         'classifier__C': [0.001, 0.01, 0.1, 1, 10],
         'classifier__solver': ['liblinear']
     }
     clf = GridSearchCV(pipe, param_grid, cv=10, n_jobs=-1)
     clf.fit(X_train, y_train)
     ```

3. **Report Automation**:
   - Generated user-level engagement probability reports with top influencing factors.
   - Example output:
     | Member ID | Probability of Engagement | Top Predictors               |
     |-----------|----------------------------|------------------------------|
     | 271307    | 97.7%                      | Condition: Cardiovascular, Q1|

---

## Future Work

- Refine the logistic regression model to enhance recall for engagement predictions.
- Develop an interactive Tableau dashboard for real-time insights.
- Explore additional machine learning models (e.g., gradient boosting) for comparison.

---

## Repository Structure

```
healthcare-engagement-project/
├── data/                      # Raw and cleaned datasets
├── notebooks/                 # Jupyter notebooks for analysis
├── scripts/                   # Python scripts for preprocessing and modeling
├── outputs/                   # Generated reports and visualizations
├── README.md                  # Project documentation
```
