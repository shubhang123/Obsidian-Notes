# ReLU and Leaky ReLU Activation Functions

## ReLU (Rectified Linear Unit) Overview

### Definition

The Rectified Linear Unit (ReLU) is a widely used activation function in artificial neural networks (ANNs) that introduces non-linearity by outputting the input if it is positive; otherwise, it outputs zero. It is favored for its simplicity and effectiveness in deep learning.

### Formula

$$f(z) = \max(0, z)$$

Where:

- $z$: Input to the neuron (weighted sum plus bias, i.e., $z = Wx + b$)
- $f(z)$: Output, where $f(z) = z$ if $z > 0$, else $f(z) = 0$

### Properties

- **Non-Linear**: Piecewise linear but non-linear due to the threshold at zero, enabling complex pattern modeling
- **Sparse Activation**: Only positive inputs activate neurons, leading to sparse networks
- **Non-Differentiable at $z = 0$**: Subgradients (typically 0) are used for optimization at $z = 0$

### Role in ANNs

- **Purpose**: Applied after the linear transformation ($z = Wx + b$) to introduce non-linearity, allowing ANNs to learn complex, non-linear relationships
- **Use Case**: Commonly used in hidden layers of deep neural networks (e.g., CNNs for image recognition, fully connected networks for regression)

### Example

- For $z = 3$, $f(z) = \max(0, 3) = 3$
- For $z = -2$, $f(z) = \max(0, -2) = 0$
- **Scenario**: In a CNN for image classification, ReLU activates neurons for positive feature responses (e.g., edges), suppressing negative responses

## Advantages of ReLU

### Avoids Vanishing Gradients

For $z > 0$, the gradient is 1, ensuring strong gradients during backpropagation, speeding up training compared to sigmoid ($f(z) = \frac{1}{1 + e^{-z}}$) or tanh ($f(z) = \frac{e^z - e^{-z}}{e^z + e^{-z}}$).

### Computational Efficiency

Simple thresholding ($\max(0, z)$) is faster than exponential functions in sigmoid or tanh.

### Sparse Activation

Zero outputs for negative inputs deactivate neurons, reducing computation and mitigating overfitting.

### Improved Convergence

Enables faster convergence in deep networks, making it suitable for complex tasks like computer vision.

### Widely Effective

Empirically successful across tasks like image recognition and NLP.

## Limitations of ReLU

### Dying ReLU Problem

Neurons with negative inputs ($z \leq 0$) output zero, and if a neuron consistently receives negative inputs (e.g., due to large negative weights or biases), it may become "dead," never activating. This halts gradient updates, reducing network capacity.

- **Cause**: Large negative gradients during backpropagation can push $z$ into the negative region permanently.

### Non-Differentiable at $z = 0$

The function is not differentiable at $z = 0$, complicating gradient-based optimization. Subgradients are used, but this can lead to instability.

### Unbounded Output

Positive inputs produce unbounded outputs, risking numerical instability or exploding gradients without regularization.

### Non-Zero-Centered

Outputs only non-negative values, which may slow convergence compared to zero-centered functions like tanh.

### Sensitivity to Learning Rate

High learning rates can exacerbate the dying ReLU problem by causing large weight updates.

## Leaky ReLU Overview

### Definition

Leaky ReLU is a variant of ReLU designed to address the dying ReLU problem by allowing a small, non-zero gradient for negative inputs. Instead of outputting zero for negative inputs, it outputs a scaled version of the input.

### Formula

$$f(z) = \begin{cases} z & \text{if } z > 0 \ \alpha z & \text{if } z \leq 0 \end{cases}$$

Where:

- $\alpha$: A small positive constant (e.g., 0.01), controlling the slope for negative inputs
- **Alternative form**: $f(z) = \max(\alpha z, z)$

### Properties

- **Non-Linear**: Maintains non-linearity with a small slope for negative inputs
- **Reduced Sparsity**: Unlike ReLU, negative inputs produce non-zero outputs, activating more neurons
- **Differentiable (Almost)**: Continuous gradient except at $z = 0$, where subgradients are used

## How Leaky ReLU Fixes ReLU Limitations

### Addresses Dying ReLU Problem

- **Problem in ReLU**: If $z \leq 0$, the output is 0, and the gradient is 0, preventing weight updates for that neuron. If this persists, the neuron becomes "dead."
- **Leaky ReLU Fix**: For $z \leq 0$, the output is $\alpha z$, and the gradient is $\alpha$, allowing small updates to weights and biases. This keeps neurons active, even for negative inputs.
- **Example**: For $z = -2$, ReLU gives $f(z) = 0$ (gradient 0), while Leaky ReLU with $\alpha = 0.01$ gives $f(z) = 0.01 \cdot (-2) = -0.02$ (gradient 0.01), enabling learning.

### Improves Training Stability

By allowing gradients for negative inputs, Leaky ReLU ensures more neurons contribute to learning, reducing the risk of network capacity loss.

### Maintains Simplicity

Like ReLU, Leaky ReLU is computationally efficient, requiring only a conditional check and multiplication for negative inputs.

## Example

- For $z = 3$, $f(z) = 3$ (same as ReLU)
- For $z = -2$, with $\alpha = 0.01$, $f(z) = 0.01 \cdot (-2) = -0.02$
- **Scenario**: In a deep network, Leaky ReLU ensures neurons with negative inputs (e.g., from low-intensity image pixels) remain active, improving feature learning compared to ReLU.

## Advantages of Leaky ReLU

### Mitigates Dying ReLU Problem

Non-zero gradients for negative inputs prevent neurons from becoming inactive, enhancing network robustness.

### Preserves ReLU Benefits

Retains computational efficiency and avoids vanishing gradients for positive inputs ($z > 0$, gradient = 1).

### Improves Learning

Allows more neurons to contribute to gradient updates, potentially improving convergence in deep networks.

### Simple Implementation

Easy to implement with a small modification to ReLU, requiring only a fixed $\alpha$.

## Limitations of Leaky ReLU

### Choice of $\alpha$

The slope $\alpha$ (e.g., 0.01) is a hyperparameter that requires tuning. A poor choice (too large or small) can affect performance. Fixed $\alpha$ may not be optimal for all neurons or layers.

### Non-Differentiable at $z = 0$

Like ReLU, it is not differentiable at $z = 0$, though subgradients mitigate this issue.

### Reduced Sparsity

Non-zero outputs for negative inputs reduce sparsity compared to ReLU, potentially increasing computational cost and overfitting risk.

### Limited Empirical Superiority

While Leaky ReLU addresses the dying ReLU problem, it does not always outperform ReLU or other variants (e.g., Parametric ReLU, ELU) in practice, requiring experimentation.

### Unbounded Output

Like ReLU, positive outputs are unbounded, risking numerical instability without regularization.

## Comparison with ReLU

- **Dying Neurons**: ReLU risks dead neurons; Leaky ReLU avoids this with non-zero negative gradients
- **Sparsity**: ReLU is sparser (more zeros); Leaky ReLU activates more neurons, which may increase computation
- **Performance**: ReLU is often sufficient for many tasks, but Leaky ReLU is preferred when dying neurons are observed or in deeper networks
- **Example**: In a CNN for image classification, ReLU may deactivate neurons for low-intensity pixels, while Leaky ReLU keeps them active with small negative outputs, potentially improving feature detection

## Practical Considerations

### When to Use ReLU

Default choice for hidden layers due to simplicity and effectiveness in most deep learning tasks (e.g., image recognition, NLP).

### When to Use Leaky ReLU

Preferred in deep networks where dying neurons are observed (e.g., during training, many neurons output 0) or when training stability is a concern.

### Implementation Tips

- **Initialization**: Use He initialization for weights to reduce the likelihood of negative $z$ values causing dying neurons
- **Tuning $\alpha$**: Common values are 0.01 or 0.1; experiment or use Parametric ReLU (where $\alpha$ is learned)
- **Regularization**: Combine with dropout or weight decay to manage overfitting and numerical stability

## Summary

The ReLU activation function ($f(z) = \max(0, z)$) is a cornerstone of deep learning due to its efficiency, avoidance of vanishing gradients, and sparse activation. However, its dying ReLU problem and non-differentiability at $z = 0$ can hinder training.

Leaky ReLU ($f(z) = \max(\alpha z, z)$) addresses the dying ReLU problem by allowing small gradients for negative inputs, improving training stability while retaining ReLU's benefits. Both are widely used in hidden layers, with Leaky ReLU being a robust alternative when ReLU's limitations impact performance.