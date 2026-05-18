# Encoding Numerical Features: Discretization (Binning) and Binarization

## Introduction
Encoding numerical features is an important feature engineering step in Machine Learning. It helps improve model interpretability, handle skewed data, reduce noise, and sometimes improve performance. Two common techniques are **Discretization (Binning)** and **Binarization**.

---

# 1. Discretization (Binning)

## What is Discretization?
Discretization converts continuous numerical values into discrete intervals (bins/categories).

Example:  
Age → `[12, 25, 67]` → `["Child", "Adult", "Senior"]`

## Why use it?
- Handles **outliers** better by reducing their impact.
- Reduces **noise** in data.
- Captures **non-linear relationships**.
- Improves **interpretability**.
- Useful for some models like **Decision Trees**.

---

## Types of Discretization

### A. Equal Width (Uniform) Binning
Divides the entire range into equal-sized intervals.

Example: `[0-20], [20-40], [40-60]`

**Advantages:**
- Simple
- Fast
- Easy to understand

**Disadvantages:**
- Sensitive to outliers
- Can create uneven data distribution

**Best for:** Uniformly distributed data

---

### B. Equal Frequency (Quantile) Binning
Each bin gets approximately the same number of samples.

Example: `[1,2,3] [4,5,6] [7,8,9]`

**Advantages:**
- Handles skewed data well
- Balanced bins

**Disadvantages:**
- Unequal interval widths
- Harder to interpret

**Best for:** Skewed datasets (salary, age, income)

---

### C. KMeans Binning
Uses K-Means clustering to create bins based on natural data groups.

Example: `[1,2,3]` and `[100,101,102]`

**Advantages:**
- Finds natural clusters
- Adaptive

**Disadvantages:**
- Computationally expensive
- Need to choose K carefully

**Best for:** Clustered data

---

### D. Custom / Domain-Based Binning
Manual bins using domain knowledge.

Example:  
Age → Child / Adult / Senior

**Advantages:**
- Highly interpretable
- Business-friendly

**Disadvantages:**
- Requires expertise
- Can introduce bias

**Best for:** Healthcare, finance, insurance

---

## Scikit-Learn Implementation
Use `KBinsDiscretizer`

```python
from sklearn.preprocessing import KBinsDiscretizer

kb = KBinsDiscretizer(n_bins=5, encode='ordinal', strategy='quantile')
X_new = kb.fit_transform(X)
```

### Important Parameters
- `n_bins` → number of bins
- `encode` → `ordinal`, `onehot`
- `strategy` → `uniform`, `quantile`, `kmeans`

---

## Common Mistakes
- Using too many bins → overfitting
- Using uniform on skewed data
- Ignoring outliers before binning
- Applying before train-test split (data leakage)

---

## Edge Cases
- Duplicate values may break quantile binning
- Small datasets can overfit
- Data drift may require re-binning later

---

# 2. Binarization

## What is Binarization?
Converts numerical values into **0 or 1** using a threshold.

Rule:  
If `x > threshold` → 1  
Else → 0

Example:  
Marks `[20, 80]`, threshold = 50 → `[0, 1]`

---

## Why use it?
- Simplifies features
- Makes decisions clearer
- Useful in image processing
- Helpful in recommendation systems

---

## Scikit-Learn Implementation

```python
from sklearn.preprocessing import Binarizer

b = Binarizer(threshold=50)
X_new = b.fit_transform(X)
```

---

## Advantages
- Very simple
- Fast
- Memory efficient
- Easy to interpret

## Disadvantages
- Major information loss
- Highly threshold dependent
- Not reversible

Example: 51 and 100 both become `1`

---

## Common Mistakes
- Choosing wrong threshold
- Ignoring missing values
- Making class imbalance worse

---

# When to Use What?

Use **Discretization** when:
- Need multiple categories
- Want better interpretability
- Handling skewed/outlier-heavy data

Use **Binarization** when:
- Only yes/no information matters
- Threshold-based decisions are needed

---

# Best Practices
1. Always visualize data first.
2. Start with **Quantile Binning** as default.
3. Use domain knowledge where possible.
4. Validate impact using cross-validation.
5. Use sklearn pipelines to avoid leakage.

---

# Final Takeaway
Discretization and Binarization are simple but powerful feature engineering techniques. They may not always improve accuracy, but they help in handling noisy/skewed data, improving interpretability, and building better ML intuition.