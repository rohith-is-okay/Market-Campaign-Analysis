# Market Campaign Response Analysis and Prediction
## Project Overview

This project analyzes customer behavior data from a marketing company to predict the likelihood of customers accepting a marketing campaign. The objective is to help the business optimize marketing spend and maximize profit by targeting customers who are most likely to respond.

Using exploratory data analysis, statistical hypothesis testing, and machine learning models, this project identifies key drivers of campaign success and evaluates multiple modeling approaches to support data-driven decision-making.


## Business Problem

Marketing campaigns incur costs for each customer contacted. Contacting uninterested customers leads to wasted spend, while failing to target interested customers results in lost revenue.

### Goal:
- Predict whether a customer will accept a marketing campaign
- Rank customers by likelihood of response
- Support profit-maximizing targeting decisions
- This is framed as a binary classification problem.

## Dataset

- Source: https://www.kaggle.com/datasets/rodsaldanha/arketing-campaign
- Observations: ~2,200 customers
- Target variable: Response
1: Customer accepted the campaign
0: Customer did not accept the campaign

### Key Feature Groups
- Demographics: Income, Education, Marital Status
- Spending Behavior: Product category spending over 2 years
- Engagement Metrics: Web visits, purchases, recency
- Campaign History: Past campaign acceptances

## Data Cleaning & Feature Engineering
### Cleaning
- Removed extreme income outlier (Income = 666666)
- Dropped rows with missing income values

### Feature Engineering
- Total_Spending: Sum of spending across all product categories
- Total_Past_Acceptances: Number of previously accepted campaigns
- Log_Income: Log-transformed income to address skewness

These engineered features were validated through statistical testing.

## Exploratory Data Analysis (EDA)
EDA focused on understanding:
- Spending distributions and skewness
- Differences between responders and non-responders
- Outliers and data quality issues
- Behavioral trends (recency, engagement)

Boxplots, distributions, and group comparisons revealed strong behavioral differences between customers who responded to campaigns and those who did not.

## Statistical Hypothesis Testing

Statistical tests were used to validate relationships observed in EDA:

| Test                                              | Result           |
| ------------------------------------------------- | ---------------- |
| Total Spending vs Response (Mann–Whitney U)       | Significant      |
| Recency vs Response (Mann–Whitney U)              | Significant      |
| Past Campaign Acceptance vs Response (Chi-square) | High Significant |
| Complaints vs Response (Chi-square)               | Not Significant  |

**Conclusion:**
Spending behavior, prior engagement, and recency are strong predictors of campaign response, while complaint history provides little predictive value.

## Modeling Approach
### Models Trained
1. Logistic Regression
  - Interpretable baseline model
  - Probability-based predictions suitable for marketing decisions
2. Random Forest Classifier
  - Captures non-linear interactions
  - Improves ranking and precision

### Preprocessing
- Standard scaling for numeric features
- One-hot encoding for categorical features
- Unified preprocessing pipeline for fair model comparison

## Model Performance
### Logistic Regression
- ROC-AUC: 0.864
- High recall for responders (captures most potential conversions)
- Lower precision (higher marketing cost)

### Random Forest
- ROC-AUC: 0.896
- Higher precision for responders
- More conservative, lower recall

| Metric                | Logistic Regression | Random Forest |
| --------------------- | ------------------- | ------------- |
| ROC-AUC               | 0.864               | 0.896         |
| Precision (Responder) | 0.43                | 0.64          |
| Recall (Responder)    | 0.75                | 0.57          |

## Model Selection Insights
- Logistic Regression is better when maximizing reach is the priority
- Random Forest is better when minimizing wasted marketing spend is critical
- Final model choice should be guided by profit-based threshold optimization, not accuracy alone
