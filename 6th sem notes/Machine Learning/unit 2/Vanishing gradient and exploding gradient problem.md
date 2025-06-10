Neural networks, especially deep ones, can encounter challenges during training related to the magnitude of gradients, known as the **vanishing gradient problem** and the **exploding gradient problem**. These issues primarily stem from the iterative process of updating network weights during backpropagation.
![[Pasted image 20250610123152.png]]
### Vanishing Gradient Problem

The vanishing gradient problem occurs when the gradients computed during backpropagation become extremely small as they are propagated backward through many layers.

- **Cause and Effect**:
    
    - This issue is particularly prominent in **Recurrent Neural Networks (RNNs)** when dealing with long sequences, limiting their ability to learn long-term dependencies and effectively giving them a "limited short-term memory".
    - It arises because the same values (from the chain rule of calculus) are multiplied repeatedly over many layers or time steps, causing the product to approach zero.
    - Certain **activation functions** are highly susceptible to this problem. For instance, the **Sigmoid activation function** is known for its "vanishing gradient problem". Its output is between 0 and 1, and at the extreme ends of its curve (where the output values saturate), the derivative (slope or gradient) approaches zero. This "kills gradients" and leads to "slow convergence" during optimization.
    - The **Tanh activation function**, while generally preferred over Sigmoid because its output is zero-centered (-1 to 1) making optimization easier, can still be prone to vanishing gradient problems.
- **Impact**:
    
    - When gradients vanish, the weight updates become negligible, meaning the network's parameters (weights and biases) barely change. This prevents deeper layers or earlier time steps from learning effectively, slowing down or entirely stopping the training process.
    - In very deep networks, the "initialization of the network" can contribute to performance degradation due to this problem.
- **Solutions/Mitigations**:
    
    - **ReLU (Rectified Linear Unit) and its variants**: The ReLU activation function is a popular solution because it "solves the vanishing gradient problem". Its formula is simply max(0,z), providing benefits similar to Sigmoid but with better performance and computational efficiency.
        - **Leaky ReLU**: This is an extension to ReLU that addresses the "dying ReLU problem" (where neurons become inactive for negative inputs). Leaky ReLU allows a small, non-zero constant gradient (e.g., 0.01) for negative inputs, unlike ReLU.
        - **Parametric ReLU (PReLU)**: PReLU gives neurons the ability to choose the best slope in the negative region, allowing them to become ReLU or Leaky ReLU with specific alpha values.
        - **Maxout**: A generalization of ReLU and Leaky ReLU that does not have drawbacks like dying ReLU, though it doubles the number of parameters.
        - **ELU (Exponential Linear Unit)**: Converges faster and produces more accurate results, similar to ReLU but with a smooth negative part that approaches -α.
    - **Long Short-Term Memory (LSTM) and Gated Recurrent Units (GRUs)**: These are special types of RNN layers designed to "tackle the limited short-term memory problem and solve the vanishing gradient problem" in RNNs.
        - LSTMs achieve this by introducing an "additional hidden vector which is referred to as cell state" (a long-term memory) and "gates" (input, output, and forget gates) that "control the data written into this long-term memory". The "forget gate" and the "additive property of cell gradients" ensure that gradients do not become zero.
        - GRUs are similar, using hidden states and two gates (reset and update) to manage information flow.
    - **ResNet (Residual Networks) and Skip Connections**: ResNet models alleviate the problem of training very deep networks. They use "skip connections" (or residual connections) that provide an "alternate shortcut path for the gradient to flow through," directly addressing the vanishing gradient issue. These connections also allow the model to learn "identity functions," ensuring that adding more layers does not degrade performance.
    - **Batch Normalization**: This technique normalizes the activations of intermediate layers during training, which "reduces internal covariate shift" and leads to "faster convergence," thereby allowing the use of "higher learning rates". It is typically placed after a convolutional or fully connected layer and before the activation function.
    - **Smaller Learning Rates**: Using a "smaller learning rate" can help to alleviate the unstable gradients problem. The learning rate (often denoted as eta or alpha) controls how much the weights are updated with each step.
    - **Gradient Clipping**: This technique can be used to alleviate unstable gradients.
    - **Layer Normalization and Dropout**: These methods can also be applied at each time step to alleviate unstable gradients.

### Exploding Gradient Problem

The exploding gradient problem is the opposite of the vanishing gradient problem, where gradients grow extremely large during backpropagation.

- **Cause and Effect**:
    
    - Similar to vanishing gradients, this problem also arises in **RNNs** when the "weight matrix is multiplied successively at various time-steps" or when the same terms are repeatedly multiplied by the chain rule of calculus, causing the result to "get very large quickly". This leads to "unstable gradients".
    - This rapid increase in gradient values can lead to **very large weight updates**, causing the model's training to become unstable and potentially result in numerical overflow or divergence (the model's parameters become too large to handle).
- **Solutions/Mitigations**:
    
    - **Gradient Clipping**: This is a common solution for exploding gradients. It involves setting a threshold for the gradient values, and if a gradient exceeds this threshold, it is scaled down to a manageable size.
    - **Smaller Learning Rates**: Reducing the "learning rate" can help prevent gradients from exploding, as it controls the step size of weight updates.
    - **Weight Regularization**: Techniques like L1 or L2 regularization can penalize large weights, indirectly helping to control exploding gradients. (This is information outside the provided sources but generally applicable to the problem).
    - **Batch Normalization**: By normalising inputs to layers, batch normalization helps to stabilise gradient flow and allows for higher learning rates, which can indirectly help prevent exploding gradients.

In summary, both vanishing and exploding gradients are challenges in training deep neural networks, especially RNNs, arising from the multiplicative nature of gradient propagation. Various architectural and optimization techniques, including the choice of activation functions, specific recurrent unit designs (LSTMs, GRUs), skip connections (ResNets), and normalization techniques, are employed to mitigate these issues and enable effective training.