The sources indicate several types of regression, primarily categorising them by the nature of the relationship they model or the algorithm used.

Regression, in general, is a statistical method used to **analyse and understand the relationship between two or more variables of interest**. Its main objective is to **construct an efficient model to predict dependent attributes from a set of independent variables**. In a regression problem, the **output variable is typically a real or continuous value**, such as salary, weight, or area. This statistical method is widely used for **prediction and forecasting** across various industries, including finance, marketing, manufacturing, and medicine.

The types of regression explicitly mentioned in the sources include:

- **Simple Linear Regression**:
    
    - This is a common regression technique where the **independent variable has a linear relationship with the dependent variable**.
    - The goal is to **plot a best-fit straight line** to summarise the relationship in the data and make predictions.
    - In this model, the objective is to find the optimal values for the model's parameters (e.g., $\theta_1$ and $\theta_2$, or 'm' and 'c' for slope and intercept), which involves **minimising a cost function**. The most common cost function for linear regression is the **Mean Squared Error (MSE)**, which measures the root mean squared error between the predicted and true values. A smaller MSE indicates a more accurate line of best fit.
- **Polynomial Regression**:
    
    - This technique involves **transforming the original features into polynomial features of a given degree** before performing the regression. This allows the model to fit non-linear relationships by using polynomial equations.
- **Support Vector Regression**:
    
    - This is listed as a type of regression, but the provided sources do not offer further specific details on its mechanism.
- **Decision Tree Regression**:
    
    - This is another type of regression listed, though the sources do not elaborate on its specific application or methodology within regression. Decision trees are generally mentioned in the context of model complexity and issues like underfitting or overfitting.
- **Random Forest Regression**:
    
    - Similar to Support Vector Regression and Decision Tree Regression, this is named as a type, but the sources do not provide further details on its operational specifics for regression tasks.

### Distinction: Logistic Regression

It is important to note that **Logistic Regression**, despite having 'regression' in its name, is presented in the sources as a **classification algorithm**, not a regression algorithm for continuous values.

- It is used to **assign observations to a discrete set of classes** (e.g., email spam or not spam, tumour malignant or benign).
- It transforms its output using the **Sigmoid function** (also known as the logistic function) to return a probability value between 0 and 1.
- Unlike linear regression, using MSE as a cost function for logistic regression would result in a **non-convex function with many local minimums**, making it difficult to find the global minimum. It is also categorised as a "Linear Classifier".