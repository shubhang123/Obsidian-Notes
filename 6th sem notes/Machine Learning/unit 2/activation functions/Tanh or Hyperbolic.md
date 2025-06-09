## Tanh (Hyperbolic Tangent) Activation Function

# **Formula:** $$f(x) = \tanh(x) = \frac{e^x - e^{-x}}{e^x + e^{-x}} = \frac{2}{1 + e^{-2x}} - 1$$

**Output Range:** -1 to 1

**Key Characteristics:**

- S-shaped curve similar to sigmoid but centered around zero
- Zero-centered output (mean output is approximately zero)
- Steeper gradient than sigmoid around zero
- Symmetric around the origin (0, 0)

## **Relationship to Sigmoid:** $$\tanh(x) = 2 \cdot sigmoid(2x) - 1$$

**When to Use:**

- Hidden layers in shallow to medium-depth networks
- When you need zero-centered outputs
- Time series and sequential data processing
- RNNs and LSTMs (historically common)

**Advantages:**

- **Zero-centered**: Unlike sigmoid, outputs can be negative, leading to more efficient gradient updates
- **Stronger gradients**: Steeper slope than sigmoid, faster convergence
- **Bounded output**: Prevents exploding activations
- **Smooth and differentiable**: Works well with gradient-based optimization

**Limitations:**

- **Vanishing Gradient Problem**: Still suffers from vanishing gradients in deep networks (though less than sigmoid)
- **Computational cost**: More expensive than ReLU due to exponential operations
- **Saturation**: Still saturates at extremes (-1 and 1)
- **Not as efficient as ReLU**: Slower training compared to modern alternatives

**Derivative:** $$f'(x) = 1 - \tanh^2(x)$$

**Comparison with Sigmoid:**

- **Better than sigmoid** because it's zero-centered
- **Similar vanishing gradient issues** but less severe
- **Preferred over sigmoid** for hidden layers when not using ReLU

**Modern Usage:**

- Less common in deep networks (replaced by ReLU variants)
- Still used in RNNs, LSTMs, and GRUs
- Occasionally used when zero-centered activation is specifically needed
- Good choice for shallow networks

Tanh is essentially a scaled and shifted sigmoid that addresses the zero-centering issue but still faces vanishing gradient problems in very deep networks.