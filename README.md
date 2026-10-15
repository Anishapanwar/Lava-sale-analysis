# LAVA SALE ANALYSIS
# 📊 Advanced E-Commerce Analytics: Multi-Source Data Pipeline & Power BI Star Schema

![Power BI](https://shields.io)
![Power Query](https://shields.io)
![DAX](https://shields.io)
![Markdown](https://shields.io)

An end-to-end data engineering and business intelligence project that transforms dirty, unnormalized flat files spanning customer demographics, localized product catalogs, order headers, and line-item transactional logs into a optimized, relational **Star Schema model** designed for rapid reporting.

---

## 🎯 1. Project Objective

The core objective of this project is to build a reliable, high-performance analytical pipeline that unifies disparate operational data streams into a single source of truth. By executing automated exploratory data analysis (EDA) and data cleansing inside Power Query, the pipeline remedies data-entry errors, structural anomalies, and text variations. The end-to-end data model equips retail business managers with clear financial telemetry into gross revenues, transaction sizes, and local demand vectors.

---

## 🗄️ 2. Data Description & Schema Architecture

The relational ecosystem ingests data across four flat source streams, separating high-velocity transactional facts from dimensional profiles.

### 🧩 Relational Star Schema Blueprint
To maximize Query Folding and eliminate circular dependency errors, the flat datasets are decomposed into a multi-tiered Star Schema model:

```text
    [Dim_Customers]                  [Dim_Products]                  [Dim_Calendar]
    (customer_id Key)                (product_id Key)               (order_date Link)
           │                                │                                │
           └───► 1 : * (Many) ◄─────────────┼────────────────────────────────┘
                         │                  │
                 [Fact_Order_Header]        │
                 (order_id Primary Key)     │
                         │                  │
                         └───► 1 : * ◄──────┘
                                 │
                         [Fact_Order_Items]
```

### 📋 Data Catalog Reference

| Table Name | Entity Type | Attributes & Schema Mapping | Relational Join Keys / Cardinality |
| :--- | :--- | :--- | :--- |
| **`Fact_Order_Header`** | Transactional Fact | `order_id`, `customer_id`, `order_date`, `payment_method` | `customer_id` (Many-to-1 join to Dim_Customers) |
| **`Fact_Order_Items`** | Transactional Fact | `order_item_id`, `order_id`, `product_id`, `quantity`, `unit_price` | `order_id` (Many-to-1 join to Fact_Order_Header)<br>`product_id` (Many-to-1 join to Dim_Products) |
| **`Dim_Customers`** | Dimensional Profile | `customer_id`, `customer_name`, `city`, `signup_date` | `customer_id` (Unique Primary Key, 1:M) |
| **`Dim_Products`** | Dimensional Profile | `product_id`, `product_name`, `category`, `base_price` | `product_id` (Unique Primary Key, 1:M) |

---

## 🛠️ 3. Data Cleansing & ETL Transformation Pipeline

The exploratory data analysis exposed several critical data anomalies that were successfully resolved inside Power Query using automated **M Scripting**:

### 🚨 Critical Vulnerabilities Audited & Remediation Protocols:

* **Geographic Casing & City Standardizations:** Identified widespread structural duplications in regional dimensions (e.g., text entries matching `"DELHI"`, `"delhi"`, and `"Delhi"`; alongside regional string anomalies such as `"Bangalore"` vs. `"Bengaluru"`). Reconciled utilizing localized text replacements and applied absolute word casing transformations (`Capitalize Each Word`).
* **Categorical Imputations & Missing Attributes:** Addressed empty rows and unmapped metadata constraints (e.g., missing product classifications for `P003` and misallocated item segments where tablets were tagged as a `"Smartphone"`). Imputed empty cells with uniform system fallbacks to prevent `(Blank)` visual grouping anomalies.
* **Pricing Scale Restructuring:** Resolved critical decimal-point omission errors where transaction items showed inflated integer scales (e.g., item values listed at `77415` instead of `774.15`). Fixed by applying data type verification and adding a global scaling divisor inside Power Query.
* **Null Dimensional Keys:** Sanitized anonymous checkout logs with absent user strings by binding empty foreign keys to a default master record string (`"CUST-UNKNOWN"`), preserving structural integrity across relational model borders.

---

## 📈 4. Core Analytical DAX Expressions

The semantic model calculates core metrics using explicit, high-efficiency Data Analysis Expressions (DAX) to optimize resource consumption:

### Gross Revenue Generation Tracker
```dax
Total Gross Sales = 
SUMX(
    'Fact_Order_Items',
    'Fact_Order_Items'[quantity] * 'Fact_Order_Items'[unit_price]
)
```

### Volumetric Unit Volume Monitor
```dax
Total Units Sold = SUM('Fact_Order_Items'[quantity])
```

### Average Basket Value Evaluator (AOV)
```dax
Average Order Value (AOV) = 
DIVIDE(
    [Total Gross Sales],
    DISTINCTCOUNT('Fact_Order_Header'[order_id]),
    0
)
```

---

## 🏁 5. Project Conclusion & Delivery Outcomes

Transitioning the data pipeline from loosely connected flat tables into a strict Star Schema provides structural analytical trust. Downstream dashboards can seamlessly slice regional metrics without data skewing, financial aggregations accurately capture real transactional value, and performance remains optimized under query expansion.

---




