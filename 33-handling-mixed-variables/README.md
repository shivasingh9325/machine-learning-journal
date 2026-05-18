# Feature Engineering for Mixed Variables

## Introduction
Mixed variables are columns where **numerical and categorical information exist together** in the same feature. This creates problems because machine learning models expect clean and consistent data types. The solution is to **separate mixed data into independent numerical and categorical columns**.

---

# What are Mixed Variables?

A mixed variable contains both:
- **Numerical values** (numbers)
- **Categorical values** (labels/text)

Example:
`Cabin = C123`

Here:
- `C` → categorical (cabin class/block)
- `123` → numerical (cabin number)

Another example:
`Ticket = PC 17599`

Here:
- `PC` → category
- `17599` → number

---

# Why is Mixed Data a Problem?

Problems caused:
- Models cannot interpret mixed formats directly.
- Feature importance becomes misleading.
- Data visualization becomes harder.
- Missing values become harder to handle.

Example:
`A23`, `B45`, `C12`
Model sees strings, not useful patterns.

---

# Solution: Split the Variable

Convert:

`C123`

into:

| Cabin_Type | Cabin_Number |
|------------|--------------|
| C          | 123          |

Benefits:
- Cleaner features
- Better model learning
- Easier preprocessing

---

# Techniques for Handling Mixed Variables

## 1. String Splitting
Use when format is simple and consistent.

Example:
`C123`

Split into:
- first letter → category
- remaining digits → number

Python:
```python
df['Cabin_Type'] = df['Cabin'].str[0]
df['Cabin_Number'] = df['Cabin'].str[1:]
```

Best for:
- fixed formats

---

## 2. Regular Expressions (Regex)
Useful for messy or inconsistent data.

Example:
`PC 17599`

Extract number:
```python
df['Ticket_Number'] = df['Ticket'].str.extract('(\d+)')
```

Extract text:
```python
df['Ticket_Type'] = df['Ticket'].str.extract('([A-Za-z]+)')
```

Best for:
- alphanumeric values
- complex strings

---

# Handling Missing Values After Splitting

After splitting, missing values often appear.

Example:
`NaN`

### Numerical Column
Options:
- fill with `0`
- fill with `median`
- fill with `mean`

```python
df['Cabin_Number'].fillna(0)
```

Recommended: **median**

---

### Categorical Column
Options:
- `"Missing"`
- `"Unknown"`

```python
df['Cabin_Type'].fillna('Missing')
```

Recommended: `"Missing"`

---

# Advantages
✅ cleaner data  
✅ better model accuracy  
✅ easier interpretation  
✅ improved visualizations  
✅ easier preprocessing pipeline  

---

# Disadvantages
❌ requires extra preprocessing  
❌ regex can be slow on large data  
❌ bad splitting may lose information  

---

# Common Mistakes
- not checking data format first
- using wrong regex
- forgetting missing values
- converting extracted numbers as strings instead of numeric

Fix:
```python
pd.to_numeric()
```

---

# Edge Cases
1. No numerical part (`"ABC"`)
2. No categorical part (`"123"`)
3. Multiple categories (`"AB123"`)
4. Special symbols (`"#12A"`)

Always inspect raw data first:
```python
df['column'].unique()
```

---

# Best Practices
1. Explore data before splitting.
2. Use simple string methods first.
3. Use regex only when needed.
4. Handle missing values immediately.
5. Convert extracted numbers to numeric type.
6. Validate output after transformation.

---

# Final Takeaway
Mixed variables are common in real-world datasets. The best approach is simple: **split numerical and categorical parts into separate columns, then handle missing values properly.** This creates cleaner data, better features, and improves model performance.