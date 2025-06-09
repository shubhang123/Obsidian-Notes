## Where the Cost Function Comes In

In linear regression, we fit the parameters (intercept and slopes) by **minimizing** a cost function. In practice this happens during the “model training” step:

1. **Define hypothesis**  
   We propose  
   $$
   \hat y = \beta_0 + \beta_1 x + \dots + \beta_p x_p.
   $$
2. **Compute cost**  
   For a given choice of parameters $\boldsymbol{\beta}$, the cost function measures how well the line explains the training data.  
3. **Optimize parameters**  
   We adjust $\boldsymbol{\beta}$ to find the minimum of that cost function—i.e. the parameter values that make predictions as close as possible to the actual targets.  

---

## Definition of the Cost Function

The most common cost function in linear regression is the **Mean Squared Error (MSE)**. For $m$ training examples, it’s defined as:

$$
J(\boldsymbol{\beta})
= \frac{1}{2m}\sum_{i=1}^{m}
  \bigl(\hat y^{(i)} - y^{(i)}\bigr)^2
= \frac{1}{2m}\sum_{i=1}^{m}
  \bigl(\mathbf{x}^{(i)\top}\boldsymbol{\beta} - y^{(i)}\bigr)^2.
$$

- The factor $\tfrac12$ is a convenience so that the derivative is simpler (it cancels the 2 in front).  
- $\hat y^{(i)} = \mathbf{x}^{(i)\top}\boldsymbol{\beta}$ is the model’s prediction for the $i$-th example.  
- $y^{(i)}$ is the true label.  

---

## Intuition Behind the Cost Function

- Each term $(\hat y^{(i)} - y^{(i)})^2$ is the **squared error** for one data point.  
- Squaring penalizes large errors more heavily and ensures the cost is always non-negative.  
- Summing over all $m$ points gives a single measure of overall “badness of fit.”  
- Dividing by $m$ (or $2m$) makes the scale independent of dataset size and simplifies gradient expressions.

---

## How It’s Minimized

To find the best parameters, we solve:

$$
\boldsymbol{\beta}^\star = \arg\min_{\boldsymbol{\beta}} J(\boldsymbol{\beta}).
$$

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
