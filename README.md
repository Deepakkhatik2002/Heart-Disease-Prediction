# Heart-Disease-Prediction-Using-Machine-Learning

## ABSTRACT

Cardiovascular disease (CVD) is a leading cause of death globally. Early prediction of heart disease can lead to timely interventions and save lives. This project develops a machine-learning model to predict the 10-year risk of coronary heart disease (CHD) using the **Logistic Regression** algorithm. The model is trained on the Framingham Heart Study dataset and evaluated on its performance using metrics like accuracy, precision, recall, and F1-score. A key challenge in this project is handling the **imbalanced dataset**, where positive CHD cases are significantly underrepresented.

**Keywords:** Heart Disease Prediction, Cardiovascular Disease, Machine Learning, **Logistic Regression**, Imbalanced Data, Framingham Heart Study.

-----

## Overview

The ability to predict the 10-year risk of coronary heart disease (CHD) is a critical task in preventive medicine. By identifying high-risk individuals, healthcare providers can recommend lifestyle changes and treatments to mitigate that risk.

This project leverages the well-known Framingham Heart Study dataset to build a binary classification model. The goal is to analytically determine whether a patient is at risk of developing CHD within the next 10 years based on a set of demographic, behavioral, and medical risk factors. The primary algorithm explored in this notebook is **Logistic Regression**.

-----

## Project Goal

The main aim of this project is the detection of 10-year coronary heart disease (CHD) risk. This is essential for identifying at-risk patients who may benefit from early medical intervention.

This will be achieved by:

1.  Loading and preprocessing the Framingham dataset.
2.  Handling missing values and scaling features.
3.  Training a **Logistic Regression** classifier.
4.  Evaluating the model's performance, with a special focus on its ability to identify positive CHD cases (Recall) given the data's imbalanced nature.

-----

## Data Source

The dataset was retrieved from the Framingham Heart Study, an ongoing cardiovascular cohort study. It is a popular public dataset available on platforms like Kaggle.

  * **Dataset:** [Framingham Heart Study Dataset (Kaggle)](https://www.google.com/search?q=https://www.kaggle.com/datasets/amanajmera1/framingham-heart-study-dataset)
  * **Original Rows:** 4,240
  * **Rows Used (After Cleaning):** 3,751 (Rows with NaN values were dropped)
  * **Attributes:** 15 (After dropping 'education')
  * **Details:**
      * Features include 'age', 'Sex\_male', 'cigsPerDay', 'totChol', 'sysBP', 'glucose', and others.
      * The target variable is **'TenYearCHD'**.
      * 'TenYearCHD' is binary: **`1`** (at risk of CHD) and **`0`** (not at risk).
  * **Key Finding:** The dataset is **highly imbalanced**.
      * **Not at Risk (Class 0):** 3,179
      * **At Risk (Class 1):** 572

-----

## Project Workflow

1.  **Import Libraries:** Imported `numpy`, `pandas`, `matplotlib`, `seaborn`, and `sklearn`.
2.  **Load Data:** Loaded the `framingham.csv` file into a pandas DataFrame.
3.  **Data Preprocessing:**
      * Dropped the 'education' column.
      * Removed all rows with missing values using `.dropna()`.
      * Selected a subset of features (`X`) for the model: 'age', 'Sex\_male', 'cigsPerDay', 'totChol', 'sysBP', 'glucose'.
      * Separated the features (`X`) from the target variable (`y` - 'TenYearCHD').
      * Scaled the features (`X`) using `StandardScaler`.
      * Split the data into training and testing sets using a 70/30 split (`test_size=0.3`).
4.  **Exploratory Data Analysis (EDA):**
      * Investigated the class imbalance by plotting a `countplot` of the 'TenYearCHD' target variable.
5.  **Model Training:**
      * The project implements a **Logistic Regression** classifier (`sklearn.linear_model.LogisticRegression`).
      * The model was `fit` on the training data (`X_train`, `y_train`).
6.  **Model Evaluation:**
      * The trained model was used to make predictions (`y_pred`) on the test set (`X_test`).
      * Performance was evaluated using `accuracy_score`, a confusion matrix, and a full `classification_report`.

-----

## Algorithm Used

  * **Logistic Regression:** A linear model used for binary classification. It works by estimating the probability that a given input point belongs to a certain class (in this case, Class 1 or 'At Risk'). It is a foundational and highly interpretable classification algorithm.

-----

## Results

The Logistic Regression model was evaluated on the unseen 30% test set, yielding the following performance:

  * **Accuracy:** 0.849 (or 84.9%)

While the overall accuracy appears high, the classification report reveals a significant issue stemming from the class imbalance:

| Class | Precision | Recall | F1-Score | Support |
| :--- | :--- | :--- | :--- | :--- |
| **0 (No CHD)** | 0.85 | 0.99 | 0.92 | 951 |
| **1 (CHD)** | 0.61 | 0.08 | 0.14 | 175 |
| | | | | |
| **Accuracy** | | | **0.85** | **1126** |
| **Macro Avg** | 0.73 | 0.54 | 0.53 | 1126 |
| **Weighted Avg**| 0.82 | 0.85 | 0.80 | 1126 |

A confusion matrix was also generated, showing that the model only correctly identified **13** out of the **175** actual positive cases in the test set.

-----

## Conclusion

This project successfully implemented a **Logistic Regression** classifier to predict 10-year CHD risk. The model achieved a high accuracy of 84.9%.

However, this accuracy score is **highly misleading**. Due to the imbalanced nature of the dataset, the model has learned to primarily predict the majority class (Class 0 - 'No CHD').

The critical finding is the model's extremely poor **Recall for Class 1 (0.08 or 8%)**. This means the model failed to identify 92% of the patients who were actually at risk of developing CHD. In a medical context, this (a high number of "false negatives") is an unacceptable outcome, as high-risk patients would be incorrectly classified as safe.

Therefore, the model in its current state is not effective for its intended clinical purpose.

-----

## Future Work

To improve the model's predictive power, especially its ability to detect positive cases (recall), the following steps are recommended:

  * **Handle Imbalanced Data:** Apply data sampling techniques like **SMOTE** (Synthetic Minority Over-sampling Technique) or ADASYN to oversample the minority class (Class 1) before training.
  * **Feature Engineering:** Explore the impact of other features in the dataset that were not used in this model.
  * **Try Different Algorithms:** Experiment with ensemble methods that often perform better on imbalanced datasets, such as **Random Forest** or **XGBoost**.
  * **Hyperparameter Tuning:** Tune the parameters of the Logistic Regression model (e.g., the `C` parameter for regularization) or other models to optimize for Recall or F1-Score instead of just accuracy.
