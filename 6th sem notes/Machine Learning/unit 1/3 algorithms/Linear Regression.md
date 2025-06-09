Linear regression is one of the simplest—and most widely used—supervised learning algorithms in machine learning. It’s primarily employed for predictive analysis, modeling a continuous target variable (for example, house prices, product costs, or salaries) as a function of one or more independent (input) variables. By assuming a linear relationship between the inputs and the output, linear regression estimates the best-fit line (or hyperplane in multiple dimensions) that explains how changes in each independent variable influence the dependent variable. This straightforward approach makes it both easy to implement and highly interpretable, which is why it remains a foundational tool for forecasting and data-driven decision-making.

![[Pasted image 20250609150627.png]]

## Hypothesis Function for Simple Linear Regression

The model assumes a linear relationship between an input \(x\) and an output \(y\), plus random noise:

$$
y = \beta_0 + \beta_1\,x + \varepsilon
$$

- **$x$**  
  Independent variable (feature) from the training data  
- **$y$**  
  Dependent variable (label) we want to predict  
- **$\beta_0$**  
  Intercept: the value of $y$ when $x = 0$  
- **$\beta_1$**  
  Slope (coefficient): the change in $y$ for a one-unit change in $x$  
- **$\varepsilon$**  
  Error term: captures noise or any variation not explained by the linear model  


Linear regression is a widely used statistical method that helps to **analyse and understand the relationship between two or more variables of interest**. Its primary goal is to **construct an efficient model to predict dependent attributes from a set of independent variables**. In a linear regression problem, the **output variable is typically a real or continuous value**, such as salary, weight, or area. This statistical method is used for **prediction and forecasting** in various industries, including finance, marketing, manufacturing, and medicine.

In this method, the relationship between the independent and dependent variables is assumed to be **linear**. This linear relationship can be summarised by a straight line, known as the **best-fit line**. The main goal of simple linear regression is to consider the given data points and plot this best-fit line to fit the model in the best way possible. This line can then be used to make predictions based on the data.

**Key Terminologies in Linear Regression:**

- **Dependent Variable (Y):** This is the variable that the model attempts to **understand or forecast**.
- **Independent Variables (X):** These are the factors that **influence the dependent variable** and provide information regarding its relationship with the target.

**Cost Function in Linear Regression:** To determine the best-fit line, a **cost function** is used to measure how well the model's predictions align with the actual observed values. For linear regression, the most common cost function is the **Mean Squared Error (MSE)**.

The MSE measures the **Root Mean Squared error between the predicted value and the true value**. It is calculated as the sum of the squared differences between the predictions and the actual values, divided by the number of observations. The formula for MSE is: 

# $\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2$

A **smaller MSE value indicates that the model's predictions are closer to the actual values**, meaning the line of best fit is more accurate. However, if the data is widely scattered around the regression line, it might be impossible to achieve a very small MSE. Unlike in logistic regression, where using MSE would result in a non-convex function with many local minimums, making it very difficult to minimise and find the global minimum, MSE is suitable for linear regression.

**Minimising the Cost Function:** The primary goal in training a linear regression model is to **minimise this cost function**. This is achieved by finding the optimal values for the model's parameters (weights or coefficients, often denoted as $\theta_1$ and $\theta_2$, or 'm' and 'c' which refer to coefficient 1 and coefficient 2, or weight 1 and weight 2).

The process of minimising the cost function typically involves:

1. **Initialisation:** The model initially selects parameter values randomly.
2. **Iterative Updates:** These parameter values are then iteratively updated to minimise the cost function until it reaches its minimum.
3. **Gradient Descent:** The process of reducing the cost value is done using **Gradient Descent**. Gradient Descent helps to **find the global minimum of the cost function** by indicating the direction in which the parameters should be adjusted. This involves calculating the derivatives (gradients) with respect to the parameters (m and c). The 'learning rate' (L), also sometimes represented as $\alpha$ or $\eta$ or $\epsilon$, controls the step size of these updates. The parameters are updated using the following equation where L is the learning rate: $m = m - L \times (\text{derivative of cost function with respect to } m)$ $c = c - L \times (\text{derivative of cost function with respect to } c)$
4. **Convergence:** This iterative process continues until the cost function reaches its minimum, at which point the model obtains the best parameter values for predicting the dependent variable.
