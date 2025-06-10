A **1x1 convolution** is a convolutional operation where the filter has a spatial dimension of 1x1. Although its spatial dimension is small, the depth (number of channels in the filter) can match the number of channels in the input feature map. It operates on each spatial location independently across the different input channels.

Here are its key uses and how it functions within a CNN:

- **Dimension Reduction**:
    
    - A 1x1 convolution can **reduce the number of feature channels (depth)** without changing the spatial dimensions (height and width) of the feature map.
    - This is crucial for **reducing computational cost** and the total number of parameters in a network. For instance, it can embed 192 input channels into 32 channels.
    - In architectures like the **Inception Network**, 1x1 convolutional layers are often incorporated for dimensionality reduction _before_ larger convolutions (e.g., 3x3 and 5x5) to manage computational expense. An example illustrates how using a 1x1 convolution can drastically reduce the number of operations compared to performing a 5x5 convolution directly.
- **Adding Non-linearity**:
    
    - When a 1x1 convolution is combined with an **activation function**, it can introduce non-linearity in the channel dimension of the network. This ability to add non-linearity is based on concepts from the Network In Network paper.
- **Computational Efficiency**:
    
    - It effectively acts like a **fully connected layer across channels** for each pixel.
    - By reducing the number of channels, 1x1 convolutions make subsequent convolutional operations less computationally expensive. This is a key reason for their use in networks like Inception, which are "heavily engineered" to push performance in terms of speed and accuracy.

In summary, a 1x1 convolution is a versatile tool in CNNs that, despite its small filter size, plays a significant role in **dimension reduction and adding non-linearity across channels**, ultimately contributing to **more efficient and robust network architectures**.