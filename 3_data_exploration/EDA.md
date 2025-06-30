
# 📊 Exploratory Data Analysis (EDA) Report

---

## 📦 Dataset Overview

- **Shape**: 32,065 rows × 23 columns  
- **Data Types**:  
  - `datetime64`: 1 (`timestamp`)  
  - `float64`: 21 numerical features  
  - `object`: 1 categorical feature  
- **Missing Values**: None

---

### 🧾 Preview of the Data

```python
# Show the first five rows of the dataset
df.head()
```

| timestamp           | eta_variation_hours | traffic_congestion_level |
|---------------------|---------------------|---------------------------|
| 2021-01-01 00:00:00 | 4.998               | 5.928                     |
| 2021-01-01 01:00:00 | 0.985               | 1.592                     |
| 2021-01-01 02:00:00 | 4.973               | 8.788                     |
| 2021-01-01 03:00:00 | 3.095               | 0.045                     |
| 2021-01-01 04:00:00 | 3.216               | 8.005                     |

| warehouse_inventory_level | delay_probability | risk_classification |
|----------------------------|-------------------|----------------------|
| 985.717                    | 0.885             | Moderate Risk        |
| 396.700                    | 0.544             | High Risk            |
| 832.409                    | 0.803             | High Risk            |
| 0.573                      | 0.026             | High Risk            |
| 914.925                    | 0.991             | High Risk            |

---

### 📋 DataFrame Summary

```python
# Check structure, data types, and non-null counts
df.info()
```

- 23 columns, all non-null  
- Data types: `float64`, `datetime64`, `object`  
- Categorical of interest: `risk_classification`

---

### 📊 Descriptive Statistics Summary

```python
# Generate basic statistics for numerical columns
df.describe()
```

| Metric                   | Mean  | Std Dev | Min   | 25%   | 50%   | 75%   | Max-|
|--------------------------|-------|---------|-------|-------|-------|-------|-----|
| eta_variation_hours      | 2.89  | 2.27    | -2.00 | 1.19  | 3.88  | 4.88  | 5.00|
| delay_probability        | 0.70  | 0.32    | 0.00  | 0.46  | 0.84  | 0.98  | 1.00|
| delivery_time_deviation  | 5.18  | 4.16    | -2.00 | 1.27  | 6.11  | 9.25  | 10.0|

---

### ✅ Summary

- Distributions are non-normal with noticeable outliers  
- Risk classification is imbalanced toward "High Risk"  
- This EDA was read-only — no data was modified or used for modeling

---
