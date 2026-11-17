# Automated Sales Reporting Using Power Query

An Excel-based sales reporting project demonstrating data integration, cleaning, transformation, validation, and visualization using Microsoft Power Query, PivotTables, and PivotCharts.

![Sales Performance Dashboard](screenshots/DASHBOARD%20SCREENSHOT.png)

## Project Overview

This project simulates a retail company's monthly sales reporting workflow. Sales transactions are stored across multiple CSV files, while product and store information is maintained in separate reference tables.

The objective is to build a repeatable data preparation workflow and an Excel dashboard that summarizes verified sales performance.

**Note:** All data used in this project is synthetic and does not represent actual company operations.

## Tools & Technologies

- Microsoft Excel
- Power Query (ETL)
- Power Query M Language
- PivotTables and PivotCharts
- GitHub

## Dataset

The dataset covers January–June 2026.

| Data Source | Description |
|---|---|
| Monthly Sales | 6 CSV files containing 732 raw records |
| Products | 8 product reference records |
| Stores | 4 store reference records |
| Cleaned Sales | 720 unique transactions after deduplication |

The dataset contains intentional quality issues, including duplicated transactions and missing values, to demonstrate data cleaning and validation.

## ETL Workflow

### 1. Data Extraction and Consolidation

Imported six monthly sales CSV files using Power Query's **From Folder** feature.

The files were combined into a single query to provide a consolidated sales dataset.

### 2. Data Cleaning

Removed 12 duplicate records based on `Transaction_ID`, reducing the dataset from 732 raw records to 720 unique transactions.

### 3. Data Integration

Performed Left Outer Joins to enrich sales transactions with information from two reference tables:

- `products.csv`: Product names, categories, and list prices.
- `stores.csv`: City and region information.

### 4. Data Validation

Created a custom `Data_Status` column using conditional logic in Power Query M.

The validation checks for:

- Missing or invalid quantities
- Missing or negative unit prices
- Unmatched product references
- Unmatched store references

Transactions with detected issues are retained and flagged instead of being automatically deleted.

### 5. Sales Calculation

Created a calculated column named `Total_Sales_IDR`.

```powerquery
if [Data_Status] = "Valid"
then [Quantity] * [Unit_Price_IDR]
else null
```

Only transactions passing the validation rules contribute to verified sales revenue.

### 6. Data Visualization

Loaded the transformed data into Microsoft Excel and built a dashboard using PivotTables and PivotCharts.

## Dashboard & Key Findings

The dashboard includes three visualizations:

- Monthly Sales Revenue
- Sales Revenue by Product Category
- Sales Revenue by City

### Summary

| Metric | Result |
|---|---|
| Verified Sales Revenue | IDR 1,331,250,000 |
| Unique Transactions | 720 |
| Highest Revenue Month | April 2026 |
| April Revenue | IDR 246,425,000 |
| Highest Revenue Category | Display |
| Display Revenue | IDR 574,000,000 |
| Highest Revenue City | Surabaya |
| Surabaya Revenue | IDR 387,060,000 |

### Insights

**Monthly Performance:** Revenue decreased from January through March before recovering in April. April recorded the highest revenue during the six-month period.

**Product Performance:** Display products contributed approximately 43.1% of verified revenue, making them the largest revenue-generating category.

**Geographic Performance:** Surabaya recorded the highest verified sales revenue at approximately IDR 387.06 million, followed by Jakarta.

These findings are illustrative because the dataset is synthetic.

## Repository Structure

```text
automated-sales-reporting-power-query/
├── data/
│   ├── monthly_sales/
│   │   ├── sales_2026_01.csv
│   │   ├── sales_2026_02.csv
│   │   ├── sales_2026_03.csv
│   │   ├── sales_2026_04.csv
│   │   ├── sales_2026_05.csv
│   │   └── sales_2026_06.csv
│   ├── products.csv
│   └── stores.csv
├── workbook/
│   └── Automated_Sales_Reporting.xlsx
├── screenshots/
│   └── dashboard.png
└── README.md
```

## How to Use

1. Download or clone this repository.
2. Open `workbook/Automated_Sales_Reporting.xlsx` in Microsoft Excel with Power Query support.
3. Open **Data > Queries & Connections** to inspect the existing queries.
4. Update the source paths in Power Query to match the local locations of the CSV files.
5. Refresh the Power Query queries to reload and transform the source data.
6. Refresh the PivotTables to update the dashboard.

The workbook uses locally referenced CSV files, so the data source paths must be adjusted when opening the project on another computer.

## Learning Outcomes

Through this project, I practiced:

- Combining multiple CSV files using Power Query
- Data cleaning and duplicate removal
- Integrating reference data with Left Outer Joins
- Data quality validation using conditional logic
- Writing basic Power Query M expressions
- Building Excel PivotTables and PivotCharts
- Creating a sales performance dashboard

## Future Improvements

- Implement automated refresh scheduling
- Add interactive dashboard slicers
- Expand data quality reporting
- Incorporate additional reporting metrics
- Explore Power BI for more advanced business intelligence reporting

---

**Project Type:** Personal Portfolio Project  
**Dataset:** Synthetic Retail Sales Data  
**Tools:** Microsoft Excel, Power Query
