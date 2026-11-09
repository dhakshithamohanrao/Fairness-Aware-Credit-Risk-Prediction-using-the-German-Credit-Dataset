# Fairness-Aware Credit Risk Prediction Using the German Credit Dataset

## Project Overview

This project investigates fairness and ethical considerations in machine learning-based credit risk prediction using the German Credit Dataset.

A Random Forest classifier is developed to predict whether a loan applicant represents a good or bad credit risk. The project evaluates potential age-related bias in the baseline model and applies a fairness mitigation technique called **Reweighing** to reduce disparities between demographic groups.

The objective is to demonstrate how predictive performance and fairness can be considered together when developing responsible AI systems for financial decision-making.

## Project Information

- **Student:** Dhakshitha Mohan Rao
- **Student ID:** GH1044699
- **Module:** M515 – Ethical Issues for AI
- **Project Type:** Individual Project
- **Dataset:** German Credit Dataset

## Problem Statement

Financial institutions increasingly use machine learning models to automate credit risk assessment. Although these models can improve efficiency and consistency, they may also reproduce biases present in historical data.

This project addresses two key questions:

1. How accurately can a machine learning model classify loan applicants as good or bad credit risks?
2. Does the model produce different prediction outcomes for younger and older applicants?

Age is selected as the protected attribute:

- **Privileged group:** Applicants aged 25 years and above.
- **Unprivileged group:** Applicants below 25 years.

## Dataset

**Source:** [German Credit Dataset – UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/statlog+(german+credit+data))

The dataset contains:

- 1,000 loan applicant records.
- 20 input features.
- 1 target variable.
- Numerical and categorical attributes.

The features include credit history, loan duration, credit amount, savings, employment duration, personal characteristics, housing, and age.

The target variable represents credit risk:

- `1` – Good credit risk.
- `0` – Bad credit risk.

## Tools & Technologies

- **Python** – Programming and analysis
- **Pandas & NumPy** – Data manipulation and preprocessing
- **Matplotlib & Seaborn** – Exploratory data analysis and visualisation
- **Scikit-learn** – Machine learning, preprocessing, and model evaluation
- **Jupyter Notebook / Google Colab** – Development environment

## Project Workflow

### 1. Exploratory Data Analysis (EDA)

The dataset was examined to understand its structure, feature distributions, and potential data quality issues.

Key activities:
- Dataset structure and data type inspection.
- Missing-value assessment.
- Statistical summary of numerical features.
- Credit risk distribution analysis.
- Applicant age and credit amount distributions.
- Comparison of credit risk across age groups.

**Key observation:** The dataset contains 1,000 records with no missing values. The target distribution consists of 700 good credit applicants and 300 bad credit applicants.

### 2. Data Preprocessing

The following preprocessing steps were performed:

- Converted the target variable into binary classification labels.
- Applied Label Encoding to categorical variables.
- Created age groups for fairness assessment.
- Separated input features and target variable.
- Split the dataset into training and testing sets using an 80:20 ratio.
- Used stratified sampling and `random_state=42`.

### 3. Baseline Machine Learning Model

A Random Forest Classifier was trained without fairness intervention to establish a baseline for predictive performance and fairness evaluation.

**Baseline performance:**

| Metric | Result |
|---|---:|
| Accuracy | 0.780 |
| Precision – Good Credit | 0.81 |
| Recall – Good Credit | 0.89 |
| F1-score – Good Credit | 0.85 |
| Precision – Bad Credit | 0.67 |
| Recall – Bad Credit | 0.52 |
| F1-score – Bad Credit | 0.58 |

Feature importance analysis identified credit amount, account status, loan duration, age, and loan purpose among the most influential features.

### 4. Fairness Assessment

The baseline model was evaluated using two fairness metrics:

- **Statistical Parity Difference (SPD):** Measures the difference in positive prediction rates between unprivileged and privileged groups. A value closer to zero indicates greater statistical parity.
- **Disparate Impact (DI):** Measures the ratio of positive prediction rates between unprivileged and privileged groups. A value closer to one indicates greater statistical parity.

**Baseline fairness results:**

| Fairness Metric | Result |
|---|---:|
| Privileged Positive Prediction Rate | 0.802 |
| Unprivileged Positive Prediction Rate | 0.571 |
| Statistical Parity Difference | -0.231 |
| Disparate Impact | 0.712 |

The results indicate a disparity in favourable predictions between the two age groups, with younger applicants receiving a lower positive prediction rate.

### 5. Fairness Mitigation – Reweighing

A reweighing-inspired sample weighting approach was implemented to reduce age-related disparities.

The approach assigns greater weight to training observations belonging to applicants below 25 years of age.

A second Random Forest classifier was trained using these sample weights and evaluated against the same test dataset.

### 6. Baseline vs Fairness-Aware Model

The following table compares predictive performance and fairness before and after the intervention.

| Metric | Baseline Model | Fairness-Aware Model |
|---|---:|---:|
| Accuracy | 0.780 | 0.775 |
| Statistical Parity Difference | -0.231 | -0.076 |
| Disparate Impact | 0.712 | 0.908 |

**Key observations:**

- Statistical Parity Difference moved closer to zero.
- Disparate Impact improved towards one.
- Accuracy decreased slightly from 78.0% to 77.5%.
- The fairness-aware model reduced the observed disparity between age groups while maintaining similar predictive accuracy.

## Key Findings

1. The baseline Random Forest model achieved 78% accuracy on the test dataset.
2. Credit amount, loan duration, age, and credit history were among the most important predictive features.
3. The baseline model showed differences in positive prediction rates between younger and older applicants.
4. The baseline Statistical Parity Difference was -0.231, indicating a disparity between the groups.
5. The fairness mitigation approach improved the Statistical Parity Difference to -0.076.
6. Disparate Impact improved from 0.712 to 0.908.
7. Predictive accuracy decreased only slightly, from 0.780 to 0.775.

## Ethical Considerations

This project highlights the importance of fairness in automated financial decision-making.

Key ethical considerations include:

- Potential age-related discrimination in credit scoring.
- The influence of historical data on machine learning predictions.
- Transparency and interpretability of automated lending decisions.
- The need to evaluate fairness alongside predictive performance.
- The importance of responsible AI governance and continuous model auditing.

## Limitations

- The dataset contains only 1,000 observations, which may limit generalisability.
- Fairness assessment focuses only on age as the protected attribute.
- The age threshold of 25 years is a project-defined grouping.
- Statistical Parity Difference and Disparate Impact capture only specific dimensions of fairness.
- The implemented weighting approach is a simplified reweighing-inspired intervention rather than a full implementation of the AIF360 Reweighing algorithm.
- Further evaluation using Equal Opportunity and Equalized Odds would provide additional fairness insights.

## Future Work

Potential improvements include:

- Evaluate fairness across additional protected attributes.
- Implement formal reweighing using the AI Fairness 360 (AIF360) library.
- Compare different fairness mitigation techniques.
- Evaluate Equal Opportunity and Equalized Odds.
- Investigate alternative classification algorithms.
- Perform more comprehensive model explainability and bias analysis.
- Test the approach on larger and more diverse credit datasets.

## Conclusion

This project demonstrates the importance of integrating fairness evaluation into machine learning-based credit risk prediction.

Although the baseline Random Forest model achieved 78% accuracy, fairness assessment revealed disparities in prediction outcomes across age groups.

After applying a sample weighting intervention, the Statistical Parity Difference improved from -0.231 to -0.076, while Disparate Impact increased from 0.712 to 0.908. Accuracy remained relatively stable at 77.5%.

The findings highlight that responsible AI systems should not be evaluated solely on predictive accuracy. Fairness, transparency, and ethical considerations are equally important, particularly in high-impact applications such as financial services.

## References

1. Barocas, S., Hardt, M. and Narayanan, A. (2019). *Fairness and Machine Learning*. https://fairmlbook.org/
2. Breiman, L. (2001). Random Forests. *Machine Learning*, 45(1), 5–32.
3. Dua, D. and Graff, C. (2019). *UCI Machine Learning Repository*. https://archive.ics.uci.edu/
4. Mehrabi, N. et al. (2021). A Survey on Bias and Fairness in Machine Learning. *ACM Computing Surveys*, 54(6), 1–35.
5. Pedreschi, D., Ruggieri, S. and Turini, F. (2008). Discrimination-aware Data Mining. *Proceedings of the 14th ACM SIGKDD International Conference on Knowledge Discovery and Data Mining*, 560–568.

---

**Author:** Dhakshitha Mohan Rao  
**Module:** M515 – Ethical Issues for AI  
**Project:** Individual Project – Fairness-Aware Credit Risk Prediction
