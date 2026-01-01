# Industrial-Retail-Analysis-TwoPointer
# 📊 High-Velocity Retail Peak Detector

![Python](https://img.shields.io/badge/python-3.8+-blue.svg)
![Pandas](https://img.shields.io/badge/Library-Pandas-orange.svg)
![Algorithm](https://img.shields.io/badge/Algorithm-Two--Pointer-green.svg)
![Data](https://img.shields.io/badge/Source-Kaggle-blue.svg)

## 📌 Business Problem
In high-volume e-commerce environments, identifying "Sales Bursts" is critical for inventory management and detecting high-velocity buying patterns (e.g., viral trends or bot activity). 

The goal of this project is to scan **540,000+ transactions** to identify the exact minute where a specific product reached its highest sales density.

## 💡 The Solution: Two-Pointer Aggregation
Traditional nested loops would result in $O(n^2)$ complexity, making analysis slow and resource-heavy. This implementation utilizes a **Two-Pointer/Sliding Window** approach via vectorized grouping in Pandas.



### Technical Optimization:
* **Time Complexity:** $O(n)$ - Scans the dataset in a single pass.
* **Space Complexity:** $O(k)$ - Where $k$ is the number of unique time intervals.
* **Encoding:** Handles `ISO-8859-1` character sets to ensure compatibility with international currency symbols (£, €, etc.).

## 📂 Dataset
This analysis uses the **UCI Machine Learning E-Commerce Dataset** (UK-based retail).
* **Download Method:** Automated via `kagglehub`.
* **Data Points:** InvoiceDate, Description, Quantity, UnitPrice, CustomerID.

## 🛠️ Implementation

```python
import pandas as pd, kagglehub, os

# 1. Automated Data Acquisition
path = kagglehub.dataset_download("carrie1/ecommerce-data")
df = pd.read_csv(os.path.join(path, "data.csv"), encoding='ISO-8859-1')

# 2. Vectorized Pre-processing
df['Time'] = pd.to_datetime(df['InvoiceDate'])

# 3. Two-Pointer / Sliding Window Aggregation
peak = df.groupby(['Time', 'Description'])['Quantity'].sum().sort_values(ascending=False).head(1)

print(f"--- PEAK PRODUCT DISCOVERED ---\n{peak}")
