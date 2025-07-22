# Excel Sales & Financial Analytics Dashboard

> **Comprehensive Sales & Financial Performance Analysis using Excel Power Tools**

[![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)](https://www.microsoft.com/en-us/microsoft-365/excel)
[![Power Query](https://img.shields.io/badge/Power%20Query-F2C811?style=for-the-badge&logo=power-bi&logoColor=black)](https://docs.microsoft.com/en-us/power-query/)
[![DAX](https://img.shields.io/badge/DAX-FF6F00?style=for-the-badge&logo=power-bi&logoColor=white)](https://docs.microsoft.com/en-us/dax/)

## Project Overview

This project delivers a comprehensive **Sales & Financial Analytics Dashboard** for AtliQ Hardware, transforming raw transactional data into actionable business insights. Built entirely in Excel using advanced analytics tools, it provides stakeholders with clear visibility into sales performance, market trends, and financial metrics.

### About AtliQ Hardware

AtliQ Hardware is a leading electronics manufacturer specializing in:
- Personal computers and peripherals
- Mice, printers, and accessories
- Consumer electronics

**Distribution Channels:**
- **Retail Partners:** Croma, Best Buy, and other brick-and-mortar stores
- **E-commerce Platforms:** Amazon, Flipkart, and online marketplaces

## Dashboard Preview

### Interactive Demo
![Dashboard Demo](assets/report_demo.gif)

### Report Screenshots

| Report Type | Preview |
|-------------|---------|
| **P&L Fiscal Year Overview** | ![P&L Fiscal Year](assets/pnl_fiscal_year.jpg) |
| **Monthly P&L Analysis** | ![P&L By Month](assets/pnl_by_month.jpg) |
| **Net Sales Comparison** | ![Net Sales Comparison](assets/net_sales_comparison.jpg) |
| **Market vs Target Performance** | ![Market vs Target](assets/market_vs_target.jpg) |
| **Customer Performance (Page 1)** | ![Customer Performance 1](assets/customer_perf_1.jpg) |
| **Customer Performance (Page 2)** | ![Customer Performance 2](assets/customer_perf_2.jpg) |
| **Data Model Relationships** | ![Data Model](assets/data_model.png) |

## Business Problem

AtliQ Hardware faced challenges with:
- **Manual Reporting:** Time-consuming, error-prone financial reports
- **Scattered Data:** Multiple data sources without centralized analysis
- **Limited Insights:** Lack of actionable business intelligence
- **Performance Tracking:** No systematic way to monitor sales targets vs. actuals

## Solution Delivered

A comprehensive Excel-based analytics solution featuring:
- **ETL Pipeline** using Power Query
- **Interactive Report** with filtering
- **Custom Financial Calendar** aligned with business needs
- **Advanced Calculations** using DAX measures
- **Multi-dimensional Analysis** across time, geography, and customers

## Dataset Information

| Attribute | Details |
|-----------|---------|
| **Total Records** | 799,962 transactions |
| **Time Period** | FY 2019 - FY 2021 |
| **Markets Covered** | Multiple countries including India, USA, Canada, Etc. |
| **Product Categories** | PCs, Peripherals, Accessories |

### Data Sources

1. **`fact_sales_monthly`** - Core sales transactions
2. **`fact_ns_targets_2021`** - Sales targets for FY 2021
3. **`dim_customer`** - Customer master data
4. **`dim_market`** - Market/geography information
5. **`dim_product`** - Product catalog
6. **`dim_date`** - Custom fiscal calendar

## Technical Implementation

### **Power Query (ETL)**
```m
// Custom Fiscal Year Logic
= if Date.Month([date]) >= 8 
  then "FY " & Text.From(Date.Year([date])+1) 
  else "FY " & Text.From(Date.Year([date]))

// Date Range Generation
= List.Dates(#date(2018, 09, 01), 1100, #duration(1, 0, 0, 0))
```

### **Key DAX Measures**

#### Financial Metrics
```dax
Net Sales = SUM(fact_sales_monthly[Net Sales Amount])

COGS = SUM(fact_sales_monthly[Freight Cost]) + 
       SUM(fact_sales_monthly[Manufacturing Cost])

Gross Margin = [Net Sales] - [COGS]

Gross Margin % = DIVIDE([Gross Margin], [Net Sales], 0)
```

#### Growth Analytics
```dax
Net Sales LY = CALCULATE([Net Sales], SAMEPERIODLASTYEAR(dim_date[Date]))

Net Sales Change = [Net Sales] - [Net Sales LY]

% Growth = DIVIDE([Net Sales Change], [Net Sales LY], 0)
```

#### Target Analysis
```dax
Target 2021 = SUM(fact_ns_targets_2021[Net Sales Target])

2021 vs Target = [2021] - [Target 2021]

Target Achievement % = DIVIDE([2021 - Target 2021], [Target 2021], 0)
```

### **Technology Stack**

| Tool | Purpose | Features Used |
|------|---------|---------------|
| **Excel** | Primary Platform | Pivot Tables, Conditional Formatting |
| **Power Query** | Data Transformation | ETL, Data Cleaning, Custom Columns |
| **Power Pivot** | Data Modeling | Relationships, Calculated Columns |
| **DAX** | Business Logic | Time Intelligence, Calculations |

## Key Business Insights

### **Explosive Growth Story**
- **Net Sales Growth:** ₹2.87 Cr (FY19) → ₹15.42 Cr (FY21)
- **Growth Multiple:** **5.37x increase** over 3 years
- **FY21 Performance:** **222% YoY growth** - breakthrough year

### **Seasonal Trends**
- **Peak Month:** December FY21 (₹7.81 Cr)
- **Growth Pattern:** Strong Q2 performance (Oct-Dec)
- **Opportunity:** Leverage festive season strategies

### **Market Performance**
- **Top Market:** India (₹15.42 Cr in FY21)
- **Challenge:** All markets missed FY21 targets
- **Action Required:** Reassess forecasting methodology

### **Customer Diversification**
- **India Growth:** 321.8% YoY (₹4.79 Cr → ₹15.42 Cr)
- **Top Contributors:** Amazon, AtliQ Exclusive, Flipkart
- **Risk Mitigation:** No single customer >14% dependency

## Strategic Recommendations

### **Performance Optimization**
1. **Target Setting:** Implement data-driven forecasting models
2. **Market Expansion:** Focus resources on high-growth markets
3. **Seasonal Planning:** Capitalize on Q2 peak performance patterns

### **Analytical Enhancements**
1. **Profitability Analysis:** Deep-dive into product-wise margins
2. **Customer Segmentation:** Develop targeted retention strategies
3. **Competitive Analysis:** Benchmark against industry standards

## Getting Started

### **Prerequisites**
- Microsoft Excel 2016 or later
- Power Query Add-in (if using Excel 2010-2013)
- Basic understanding of Excel formulas

## Author

**Durgesh Nautiyal**
- LinkedIn: [Your LinkedIn Profile](https://linkedin.com/in/your-profile)
- Email: your.email@example.com
