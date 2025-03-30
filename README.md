# Power BI: Financial Analysis Report

## Project Overview
This Power BI project provides a financial performance analysis, focusing on key metrics such as Sales, Profit, Discounts, and Profit Margin % for both Current Year (CY) and Prior Year (PY).
The dashboard is designed with interactive filters and drill-throughs, enabling users to analyze regional trends, discount impact, and product-level profitability.
________________________________________
## Dataset & Data Model
The analysis is based on financial transaction data, structured into the following tables:
- Dim_Date – A Date Table was created using CALENDAR DAX, ensuring time intelligence calculations.
- Financial Data – Contains sales transactions, including revenue, cost, discounts, and product details.
- Analysis Table – Holds calculated values for Current Year and Prior Year KPIs.

Data Model Relationships
Financial Data is linked to Dim_Date via Date.
Other relationships ensure time-based trend analysis and product-level insights.
________________________________________
## Key Features
Dynamic KPIs for Current vs Prior Year – Measures year-over-year growth trends.

Top 3 Products by Sales (Prior Year) – Identifies best-selling products dynamically.

Profitability Analysis – Tracks Profit, Profit Margin %, and Discount impact.

Regional & Product-Level Insights – Analyzes performance across countries, segments, and discount bands.
________________________________________
## Visualizations: 
1. KPIs for Current Year (CY) vs Prior Year (PY)
- Sales Amount
- Orders
- Profit
- Profit Margin %
- Discounts Offered

2. Performance Analysis
- Orders by Country – Identifies high-performing regions.
- Profit Margin by Country & Segment – Shows variations in profitability.
- % of Discounts Offered by Discount Band – Highlights discount impact on sales.
- Sales Trend Over Time – Compares monthly performance.

3. Top 3 Products by Sales (PY)
- Identifies best-selling products from the prior year.
- Highlighted in a different color to make them stand out.

## DAX Calculations 
TIME INTELLIGENCE DAX
- Enables to compare KPIs CY to PY

   ```Date Table = ADDCOLUMNS(CALENDARAUTO(), "Month No",MONTH([Date]),"Month name",FORMAT([Date],"MMMM"),"Year",YEAR([Date]))```

FINANCIAL ANALYSIS
1.	Financial Analysis Calculations for Current Year (CY)

```Sales Amount = sum(‘Financial data’[Net Sales])```

```Profit = sum(‘Financial data’[Profit])```

```Orders = sum(‘Financial data’[Unit Sold])```

```Discounts Offered = sum(‘Financial data’[Discounts])```

```Profit Margin % = DIVIDE([Profit], [Sales Amount],0)```

2. Financial Analysis Calculations for Prior Year (PY) were created similarly to the CY
  
3.	Top 3 Products by Sales (PY) - dynamically filters the top 3 products and ensures the selection is interactive and adjusts based on applied slicers.
   
```Top 3 Products by Sales =  CALCULATE([Sales Amount], TOPN(3, ALLSELECTED('Financial data'[Product]),  [Sales Amount], DESC),VALUES('Financial data'[Product]) )``` 

4.	Top Highlight (Conditional Formatting for Top 3 Products)

```Top Highlight =  IF(ISBLANK([Top 3 Products by Sales]), 0, 1)``` 

Purpose: Highlights the Top 3 products in another color using conditional formatting.

## Insights & Findings
1. Sales Performance:
- Sales increased by +249.46% YoY, reaching $92.3M.
- Orders grew by 225.36%, reflecting strong demand.
  
2. Profitability & Discounts:
- Profit Margin declined by -3.97%, indicating a potential impact of increased discounts (up by 229.04%).
- Discount impact varies by discount band, with high-discount segments underperforming in profitability.
  
3. Top 3 Products:
- The best-selling products from the prior year are dynamically identified.
- Highlighting helps compare their contribution to overall sales trends.

![Screenshot (37)](https://github.com/user-attachments/assets/b1f0eaaa-3248-40aa-954d-7e1e71fa6969)
