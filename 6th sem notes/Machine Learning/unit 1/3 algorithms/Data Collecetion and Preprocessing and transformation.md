steps involved in data preparation for ML is 
data collection -> data preprocessing -> data transformation

## Steps in Data Collection

1. **Data Collection**
    
    - **Definition**: The process of gathering data from various sources, such as databases, APIs, files (e.g., CSV, JSON), web scraping, sensors, or surveys, relevant to the problem being solved.
    - **Purpose**: To compile a comprehensive dataset that represents the problem domain and contains sufficient information for the model to learn patterns.
    - **Details**:
        - Sources may include structured data (e.g., SQL databases), semi-structured data (e.g., JSON, XML), or unstructured data (e.g., text, images).
        - Challenges include missing values, inconsistent formats (e.g., date formats like "MM/DD/YYYY" vs. "DD-MM-YY"), duplicate entries, or irrelevant data.
        - Techniques involve querying databases, extracting data via APIs, or collecting real-time data from IoT devices.
        - Quality checks are performed to identify outliers, errors, or biases in the collected data.
    - **Example**: Collecting sales data from a company’s transaction database, customer reviews from a website, or sensor readings from IoT devices.
2. **Data Augmentation**
    
    - **Definition**: The process of enhancing the dataset by generating additional data or modifying existing data to improve model robustness and generalization.
    - **Purpose**: To increase the size and diversity of the dataset, especially when the original data is limited, to prevent overfitting and improve model performance.
    - **Details**:
        - Common in domains like computer vision and natural language processing.
        - Techniques for images include rotation, flipping, cropping, scaling, or adjusting brightness/contrast. For text, methods include synonym replacement or back-translation.
        - Synthetic data generation may use algorithms like SMOTE (Synthetic Minority Oversampling Technique) for imbalanced datasets or generative models (e.g., GANs).
        - Ensures the model is exposed to varied scenarios, improving its ability to handle real-world data.
    - **Example**: For an image classification task, augmenting a dataset of cat images by rotating, flipping, or adding noise to create variations, thus increasing the dataset size.
3. **Data Labeling**
    
    - **Definition**: The process of assigning meaningful labels or categories to data points, typically for supervised learning tasks, to enable the model to learn relationships between inputs and outputs.
    - **Purpose**: To provide ground truth labels that guide the model in learning patterns and making accurate predictions.
    - **Details**:
        - Labels can be binary (e.g., "spam" vs. "not spam"), multi-class (e.g., "cat," "dog," "bird"), or continuous (e.g., house prices).
        - Can be performed manually by domain experts or through automated tools (e.g., pre-trained models or rule-based systems).
        - Accuracy is critical, as incorrect labels can mislead the model and degrade performance.
        - Challenges include time and cost for manual labeling, label inconsistency, or ambiguity in complex tasks (e.g., sentiment analysis).
        - Crowdsourcing platforms or active learning can be used to streamline the process.
    - **Example**: Labeling a dataset of emails as "positive," "negative," or "neutral" for sentiment analysis, or annotating medical images with diagnoses like "benign" or "malignant."


# Data Preprocessing Overview

Data preprocessing is a critical step in preparing raw data for machine learning models. The quality of input data significantly impacts a model’s ability to learn effectively, making preprocessing essential for transforming raw, often inconsistent, incomplete, or noisy data into a clean, structured dataset. This process ensures the data is formatted and cleaned to meet the requirements of machine learning algorithms, improving model performance and reliability.

## Steps in Data Preprocessing

### 1. Formatting

- **Definition**: The process of standardizing the structure and format of raw data to ensure consistency and compatibility with machine learning algorithms.
- **Purpose**: To convert data from diverse sources into a uniform format suitable for analysis, addressing issues like inconsistent data types, date formats, or encoding.
- **Details**:
    - Involves handling variations in data representation, such as converting date formats (e.g., “MM/DD/YYYY” to “YYYY-MM-DD”), standardizing text (e.g., lowercase conversion), or encoding categorical variables (e.g., one-hot encoding or label encoding).
    - Ensures numerical data is in appropriate formats (e.g., converting strings like “$1,000” to numeric 1000).
    - Addresses file format issues, such as converting JSON, XML, or text files into tabular formats like CSV.
    - Tools like Pandas in Python or data transformation pipelines are commonly used.
- **Example**: Converting a dataset with mixed date formats (e.g., “01-15-2023” and “15/01/23”) into a consistent “YYYY-MM-DD” format, or encoding categorical variables like “red,” “blue,” “green” into numerical values.

### 2. Data Cleaning

- **Definition**: The process of identifying and correcting errors, inconsistencies, and inaccuracies in the dataset, such as missing values, duplicates, outliers, or noisy data.
- **Purpose**: To improve data quality by ensuring the dataset is accurate, complete, and reliable, which enhances model performance.
- **Details**:
    - Involves handling missing data, removing or correcting duplicates, identifying and addressing outliers, and smoothing noisy data.
    - Requires careful consideration to avoid introducing bias or losing valuable information.
    - Common tools include Python libraries (e.g., Pandas, NumPy) or statistical software for data manipulation.

#### 2.1 Ways to Handle Missing Data During Cleaning

Missing data can occur due to errors in data collection, sensor failures, or incomplete records. Handling missing values appropriately is crucial to prevent biased or inaccurate models. Common methods include:

1. **Using Attribute Mean to Fill in the Missing Value**
    
    - **Description**: Replace missing values with the mean (average) of the attribute (column) for numerical data.
    - **Process**: Calculate the mean of non-missing values in the attribute and impute this value for missing entries.
    - **Advantages**:
        - Simple and preserves the dataset’s size.
        - Maintains the overall distribution’s central tendency.
    - **Disadvantages**:
        - Can distort variance and correlations if missing data is not random.
        - Not suitable for categorical data.
    - **Example**: In a dataset of heights, if some entries are missing, replace them with the mean height (e.g., 170 cm).
2. **Predict the Missing Value Using Learning Algorithms (e.g., Decision Tree)**
    
    - **Description**: Use a machine learning algorithm, such as a decision tree, k-nearest neighbors (k-NN), or regression, to predict missing values based on other attributes.
    - **Process**: Treat the attribute with missing values as the target variable and use other features to train a model to predict the missing entries.
    - **Advantages**:
        - Can capture complex relationships between attributes.
        - More accurate than mean imputation for non-random missing data.
    - **Disadvantages**:
        - Computationally expensive for large datasets.
        - Risk of overfitting if the prediction model is too complex.
    - **Example**: Predicting missing house prices using a decision tree trained on features like location, size, and number of bedrooms.
3. **Using a Global Constant (e.g., “NA” or 0)**
    
    - **Description**: Replace missing values with a predefined constant, such as “NA” for categorical data or 0 for numerical data.
    - **Process**: Assign a constant value to all missing entries, ensuring the model recognizes it as a distinct category or placeholder.
    - **Advantages**:
        - Simple and quick to implement.
        - Preserves the dataset’s structure.
    - **Disadvantages**:
        - Can introduce bias if the constant is misinterpreted by the model (e.g., 0 may imply a valid value).
        - Not suitable for algorithms sensitive to specific values.
    - **Example**: In a survey dataset, replacing missing responses with “NA” for a question about preferences.
4. **Ignore the Tuple**
    
    - **Description**: Remove rows (tuples) with missing values from the dataset.
    - **Process**: Delete any record containing one or more missing values, reducing the dataset size.
    - **Advantages**:
        - Simple and ensures only complete data is used.
        - Effective if missing data is minimal and random.
    - **Disadvantages**:
        - Can lead to significant data loss if many records have missing values.
        - May introduce bias if missing data is not random (e.g., certain groups are more likely to have missing values).
    - **Example**: In a dataset of customer purchases, removing rows where customer age is missing, if only a small percentage of records are affected.

#### 2.2 Techniques to Identify Outliers and Smooth Out Noisy Data

Outliers are data points that deviate significantly from the rest of the dataset, while noisy data includes random errors or variations. Identifying and handling these issues improves data quality. Common techniques include:

1. **Binning (Bin Mean, Bin Median, Bin Boundary)**
    
    - **Description**: Divide the data into bins (intervals) and smooth values within each bin to reduce noise or handle outliers.
    - **Process**:
        - **Bin Mean**: Replace all values in a bin with the mean of the bin’s values.
        - **Bin Median**: Replace all values in a bin with the median of the bin’s values.
        - **Bin Boundary**: Replace values with the nearest boundary (minimum or maximum) of the bin.
        - Data is first sorted, then partitioned into equal-frequency or equal-width bins.
    - **Advantages**:
        - Simple and effective for smoothing noisy data.
        - Reduces the impact of outliers by averaging or aligning values.
    - **Disadvantages**:
        - May lose fine-grained information due to averaging.
        - Bin size selection can affect results.
    - **Example**: For a dataset of ages, divide into bins (e.g., 0-20, 21-40, 41-60), and replace values in each bin with the mean (e.g., all ages in 21-40 become 30).
2. **Clustering**
    
    - **Description**: Group similar data points into clusters and identify outliers as points that do not belong to any cluster or form small clusters.
    - **Process**: Apply clustering algorithms like k-means or DBSCAN to group data, then flag points far from cluster centroids or in sparse regions as outliers. Noisy data can be smoothed by assigning values closer to cluster centers.
    - **Advantages**:
        - Captures natural patterns in the data.
        - Effective for detecting outliers in complex, multidimensional datasets.
    - **Disadvantages**:
        - Computationally intensive for large datasets.
        - Requires choosing the number of clusters or distance thresholds.
    - **Example**: In a dataset of customer purchases, clustering customers by spending behavior and identifying those with unusual patterns (e.g., extremely high or low spending) as outliers.
3. **Regression**
    
    - **Description**: Fit a regression model to the data to identify outliers as points with large residuals and smooth noisy data by predicting expected values.
    - **Process**: Train a regression model (e.g., linear or polynomial) to capture the relationship between variables. Outliers are points with high residuals (differences between predicted and actual values). Noisy data can be replaced with predicted values.
    - **Advantages**:
        - Leverages relationships between variables to detect anomalies.
        - Can smooth data while preserving trends.
    - **Disadvantages**:
        - Assumes a specific relationship (e.g., linear) that may not always apply.
        - Sensitive to the choice of regression model.
    - **Example**: In a dataset of house prices vs. size, fitting a linear regression model and flagging houses with prices far from the predicted line as outliers, or replacing noisy price values with predicted ones.


data transformation
last stae in preparing data for ML tasks

data can be transformed through normalization / scaling, decomposition or aggregration

1) normalization with examples
		1. min max normalizton 
		2. z score normalization ( zero mean normalization )
		3. decimal scaling