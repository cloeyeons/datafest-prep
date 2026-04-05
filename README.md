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

Regression Analysis Results



| Variable | Coef. ($\beta$) | Std.Err | P-Value ($P>\|t|$) | Significance || :--- | :---: | :---: | :---: | :---: || Parental_Involvement | 1.3825 | 0.250 | 0.000 | ⭐⭐⭐ || Peer_Influence | 0.8680 | 0.230 | 0.000 | ⭐⭐⭐ || Family_Income | 0.8483 | 0.234 | 0.000 | ⭐⭐⭐ || Parental_Education_Level | 0.6966 | 0.223 | 0.002 | ⭐⭐ || Access_to_Resources | 0.5611 | 0.249 | 0.024 | ⭐ || Hours_Studied | 0.2409 | 0.029 | 0.000 | ⭐⭐⭐ || Attendance | 0.2219 | 0.015 | 0.000 | ⭐⭐⭐ || Sleep_Hours | 0.2207 | 0.118 | 0.062 | NS || Physical_Activity | 0.2892 | 0.169 | 0.087 | NS || Extracurricular_Activities | 0.5033 | 0.354 | 0.156 | NS |

> **Note:** Model Constant (Intercept) = `-41.7606`.  
> **Significance Levels:** ⭐⭐⭐ $P < 0.001$, ⭐⭐ $P < 0.01$, ⭐ $P < 0.05$, **NS** = Not Significant.

---

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

write here
