## Project Overview

**System Threat Forecaster** is a complete end-to-end machine learning project aimed at predicting the probability of a system being infected by malware families based on system properties and threat reports collected by antivirus software. Over the course of three months, I performed extensive exploratory data analysis (EDA), feature engineering, model building, hyperparameter tuning, and evaluation to build a predictive model that achieved a solid accuracy of **0.63**. This accuracy compares favorably to the industry standard of **0.70** for actual threat forecasting, indicating a competitive model despite the complex dataset.

## Project Steps

### 1. Data Exploration and Initial Manipulation

I began the project by inspecting the data and performing basic exploration. Key steps included:
- **Checking data shape**, obtaining feature information, using the `describe()` method for statistical summaries, and checking for null values.
- **Grouping features into seven categories**:
  1. System specifications
  2. Operating system info
  3. Security settings
  4. Hardware characteristics
  5. Geographic location
  6. Antivirus-related features
  7. Date columns
- From these categories, **antivirus features and security settings were identified as the most important**.
- The dataset consisted of **100,000 rows and 75 features**, with 30 out of 40 numerical features having missing values. Only 3 categorical features had missing values.

### 2. Visualizing and Handling Missing Values

I explored categorical columns in-depth, visualizing their distributions using **Matplotlib** and **Seaborn** to understand their spread and detect any anomalies. During this phase, I also performed **skewness analysis** and examined the **types of distributions** present in the dataset to ensure that my imputation strategies were statistically sound.

To handle missing values, I carefully selected appropriate manipulation techniques based on my **statistical knowledge**:
- For **numerical features**, I assessed their skewness and distribution shape before deciding on an imputation strategy.  
  - **Non-skewed features** (approximately normally distributed) were imputed using the **median**, ensuring robustness against outliers.  
  - **Highly skewed features** (those with a long tail or concentrated in a few categories) were imputed using the **mode**, preserving the data’s distributional integrity.  
- For **categorical features**, I inspected their frequency distributions and replaced missing values with the **mode**, ensuring that no artificial bias was introduced.

By aligning my imputation strategies with the underlying data distribution and leveraging statistical soundness, I ensured that the missing value treatment did not distort the dataset or introduce inconsistencies, leading to more reliable modeling outcomes.


### 3. Identifying Correlations and Reducing Features

I created a **heatmap** to visualize feature correlations, using the mask feature to identify pairs of features with a correlation above **0.8**. After careful inspection, I removed one feature from each highly correlated pair. The decision was based on:
- **Chi-square tests** for categorical features. Created new features and modified existing ones based on results of these statistical tests.
- Correlation with the target feature.
- **Domain knowledge** to guide feature selection.

Additionally, I **detected and handled outliers** using visualization techniques like **box plots**. Depending on the situation, I either dropped outliers or imputed them using the **median**.

### 4. Feature Encoding and Scaling

To prepare the dataset for modeling, I experimented with various feature encoding techniques:
- **Frequency encoding**
- **Target encoding**
- **Label encoding**

For categorical features, I ultimately settled on **one-hot encoding**, as it maintained the dataset’s structure and improved performance in the models I tested.

To handle numerical features, I experimented with:
- **StandardScaler** for scaling features to a standard distribution.
- **MinMaxScaler** to scale features between specific ranges, especially useful for tree-based models.

### 5. Feature Engineering and Selection

During feature engineering, I inspected features and made several transformations to improve the model's performance:

- **Converted categorical features to numerical**, where necessary, ensuring the transformations were meaningful and did not distort the data.
- **Clubbed various categories together** and introduced new categories where applicable, ensuring that the original distribution of the data was preserved.
- Experimented with **feature reduction techniques** to minimize feature dimensionality while retaining important information:
  - **PCA (Principal Component Analysis)** was used to reduce the dataset’s dimensionality by identifying key components.
  - **Recursive Feature Elimination (RFE)** was applied to remove less important features and prioritize the most impactful ones.

These transformations and feature engineering steps ensured that the dataset was refined and optimized for improved model accuracy, without losing essential information.

### 6. Building the First Model: Logistic Regression

As a baseline, I built a simple **logistic regression** model, which provided a decent starting point with an accuracy of **0.61**. This baseline model helped me evaluate the performance of subsequent models.

### 7. Advanced Modeling and Hyperparameter Tuning

I proceeded to experiment with more advanced models and techniques, such as:
- **Random Forest**
- **LightGBM**
- **XGBoost**
- **MLP Classifier** and more

Using **5-fold cross-validation**, I evaluated the models thoroughly and tuned their hyperparameters to maximize performance. I experimented with hyperparameters like:
- Number of trees.
- Learning rates.
- Max depth and more.

### 8. Feature Importance Analysis

For further insight, I analyzed feature importances using **XGBoost** and **Random Forest** models. By inspecting the most important features, I fine-tuned the model and experimented with different thresholds for selecting or removing features.

### 9. Ensemble Methods

To enhance performance, I explored **ensemble techniques**, including:
- **Bagging**
- **Boosting**
- **Stacking**

I combined predictions from multiple models, which led to improvements in model robustness.

### 10. Final Model: XGBoost Classifier

After extensive experimentation, the **XGBoost classifier** with hyperparameter tuning yielded the highest accuracy of **0.63**. Despite the challenges of the dataset, this accuracy is very competitive and demonstrates the model's predictive power relative to the industry standard of **0.70** for malware threat forecasting.

### 11. Model Evaluation

To ensure comprehensive evaluation, I used various performance metrics beyond just accuracy:
- **Precision**
- **Recall**
- **F1-score**

However, **accuracy** remained the primary metric due to its alignment with the project’s goal of accurate threat prediction.

---

## Conclusion

The System Threat Forecaster project involved thorough data exploration, feature engineering, model building, and tuning. The final model, a hyperparameter-tuned XGBoost classifier, achieved an impressive accuracy of **0.63**, a result that stands out in the context of industry standards for malware threat detection.

This project provided an end-to-end understanding of how to work with complex datasets, handle feature engineering, and optimize machine learning models for real-world performance. It demonstrated the importance of detailed preprocessing, feature selection, and model tuning to achieve strong results in a competitive field.
