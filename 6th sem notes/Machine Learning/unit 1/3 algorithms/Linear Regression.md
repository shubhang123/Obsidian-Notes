Linear regression is one of the simplest—and most widely used—supervised learning algorithms in machine learning. It’s primarily employed for predictive analysis, modeling a continuous target variable (for example, house prices, product costs, or salaries) as a function of one or more independent (input) variables. By assuming a linear relationship between the inputs and the output, linear regression estimates the best-fit line (or hyperplane in multiple dimensions) that explains how changes in each independent variable influence the dependent variable. This straightforward approach makes it both easy to implement and highly interpretable, which is why it remains a foundational tool for forecasting and data-driven decision-making.

![[Pasted image 20250609150627.png]]

## Hypothesis Function for Simple Linear Regression

The model assumes a linear relationship between an input xx and an output yy, plus random noise:

y=β0+β1 x+εy = \beta_0 + \beta_1\,x + \varepsilon

- **xx**  
    Independent variable (feature) from the training data
    
- **yy**  
    Dependent variable (label) we want to predict
    
- **β0\beta_0**  
    Intercept: the value of yy when x=0x = 0
    
- **β1\beta_1**  
    Slope (coefficient): the change in yy for a one-unit change in xx
    
- **ε\varepsilon**  
    Error term: captures noise or any variation not explained by the linear model