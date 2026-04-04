# 🚀 Machine Learning Pipelines (Scikit-Learn)

## 📌 Overview
Machine Learning Pipelines in Scikit-Learn allow you to combine **data preprocessing + feature engineering + model training** into a single workflow. This makes your code cleaner, prevents errors, and ensures consistency from training to deployment.

---

## 🎯 Why Use Pipelines?

- 🧹 **Simplification**: Combine multiple steps into one object  
- 🔁 **Consistency**: Same transformations applied everywhere  
- 🔒 **Prevents Data Leakage**  
- 🧠 **Reproducibility**: Easy to debug and reuse  
- 🚀 **Deployment Ready**: Save entire workflow in one file  

---

## ⚙️ Pipeline Workflow

Raw Data → Preprocessing → Feature Engineering → Model → Prediction

Example:

    pipe = Pipeline([
        ('trf1', trf1),  # missing value handling
        ('trf2', trf2),  # encoding
        ('trf3', trf3),  # scaling
        ('trf4', trf4),  # feature selection
        ('trf5', trf5)   # model
    ])

👉 Each step runs sequentially from top to bottom.

---

## ✂️ Train-Test Split

    X_train, X_test, y_train, y_test = train_test_split(
        df.drop(columns=['Survived']),
        df['Survived'],
        test_size=0.2,
        random_state=42
    )

- X → features  
- y → target  
- 80% training, 20% testing  

---

## 🧠 fit vs transform vs fit_transform

- **fit()** → Learns from data (mean, categories, etc.)  
- **transform()** → Applies learned changes  
- **fit_transform()** → fit + transform together  

### 🔥 Golden Rule:
👉 **Fit only on training data**  
👉 **Transform both training and test data**

---

## 🏋️ Model Training

    pipe.fit(X_train, y_train)

✔ Applies all preprocessing  
✔ Trains model using X_train and y_train  

---

## 🔮 Prediction

    y_pred = pipe.predict(X_test)

✔ Only transformation is applied  
✔ No learning happens here  

---

## 🔁 Cross Validation

    from sklearn.model_selection import cross_val_score
    cross_val_score(pipe, X_train, y_train, cv=5, scoring='accuracy').mean()

### 📌 What it does:
- Splits training data into 5 parts  
- Trains model 5 times  
- Tests on different parts  
- Returns average accuracy  

### 🧠 One-liner:
👉 Train many times → Test many times → Take average  

---

## 🔍 GridSearchCV (Hyperparameter Tuning)

### Step 1: Define parameters

    params = {
        'decisiontreeclassifier__max_depth': [1, 2, 3, 4, 5, None]
    }

### Step 2: Apply GridSearch

    from sklearn.model_selection import GridSearchCV
    grid = GridSearchCV(pipe, params, cv=5, scoring='accuracy')
    grid.fit(X_train, y_train)

### 🔥 Important Rule:
👉 step_name__parameter_name  

Example:
👉 decisiontreeclassifier__max_depth  

---

## ❗ Common Errors & Fixes

### ❌ Invalid parameter error
Error:
    Invalid parameter 'trf5'

✔ Reason: Step name mismatch  
✔ Fix:

    pipe.get_params().keys()

👉 Use correct step name  

---

### ⚠️ Feature name warning

    X does not have valid feature names

✔ Reason:
- Training data = DataFrame  
- Prediction data = list/array  

✔ Fix:

    test_input = pd.DataFrame(
        [[22, 7.25, 'male', 'S']],
        columns=X_train.columns
    )

---

## 📊 fit / train / predict confusion (VERY IMPORTANT)

| Step        | Data Used        | Purpose |
|------------|----------------|--------|
| fit        | X_train        | Learn patterns |
| transform  | X_train + X_test | Apply changes |
| model.fit  | X_train + y_train | Train model |
| predict    | X_test         | Make predictions |

---

## 🔥 Complete Workflow

    # Step 1: Split
    X_train, X_test, y_train, y_test = train_test_split(...)

    # Step 2: Cross-validation
    cross_val_score(pipe, X_train, y_train, cv=5)

    # Step 3: Hyperparameter tuning
    grid.fit(X_train, y_train)

    # Step 4: Final training
    pipe.fit(X_train, y_train)

    # Step 5: Testing
    pipe.score(X_test, y_test)

---

## 🚀 Deployment

    import pickle
    pickle.dump(pipe, open('model.pkl', 'wb'))

    pipe = pickle.load(open('model.pkl', 'rb'))

👉 Entire preprocessing + model saved in one file  

---

## 🧩 Extra Concepts

### ColumnTransformer
Used to apply different transformations to different columns:

- Numerical → Scaling  
- Categorical → Encoding  

---

## 🧠 Important Rules (Must Remember)

- ✅ Fit only on training data  
- ❌ Never fit on test data  
- ✅ Keep input format consistent  
- ✅ Always use pipelines  
- ✅ Use cross-validation for better accuracy  

---

## 🔥 Final Summary

- Pipelines automate ML workflows  
- Cross-validation gives reliable evaluation  
- GridSearch finds best parameters  
- Training uses X_train + y_train  
- Testing uses unseen data  

---

## ⚡ One-Line Memory Tricks

- Pipeline → "Chain everything into one object"  
- Cross-validation → "Train many times, average result"  
- GridSearch → "Try all combinations, pick best"  
- fit vs transform → "Learn from train, apply to all"  

---