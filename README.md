Share: 108  Eur: 108  Units: 108
Obs modello: 49759
                            OLS Regression Results                            
==============================================================================
Dep. Variable:                    eur   R-squared:                       0.176
Model:                            OLS   Adj. R-squared:                  0.176
Method:                 Least Squares   F-statistic:                     2121.
Date:                Tue, 21 Apr 2026   Prob (F-statistic):               0.00
Time:                        00:12:57   Log-Likelihood:            -1.0912e+05
No. Observations:               49759   AIC:                         2.183e+05
Df Residuals:                   49753   BIC:                         2.183e+05
Df Model:                           5                                         
Covariance Type:            nonrobust                                         
===================================================================================
                      coef    std err          t      P>|t|      [0.025      0.975]
-----------------------------------------------------------------------------------
const               2.4408      0.470      5.193      0.000       1.520       3.362
log_price           1.7299      0.027     63.809      0.000       1.677       1.783
log_market_size     0.2915      0.028     10.283      0.000       0.236       0.347
HHI                -0.6911      0.196     -3.519      0.000      -1.076      -0.306
lag_sales        3.282e-06   4.25e-08     77.222      0.000     3.2e-06    3.37e-06
is_brand           -0.4537      0.021    -21.914      0.000      -0.494      -0.413
==============================================================================
Omnibus:                     5210.384   Durbin-Watson:                   1.102
Prob(Omnibus):                  0.000   Jarque-Bera (JB):             7848.313
Skew:                          -0.788   Prob(JB):                         0.00
Kurtosis:                       4.141   Cond. No.                     1.27e+07
==============================================================================

Notes:
[1] Standard Errors assume that the covariance matrix of the errors is correctly specified.
[2] The condition number is large, 1.27e+07. This might indicate that there are
strong multicollinearity or other numerical problems.

=== INTERPRETAZIONE ===
log_price: coeff=1.7299, p=0
log_market_size: coeff=0.2915, p=8.917e-25
HHI: coeff=-0.6911, p=0.0004336
lag_sales: coeff=0.0000, p=0
is_brand: coeff=-0.4537, p=6.1e-106
