# ColumnTransformer — Practical Notes

## 📌 What is ColumnTransformer?
`ColumnTransformer` is used to apply **different preprocessing steps to different columns** in a dataset.

It is especially useful when your dataset contains:
- Numerical data (age, salary)
- Categorical data (gender, city)
- Ordinal data (low, medium, high)

---

## ❌ Problem Without ColumnTransformer
Manually preprocessing data leads to:
- Multiple steps (imputation, encoding)
- Separate transformations for each column
- Manual concatenation → messy and error-prone code

### Example Workflow (Bad Way):
1. Handle missing values
2. Encode categorical columns
3. Merge all results manually

👉 This becomes **complex and hard to maintain**

---

## ✅ Solution: ColumnTransformer
ColumnTransformer allows you to:
- Apply multiple transformations **in one step**
- Keep code clean and scalable
- Avoid manual concatenation

---

## 🔧 Basic Syntax

```python
from sklearn.compose import ColumnTransformer
```

```python
ct = ColumnTransformer(
    transformers=[
        ('name1', transformer1, [col1, col2]),
        ('name2', transformer2, [col3]),
    ]
)
```

---

## 🧪 Example Use Case

### Problem:
- `fever` → missing values → Imputation
- `cough` → ordinal → Ordinal Encoding
- `gender`, `city` → nominal → One Hot Encoding

---

## 🔧 Hard Way (Not Recommended)

```python
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import OneHotEncoder, OrdinalEncoder

# Imputation
si = SimpleImputer()
fever = si.fit_transform(df[['fever']])

# Ordinal Encoding
oe = OrdinalEncoder(categories=[['Mild', 'Strong']])
cough = oe.fit_transform(df[['cough']])

# One Hot Encoding
ohe = OneHotEncoder(sparse_output=False)
gender_city = ohe.fit_transform(df[['gender', 'city']])

# Manual Concatenation
import numpy as np
final = np.concatenate([fever, cough, gender_city], axis=1)
```

### ❌ Problems:
- Too many steps
- Manual merging
- Hard to scale

---

## 🚀 Pro Way (Using ColumnTransformer)

```python
from sklearn.compose import ColumnTransformer
from sklearn.impute import SimpleImputer
from sklearn.preprocessing import OneHotEncoder, OrdinalEncoder

ct = ColumnTransformer(
    transformers=[
        ('impute_fever', SimpleImputer(), ['fever']),
        ('encode_cough', OrdinalEncoder(categories=[['Mild', 'Strong']]), ['cough']),
        ('onehot', OneHotEncoder(sparse_output=False, drop='first'), ['gender', 'city'])
    ],
    remainder='passthrough'
)
```

### Apply Transformation:
```python
transformed_data = ct.fit_transform(df)
```

---

## ⚙️ Important Parameter: `remainder`

Controls what happens to columns **not specified**

- `'drop'` → removes remaining columns (default)
- `'passthrough'` → keeps remaining columns

```python
remainder='passthrough'
```

---

## ⚠️ Common Mistakes

### 1. Forgetting column list
```python
('imputer', SimpleImputer(), 'fever')  # ❌
```

✔ Fix:
```python
('imputer', SimpleImputer(), ['fever'])  # ✅
```

---

### 2. Sparse output issue
```python
OneHotEncoder()  # ❌ may give sparse matrix
```

✔ Fix:
```python
OneHotEncoder(sparse_output=False)
```

---

### 3. Column order confusion
- Output order = same as transformers list
- Not same as original dataframe

---

## ✅ Advantages
- Clean and readable code
- All preprocessing in one place
- Works seamlessly with pipelines
- Reduces human error

---

## ❌ Disadvantages
- Slight learning curve
- Output is NumPy array (not DataFrame by default)

---

## 🧠 Key Takeaways
- Use ColumnTransformer for mixed data types
- Avoid manual preprocessing
- Combine multiple transformations easily
- Use with pipelines for production-ready ML

---

## 🚀 Extra Tips

Convert output to DataFrame:
```python
import pandas as pd

pd.DataFrame(transformed_data)
```

---

Check transformers:
```python
ct.transformers_
```

---

## 🔗 Best Practice
Use ColumnTransformer with Pipeline:

```python
from sklearn.pipeline import Pipeline
```

👉 This makes your workflow:
- Reproducible
- Clean
- Production-ready

---

## 📌 Summary
- ColumnTransformer = apply different transformations to different columns
- Replaces messy manual preprocessing
- Essential for real-world ML workflows