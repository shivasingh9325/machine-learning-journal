# 🔢 Encoding Categorical Data (Ordinal Encoding & Label Encoding)

## 🔹 Overview
In machine learning, models cannot understand **textual (categorical) data**, so I need to convert it into **numerical form**.  
Here, I worked with a dataset (`customer.csv`) and applied encoding techniques to transform categorical features.

---

## 🔹 Types of Categorical Data

### 1. 🏷️ Nominal Data
- No inherent order  
- Examples:
  - State  
  - City  
  - Branch  

👉 No ranking exists between categories  

---

### 2. 📊 Ordinal Data
- Has a **clear order or ranking**  
- Examples:
  - Review → Poor < Average < Good  
  - Education → School < UG < PG  

👉 Order matters here  

---

## 🔹 Ordinal Encoding

### 📌 What I Did
I used **OrdinalEncoder** to encode ordinal input features like:
- Review  
- Education  

### 📌 Code Example

    from sklearn.preprocessing import OrdinalEncoder

    oe = OrdinalEncoder(categories=[['Poor','Average','Good'],
                                    ['School','UG','PG']])

    X_encoded = oe.fit_transform(X)

---

### 📌 How it Works

| Category | Encoded Value |
|----------|--------------|
| Poor     | 0            |
| Average  | 1            |
| Good     | 2            |

| Category | Encoded Value |
|----------|--------------|
| School   | 0            |
| UG       | 1            |
| PG       | 2            |

---

### ⚠️ Important
- I **must define the order manually** using `categories`
- Otherwise, encoding may happen alphabetically → ❌ incorrect relationships

---

## 🔹 Label Encoding

### 📌 What I Did
I used **LabelEncoder** for the **target column (y)**:

- Purchased (Yes/No)

### 📌 Code Example

    from sklearn.preprocessing import LabelEncoder

    le = LabelEncoder()

    y_encoded = le.fit_transform(y)

---

### 📌 Example Mapping

| Category | Encoded Value |
|----------|--------------|
| No       | 0            |
| Yes      | 1            |

---

## 🔹 Key Differences

| Feature            | OrdinalEncoder        | LabelEncoder        |
|--------------------|----------------------|---------------------|
| Used for           | Input features (X)   | Target variable (y) |
| Handles order      | Yes                  | No                  |
| Custom order       | Yes                  | No (alphabetical)   |

---

## 🔹 Best Practices 💡

### ✔️ Use Correct Encoding Type
- Ordinal data → OrdinalEncoder  
- Nominal data → OneHotEncoder  
- Target labels → LabelEncoder  

---

### ✔️ Avoid Wrong Encoding
- Never use LabelEncoder on input features ❌  
- It introduces **false ordering**  

---

### ✔️ Always Define Order
- For ordinal data, explicitly define category order  
- Prevents incorrect model learning  

---

### ✔️ Keep Track of Mappings
- Important for:
  - Model interpretation  
  - Debugging  
  - Deployment  

---

## 🔹 Advantages ✅

- Converts categorical → numerical  
- Helps models process non-numeric data  
- Preserves order (in ordinal encoding)  

---

## 🔹 Disadvantages ❌

- Wrong encoding can mislead models  
- LabelEncoder may introduce false relationships  
- Not suitable for nominal data  

---

## 🔹 When to Use What?

| Scenario                     | Technique          |
|-----------------------------|--------------------|
| Ranked categories           | OrdinalEncoder     |
| Unordered categories        | OneHotEncoder      |
| Target variable             | LabelEncoder       |

---

## 🔹 Pro Tips 🚀

- Use `ColumnTransformer` to apply encoding to specific columns  
- Combine encoding with pipelines (`Pipeline`)  
- Always split data before encoding (to avoid data leakage)  
- Save encoders using `pickle` or `joblib` for reuse  

---

## 🔹 Summary

- Machine learning models require **numerical input**  
- I used:
  - **OrdinalEncoder** → for ordered features  
  - **LabelEncoder** → for target variable  
- Correct encoding is critical for **model accuracy and performance**
