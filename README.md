# Pizza-Sales-Analysis-Project
## Overview: Sales Performance Analysis for Pizza Store
## Problem Statement:
The management team of a pizza store wanted to gain deeper insights into their sales performance. They needed a clear understanding of:
Total revenue trend
Best and worst selling pizzas
Peak order hours
Monthly sales performance
Category and size contribution
However, the sales data was stored in raw transactional format, making it difficult to extract meaningful business insights quickly.
To enable data-driven decision-making, the goal was to build a centralized, interactive dashboard using Power BI that transforms raw data into actionable insights.

## Key Challenges and Solutions:

### Raw Transaction-Level Data
Challenge:
The dataset contained detailed transaction-level records, which made high-level performance tracking difficult.
Solution :Used Power Query to clean and structure the dataset properly for analysis.

### Data Cleaning and Transformation
Challenge:
The dataset required formatting, column adjustments, and validation before analysis.
Solution:
Removed duplicates
Handled missing value
Converted data types correctly
Created calculated columns for better time analysis

### Time-Based Sales Analysis
Challenge:
Management wanted insights by hour, day, and month.
Solution:
Created time-based columns such as:
Day Name
Month
Hour of Order
This enabled time-series analysis.

### Data Preparation with Power Query

The original dataset contained order-level information including:
Order ID,Order Date,Pizza Name,Category,Size,Quantity,Price
# Using Power Query:
Cleaned and formatted data
Created calculated columns
Ensured proper relationships in data model
Structured dataset for efficient DAX calculations

## Metrics Creation Using DAX

After cleaning and modeling the data, I created key business metrics using DAX.

## Key Metrics:
Total Revenue
Total Order
Total Pizzas Sold
Average Order Value
Sales by Category
Sales by Size
Top 5 Best-Selling Pizzas
Bottom 5 Worst-Selling Pizzas
Monthly Sales Trend
Peak Sales Hours

## Sample DAX Formulas:
Total Revenue = SUM(Sales[Total Price])

Total Orders = DISTINCTCOUNT(Sales[Order ID])

Total Pizzas Sold = SUM(Sales[Quantity])

Average Order Value = DIVIDE([Total Revenue], [Total Orders], 0)

Revenue % = DIVIDE( [Total Revenue],
    CALCULATE([Total Revenue], ALL(Sales)),0)

Performance Status =
IF (
    [TOTAL_SALES] > [Average Sales],
    "Good",
    "Poor"
)

Category Contribution % =
DIVIDE (
    [TOTAL_SALES],
    CALCULATE (
        [TOTAL_SALES],
        ALL ( Table1[pizza_category] )
    )
)

Category Rank =
RANKX (
    ALL ( Table1[pizza_category] ),
    [TOTAL_SALES],
    ,
    DESC
)

Overall_sales =
CALCULATE (
    [TOTAL_SALES],
    REMOVEFILTERS ( Table1[pizza_category] )
)

# Time Intelligence Measures

YTD Sales =
TOTALYTD (
    [TOTAL_SALES],
    Table1[order_date]
)

Last_month =
VAR LatestDate =
    MAX ( Table1[order_date] )
RETURN
    CALCULATE (
        SUM ( Table1[total_price] ),
        DATESINPERIOD (
            Table1[order_date],
            LatestDate,
            -1,
            MONTH
        )
    )


weekday = WEEKDAY(Table1[order_date])

WEEKDAY/WEEKEND = IF(OR(Table1[weekday]=2,Table1[weekday]=7),"weekday","weekend")

weeldaysen = FORMAT(Table1[weekday],"DDDD")

 ## Key Insights:

The final dashboard provided actionable insights including:
 Revenue Trend Analysis across months
 Identification of top-performing pizzas
 Peak order hours (business rush time)
 Category-wise and size-wise contribution
 Low-performing items for possible optimization

## Dashboard Preview

<img src="<img width="1326" height="748" alt="Pizza sales Dashboard" src="https://github.com/user-attachments/assets/64724b11-b7b1-4f58-8df3-eff8420ea76c" />
" width="900"/>

## Tools, Software, and Techniques:
Microsoft Excel – Raw data source
Power Query – Data cleaning and transformation
Power BI – Dashboard development
DAX – KPI and metric calculation
Data Modeling – Relationship management

## Business Impact:
Improved visibility into revenue drivers
Identified sales trends and peak business hour
Enabled data-driven inventory and pricing decisions
Supported management with strategic planning insights

## References:
Power BI Documentation: https://learn.microsoft.com/en-us/power-bi/
DAX Guide: https://dax.guide/




 

Hour of Order

This enabled time-series analysis.
