In the context of neural networks and machine learning, **parameters** and **hyperparameters** play distinct but crucial roles in the learning process.

### Parameters

**Parameters** are the internal variables of a model that are learned or optimised during the training process. These values define the specific mapping from input to output that the model learns from the data.

- **What they are:**
    - The primary examples of parameters in neural networks are **weights** and **biases**.
    - **Weights** (e.g., `W1,1`, `W1,2`, `W` in general notation) represent the strength of connections between neurons. They determine how much influence one neuron has on another.
    - **Biases** are additional learnable values associated with each neuron that adjust the output of the activation function.
    - In the context of linear regression, parameters are often referred to as coefficients (e.g., `θ1` and `θ2`, or `m` and `c`).
    - In Recurrent Neural Networks (RNNs), `A`, `B`, and `C` are mentioned as network parameters.
- **How they are learned:**
    - The **goal of backpropagation is to optimise these weights** (and biases) so that the neural network can correctly map arbitrary inputs to outputs.
    - This optimisation involves calculating the **total error** between the network's predictions and the actual target outputs.
    - The error is then propagated **backward** through the network to determine how much each weight contributed to the error.
    - Using concepts from calculus, such as **partial derivatives** and the **chain rule**, the changes needed for each weight are calculated.
    - Weights are iteratively updated in a direction that **minimises the cost function** (e.g., Mean Squared Error (MSE)), which quantifies how wrong the predictions are relative to the target outcome. This iterative update process is an application of **gradient descent**.

### Hyperparameters

**Hyperparameters** are external configuration settings for a model or algorithm that are **set _before_ the training process begins** and are not learned from the data itself. They control the learning process and influence the model's performance.

- **Examples of Hyperparameters:**
    
    - **Learning Rate (eta/alpha/epsilon):** This determines the step size taken during each iteration of weight updates in gradient descent. A smaller learning rate (e.g., 0.0001) can lead to higher accuracy but slower convergence. It's crucial for alleviating unstable gradients in RNNs.
    - **Epsilon (ε) in Q-Learning:** This parameter balances the **exploration** (taking random actions to discover new states) and **exploitation** (selecting actions based on current known maximum Q-values) strategies of an agent. Initially, epsilon rates are higher for exploration and decrease as the agent becomes more confident in its Q-value estimates.
    - **Beam Width (k) in Beam Search:** In sequence generation tasks (like machine translation), beam search uses a beam width (`k`) to control how many of the most likely partial sequences are expanded and retained at each step. A wider beam width can improve translation quality but increases computational cost and memory usage.
    - Other examples mentioned or implied in the sources (though not explicitly called hyperparameters) include:
        - The choice of **activation function** (e.g., Sigmoid, Tanh, ReLU, Softmax).
        - **Kernel size** and **stride** in convolutional and pooling layers.
        - **Padding** strategy (valid or same).
        - The **number of layers** and **neurons** in a network.
- **Distinction from Parameters:** Unlike parameters, which are internal to the model and learned from the data, hyperparameters are set by the human developer or determined through separate processes like hyperparameter tuning. They guide _how_ the learning takes place, rather than being what is learned.

In the context of machine learning and neural networks, **hyperparameters** are external configuration settings that are **set _before_ the training process begins** and are not learned from the data itself [Source 0]. They control the learning process and significantly influence the model's performance [Source 0].

While the provided sources do not explicitly use the term "hyperparameter tuning" to describe an automated search process (like grid search or random search), they do discuss the **selection and impact of various hyperparameters**, which is the core idea behind tuning. The sources explain how the choice of these settings can affect a model's behaviour, performance, and efficiency.

Here are examples of hyperparameters mentioned in the sources and insights into their selection:

- **Learning Rate (eta/alpha/epsilon/L)**:
    
    - This hyperparameter determines the **step size taken during each iteration of weight updates** in gradient descent [Source 0, 57, 203].
    - A **smaller learning rate** (e.g., 0.0001) can lead to **higher accuracy** but may result in **slower convergence** [Source 0, 203].
    - It is crucial for alleviating **unstable gradients** (exploding or vanishing gradients) in Recurrent Neural Networks (RNNs) [Source 0, 244].
- **Epsilon (ε) in Q-Learning**:
    
    - This hyperparameter balances the **exploration** (taking random actions to discover new states) and **exploitation** (selecting actions based on current known maximum Q-values) strategies of an agent [Source 0, 37].
    - Initially, **epsilon rates are higher for exploration** and decrease as the agent becomes more confident in its Q-value estimates [Source 0, 42].
- **Beam Width (k) in Beam Search**:
    
    - In sequence generation tasks (such as machine translation), beam search uses a beam width (`k`) to control **how many of the most likely partial sequences are expanded and retained at each step** [Source 0, 278].
    - A **wider beam width** can **improve translation quality** by exploring more candidate sequences, but it **increases computational cost and memory usage linearly with `k`** [Source 0, 279].
    - A narrow beam width is fast and uses less memory but may result in suboptimal translations, while a wide beam width provides better translations but is slower and requires more memory [Source 279].
- **Activation Functions**:
    
    - These functions introduce **non-linearity** into the network, enabling it to learn complex patterns [Source 0, 4, 8, 60, 88].
    - The **choice of activation function depends on the problem type and the expected output range** [Source 18].
    - For example, **ReLU** is recommended for **hidden layers** as a general rule of thumb, or its variant, **Leaky ReLU**, which addresses the "dying ReLU" problem [Source 19, 20, 27].
    - **Sigmoid** or **Tanh** are suitable for output values in the range (0,1) or (-1,1) respectively, but not for values larger than 1 [Source 13, 14, 18].
    - **Softmax** is used in the last layer for **classification tasks** to predict a probability distribution over mutually exclusive class labels [Source 18, 19, 20].
    - **Hyperbolic Tangent (Tanh)** is mentioned as a saturating activation function that can help alleviate unstable gradients in RNNs [Source 244].
    - **Parametric ReLU (PReLU)** allows neurons to choose the best slope in the negative region, potentially becoming ReLU or Leaky ReLU with certain alpha values [Source 15].
- **Network Architecture (e.g., Number of Layers, Neurons)**:
    
    - The **number of layers and neurons** in a network are hyperparameters influencing its complexity [Source 0].
    - Neural networks with more hidden layers are generally **better at learning complex patterns** [Source 22].
    - Historically, improving the performance of deep neural networks often involved **increasing their size** (i.e., depth) [Source 171].
- **Kernel Size / Filter Size (F) in CNNs**:
    
    - In Convolutional Neural Networks (CNNs), the kernel size defines the **field of view of the convolution** [Source 163] and is part of the output size calculation [Source 69, 95, 101]. LeNet, for example, used 5x5 filters [Source 167, 168].
- **Stride (S) in CNNs**:
    
    - Stride defines the **step size with which the convolution filter moves across the input** [Source 66, 68, 92, 94, 101, 160].
    - A stride greater than 1 (e.g., stride of 2) can be used for **downsampling** the image, reducing its spatial dimensions [Source 66, 94, 101, 163, 82, 98, 110, 111].
- **Padding (P) in CNNs**:
    
    - Padding involves adding "dummy" pixels (usually zeros) around the border of the input image or feature map [Source 66, 92, 160].
    - It helps **control the spatial size of the output feature maps** ("valid" padding results in shrinking, "same" padding maintains size) [Source 66, 67, 92, 93, 161].
    - Padding is important for building deeper networks without excessive shrinking of feature map dimensions and for retaining information at image borders [Source 161].
- **Dropout**:
    
    - Mentioned as a novel technique implemented in AlexNet [Source 170] and as a method to alleviate unstable gradients in RNNs [Source 244]. (Outside sources clarify that dropout is a regularization hyperparameter, typically expressed as a rate, that helps prevent overfitting by randomly deactivating neurons during training.)
- **Batch Normalization Placement**:
    
    - This technique normalizes layer outputs to stabilize training. Its placement is typically **after a convolutional (or fully connected) layer and before the activation function** [Source 84, 99, 113].
- **Optimizer and Loss Function**:
    
    - The choice of **optimizer** (e.g., 'adam' in the Keras example) and **loss function** (e.g., 'categorical_crossentropy' for classification, Mean Squared Error for regression) are also hyperparameters set during model compilation [Source 72, 73, 83, 98, 104, 105, 111]. The loss function quantifies the error between predictions and ground truth, and the goal of training is to minimize this loss [Source 72, 104].

In summary, while the sources do not explicitly detail automated "hyperparameter tuning" methodologies, they provide crucial information on the **nature and impact of hyperparameters**, guiding their intelligent selection based on problem characteristics, desired model performance, and computational constraints.