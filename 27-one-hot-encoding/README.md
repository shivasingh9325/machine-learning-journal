# One Hot Encoding (OHE) — Practical Notes

## 📌 What is One Hot Encoding?
One Hot Encoding (OHE) is a technique used to convert **categorical (nominal) data** into a numerical format so that machine learning models can understand it.

- Most ML algorithms **cannot process text directly**
- OHE converts each category into a **separate binary column (0 or 1)**

### Example
| Brand | BMW | Audi | Tata |
|------|-----|------|------|
| BMW  | 1   | 0    | 0    |
| Tata | 0   | 0    | 1    |

---

## ⚠️ Dummy Variable Trap
If a feature has **n categories**, OHE creates **n columns**, which leads to **multicollinearity (redundant information)**.

### ✔️ Solution:
Use only **n-1 columns**

```python
pd.get_dummies(df, drop_first=True)
```

---

## ⚠️ High Cardinality Problem
When a feature has too many categories:
- Too many columns are created
- Model becomes slow and inefficient

### ✔️ Solution:
Group rare categories into `"uncommon"`

```python
counts = df['brand'].value_counts()
rare = counts[counts < 10].index

df['brand'] = df['brand'].replace(rare, 'uncommon')
```

---

## 🔧 Method 1: Pandas `get_dummies`

### Basic Usage:
```python
pd.get_dummies(df['brand'])
```

### Recommended:
```python
pd.get_dummies(
    df['brand'],
    drop_first=True,
    dtype=int
)
```

### ⚠️ Common Mistake:
```python
pd.get_dummies(df['brand'])  # may give True/False
```

✔ Fix:
```python
pd.get_dummies(df['brand'], dtype=int)
```

### ✅ Advantages
- Simple and fast
- Good for quick analysis

### ❌ Disadvantages
- Does not remember categories
- Issues with unseen data

---

## 🔧 Method 2: OneHotEncoder (Recommended)

### Setup:
```python
from sklearn.preprocessing import OneHotEncoder
import numpy as np

ohe = OneHotEncoder(
    drop='first',
    sparse_output=False,
    dtype=np.int32
)
```

### Fit & Transform:
```python
encoded = ohe.fit_transform(df[['brand']])
```

---

### ⚠️ Common Mistakes

#### 1. Wrong parameter
```python
OneHotEncoder(sparse=False)  # ❌
```

✔ Fix:
```python
OneHotEncoder(sparse_output=False)
```

#### 2. Wrong input shape
```python
ohe.fit_transform(df['brand'])  # ❌
```

✔ Fix:
```python
ohe.fit_transform(df[['brand']])  # ✅
```

#### 3. Unseen categories
```python
OneHotEncoder(handle_unknown='ignore')
```

---

### ✅ Advantages
- Works in ML pipelines
- Handles train/test consistency
- Can handle unseen categories

### ❌ Disadvantages
- Slightly complex
- Requires fitting

---

## 🧠 Key Takeaways
- Converts categorical data → numerical (0/1)
- Avoid dummy variable trap
- Handle high cardinality
- Use:
  - `get_dummies()` → quick work
  - `OneHotEncoder` → production

---

## 🚀 Extra Tips

Check unique values:
```python
df['brand'].nunique()
```

Convert boolean to int:
```python
df_encoded.astype(int)
```

---

## 📌 Alternatives (for large datasets)
- Target Encoding
- Frequency Encoding