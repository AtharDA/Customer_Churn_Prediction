# Customer Churn Prediction

**Author:** Mohammed Athar Ansari

## Project Overview

This project explores customer churn in the IBM Telco Customer Churn
dataset and compares two classification models: Logistic Regression and
Decision Tree. The goal is to identify customers who may leave the
service and understand how model performance changes depending on the
metric used.

## Business Problem

Customer churn can affect recurring revenue and customer retention. A
churn prediction model can help a business identify customers who may be
at risk and prioritize retention efforts. Model selection should
consider both the number of churners identified and the number of
customers incorrectly flagged.

## Dataset and Preparation

The project uses the IBM Telco Customer Churn dataset.

-   Original dataset: 7,043 rows and 21 columns.
-   `TotalCharges` was converted to a numeric field.
-   The 11 records with missing `TotalCharges` values had a tenure of
    zero and were removed.
-   Cleaned dataset: 7,032 rows and 21 columns, with no missing values.
-   Target: `Churn`, encoded as `No = 0` and `Yes = 1`.
-   `customerID` was excluded from model features.
-   The cleaned data contains 5,163 non-churn customers and 1,869 churn
    customers.

The cleaned dataset was split into training and test sets using an 80/20
split, `random_state=42`, and stratification. The test set contains
1,407 customers.

## Project Workflow

1.  **Data understanding and EDA** --- inspected data quality and
    explored churn distribution, churn by contract type, and churn by
    tenure group.
2.  **Feature engineering and preprocessing** --- separated numerical
    and categorical features, scaled numerical features, and one-hot
    encoded categorical features.
3.  **Model building** --- trained and saved Logistic Regression and
    Decision Tree pipelines.
4.  **Model evaluation** --- compared both models using accuracy,
    precision, recall, F1-score, ROC-AUC, confusion matrices, and
    classification reports.

## Models and Results

Both models were evaluated on the same held-out test set.

  Metric                Logistic Regression   Decision Tree
  ------------------- --------------------- ---------------
  Accuracy                            80.4%           73.3%
  Precision (Churn)                   64.8%           49.9%
  Recall (Churn)                      57.2%           79.9%
  F1-score (Churn)                    60.8%           61.5%
  ROC-AUC                             83.6%           81.8%

### Interpretation

-   **Logistic Regression** achieved higher accuracy, churn precision,
    and ROC-AUC.
-   **Decision Tree** achieved higher churn recall and a slightly higher
    churn F1-score.
-   Decision Tree identified a larger proportion of actual churners, but
    its lower precision means more customers flagged as likely to churn
    did not actually churn.

### Business Recommendation

The preferred model depends on the cost of missed churn versus
unnecessary retention outreach. If identifying as many churners as
possible is the main priority, Decision Tree is a promising candidate.
If higher precision and stronger overall discrimination are more
important, Logistic Regression is a reasonable choice. These results do
not establish one model as best for every business objective.

EDA also showed that churn was highest among month-to-month contract
customers (42.71%) and customers with 0--12 months of tenure
(approximately 47.5%). These are useful groups for further investigation
and for designing retention strategies; the observed associations do not
establish causation.

## Technologies Used

-   Python
-   pandas
-   Matplotlib
-   scikit-learn
-   joblib
-   Jupyter Notebook

## Project Structure

``` text
Customer_Churn_Prediction/
├── data/
│   ├── raw/
│   └── processed/
│       └── customer_churn_cleaned.csv
├── notebooks/
│   ├── 1_Data_Understanding_and_EDA.ipynb
│   ├── 2_Feature_Engineering.ipynb
│   ├── 3_Model_Building.ipynb
│   └── 4_Model_Evaluation_and_Insights.ipynb
├── models/
│   ├── logistic_regression.joblib
│   └── decision_tree.joblib
├── outputs/
│   ├── model_comparison.csv
│   └── confusion_matrices.png
├── README.md
└── requirements.txt
```

The tree above reflects the intended project layout and expected
generated outputs; include each file in the repository only if it exists
in your local project.

## How to Run

1.  Download or clone the project repository once it is published.
2.  Install the required dependencies listed in `requirements.txt`.
3.  Place the original dataset in `data/raw/`.
4.  Open the notebooks in order and run their cells:
    -   `1_Data_Understanding_and_EDA.ipynb`
    -   `2_Feature_Engineering.ipynb`
    -   `3_Model_Building.ipynb`
    -   `4_Model_Evaluation_and_Insights.ipynb`

The notebooks use relative paths and expect to be run from the
`notebooks/` directory. The original dataset is not embedded in this
README.

## Limitations and Next Steps

-   The results are based on a single stratified train/test split.
-   The Decision Tree's higher recall comes with lower precision.
-   Further validation and decision-threshold tuning could help align
    model predictions with business retention costs.
-   No deployed application is included in this project at this stage.

## Author

**Mohammed Athar Ansari**
