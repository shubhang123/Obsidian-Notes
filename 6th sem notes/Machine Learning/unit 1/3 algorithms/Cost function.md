Linear regression is a widely used statistical method that helps to **analyse and understand the relationship between two or more variables of interest**. Its primary goal is to **construct an efficient model to predict dependent attributes from a set of independent variables**. In a linear regression problem, the **output variable is typically a real or continuous value**, such as salary, weight, or area. It is often used for prediction and forecasting in various industries, including finance, marketing, manufacturing, and medicine.

In this method, the relationship between the independent and dependent variables is assumed to be **linear**, meaning it can be summarised by a straight line, known as the **best-fit line**.

**Key Terminologies in Linear Regression:**

- **Dependent Variable (Y):** This is the variable that the model attempts to understand or forecast.
- **Independent Variables (X):** These are the factors that influence the dependent variable and provide information about its relationship with the target.
- **Best-fit Line:** In linear regression, the model aims to plot a straight line that best fits the given data points. This line summarises the relationship in the data and can be used to make predictions.

**Cost Function in Linear Regression:** To determine the best-fit line, a **cost function** is used to measure how well the model's predictions align with the actual observed values. For linear regression, the most common cost function is the **Mean Squared Error (MSE)**.

The MSE measures the **Root Mean Squared error between the predicted value and the true value**. It is calculated as the sum of the squared differences between the predictions and the actual values, divided by the number of observations. The formula for MSE is: **MSE = Sum [ (Prediction - Actual)² ] * (1 / num_observations)**

A **smaller MSE value indicates that the model's predictions are closer to the actual values**, meaning the line of best fit is more accurate. Unlike in logistic regression, where using MSE would result in a non-convex function with many local minimums, MSE is suitable for linear regression.

**Minimising the Cost Function:** The primary goal in training a linear regression model is to **minimise this cost function**. This is achieved by finding the optimal values for the model's parameters (weights or coefficients, often denoted as $\theta_1$ and $\theta_2$, or 'm' and 'c' in a simple linear equation like $y = mx + c$).

The process of minimising the cost function typically involves:

1. **Initialisation:** The model initially selects the parameter values randomly.
2. **Iterative Updates:** These parameter values are then iteratively updated using an optimisation algorithm called **Gradient Descent**.
3. **Gradient Descent:** Gradient descent helps to **find the global minimum of the cost function** by indicating the direction in which the parameters should be adjusted. The 'learning rate' (L) in gradient descent controls the step size of these updates.
4. **Convergence:** This iterative process continues until the cost function reaches its minimum, at which point the model obtains the best parameter values for predicting the dependent variable.