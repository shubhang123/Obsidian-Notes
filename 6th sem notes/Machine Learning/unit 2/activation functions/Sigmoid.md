## Sigmoid Activation Function

# **Formula:** $$f(x) = \frac{1}{1 + e^{-x}}$$

**Output Range:** 0 to 1
![[Pasted image 20250609235351.png]]
**Key Characteristics:**

- S-shaped curve that smoothly transitions between 0 and 1
- Differentiable everywhere, making it suitable for backpropagation
- Outputs can be interpreted as probabilities since they're bounded between 0 and 1
- Symmetric around the point (0, 0.5)

**When to Use:**

- Binary classification problems (output layer)
- When you need probabilistic outputs
- Hidden layers in shallow networks
- Problems requiring smooth, continuous activation

**Advantages:**

- Smooth gradient, good for gradient descent
- Output bounded between 0 and 1
- Easy to understand and implement
- Historically well-studied and reliable

**Limitations:**

- **Vanishing Gradient Problem**: Gradients become very small for large positive/negative inputs, slowing training in deep networks
- **Not Zero-Centered**: Outputs are always positive, which can cause inefficient gradient updates
- **Computational Cost**: Exponential function is more expensive than simpler alternatives
- **Saturation**: Function saturates at extremes (approaches 0 or 1), leading to slow learning

**Derivative:** $$f'(x) = f(x)(1 - f(x))$$

**Modern Usage:**

- Primarily used in output layers for binary classification
- Largely replaced by ReLU in hidden layers due to vanishing gradient issues
- Still useful when probabilistic interpretation is needed

The sigmoid function was dominant in early neural networks but has been largely superseded by ReLU and its variants for hidden layers in deep networks, though it remains important for binary classification outputs.