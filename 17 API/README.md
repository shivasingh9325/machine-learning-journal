# 📡 Fetching Data from APIs & Converting to Pandas DataFrame

## 🔹 Overview
Fetching data from APIs is an essential skill in machine learning, especially when real-world datasets are not available in structured formats like CSV files or databases.

---

## 🔹 What is an API?
An **API (Application Programming Interface)** allows different software systems to communicate and exchange data.

### 📌 In Data Science:
- APIs act as **data pipelines**
- They enable access to **real-time and dynamic data**
- Common use cases:
  - Weather data
  - Stock market data
  - Movie databases
  - Social media analytics

---

## 🔹 Workflow: API → DataFrame

### 1. 📥 Sending a Request
Use Python’s `requests` library to fetch data:

```python
import requests

response = requests.get("API_URL")


## 🔹 Workflow: API → DataFrame

### 2. ✅ Check Response Status
Ensure the request was successful:

    response.status_code

- `200` → Success  
- `404` → Not Found  
- `500` → Server Error  

---

### 3. 🔄 Convert to JSON
APIs usually return data in JSON format:

    data = response.json()

- JSON is similar to Python dictionaries  
- Helps understand data structure before extraction  

---

### 4. 🧹 Extract Relevant Data
Select only useful fields:

- ID  
- Title  
- Release Date  
- Overview  
- Popularity  
- Vote Average  
- Vote Count  

---

### 5. 🐼 Convert to DataFrame

    import pandas as pd
    df = pd.DataFrame(extracted_data)

---

### 6. 🔁 Handling Pagination
APIs often limit results per request → use loops:

    all_data = []

    for page in range(1, total_pages + 1):
        response = requests.get(f"API_URL&page={page}")
        data = response.json()
        all_data.extend(data["results"])

---

### 7. 💾 Export Data

    df.to_csv("data.csv", index=False)

---

## 🔹 Practical Example: TMDB API
Using a movie database API to:
- Fetch movie data  
- Handle multiple pages  
- Build a complete dataset (~hundreds of pages)  
- Convert into a structured DataFrame  

---

## 🔹 Best Practices 💡

### ✔️ Data Cleaning
- Handle missing values (`NaN`)  
- Convert data types (dates, numbers)  
- Normalize nested JSON data  

---

### ✔️ Error Handling

    if response.status_code != 200:
        print("Error fetching data")

---

### ✔️ Rate Limiting
- APIs restrict number of requests  
- Use delays:

    import time
    time.sleep(1)

---

### ✔️ API Keys Security
- Never expose API keys in public repos  
- Use environment variables:

    import os
    API_KEY = os.getenv("API_KEY")

---

## 🔹 Advantages ✅

- Access to **real-time data**  
- No need to manually collect datasets  
- Scalable for large data pipelines  
- Useful for **production ML systems**  

---

## 🔹 Disadvantages ❌

- Rate limits & request restrictions  
- Dependency on external services  
- Data may be incomplete or inconsistent  
- Requires handling pagination & errors  

---

## 🔹 When to Use APIs in ML?

Use APIs when:
- Data is **continuously changing**  
- No static dataset is available  
- Building **real-world ML applications**:
  - Recommendation systems  
  - Live dashboards  
  - Prediction services  

---

## 🔹 Pro Tips 🚀

- Use `pd.json_normalize()` for nested JSON  
- Cache API responses to avoid repeated calls  
- Log API responses for debugging  
- Use async requests (`aiohttp`) for faster data fetching  

---

## 🔹 Summary

- APIs are a **primary source of real-world data**  
- Process:  
  **Request → JSON → Extract → DataFrame → Export**  
- Handling pagination and cleaning data are critical steps  
- Mastering APIs is essential for **industry-level ML projects**
