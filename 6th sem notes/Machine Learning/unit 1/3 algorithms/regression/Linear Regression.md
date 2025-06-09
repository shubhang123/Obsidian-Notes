# Linear Regression Overview

Linear regression is a fundamental supervised learning algorithm widely used in machine learning for predictive analysis. It models a continuous target variable (e.g., house prices, product costs, or salaries) as a function of one or more independent variables. By assuming a linear relationship between inputs and outputs, linear regression estimates the best-fit line (or hyperplane in higher dimensions) to describe how changes in independent variables affect the dependent variable. Its simplicity and interpretability make it a cornerstone for forecasting and data-driven decision-making.

## Hypothesis Function for Simple Linear Regression

The model assumes a linear relationship between an input $x$ and an output $y$, plus random noise:

# $y = \beta_0 + \beta_1 x + \varepsilon$

- **$x$**: Independent variable (feature) from the training data
- **$y$**: Dependent variable (label) to predict
- **$\beta_0$**: Intercept, the value of $y$ when $x = 0$
- **$\beta_1$**: Slope (coefficient), the change in $y$ for a one-unit change in $x$
- **$\varepsilon$**: Error term, capturing noise or variation not explained by the linear model

## Purpose and Applications

Linear regression is a statistical method used to **analyze and understand relationships** between variables. Its primary goal is to **construct an efficient model to predict dependent attributes** from a set of independent variables. The output variable is typically a real or continuous value, such as salary, weight, or area. This method is widely applied in industries like finance, marketing, manufacturing, and medicine for **prediction and forecasting**.

The relationship between independent and dependent variables is assumed to be **linear**, represented by a **best-fit line**. The goal of simple linear regression is to fit this line to the data points as accurately as possible, enabling reliable predictions.

## Key Terminologies

- **Dependent Variable ($y$)**: The variable the model aims to predict or understand.
- **Independent Variables ($x$)**: Factors that influence the dependent variable, providing insights into its relationship with the target.

## Cost Function in Linear Regression

To determine the best-fit line, a **cost function** measures how well the model's predictions align with actual values. The most common cost function for linear regression is the **Mean Squared Error (MSE)**, which calculates the average of the squared differences between predicted and actual values:

# $\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$

- A **smaller MSE** indicates predictions closer to actual values, signifying a more accurate best-fit line.
- If data is widely scattered, achieving a very small MSE may be challenging.
- Unlike logistic regression, where MSE leads to a non-convex function with multiple local minima, MSE is suitable for linear regression as it forms a convex function, making optimization easier.

## Minimizing the Cost Function

The goal of training a linear regression model is to **minimize the cost function** by finding optimal parameter values (weights or coefficients, denoted as $m$ for slope and $c$ for intercept, or sometimes $\theta_1$ and $\theta_0$). This is achieved through:

1. **Initialization**: Parameters are initially set to random values.
    
2. **Iterative Updates**: Parameters are iteratively adjusted to reduce the cost function.
    
3. **Gradient Descent**: This algorithm finds the global minimum of the cost function by computing gradients (derivatives) with respect to the parameters ($m$ and $c$). The **learning rate ($L$)**, also denoted as $\alpha$ or $\eta$, controls the step size of updates. The update rules are:
    
    ## $m = m - L \times \frac{\partial \text{MSE}}{\partial m}$
    
    
    ## $c = c - L \times \frac{\partial \text{MSE}}{\partial c}$


4. **Convergence**: The process continues until the cost function reaches its minimum, yielding the optimal parameters for accurate predictions.