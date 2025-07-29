# 📊 Vendor Performance Analytics Project

This project is designed to analyze and optimize vendor performance based on historical purchase data, inventory movements, and invoice validations. It combines **data engineering**, **Python scripting + SQLlite**, **Power BI Dashboard,  Business Insight Reporting**, and **exploratory data analysis (EDA)** to produce a clear vendor efficiency dashboard.

> **Note**: `Sales.csv & Purchases.csv` is > 1GB and excluded from GitHub.
---

## 🎯 Project Goals

- Ingest and preprocess raw inventory and purchase data.
- Detect inconsistencies in vendor invoicing.
- Analyze inventory inflow/outflow patterns.
- Generate visual dashboards for vendor evaluation.
- Identify high-performing vendors and cost leakages.

--
## 📁 Folder & File Structure

```
Vendor Performance Project/
├── 01_data/                   # Raw input datasets (CSV)
├── 02_logs/                   # Logging & intermediate outputs
├── .ipynb_checkpoints/        # Auto-saved notebook versions
├── Exploratory Data Analysis.ipynb   # Visual data insights
├── Inventory_db.ipynb         # Inventory-specific analysis
├── get_vendor_summary.py      # Summary script for vendors
├── ingestion_db.py            # Data ingestion pipeline
├── vendor_performance.pbix    # Power BI dashboard file
├── README.md                  # Project documentation
└── .gitignore                 # Files/folders excluded from Git
```



---

## 🔁 Workflow Overview

### 1️⃣ Data Ingestion (`ingestion_db.py`)
- Reads multiple raw datasets: inventory, vendor purchases, prices, invoices.
- Cleans nulls, removes duplicates.
- Validates schema and logs status in `02_logs/`.

### 2️⃣ Data Transformation (`get_vendor_summary.py`)
- Merges and aggregates data by:
  - Vendor
  - Invoice correctness
  - Purchase quantity/value
- Generates structured output tables for dashboard integration.

### 3️⃣ Exploratory Data Analysis (`Exploratory Data Analysis.ipynb`)
- Plots trends:
  - Purchase volume by vendor
  - Price variation across periods
  - Inventory flow vs. demand
- Visuals created using `matplotlib`, `seaborn`.

### 4️⃣ Inventory Deep Dive (`Inventory_db.ipynb`)
- Calculates:
  - Inventory changes over time
  - Overstock/understock patterns
- Compares `begin_inventory` vs `end_inventory`.

### 5️⃣ Power BI Dashboard (`vendor_performance.pbix`)
- Visual representation of:
  - Top vendors by volume/value
  - Average purchase price
  - Invoice correctness %
  - Time series trends

---

### Data Ingestion: Dataframe to Database
- The project includes a dedicated ingestion pipeline that automates the process of loading CSV data into a structured relational database for further analysis and reporting.
- Script: ingestion_db.py
  This script performs the following:
   -Connects to SQLite Database
   -Creates or connects to inventory.db.
   -All tables are created if they don’t exist already.
-Reads Data from CSV Files
  -Located in the 01_data/ folder.
-Reads multiple CSVs: vendors.csv, invoices.csv, purchases.csv, etc.
-Cleans & Validates Data & Removes duplicates.
  -Handles missing values where appropriate.
-Formats columns (e.g., date parsing, data types).
-Creates Tables
  -Uses pandas.DataFrame.to_sql() to load data.





## 🧾 Input Datasets (in `01_data/`)

| File Name              | Description                          |
|------------------------|--------------------------------------|
| `begin_inventory.csv`  | Starting stock levels by product     |
| `end_inventory.csv`    | Ending stock levels                  |
| `purchase_prices.csv`  | Item-wise vendor pricing             |
| `purchases.csv`        | Main transaction dataset (large)     |
| `vendor_invoice.csv`   | Vendor billing and invoice details   |

> **Note**: `purchases.csv  `Sales.csv ` `is >1GB and excluded from GitHub.
---

## 📈 Statistical Analysis & Hypothesis Testing

As part of our **Vendor Performance Analytics**, statistical methods were employed to validate assumptions and provide data-driven insights into vendor behavior, pricing differences, and invoice reliability. These techniques ensure that decisions are **objective**, **quantifiable**, and **auditable**.

---

### 🎯 Objectives
- Determine whether different vendors charge significantly different prices.
- Identify if invoice discrepancies are more frequent with specific vendors.
- Statistically validate patterns observed in the exploratory data analysis.

---

### 1️⃣ T-Test: Comparing Vendor Prices

An **Independent Samples T-Test** was used to compare the average product prices between two vendors (e.g., *Vendor A* and *Vendor B*).

#### 🔬 Hypotheses

- **H₀ (Null Hypothesis):** There is **no significant difference** in average prices between vendors.  
- **H₁ (Alternative Hypothesis):** There **is a significant difference** in average prices between vendors.

> If the **p-value < 0.05**, the null hypothesis is rejected, indicating that the pricing difference between vendors is **statistically significant**.

---

These tests contribute to more accurate **vendor selection**, **cost optimization**, and **invoice auditing** in a business intelligence context.




