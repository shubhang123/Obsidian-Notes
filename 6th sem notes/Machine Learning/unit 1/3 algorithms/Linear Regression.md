# Linear Regression Overview

## What It Does

Linear regression is a supervised machine learning algorithm used to **predict a continuous target variable** based on one or more input features. It assumes a **linear relationship** between the features and the target, making it ideal for tasks such as:

- Predicting house prices based on features like size or location.
- Forecasting sales using advertising budgets.
- Estimating outcomes like temperature or medical metrics (e.g., cholesterol levels).

When applied, it:

- Fits a straight line (or hyperplane for multiple features) to the data to minimize prediction errors.
- Provides coefficients that show how each feature influences the target.
- Is widely used in fields like finance, real estate, and healthcare for regression tasks.

## Mathematical Representation

Linear regression predicts the target ( y ) as a linear combination of input features ( x ).

### Simple Linear Regression (One Feature)

[ \hat{y} = \beta_0 + \beta_1 x ]

- ( \hat{y} ): Predicted value of the target.
- ( x ): Single input feature.
- ( \beta_0 ): Intercept (value of ( \hat{y} ) when ( x = 0 )).
- ( \beta_1 ): Slope (change in ( \hat{y} ) per unit change in ( x )).

### Multiple Linear Regression (Multiple Features)

[ \hat{y} = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \dots + \beta_m x_m ]

- ( x_1, x_2, \dots, x_m ): Input features.
- ( \beta_1, \beta_2, \dots, \beta_m ): Coefficients representing the impact of each feature.
- ( m ): Number of features.

### Objective

The goal is to find coefficients ( \beta_0, \beta_1, \dots, \beta_m ) that minimize the **sum of squared errors**:  
[ J(\beta) = \sum_{i=1}^n (y_i - \hat{y}_i)^2 ]

- ( n ): Number of data points.
- ( y_i ): Actual target value for the ( i )-th data point.
- ( \hat{y}_i ): Predicted value for the ( i )-th data point.
- Coefficients are typically optimized using **Ordinary Least Squares (OLS)** or **Gradient Descent**.