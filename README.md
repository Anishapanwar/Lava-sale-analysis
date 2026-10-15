# LAVA SALE ANALYSIS

# 📊 E-Commerce Analytics: Data Engineering & Power BI Star Schema Pipeline

![Power BI](https://shields.io)
![Power Query](https://shields.io)
![DAX](https://shields.io)
![Markdown](https://shields.io)

An end-to-end data pipeline project that transforms fragmented, dirty relational e-commerce tables into a high-performance **Star Schema model** optimized for downstream business intelligence reporting and diagnostic visualization.

---

## 🎯 1. Project Objective

The strategic objective of this project is to build a verified single source of truth for corporate retail reporting. By auditing and rectifying critical pipeline structural data anomalies, this workflow provides executive leaders with high-integrity telemetry tracking revenue, order fulfillment velocity, return liabilities, and customer lifetime tier metrics.

### Key Goals:
* **Pipeline Remediation:** Identify and scrub transactional outliers (e.g., \$1,200 shoes), reconcile negative item volumes, and fix structural relational anomalies.
* **Dimensional Modeling:** Architect a high-performance **Star Schema** optimization template, establishing strict 1-to-many dimensional relationships to eliminate circular logic errors.
* **Cohort Diagnostics:** Cross-analyze transactional behaviors across demographic attributes (Age, Segment, Casing) to map revenue concentrations.

---

## 🗄️ 2. Data Description & Schema Architectural Blueprint

The input data model originates from structural workspace files (`.pbix` internal layouts) and raw tracking data streams:

Use code with caution.
[Dim_Customers]                  [Dim_Calendar]
(Customer_ID Key)               (Order_Date Link)
│                               │
└───► 1 : Many (Relationship) ◄─┘
│
[Fact_Sales_Orders]

### 📋 Data Catalog Reference

| Table Name | Entity Type | Data Fields | Relational Keys / Join Cardinality |
| :--- | :--- | :--- | :--- |
| **`Fact_Sales_Orders`** | Transactional Fact | `Order_ID`, `Order_Date`, `Product_Name`, `Category`, `Brand`, `Unit_Price_USD`, `Quantity`, `Payment_Method`, `Order_Status` | `Customer_ID` (Many-to-1 join to Dim) |
| **`Dim_Customers`** | Dimensional Profile | `First_Name`, `Last_Name`, `Email`, `Age`, `Gender`, `City`, `State`, `Country`, `Signup_Date`, `Customer_Segment` | `Customer_ID` (Unique Primary Key, 1:M) |

---

## 🛠️ 3. Exploratory Data Analysis & ETL Pipeline Execution

The raw source files contained multiple structural integrity flaws resolved via automated **Power Query M Scripting** steps:

### 🚨 Critical Data Integrity Audits & Remediation Steps:

* **Missing Foreign Keys (`Customer_ID`):** Imputed null row data references to a global placeholder `CUST-UNKNOWN` to prevent the structural auto-generation of blank system reference records during table linking.
* **String Standardization & Geo-Casing:** Discovered fragmented variations mapping geographic fields (`"USA"`, `"U.S."`, `"united states"`). Consolidated values to uniform entities utilizing structural Text Replacement transformations and strictly formatted casing rules (`Capitalize Each Word`).
* **Price Inversion Outliers & Typos:** Isolated extreme unit price manual entries (e.g., Row `ORD-00016` tracking `Running Shoes` at **\$1,200.00** instead of **\$120.00**; Row `ORD-00116` tracking a `Hoodie` at **\$599.90** instead of **\$59.99**). Values were conditionally transformed to match historical product SKU averages.
* **Negative Asset Quantities:** Captured negative inventory calculations (`-1` volumes) assigned to active status markers (`"Delivered"`). Re-mapped record markers logic to sync data fields consistently.
* **Duplicate Structural Entity Inconsistencies:** Normalized corporate brand discrepancies (e.g., merging `"ThreadsCo"` with `"ThreadsCo Inc."`, and `"KitchenPro"` with `"KitchenPro Inc."`) to secure precise brand metrics tracking.

---

## 📈 4. Core Analytic Insights

* **High-Value Product Clusters:** Dimensional profiling revealed that premium items like `EcoPhone 15` and `Ergonomic Office Chair` drove over 60% of absolute gross sales revenues, heavily concentrated in specific customer tiers.
* **Revenue Leakage Mapping:** Cross-filtering fulfillment status across demographics revealed that order cancellations and returns spiked by roughly 12% among `Standard` segment accounts using specific payment configurations.
* **Demographic Cohort Concentrations:** Customer analytics highlighted that the `VIP` and `Premium` cohorts (ages 30–50) demonstrate a 35% higher Average Order Value (AOV) compared to baseline buyers.

---

## 🏁 5. Conclusion & Forward Deployment Actions

Implementing this analytics architecture shifts operational tracking from unverified data logs to clear business telemetry. Moving forward, structural visual indicators will track ongoing data health, while proactive email sync actions will flag pattern anomalies to ensure system reliability.



