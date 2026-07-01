## Page 1: Executive Summary
Purpose: High-level KPIs and trends for executives

Required Visualizations:

-	Four KPI Cards: Display Total Revenue, Total Orders, Average Order Value, and Total Quantity Sold

-	Revenue Trend Line Chart: Monthly revenue over time (use ORDERS[O_ORDERDATE])

-	Top 10 Customers Bar Chart: Show revenue by customer name (horizontal bars preferred)

-	Revenue by Region Donut Chart: Show geographic distribution of sales

-	Global Slicers: Add slicers for Year (from O_ORDERDATE) and Region that filter all pages

## Page 2: Product Analysis
Purpose: Detailed product performance metrics

Required Visualizations:

-	Product Performance Table: Show Part Name, Total Revenue, Quantity Sold, and Average Price (use conditional formatting for top/bottom performers)

-	Revenue by Product Type Column Chart: Use PART[P_TYPE] field

-	Quantity vs. Revenue Scatter Plot: X-axis: Quantity Sold, Y-axis: Revenue, Size: Number of Orders, by Part Name

-	Top 5 Parts by Revenue Card: Show top 5 product names with revenue

-	Page-Level Slicer: Add a slicer for Product Type (P_TYPE) that only filters this page

## Page 3: Customer & Supplier Insights
Purpose: Customer segmentation and supplier performance

Required Visualizations:

-	Customer Segmentation Clustered Column Chart: Revenue by Customer Market Segment (CUSTOMER[C_MKTSEGMENT])

-	Top Suppliers Table: Show Supplier Name, Nation, Total Revenue, Number of Parts Supplied

-	Customer Distribution Map: Filled map or bubble map showing number of customers by country (NATION[N_NAME])

-	Order Priority Breakdown Pie Chart: Show distribution by ORDERS[O_ORDERPRIORITY]

-	Cross-Filtering Setup: Ensure clicking on the map filters other visuals on this page


