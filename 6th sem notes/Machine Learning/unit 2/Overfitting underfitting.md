**Overfitting and Underfitting** are two common problems encountered when training machine learning models, particularly neural networks, relating to how well the model generalises from the training data to new, unseen data. Both issues can hinder a model's effectiveness in real-world scenarios.

### Overfitting

**Overfitting** occurs when a machine learning algorithm performs exceptionally well on its training data but fails to perform effectively on new, unseen test sets. It indicates that the model has **memorised all the training data**, including noise or specific details irrelevant to the underlying patterns, rather than learning the general relationships.

- **Characteristics**:
    - The algorithm works well on the training set.
    - It is unable to perform better on the test sets.
    - It memorises all training data but fails on new data.
    - It is also known as a problem of **high variance**.
- **Causes**:
    - Using **unnecessary explanatory variables** can lead to overfitting.
    - A "deep decision tree that memorises all training data" is an example of overfitting.
    - **Very deep networks** can be susceptible to overfitting.

### Underfitting

**Underfitting** is the opposite problem, where the machine learning algorithm performs poorly even on the training set itself. This indicates that the model is **too simple** and has not learned the fundamental patterns or details within the data.

- **Characteristics**:
    - The algorithm works so poorly that it is **unable to fit even a training set well**.
    - It is "too simple, ignoring details".
    - It is also known as a problem of **high bias**.
- **Causes**:
    - A "decision tree with only one level" is given as an example of underfitting, being too simple.

### Mitigation Techniques

Several techniques are employed to address or detect overfitting and underfitting:

- **Cross-Validation**: This is a crucial technique for assessing how well a statistical analysis generalises to an independent data set. It can **"detect over-fitting with ease"** and helps prevent a machine learning model from both overfitting and underfitting. The goal of cross-validation is to ensure the model maintains similar efficiency on new data as it does on the training set.
- **Pooling Layers (Sub-sampling)**: In Convolutional Neural Networks (CNNs), pooling layers are used to reduce the spatial dimensions of feature maps. This process helps to **"reduce computation and control overfitting"** and also **"helps reduce over fitting"** by extracting representative features from the input tensor and reducing the number of parameters.
- **Batch Normalization**: This technique normalises the activations of intermediate layers during training. While not directly stated as preventing overfitting, its benefits include **faster convergence** and allowing **higher learning rates**, which contribute to training stability and can indirectly help prevent overfitting. It also "reduces internal covariate shift".
- **Architectural Considerations**: While very deep networks can be susceptible to overfitting, it's important to note that performance degradation in very deep networks (where error is worse on both training and testing data) is distinct from overfitting; it could also be attributed to optimisation function, network initialization, and the vanishing gradient problem. Architectures like **ResNet** (Residual Networks) alleviate these deep network training problems, including issues that might be mistaken for or exacerbate overfitting.