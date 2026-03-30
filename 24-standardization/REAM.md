# Feature Scaling in Machine Learning

Feature scaling is a critical pre-processing step in machine learning, designed to bring numerical features of a dataset onto a similar, manageable scale. This ensures that no single feature dominates the model's learning due to having a larger range of values. It is especially important for distance-based algorithms and optimization techniques like gradient descent.

## Standardization (Z-score Normalization)

Standardization, also known as Z-score normalization, transforms numerical features so that:
- Mean = 0
- Standard Deviation = 1

The formula used is:

z = (x - mean) / standard_deviation

This process centers the data around the origin and rescales it based on its variance.

## Key Takeaways & Intuition

### Geometric Intuition
- Involves mean centering (shifting data around zero)
- Scales data using standard deviation for uniform spread

### Impact of Outliers
- Standardization does **not reduce the effect of outliers**
- Extreme values still influence mean and standard deviation
- Outliers appear as high Z-scores

### When to Use Standardization
Recommended for:
- K-Nearest Neighbors (KNN)
- Principal Component Analysis (PCA)
- Gradient Descent-based algorithms:
  - Linear Regression
  - Logistic Regression
  - Neural Networks

### When to Skip Standardization
Not required for:
- Decision Trees
- Random Forests
- XGBoost

These algorithms are generally invariant to feature scaling.

## Practical Implementation

Standardization can be implemented using the `StandardScaler` class from the Scikit-learn library.

## Impact on Model Performance

Applying standardization can significantly improve model performance for scale-sensitive algorithms by ensuring balanced feature contributions.