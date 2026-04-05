# datafest-prep

Research Question: Which factor has the most significant impact on the student's performance change?

Approaches:
1. Compare controllable vs. uncontrollable variables
2. Combination of factors that maximizes growth (Prediction)

Data Cleaning: Remove null data, 6378 left

Controllable
- hours studied
- attendance
- extracurricular activities
- sleep hours
- physical activity 

Uncontrollable
- family income
- access to resources
- parental education level
- peer influence
- parental involvement

## Approach 1

### 1. Correlation Analysis

| Rank | Feature | Correlation ($r$) | Strength |
| :--- | :--- | :--- | :--- |
| 1 | **Attendance** | `0.177668` | 🟡 Low-Moderate |
| 2 | **Hours_Studied** | `0.099537` | ⚪ Weak |
| 3 | **Parental_Involvement** | `0.064138` | ⚪ Weak |
| 4 | **Peer_Influence** | `0.047628` | ⚪ Very Weak |
| 5 | **Family_Income** | `0.042692` | ⚪ Very Weak |
| 6 | **Parental_Education_Level** | `0.041427` | ⚪ Very Weak |
| 7 | **Access_to_Resources** | `0.021637` | ⚪ Very Weak |
| 8 | **Sleep_Hours** | `0.018767` | ⚪ Very Weak |
| 9 | **Extracurricular_Activities** | `0.014628` | ⚪ Very Weak |
| 10 | **Physical_Activity** | `0.013673` | ⚪ Very Weak |

---

### 2. Multiple Linear Regression Results
The regression model reveals the specific impact of each variable while controlling for all other factors.

| Variable | Coef. (β) | Std.Err | P-Value (P > \|t\|) | Significance |
| :--- | :---: | :---: | :---: | :---: |
| **Parental_Involvement** | **1.3825** | 0.250 | `0.000` | ⭐⭐⭐ |
| **Peer_Influence** | **0.8680** | 0.230 | `0.000` | ⭐⭐⭐ |
| **Family_Income** | **0.8483** | 0.234 | `0.000` | ⭐⭐⭐ |
| **Parental_Education_Level** | **0.6966** | 0.223 | `0.002` | ⭐⭐ |
| **Access_to_Resources** | **0.5611** | 0.249 | `0.024` | ⭐ |
| **Hours_Studied** | **0.2409** | 0.029 | `0.000` | ⭐⭐⭐ |
| **Attendance** | **0.2219** | 0.015 | `0.000` | ⭐⭐⭐ |
| Sleep_Hours | 0.2207 | 0.118 | `0.062` | NS |
| Physical_Activity | 0.2892 | 0.169 | `0.087` | NS |
| Extracurricular_Activities | 0.5033 | 0.354 | `0.156` | NS |

> **Note:** Model Constant (Intercept) = `-41.7606`  
> **Significance Levels:** ⭐⭐⭐ P < 0.001, ⭐⭐ P < 0.01, ⭐ P < 0.05, **NS** = Not Significant.

### 3. Key Findings

#### 🚀 High Impact Drivers
* **Parental Involvement** is the most influential factor in the model. For every unit increase in parental involvement, the predicted score increases by **1.38 points**, holding other factors constant.
* **Peer Influence** and **Family Income** also show high positive coefficients, suggesting that social environment and financial stability are strong predictors of success.

### ⚠️ Statistical Observations
* **Attendance** has the highest raw correlation but a smaller unit-coefficient (0.22) compared to environmental factors. This suggests that while attendance is necessary, it is one of many incremental contributors.
* **Sleep, Physical Activity, and Extracurriculars** did not reach statistical significance ($P > 0.05$). In this specific dataset, these lifestyle factors do not have a reliable direct impact on grades.

---

### 🛠️ Tech Stack
* **Language:** Python
* **Analysis:** `Statsmodels`, `Pandas`, `NumPy`
* **Methodology:** Ordinary Least Squares (OLS) Regression



## Approach 2

### 1. Predicted score change for controllable variables

| Hours Studied | Attendance | Extracurricular | Sleep Hours | Physical Activity | Predicted Score Diff |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 44 | 100 | Yes | 10 | 5 | 4.11 |
| 44 | 100 | Yes | 9 | 5 | 3.90 |
| 44 | 99 | Yes | 10 | 5 | 3.89 |
| 43 | 100 | Yes | 10 | 5 | 3.87 |
| 44 | 100 | Yes | 8 | 5 | 3.69 |
| 44 | 99 | Yes | 9 | 5 | 3.68 |
| 44 | 98 | Yes | 10 | 5 | 3.66 |
| 43 | 100 | Yes | 9 | 5 | 3.66 |
| 44 | 100 | No | 10 | 5 | 3.66 |
| 43 | 99 | Yes | 10 | 5 | 3.65 |

### 2. Predicted score change for controllable variables

| Family Income | Access to Resources | Parental Education | Peer Influence | Parental Involvement | Predicted Score Diff |
| :--- | :--- | :--- | :--- | :--- | :--- |
| High | High | Postgraduate | Positive | High | -3.44 |
| High | High | College | Positive | High | -3.57 |
| High | Medium | Postgraduate | Positive | High | -4.22 |
| High | Medium | College | Positive | High | -4.34 |
| High | Low | Postgraduate | Positive | High | -4.34 |
| High | Low | College | Positive | High | -4.47 |
| Medium | High | Postgraduate | Positive | High | -4.61 |
| High | High | Postgraduate | Neutral | High | -4.61 |
| High | High | Postgraduate | Positive | Medium | -4.63 |
| Medium | High | College | Positive | High | -4.73 |

---

## Model Performance – Random Forest Classifier

We converted the regression task (`Score_Diff`) into a binary classification problem:  
**Improved = 1** if `Score_Diff > 0`, else **0**.

### Evaluation Metrics (test set, 20% holdout)

| Metric       | Score  |
|--------------|--------|
| Accuracy     | 0.6207 |
| ROC-AUC      | 0.5043 |

### Classification Report

| Class | Precision | Recall | F1-score | Support |
|-------|-----------|--------|----------|---------|
| 0 (No improvement) | 0.68 | 0.82 | 0.74 | 861 |
| 1 (Improved)       | 0.36 | 0.21 | 0.27 | 415 |

- **Macro avg**: precision = 0.52, recall = 0.52, f1 = 0.51  
- **Weighted avg**: precision = 0.58, recall = 0.62, f1 = 0.59

### Confusion Matrix

|              | Predicted: 0 | Predicted: 1 |
|--------------|--------------|--------------|
| Actual: 0    | 703          | 158          |
| Actual: 1    | 326          | 89           |

### Feature Importance (Top 5)

| Feature                               | Importance |
|---------------------------------------|------------|
| Attendance                            | 0.3484     |
| Hours_Studied                         | 0.3448     |
| Sleep_Hours                           | 0.1492     |
| Physical_Activity                     | 0.1186     |
| Extracurricular_Activities (binary)   | 0.0390     |

### Interpretation

- The model performs **only slightly better than random guessing** (ROC‑AUC ≈ 0.50).  
- It has **high false negatives** (326 actual improvements missed) and **low recall for class 1** (0.21).  
- Attendance and study hours are the most important features, but overall predictive power is weak.  
- Suggests that `Score_Diff` (or its binary form) is largely **unpredictable** from the available student activity features.

### Next steps

- Collect more informative features (e.g., prior test scores, study quality, teacher feedback).  
- Consider predicting the raw `Exam_Score` instead of the difference.  
- Try other algorithms (logistic regression, gradient boosting) or feature engineering.
