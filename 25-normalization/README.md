# 📊 Feature Scaling – Normalization Techniques

## 📌 Overview

Feature scaling is a crucial preprocessing step in Machine Learning that ensures numerical features are brought to a similar scale without distorting their underlying distribution.

It improves:

* Model performance
* Convergence speed (especially for gradient-based algorithms)
* Fair contribution of all features

---

## 🎯 Why Feature Scaling?

* Features may have different ranges (e.g., income vs age)
* Distance-based algorithms (KNN, SVM) are sensitive to scale
* Prevents dominance of high-magnitude features

---

## 🔹 Min-Max Scaling (Normalization)

### 📐 Formula

x' = (x - xmin) / (xmax - xmin)

### 💡 Intuition

Transforms data into a fixed range, typically **[0, 1]**

### ✅ Advantages

* Preserves original distribution shape
* Simple and widely used
* Useful in neural networks and image processing

### ❌ Disadvantages

* Highly sensitive to outliers

---

## 🔹 Mean Normalization

### 📐 Formula

x' = (x - mean) / (xmax - xmin)

### 💡 Intuition

Centers data around zero while keeping values within a bounded range

### ✅ Use Case

* When centering data is beneficial

---

## 🔹 MaxAbs Scaling

### 📐 Formula

x' = x / |xmax|

### 💡 Intuition

Scales data based on maximum absolute value

### ✅ Advantages

* Range becomes **[-1, 1]**
* Preserves sparsity (important for sparse datasets)
* No shifting (data not centered)

---

## 🔹 Robust Scaling

### 📐 Formula

x' = (x - median) / IQR

Where:

* IQR = Q3 - Q1

### 💡 Intuition

Uses median and interquartile range instead of mean and standard deviation

### ✅ Advantages

* Resistant to outliers
* Works well with skewed or noisy data

---

## ⚖️ Comparison of Scaling Techniques

| Method             | Range     | Outlier Sensitivity | Best Use Case                |
| ------------------ | --------- | ------------------- | ---------------------------- |
| Min-Max Scaling    | [0,1]     | High                | Clean data, image processing |
| Mean Normalization | Varies    | Moderate            | Centered data requirements   |
| MaxAbs Scaling     | [-1,1]    | Moderate            | Sparse datasets              |
| Robust Scaling     | Unbounded | Low                 | Data with outliers           |

---

## 🔁 Normalization vs Standardization

### 🔹 Normalization

* Scales data to a fixed range (usually 0–1)
* Sensitive to outliers
* Used when bounds are required

### 🔹 Standardization

* Centers data around mean = 0 and std = 1
* Less affected by outliers
* Preferred for algorithms assuming normal distribution

---

## 🧠 When to Use What?

* ✅ Use **Min-Max Scaling** → when data is clean and bounded scaling is needed
* ✅ Use **MaxAbs Scaling** → when working with sparse data
* ✅ Use **Robust Scaling** → when dataset contains outliers
* ✅ Use **Standardization** → when model assumes normal distribution

---

## 🧪 Practical Implementation (Python - sklearn)

```python
from sklearn.preprocessing import MinMaxScaler, MaxAbsScaler, RobustScaler

# Min-Max Scaling
scaler = MinMaxScaler()
df_scaled = scaler.fit_transform(df)

# MaxAbs Scaling
scaler = MaxAbsScaler()
df_scaled = scaler.fit_transform(df)

# Robust Scaling
scaler = RobustScaler()
df_scaled = scaler.fit_transform(df)
```

---

## ✅ Summary

Feature scaling is essential for many machine learning algorithms. Choosing the right technique depends on:

* Presence of outliers
* Data distribution
* Type of algorithm being used

Proper scaling leads to better accuracy, faster training, and more stable models.
