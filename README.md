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
### Correlation Coefficient Table(from highest to lowest)
Attendance                    0.177668
Hours_Studied                 0.099537
Parental_Involvement          0.064138
Peer_Influence                0.047628
Family_Income                 0.042692
Parental_Education_Level      0.041427
Access_to_Resources           0.021637
Sleep_Hours                   0.018767
Extracurricular_Activities    0.014628
Physical_Activity             0.013673



### Regression Output


==============================================================================================
                                 coef    std err          t      P>|t|      [0.025      0.975]
----------------------------------------------------------------------------------------------
const                        -41.7606      2.026    -20.612      0.000     -45.732     -37.789
Hours_Studied                  0.2409      0.029      8.296      0.000       0.184       0.298
Attendance                     0.2219      0.015     14.736      0.000       0.192       0.251
Extracurricular_Activities     0.5033      0.354      1.420      0.156      -0.191       1.198
Sleep_Hours                    0.2207      0.118      1.864      0.062      -0.011       0.453
Physical_Activity              0.2892      0.169      1.711      0.087      -0.042       0.621
Family_Income                  0.8483      0.234      3.628      0.000       0.390       1.307
Access_to_Resources            0.5611      0.249      2.255      0.024       0.073       1.049
Parental_Education_Level       0.6966      0.223      3.127      0.002       0.260       1.133
Peer_Influence                 0.8680      0.230      3.777      0.000       0.418       1.319
Parental_Involvement           1.3825      0.250      5.524      0.000       0.892       1.873
==============================================================================================






## Approach 2

write here
