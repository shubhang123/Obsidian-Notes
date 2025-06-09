# 2. Regression

Regression involves predicting continuous numerical values based on input features. The goal is to model the relationship between features and a continuous target variable, often by fitting a function that minimizes prediction errors. Regression is used in scenarios where the output is a real number, such as predicting prices or quantities.

### Subtypes of Regression

- **Simple Linear Regression**:
    - Models a linear relationship between a single feature and the target variable.
    - Equation: y = w₀ + w₁x, where w₀ is the intercept and w₁ is the slope.
    - Example: Predicting house prices based solely on square footage.
- **Multiple Linear Regression**:
    - Extends simple linear regression to multiple features.
    - Equation: y = w₀ + w₁x₁ + w₂x₂ + ... + wₙxₙ.
    - Example: Predicting house prices using features like size, location, and number of bedrooms.
- **Non-Linear Regression**:
    - Models complex, non-linear relationships between features and the target.
    - Examples: Polynomial regression, where the relationship is modeled as a polynomial function, or regression with neural networks.
    - Example: Predicting energy consumption, which may follow a non-linear pattern based on time and weather.

### Common Algorithms for Regression

- **Linear Regression**:
    - Assumes a linear relationship between features and the target.
    - Minimizes Mean Squared Error (MSE) to find the best-fitting line.
    - Strengths: Simple, interpretable, and computationally efficient.
    - Weaknesses: Assumes linearity and independence of features; sensitive to outliers.
- **Polynomial Regression**:
    - Extends linear regression by fitting a polynomial function to capture non-linear relationships.
    - Example: y = w₀ + w₁x + w₂x² + ... + wₙxⁿ.
    - Strengths: Captures non-linear patterns.
    - Weaknesses: Prone to overfitting with high-degree polynomials; sensitive to outliers.
- **Ridge Regression (L2 Regularization)**:
    - Adds a penalty term to the loss function to prevent overfitting by shrinking large weights.
    - Equation: Loss = MSE + λ∑wᵢ², where λ controls regularization strength.
    - Strengths: Handles multicollinearity (correlated features) well.
    - Weaknesses: Still assumes linearity.
- **Lasso Regression (L1 Regularization)**:
    - Adds a penalty term that encourages sparsity, setting some feature weights to zero.
    - Equation: Loss = MSE + λ∑|wᵢ|.
    - Strengths: Performs feature selection by eliminating irrelevant features.
    - Weaknesses: May struggle with highly correlated features.
- **Gradient Boosting (e.g., XGBoost, LightGBM)**:
    - Builds an ensemble of decision trees to predict continuous values, minimizing a loss function like MSE.
    - Strengths: Highly accurate, handles non-linear relationships, and robust to outliers.
    - Weaknesses: Requires careful tuning and can be computationally intensive.
- **Neural Networks**:
    - Deep learning models, such as Multi-Layer Perceptrons (MLPs), can model complex non-linear relationships.
    - Strengths: Highly flexible, suitable for large datasets and complex patterns.
    - Weaknesses: Requires significant data and computational resources; less interpretable.

### Practical Considerations

- **Evaluation Metrics**:
    - **Mean Squared Error (MSE)**: Average of squared differences between predicted and actual values; penalizes large errors heavily.
    - **Mean Absolute Error (MAE)**: Average of absolute differences; more robust to outliers.
    - **R² Score**: Proportion of variance in the target explained by the model; ranges from 0 to 1 (higher is better).
    - **Root Mean Squared Error (RMSE)**: Square root of MSE, providing error in the same units as the target.
- **Challenges**:
    - **Outliers**: Can disproportionately affect models like linear regression; robust methods like Huber loss can help.
    - **Feature Scaling**: Most regression algorithms require normalized or standardized features to ensure fair weighting.
    - **Non-Linearity**: Linear models fail when relationships are non-linear; use polynomial regression or non-linear models like neural networks.
    - **Overfitting**: Regularization techniques (e.g., Ridge, Lasso) or simpler models prevent overfitting.
- **Applications**:
    - Predicting house prices, stock prices, weather forecasting, sales forecasting, and energy consumption prediction.