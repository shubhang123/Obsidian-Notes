
## Cost Function Overview  
A **cost function** (or **loss function**) quantifies how far off a model’s predictions are from the true target values. In linear regression, it measures the average squared difference between the actual outputs and the predictions.


## Mean Squared Error (MSE) Cost for Linear Regression  
Given a training set of $n$ examples $\{(x^{(i)}, y^{(i)})\}_{i=1}^n$ and a hypothesis (prediction) function $h(x)$, the **MSE cost** is defined as  

$J = \frac{1}{n} \sum_{i=1}^n \bigl(y^{(i)} - h(x^{(i)})\bigr)^2$

- Here, $y^{(i)}$ is the actual output for the $i$-th example.
    
- $h(x^{(i)})$ is the predicted output (often $h(x)=b_0 + b_1 x$).
    
- Squaring the error ensures all differences are non-negative and penalizes larger errors more heavily.
    
- Averaging by $1/n$ normalizes the cost across different dataset sizes.
    

---

## Why MSE?

- **Smoothness**: The squared term makes $J$ differentiable everywhere, which is essential for gradient-based optimization.
    
- **Penalization of Large Errors**: Squaring amplifies larger errors, encouraging the model to avoid them.
    
- **Analytical Convenience**: The derivative of $J$ with respect to model parameters has a clean form.
    

---

## Optimizing the Cost Function

To find the best parameters ($b_0, b_1, \dots$), we minimize $J$ using **gradient descent**:


$b_j := b_j - \alpha \,\frac{\partial J}{\partial b_j}$


where


$\displaystyle \frac{\partial J}{\partial b_j}
= -\frac{2}{n} \sum_{i=1}^n \bigl(y^{(i)} - h(x^{(i)})\bigr)\,x_j^{(i)}$


- $\alpha$ is the learning rate controlling the step size.
    
- Iteration continues until $J$ converges (i.e., changes very little).
    

---

## Key Takeaways

- The cost function $J = \tfrac{1}{n}\sum_{i=1}^n (y^{(i)} - h(x^{(i)}))^2$ is central to training linear regression.
    
- Minimizing $J$ yields the parameters that best fit the data in a least-squares sense.
    
- Gradient descent leverages the derivative of $J$ to iteratively improve the model.