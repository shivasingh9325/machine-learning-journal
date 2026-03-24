# Data Gathering: Working with CSV Files

This guide provides a comprehensive overview of gathering data from various sources, focusing specifically on **CSV (Comma-Separated Values)** files, which are crucial for machine learning projects.

---

## 📌 Key Learnings

### 1. Loading CSV Data
- Use `pandas.read_csv()` to load data from local files.
- Load data directly from URLs (using `requests`).

### 2. Handling Delimiters
- Parse files with different separators (e.g., tabs for TSV files).
- Adjust using the `sep` parameter.

### 3. Managing Headers
- Handle files without headers.
- Skip rows or specify which row contains column names.

### 4. Data Subsetting
- Load only specific columns using `usecols`.
- Limit the number of rows with `nrows` to manage memory effectively.

### 5. Data Cleaning during Load
- Handle missing values with `na_values`.
- Specify `dtypes` during import to save memory.

### 6. Handling Encodings
- Resolve `UnicodeDecodeError` by specifying correct encoding (e.g., `latin-1`).

### 7. Data Transformation
- Apply functions to data while loading using the `converters` parameter.

### 8. Parsing Dates
- Automatically parse date columns with `parse_dates` for better time-series analysis.

### 9. Memory Management
- Load huge datasets in chunks using the `chunksize` parameter to prevent crashes.

---

## ✅ Summary
By mastering these techniques, you can efficiently gather, clean, and transform CSV data for machine learning projects while managing memory and avoiding common pitfalls.
