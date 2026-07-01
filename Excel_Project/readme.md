# TPC-H Analysis with Pivot Tables and Charts

## Analysis 1: Revenue Trend Analysis
Data Source: monthly_revenue

Pivot Table:

•	Rows: Year, Month

•	Values: Sum of Revenue

Chart: Line chart showing monthly revenue trend

## Analysis 2: Revenue by Region
Data Source: monthly_revenue

Pivot Table:

•	Rows: Region

•	Values: Sum of Revenue

Chart: Pie or Donut chart

## Analysis 3: Top 10 Customers
Data Source: customer_summary

Pivot Table:

•	Rows: Customer_Name

•	Values: Sum of Total_Revenue

•	Filter: Right-click on Customer_Name → Value Filters → Top 10

Chart: Horizontal bar chart

## Analysis 4: Revenue by Customer Segment
Data Source: customer_summary

Pivot Table:

•	Rows: Market_Segment

•	Values: Sum of Total_Revenue

Chart: Column chart

## Analysis 5: Product Type Performance
Data Source: product_summary

Pivot Table:

•	Rows: Product_Type

•	Values: Sum of Total_Revenue, Sum of Quantity_Sold

Chart: Column chart showing revenue by product type

## Analysis 6: Top 15 Suppliers
Data Source: supplier_summary

Pivot Table:

•	Rows: Supplier_Name, Nation

•	Values: Sum of Total_Revenue, Sum of Part_Count

•	Filter: Right-click on Supplier_Name → Value Filters → Top 10 (change to 15)

