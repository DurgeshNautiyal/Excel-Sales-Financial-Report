# Excel Sales & Financial Analytics Report

> **Comprehensive Sales & Financial Performance Analysis using Excel Power Tools**

[![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)](https://www.microsoft.com/en-us/microsoft-365/excel)
[![Power Query](https://img.shields.io/badge/Power%20Query-F2C811?style=for-the-badge&logo=power-bi&logoColor=black)](https://docs.microsoft.com/en-us/power-query/)
[![DAX](https://img.shields.io/badge/DAX-FF6F00?style=for-the-badge&logo=power-bi&logoColor=white)](https://docs.microsoft.com/en-us/dax/)

![Report Demo](assets/report_demo.gif)

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

## Report Preview

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

#### 1. Date Range Generation
```m
= List.Dates(#date(2018, 09, 01), 1100, #duration(1, 0, 0, 0))
```

#### 2. Custom Fiscal Year Logic
```m
= if Date.Month([date]) >= 8 
  then "FY " & Text.From(Date.Year([date])+1) 
  else "FY " & Text.From(Date.Year([date]))
```
### **DAX calculated column**

#### Date Table **`dim_date`**

##### 1. Fiscal Month Number
```dax
= MOD(
	MONTH(dim_date[Date]) - 8,
	12
	)
	+ 1
```

##### 2. Fiscal Month Name
```dax
= SWITCH( 
    dim_date[Fiscal Month Number],
    1, "Aug",
    2, "Sep",
    3, "Oct",
    4, "Nov",
    5, "Dec",
    6, "Jan",
    7, "Feb",
    8, "Mar",
    9, "Apr",
    10, "May",
    11, "Jun",
    12, "Jul"
)
```

##### 3. Fiscal Quarter
```dax
= SWITCH(
	TRUE(),
	MONTH(dim_date[Date]) IN {8, 9, 10}, "Q1",
	MONTH(dim_date[Date]) IN {11, 12, 1}, "Q2",
	MONTH(dim_date[Date]) IN {2, 3, 4}, "Q3",
	MONTH(dim_date[Date]) IN {5, 6, 7}, "Q4"
	)
```
### **DAX Measures**

#### Financial Metrics

##### 1. Net Sales
```dax
Net Sales = SUM(fact_sales_monthly[Net Sales Amount])
```

##### 2. COGS
```dax
COGS = SUM(fact_sales_monthly[Freight Cost]) + 
       SUM(fact_sales_monthly[Manufacturing Cost])
```

##### 3. Gross Margin
```dax
Gross Margin = [Net Sales] - [COGS]
```

##### 4. Gross Margin %
```dax
Gross Margin % = DIVIDE([Gross Margin], [Net Sales], 0)
```

#### Growth Analytics

##### 1. Net Sales Last Year
```dax
Net Sales LY = CALCULATE([Net Sales], SAMEPERIODLASTYEAR(dim_date[Date]))
```

##### 2. Net Sales Change
```dax
Net Sales Change = [Net Sales] - [Net Sales LY]
```

##### 3. % Growth
```dax
% Growth = DIVIDE([Net Sales Change], [Net Sales LY], 0)
```

#### Target Analysis

##### 1. Target 2021
```dax
Target 2021 = SUM(fact_ns_targets_2021[Net Sales Target])
```

##### 2. 2021 vs Target
```dax
2021 vs Target = [2021] - [Target 2021]
```

## **Technology Stack**

| Tool | Purpose | Features Used |
|------|---------|---------------|
| **Excel** | Primary Platform | Pivot Tables, Conditional Formatting |
| **Power Query** | Data Transformation | ETL, Data Cleaning, Custom Columns |
| **Power Pivot** | Data Modeling | Relationships, Calculated Columns |
| **DAX** | Business Logic | Time Intelligence, Calculations |

## Insights

### 1. **P & L Fiscal Year**

- Strong Revenue Growth in India.
- Net Sales increased steadily:
  - From ₹ 2.87 Cr in FY19 → ₹ 4.79 Cr in FY20 → ₹ 15.42 Cr in FY21.
  - 5.37x growth over 3 years, showing aggressive expansion.
- **FY 2021** alone saw **222% growth** from **FY 2020**, indicating a **breakout year**.

### 2. **Seasonal Trends**

- **Revenue Growth Trend for FY 2021**
  - Net Sales started low in August (₹1.65 Cr) and rapidly increased to a peak in December (₹7.81 Cr).
    - **Peak Month:** December FY21 (₹7.81 Cr)
    - **Growth Pattern:** Strong Q2 performance (Oct-Dec)
  - From Jan to Jul, Net Sales remained stable around ₹4.40–₹4.48 Cr.
  - **Insight:** Strong sales momentum in Q2 (Oct–Dec), especially December, suggests a festive or seasonal sales spike — possibly due to Diwali, holiday promotions, or year-end buying cycles.
    - **Opportunity:** Leverage festive season strategies

### 3. **Market Performance vs. Target**

#### Performance Table

| Country       | 2019      | 2020      | 2021       | 2021 - Target 2021 | %        |
|---------------|-----------|-----------|------------|--------------------|----------|
| Canada        | ₹0.44 Cr  | ₹1.14 Cr  | ₹3.34 Cr   | -₹0.67 Cr          | -16.81%  |
| India         | ₹2.87 Cr  | ₹4.79 Cr  | ₹15.42 Cr  | -₹1.66 Cr          | -9.73%   |
| Philippines   | ₹0.52 Cr  | ₹1.26 Cr  | ₹3.07 Cr   | -₹0.37 Cr          | -10.67%  |
| South Korea   | ₹1.17 Cr  | ₹1.65 Cr  | ₹4.67 Cr   | -₹0.66 Cr          | -12.40%  |
| USA           | ₹1.08 Cr  | ₹3.04 Cr  | ₹8.43 Cr   | -₹1.38 Cr          | -14.04%  |
| **Grand Total** | **₹6.08 Cr** | **₹11.88 Cr** | **₹34.92 Cr** | **-₹4.74 Cr**         | **-11.95%** |

- **Overall Shortfall**: All countries ended up below their market targets for **2021**, with a cumulative shortfall of **₹4.74 Cr**, representing an overall underperformance of **-11.95%**.
- **Best Relative Performance**: **India** had the **smallest negative deviation** from the target at **-9.73%**.
- **Largest Decline**: **Canada** witnessed the **highest shortfall** relative to its target at **-16.81%**.
- **Growth Trend**: Despite missing targets, there was robust sales growth across **all markets** from **2019 to 2021**, with sizable jumps notably in **India** and the **USA**.
- **Targets Missed in All Markets**
  - **Challenge:** All markets missed FY21 targets
  - **Action Required:** Reassess forecasting methodology

### 4. **Net Sales Insights – India**

#### (a). Key Observations

- **Significant Growth Trend**: Net sales in India show a strong upward trend over the three fiscal years analyzed.
- **FY 2019 Baseline**: Sales started at ₹2.87Cr in FY 2019, which serves as the base year for comparison.
- **FY 2020 Growth**: Net sales increased to ₹4.79Cr, a rise of ₹1.92Cr, representing a **66.89% growth** over the previous year.
- **FY 2021 Surge**: Net sales surged to ₹15.42Cr, a substantial jump of ₹10.63Cr and a **221.80% growth** over FY 2020.

#### (b). Summary Table

| Fiscal Year | Net Sales   | YoY Growth (%) | Change (₹ Cr) |
|-------------|-------------|---------------|---------------|
| FY 2019     | ₹2.87Cr     | 0.00          | —             |
| FY 2020     | ₹4.79Cr     | 66.89         | +₹1.92Cr      |
| FY 2021     | ₹15.42Cr    | 221.80        | +₹10.63Cr     |

#### (c). Interpretations

- The **market in India is experiencing exponential net sales growth**. The increase from FY 2020 to FY 2021 far outpaces the previous year’s percentage and absolute rise.
- **FY 2021 marks a pivotal acceleration**—the growth rate more than tripled compared to FY 2020, indicating possible entry into a high-growth phase, successful business strategies, or favorable market conditions.

#### (d). Actionable Insights

- **Sustain Momentum**: Leverage the factors contributing to this high growth and identify any replicable strategies.
- **Monitor Drivers**: Analyze underlying causes for the FY 2021 surge (e.g., market expansion, product launches, policy changes).
- **Future Planning**: Prepare for scaling operations and managing rapid growth risks as such aggressive increases can strain resources.

#### Conclusion

 - The data highlights **India as a rapidly expanding market** with extraordinary year-on-year sales increases from FY 2019 to FY 2021. This momentum presents significant opportunities but also calls for strategic actions to sustain and capitalize on the growth trajectory.

### 5. **Net Sales Performance Insights – India**

#### (a). Significant Net Sales Growth

- **Total Net Sales** increased from ₹2.87Cr in 2019 to ₹15.42Cr in 2021.
- The **overall growth rate** (2021 vs. 2020) is an impressive **321.80%**.

#### (b). Top-Performing Customers by Growth (2021 vs. 2020)

| Customer             | 2021 Net Sales | Growth Rate vs 2020 |
|----------------------|---------------|---------------------|
| Electricalsytical    | ₹0.84Cr       | 431.14%             |
| Girias               | ₹0.82Cr       | 428.76%             |
| Electricalsociety    | ₹0.88Cr       | 407.02%             |
| Propel               | ₹0.85Cr       | 416.47%             |
| AtliQ Exclusive      | ₹1.79Cr       | 395.23%             |

- These customers have growth rates well above the overall average, indicating strong sales expansion.

#### (c). Largest Absolute Sales Contributors (2021)

| Customer             | 2021 Net Sales |
|----------------------|----------------|
| Amazon               | ₹2.17Cr        |
| AtliQ Exclusive      | ₹1.79Cr        |
| Flipkart             | ₹0.99Cr        |
| Expression           | ₹0.82Cr        |
| Reliance Digital     | ₹0.85Cr        |

- Amazon and AtliQ Exclusive together contributed over ₹3.9Cr, reinforcing their status as leading channels.

#### (d). Broad-Based Acceleration

- Every listed customer experienced a **minimum growth of 230% year-on-year**, emphasizing strong, broad-based market acceleration.
- Traditional retail and large-format stores (e.g., Croma, Flipkart, Reliance Digital, Viveks) also saw robust gains or more than tripled their net sales from 2020.

#### (e). Market Implications

- The exceptionally high growth rates indicate successful market strategies and possibly increased consumer demand, digital adoption, or improved product-market fit.
- No major customer has stagnated—consistent triple-digit growth is seen across both traditional and online channels.

#### Conclusion

- The Indian market demonstrates outstanding net sales momentum from 2019 to 2021, with universal, high-magnitude growth among all main customers. Leaders like Amazon and AtliQ Exclusive both drive and reflect the market’s dynamism. The data suggests strong market demand, effective distribution expansion, and a favorable environment for further sales growth.

## Getting Started

### **Prerequisites**
- Microsoft Excel 2016 or later
- Power Query Add-in (if using Excel 2010-2013)
- Basic understanding of Excel formulas

## Contact Me

![P and L By Year](assets/pnl_fy_in.png)

**Durgesh Nautiyal**
- LinkedIn: [My LinkedIn Profile](https://www.linkedin.com/in/durgesh-nautiyal-95a866223/)
- Email: durgeshnautiyal11@gmail.com
