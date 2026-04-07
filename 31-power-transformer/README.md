


# 🌟 Power Transformations in Machine Learning — Box-Cox & Yeo-Johnson

## 📌 Overview
Power transformations are mathematical techniques used to **stabilize variance**, **reduce skewness**, and make data distributions closer to a **normal distribution**. They are especially useful for models like **Linear Regression** and **Logistic Regression**, which often work better when features are approximately Gaussian.

In scikit-learn, this is commonly done using `PowerTransformer`, which supports:
- **Box-Cox transformation**
- **Yeo-Johnson transformation**

## 🎯 Why Power Transformations Matter
Real-world data is often skewed, noisy, and unevenly spread. That can make model fitting harder and violate assumptions used by some algorithms.

Power transformations help by:
- reducing skewness 📉
- stabilizing variance ⚖️
- improving normality 📊
- making relationships more linear 🔗
- sometimes improving model performance 🚀

## 🧠 Intuition
Suppose a feature has a long right tail. A power transformation reshapes it so that the values are more balanced. This often makes the learning process easier for models that assume a roughly normal input distribution.

## ⚙️ 1) Box-Cox Transformation

### 📐 Formula
For strictly positive data \(x > 0\):

\[
x^{(\lambda)} =
\begin{cases}
\frac{x^\lambda - 1}{\lambda}, & \lambda \ne 0 \\
\log(x), & \lambda = 0
\end{cases}
\]

### ✅ Key Points
- Works only for **positive values**
- Automatically finds the best \( \lambda \)
- Very effective for skewed numerical data
- Common in statistical modeling

### ✅ Advantages
- Strong normalization effect
- Reduces heteroscedasticity
- Can improve regression performance

### ❌ Disadvantages
- Cannot handle zero or negative values
- Needs preprocessing if data contains non-positive values
- Less flexible than Yeo-Johnson

## ⚙️ 2) Yeo-Johnson Transformation

### 📐 Formula
For any real-valued input \(x\):

If \(x \ge 0\):

\[
x^{(\lambda)} =
\begin{cases}
\frac{(x+1)^\lambda - 1}{\lambda}, & \lambda \ne 0 \\
\log(x+1), & \lambda = 0
\end{cases}
\]

If \(x < 0\):

\[
x^{(\lambda)} =
\begin{cases}
-\frac{(-x+1)^{2-\lambda} - 1}{2-\lambda}, & \lambda \ne 2 \\
-\log(-x+1), & \lambda = 2
\end{cases}
\]

### ✅ Key Points
- Works with **positive, zero, and negative values**
- More practical for real-world data
- Default method in `PowerTransformer`
- Often the safer choice when data is not strictly positive

### ✅ Advantages
- Handles all real numbers
- More flexible than Box-Cox
- Great for messy datasets

### ❌ Disadvantages
- Slightly more complex
- Less intuitive than Box-Cox
- May not always improve model performance

## 🔍 Lambda \( \lambda \)
The parameter \( \lambda \) controls how strong the transformation is.

### Important points:
- It is estimated automatically
- Usually chosen by maximizing the likelihood of the transformed data being close to normal
- Different columns can have different values of \( \lambda \)

## 🧪 scikit-learn Implementation

### ✅ Using `PowerTransformer`
    from sklearn.preprocessing import PowerTransformer

    pt = PowerTransformer(method='yeo-johnson')  # default
    X_transformed = pt.fit_transform(X)

### Available methods
- `method='yeo-johnson'`
- `method='box-cox'`

### Important note
- `box-cox` requires all values to be **strictly positive**
- `yeo-johnson` works for **any real-valued data**

## 🔄 Workflow
1. Inspect distributions
2. Check skewness
3. Visualize (histograms / KDE / Q-Q plots)
4. Apply transformation
5. Compare before vs after
6. Train model
7. Evaluate performance

## 📊 Visual Comparison Code
    import matplotlib.pyplot as plt
    import seaborn as sns

    for col in X_train_transformed2.columns:
        plt.figure(figsize=(14, 4))

        plt.subplot(1, 2, 1)
        sns.histplot(X_train[col], kde=True)
        plt.title(f"{col} - Before")

        plt.subplot(1, 2, 2)
        sns.histplot(X_train_transformed2[col], kde=True)
        plt.title(f"{col} - After")

        plt.tight_layout()
        plt.show()

## 📈 What to Look For
- More symmetric distribution
- Reduced skewness
- Fewer extreme values
- Closer to bell curve

## 🧪 Example Result
Before transformation: R² = 0.62  
After transformation: R² = 0.68  

➡️ Indicates improved model performance

## 🧠 When to Use

Use when:
- Data is skewed
- Variance is not constant
- Using linear models:
  - Linear Regression
  - Logistic Regression
  - Ridge / Lasso

## 🚫 When NOT to Use

Avoid when using:
- Decision Trees 🌳
- Random Forest 🌲
- XGBoost ⚡

These models are not sensitive to feature distribution.

## ⚖️ Box-Cox vs Yeo-Johnson

| Feature | Box-Cox | Yeo-Johnson |
|--------|--------|-------------|
| Input | Positive only | Any real values |
| Flexibility | Low | High |
| Default | No | Yes |

## 📉 Advantages
- Reduces skewness
- Improves model performance
- Stabilizes variance
- Automatic λ selection
- Feature-wise transformation

## ⚠️ Disadvantages
- Reduces interpretability
- Not useful for all models
- Can distort relationships
- Box-Cox limited to positive values

## 🔄 Inverse Transform
    X_original = pt.inverse_transform(X_transformed)

## 🧩 Best Practices
- Fit only on training data
- Apply same transform to test data
- Use in pipelines to avoid leakage

    from sklearn.pipeline import Pipeline
    from sklearn.linear_model import LinearRegression

    pipeline = Pipeline([
        ('power', PowerTransformer()),
        ('model', LinearRegression())
    ])

## 📝 Revision Notes
- Box-Cox → only positive data
- Yeo-Johnson → works for all real values
- Lambda (λ) → controls transformation
- Always visualize before & after
- Always validate using model performance

## 🚀 Final Takeaway
Power transformations reshape skewed data into a more normal form, helping models learn better patterns. Yeo-Johnson is generally the safest choice for real-world datasets.

**Golden Rule:**  
👉 Don’t blindly transform — always verify with plots + metrics.