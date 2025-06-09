## Hypothesis Function

In linear regression, we define a **hypothesis function** h(x)h(x) that represents our model’s prediction. This function maps an input variable xx to a predicted output yy. It typically takes the form of a straight line:

```markdown
h(x) = b₀ + b₁·x
```

where b0b₀ (the intercept) and b1b₁ (the slope) are parameters the model will learn.

---

## Goal of Linear Regression

The primary objective of linear regression is to find the best-fit line that accurately predicts the dependent variable y from the independent variable x. In other words, we want to choose b₀ and b₁ such that the difference between our predicted values h(x)h(x) and the true values y is as small as possible across all training examples.

---

## Role of the Cost Function

To quantify how “off” our predictions are, we use a **cost function**. The cost function measures the average error between the predicted values and the actual values over the entire training set. By minimizing this cost function, we guide the model toward the best parameter values.

---

## Mean Squared Error (MSE) Cost Function

One of the most common cost functions in linear regression is the **Mean Squared Error** (MSE). It calculates the average of the squared differences between the predicted and actual values:

- **Why square the errors?**  
    Squaring ensures that positive and negative errors don’t cancel out and penalizes larger errors more heavily.
    
- **Why take the average?**  
    Averaging over all training examples gives a single scalar measure of overall model performance, making it easier to compare and optimize.
    

By iteratively adjusting b0b₀ and b1b₁ (e.g., via gradient descent), the algorithm seeks to minimize the MSE cost function, thereby achieving the most accurate predictions possible.
Two common methods:

1. **Normal equation (closed-form)**  
   $$ 
   \boldsymbol{\beta}^\star
   = \bigl(\mathbf{X}^\top \mathbf{X}\bigr)^{-1}\mathbf{X}^\top \mathbf{y}.
   $$  
   Works when $\mathbf{X}^\top\mathbf{X}$ is invertible and $p$ is relatively small.

2. **Gradient descent (iterative)**  
   - Compute the gradient  
     $$
     \nabla_{\boldsymbol{\beta}}J
     = \frac{1}{m}\,\mathbf{X}^\top(\mathbf{X}\boldsymbol{\beta}-\mathbf{y}).
     $$
   - Update rule  
     $$
     \boldsymbol{\beta} \;\gets\;
     \boldsymbol{\beta}
     - \alpha\,\nabla_{\boldsymbol{\beta}}J
     $$
     where $\alpha$ is the learning rate.  
   - Repeat until $J(\boldsymbol{\beta})$ stops decreasing.

---

## Why It Matters

- The cost function provides a **clear objective**: make predictions close to reality.  
- Its shape (a convex paraboloid in the case of MSE) guarantees a **single global minimum**—so gradient descent won’t get stuck in local minima.  
- By inspecting the cost value during training, you can **monitor convergence**, tune the learning rate $\alpha$, and detect issues like slow learning or divergence.
