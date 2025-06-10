
![[Pasted image 20250610113944.png]]
# Gradient Descent Optimization

## What is Gradient Descent?

Gradient descent is a fundamental optimization algorithm used to train machine learning models by iteratively adjusting model parameters (weights and biases) to minimize the cost/loss function. It's a search technique that finds the optimal values for parameters that result in the best model performance.

## Core Concept

**Objective**: Minimize the cost function by finding the optimal weights and biases that produce the lowest prediction error.

**Analogy**: Think of it like rolling a ball down a hill to find the lowest point. The algorithm takes steps downhill (in the direction of steepest descent) until it reaches the minimum.

## How It Works

### Basic Steps

1. **Initialize**: Start with random weights and biases
2. **Calculate**: Compute the cost function (e.g., Mean Squared Error for linear regression)
3. **Find Gradient**: Calculate the derivative of the cost function with respect to each parameter
4. **Update**: Adjust parameters in the opposite direction of the gradient
5. **Repeat**: Continue until convergence or maximum iterations

### Parameter Update Formula

```
w' = w - η × ∂J/∂w
```

Where:

- w' = new weight value
- w = current weight value
- η (eta) = learning rate
- ∂J/∂w = partial derivative of cost function J with respect to weight w

## Key Components

### Learning Rate (η)

- **Purpose**: Controls the size of steps taken toward the minimum
- **Too High**: May overshoot the minimum and oscillate
- **Too Low**: Convergence will be very slow
- **Typical Values**: 0.001 to 0.1

### Gradient (∂J/∂w)

- **Definition**: The slope or rate of change of the cost function
- **Direction**: Points toward the steepest increase
- **Usage**: We move in the opposite direction (negative gradient) to minimize

## Types of Gradient Descent

### Batch Gradient Descent

- **Process**: Uses entire dataset to calculate gradient
- **Pros**: Stable convergence, smooth path to minimum
- **Cons**: Slow for large datasets, requires more memory

### Stochastic Gradient Descent (SGD)

- **Process**: Uses one sample at a time to calculate gradient
- **Pros**: Fast updates, works well with large datasets
- **Cons**: Noisy convergence path, may not reach exact minimum

### Mini-batch Gradient Descent

- **Process**: Uses small batches of data (e.g., 32, 64, 128 samples)
- **Pros**: Balance between speed and stability
- **Cons**: Most commonly used in practice

## Example: Linear Regression

For linear regression with Mean Squared Error:

- **Model**: ŷ = wx + b
- **Cost Function**: J = (1/2n) × Σ(y - ŷ)²
- **Weight Update**: w = w - η × (1/n) × Σ(ŷ - y) × x
- **Bias Update**: b = b - η × (1/n) × Σ(ŷ - y)

## Advantages and Limitations

### Advantages

- Simple to understand and implement
- Works well for convex functions
- Guaranteed to find global minimum for convex problems
- Foundation for many advanced optimization algorithms

### Limitations

- Can get stuck in local minima for non-convex functions
- Sensitive to learning rate selection
- May converge slowly for certain function shapes
- Can struggle with features of different scales

## Practical Considerations

**Convergence**: Monitor the cost function to ensure it's decreasing over iterations. Stop when the change becomes negligible.

**Feature Scaling**: Normalize or standardize features to ensure all parameters update at similar rates.

**Initialization**: Random initialization of weights is crucial to avoid getting stuck in poor local minima.

**Stopping Criteria**: Set maximum iterations or minimum change threshold to prevent infinite loops.