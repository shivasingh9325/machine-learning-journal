# 📊 Mathematical Transformations in Machine Learning

Mathematical transformations are an important preprocessing step in machine learning, especially when working with numerical features that are not normally distributed. Many statistical models, such as Linear Regression and Logistic Regression, perform better when the input features are closer to a normal (Gaussian) distribution. Transforming skewed data can improve model performance, make patterns easier to learn, and reduce the impact of outliers.

## 🚀 Why Normal Distribution Matters

Some machine learning models make assumptions about the data distribution. When these assumptions are violated, the model may not perform well.

- Linear Regression often works better when features are approximately normal.
- Logistic Regression can benefit from transformed numerical features.
- Skewed data can cause poor fit, unstable coefficients, and reduced interpretability.

The main purpose of transformation is to:
- reduce skewness
- stabilize variance
- make data more symmetric
- improve model performance

## 🔍 How to Identify Data Distribution

Before applying a transformation, it is useful to inspect the distribution of a feature.

### 📈 Probability Density Function (PDF)
A PDF plot shows how values are distributed across a feature.

### 📉 QQ Plot (Quantile-Quantile Plot)
A QQ plot compares your data distribution with a normal distribution.

If the points lie close to a straight 45-degree line, the data is approximately normal.

    import scipy.stats as stats
    import matplotlib.pyplot as plt

    stats.probplot(df['Age'], dist="norm", plot=plt)
    plt.show()

## 🔄 Common Types of Transformations

Different transformations work better for different kinds of skewness.

### 🔹 Log Transformation
Best for right-skewed data.  
It compresses large values and brings them closer to the center.

    import numpy as np
    df['Fare_log'] = np.log1p(df['Fare'])

### 🔹 Reciprocal Transformation
Useful when you want very large values to become much smaller.

    df['Fare_reciprocal'] = 1 / (df['Fare'] + 1)

### 🔹 Square Transformation
Often used for left-skewed data.

    df['Age_square'] = df['Age'] ** 2

### 🔹 Square Root Transformation
Useful for moderate skewness and can reduce the effect of larger values.

    df['Age_sqrt'] = np.sqrt(df['Age'])

## 🧠 Using FunctionTransformer in scikit-learn

`FunctionTransformer` is a convenient way to apply custom mathematical transformations in scikit-learn workflows. It is especially useful when you want to keep preprocessing inside a pipeline.

    from sklearn.preprocessing import FunctionTransformer
    import numpy as np

    log_transformer = FunctionTransformer(np.log1p)
    X_train['Fare'] = log_transformer.fit_transform(X_train[['Fare']])

You can also use it inside a pipeline:

    from sklearn.pipeline import Pipeline
    from sklearn.impute import SimpleImputer
    from sklearn.linear_model import LogisticRegression
    from sklearn.compose import ColumnTransformer
    from sklearn.preprocessing import FunctionTransformer

    numeric_transformer = Pipeline(steps=[
        ('imputer', SimpleImputer(strategy='median')),
        ('log', FunctionTransformer(np.log1p))
    ])

## 📦 Practical Example: Titanic Dataset

A common example is the Titanic dataset, where features such as `Fare` are heavily right-skewed and `Age` may contain missing values.

### Before Transformation
- `Fare` has a long right tail
- `Age` may contain missing values
- Logistic Regression gives only moderate performance

### After Log Transformation
- The `Fare` distribution becomes more balanced
- The model learns patterns more effectively
- Accuracy and generalization can improve

    import numpy as np
    import matplotlib.pyplot as plt
    import seaborn as sns

    sns.histplot(df['Fare'], kde=True)
    plt.title("Fare Before Transformation")
    plt.show()

    df['Fare_log'] = np.log1p(df['Fare'])

    sns.histplot(df['Fare_log'], kde=True)
    plt.title("Fare After Log Transformation")
    plt.show()

## ⚖️ Model Sensitivity to Transformations

Not all models react to transformations in the same way.

| Model Type           | Effect of Transformation |
|---------------------|--------------------------|
| Linear Regression   | High impact ✅            |
| Logistic Regression | High impact ✅            |
| Decision Trees      | Minimal impact ❌         |
| Random Forest       | Minimal impact ❌         |

Tree-based models are usually less sensitive to feature scaling and distribution shape because they split data based on thresholds rather than assuming a specific distribution.

## ✅ Advantages

- improves performance of statistical models
- reduces skewness
- stabilizes variance
- can reduce the influence of extreme values
- helps data become more model-friendly

## ❌ Disadvantages

- transformed features may be harder to interpret
- some transformations may not help and can even hurt performance
- not every model benefits equally
- choosing the right transformation often requires experimentation

## 🧪 Best Practices

- always visualize the data before and after transformation
- try multiple transformations instead of assuming one will work best
- apply transformations only after handling missing values
- use pipelines to avoid data leakage
- fit transformations on training data and apply the same logic to test data

## 📌 Key Takeaway

The goal of mathematical transformation is not to blindly normalize every feature, but to make the data more suitable for the model you are using. Experiment with different transformations, inspect the resulting distributions, and choose the one that best improves model performance and interpretability.

## 🛠️ Quick Reference

### When to Use What
- right-skewed data → log transform
- moderate skewness → square root transform
- large-value compression → reciprocal transform
- left-skewed data → square transform

### Useful Functions
- `np.log1p()` for log transformation
- `np.sqrt()` for square root transformation
- `FunctionTransformer()` for reusable preprocessing
- `sns.histplot()` for distribution visualization
- `stats.probplot()` for QQ plots

## 🎯 Final Note

Mathematical transformation is a simple but powerful preprocessing technique. When used correctly, it can improve model performance, reveal hidden patterns, and make your machine learning pipeline more robust and effective.