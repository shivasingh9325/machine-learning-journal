# 🌐 Web Scraping → Extracting Data from Websites

## 🔹 Overview
When APIs are not available, I can use **web scraping** to extract data directly from websites. This is an important skill in machine learning for collecting real-world datasets.

---

## 🔹 Workflow: Website → DataFrame

### 1. 📥 Sending a Request
I use the `requests` library to fetch the webpage:

    import requests
    response = requests.get("URL")

---

### 2. 🚫 Handling 403 Forbidden Error
Sometimes the website blocks the request because it detects a bot.

To solve this, I use **headers** to mimic a browser request:

    headers = {
        "User-Agent": "Mozilla/5.0"
    }

    response = requests.get("URL", headers=headers)

---

### 3. 🔍 Parsing HTML with BeautifulSoup
After fetching the page, I parse the HTML using **BeautifulSoup**:

    from bs4 import BeautifulSoup

    soup = BeautifulSoup(response.text, "html.parser")

---

### 4. 🧹 Extracting Data
I extract specific elements using methods like:

- `find()` → first match  
- `find_all()` → all matches  

Example:

    soup.find_all("h2")

---

## 🔹 Extracting Key Information

I extracted the following data from the website:

- Company Name  
- Rating  
- Number of Reviews  
- Company Type  

Example:

    companies = soup.find_all("div", class_="company")

---

## 🔹 Converting to DataFrame

After collecting the data, I store it in a Pandas DataFrame:

    import pandas as pd

    df = pd.DataFrame(scraped_data)

---

## 🔹 Handling Multiple Pages (Pagination)

Websites often have multiple pages, so I loop through them:

    all_data = []

    for page in range(1, total_pages + 1):
        url = f"URL?page={page}"
        response = requests.get(url, headers=headers)
        soup = BeautifulSoup(response.text, "html.parser")
        # extract data
        all_data.extend(page_data)

---

## 🔹 Best Practices 💡

### ✔️ Respect Website Rules
- Check `robots.txt`
- Avoid scraping restricted content

---

### ✔️ Avoid Getting Blocked
- Use headers  
- Add delays:

    import time
    time.sleep(1)

- Avoid sending too many requests quickly  

---

### ✔️ Clean Extracted Data
- Remove extra spaces  
- Convert strings to numbers  
- Handle missing values  

---

### ✔️ Handle Dynamic Websites
- Some websites use JavaScript → data won’t load with `requests`
- Use tools like:
  - Selenium  
  - Playwright  

---

## 🔹 Advantages ✅

- Access data when APIs are unavailable  
- Can collect large datasets  
- Useful for **custom datasets**  

---

## 🔹 Disadvantages ❌

- Websites may block scraping  
- Structure of HTML can change anytime  
- Legal and ethical considerations  
- Slower compared to APIs  

---

## 🔹 When to Use Web Scraping?

Use web scraping when:
- No API is available  
- Data is publicly accessible  
- You need **custom or niche datasets**  

---

## 🔹 APIs vs Web Scraping ⚔️

| Feature        | API                     | Web Scraping              |
|----------------|--------------------------|----------------------------|
| Reliability    | High                     | Medium                     |
| Speed          | Fast                     | Slower                     |
| Ease of Use    | Easy                     | Moderate                   |
| Data Structure | Structured (JSON)        | Unstructured (HTML)        |
| Blocking Risk  | Low                      | High                       |

---

## 🔹 Pro Tips 🚀

- Use browser **Inspect Element** to find tags  
- Use `lxml` parser for faster performance  
- Store raw HTML for debugging  
- Build reusable scraping functions  
- Use proxies if scraping at scale  

---

## 🔹 Summary

- Web scraping is used when APIs are not available  
- Process:  
  **Request → Parse HTML → Extract Data → DataFrame → Store**  
- Handling headers and pagination is essential  
- Important for building **real-world ML datasets**
