# 🐼 Practice 1 – Core Data Wrangling with Pandas

## 📌 Objective

The goal of Day 1 was to build strong foundational skills in data wrangling using pandas. The focus was on transforming raw transactional data into a clean, analysis-ready dataset.

---

## 📂 Dataset

Simulated transaction dataset containing:
- order_id
- customer_id
- country
- product
- category
- price
- quantity
- order_date
- email

---

## 🔍 Data Inspection

Before modifying the dataset, I inspected its structure and quality using:
```python
pd.read_csv()
df.head()
df.shape
df.columns
df.dtypes
df.isna().sum()

```
---
## 📑 Column Selection

Learned the structural difference between:
```python
df["price"]      # Series (1D)
df[["price"]]    # DataFrame (2D)

```
---
## 🔎 Row Filtering

Filtered rows using boolean indexing.

Single condition:
```python
df[df["country"] == "SG"]
df.query("country == 'SG'")
```

Multi-Conditions:
```python
df[(df["country"] == "SG") & (df["category"] == "Printer")]
df.query("country == 'SG' & category == 'Printer'')
```
---
## 🧹 Handling Missing Values

Detected missing rows:
```python
df[df["price"].isna()]
```
Dropped rows selectively:
```python
df.dropna(subset=["price"])
```
Filled missing values:
```python
df_clean["quantity"] = df_clean["quantity"].fillna(1)
```
Reset Index after removing rows:
```python
df_clean.reset_index()
```
---
## 🕒 Fixing Data Types

Converted numeric types:
```python
df_clean["quantity"] = df_clean["quantity"].astype(int)
```
Converted to datetime:
```python
df_clean["order_date"] = pd.to_datetime(df_clean["order_date"])
```
Check data type to ensure data type changed:
```python
df_clean.dtypes
```
Extracted datetime features:
```python
df_clean["order_hour"] = df_clean["order_date"].dt.hour
df_clean["order_day"] = df_clean["order_date"].dt.day_name()
```
---
## 💡 Feature Engineering

Created a business metric:
```python
df_clean["revenue"] = df_clean["price"] * df_clean["quantity"]
```
