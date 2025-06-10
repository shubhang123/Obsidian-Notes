# Dropout in Machine Learning

## What is Dropout?

Dropout is a regularization technique that randomly sets a fraction of neurons to zero during training to prevent overfitting.

## How it Works

- **Training**: Randomly "drop" neurons with probability p (typically 0.5)
- **Inference**: Use all neurons but scale outputs by (1-p)

## Mathematical Formula

```
Training: y = (r * x) / (1-p)  where r ~ Bernoulli(1-p)
Inference: y = x * (1-p)
```

## Key Benefits

- **Prevents overfitting** by breaking co-adaptation between neurons
- **Improves generalization** through ensemble effect
- **Simple to implement** and computationally efficient
- **Forces robust learning** by making neurons work independently

## Common Dropout Rates

- **Hidden layers**: 0.5 (most common)
- **Input layers**: 0.1-0.2 (if used)
- **Convolutional layers**: 0.2-0.3

## Types

- **Standard Dropout**: For fully connected layers
- **Spatial Dropout**: For convolutional layers (drops entire feature maps)
- **Variational Dropout**: For RNNs (same mask across time steps)

## Best Practices

- Use inverted dropout (scale during training, not inference)
- Start with 0.5 for hidden layers
- Don't apply to output layers
- Combine with other regularization techniques
- Monitor training vs validation performance

## When to Use

- Large networks prone to overfitting
- Limited training data
- Fully connected layers
- When batch normalization isn't sufficient

Dropout is one of the most effective and widely-used regularization techniques in deep learning.