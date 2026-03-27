# 📊 Understanding Your Dataset (Initial Data Analysis)

## 🔹 Overview
Before building any machine learning model, I need to **understand the dataset properly**. This step helps prevent bias, errors, and poor model performance.

---

## 🔹 Workflow: Initial Data Analysis

### 1. 📏 Determine Data Size
I first check how big the dataset is:

    df.shape

- Returns `(rows, columns)`
- Helps understand scale of data

---

### 2. 👀 Initial Visualization
I inspect the data to get a quick idea:

    df.head()
    df.sample(5)

- `head()` → first 5 rows  
- `sample()` → random rows (better to avoid bias)  

---

### 3. 🧾 Identify Data Types
I check column types and missing values:

    df.info()

- Shows:
  - Data types (int, float, object, etc.)
  - Non-null counts
  - Memory usage  

---

### 4. ❓ Handle Missing Values
I analyze missing data:

    df.isnull().sum()

- Helps decide:
  - Fill missing values  
  - Drop rows/columns  

---

### 5. 📐 Statistical Summary
I check numerical statistics:

    df.describe()

- Includes:
  - Mean  
  - Standard deviation  
  - Min / Max  
  - Percentiles  

- Helps detect:
  - Outliers  
  - Skewed distributions  

---

### 6. 🔁 Check for Duplicates
I verify duplicate records:

    df.duplicated().sum()

- Important for data quality  
- Duplicates can bias models  

---

### 7. 🔗 Analyze Correlation
I analyze relationships between features:

    df.corr()

- Helps understand:
  - Feature relationships  
  - Which features impact the target variable  
- Useful for **feature selection**

---

## 🔹 Best Practices 💡

### ✔️ Always Understand Before Modeling
- Never jump directly to training models  
- Data understanding = better accuracy  

---

### ✔️ Handle Missing Values Carefully
- Options:
  - Fill (mean, median, mode)  
  - Drop  
  - Use ML-based imputation  

---

### ✔️ Detect Outliers
- Use:
  - Boxplots  
  - Statistical summaries  
- Outliers can distort models  

---

### ✔️ Optimize Data Types
- Convert:
  - `object` → `category`  
  - Reduce memory usage  

---

### ✔️ Understand Feature Types
- Numerical → continuous/discrete  
- Categorical → nominal/ordinal  

---

## 🔹 Advantages ✅

- Prevents model errors  
- Improves feature selection  
- Helps detect data issues early  
- Leads to better model performance  

---

## 🔹 Disadvantages ❌

- Time-consuming for large datasets  
- Requires domain understanding  
- Can be overlooked by beginners  

---

## 🔹 When to Use This?

Always perform this step:
- Before data preprocessing  
- Before feature engineering  
- Before model training  

---

## 🔹 Pro Tips 🚀

- Use visualizations:
  - `sns.heatmap()` for correlation  
  - `histplot()` for distributions  
- Create a checklist for EDA  
- Automate using tools like:
  - `pandas-profiling` / `ydata-profiling`  
- Always keep a copy of raw data  

---

## 🔹 Summary

- Understanding data is the **first step in ML**  
- Process includes:
  **Shape → Preview → Info → Missing Values → Stats → Duplicates → Correlation**  
- Proper analysis prevents bias and improves model accuracy  
- Strong EDA skills = strong ML foundation
