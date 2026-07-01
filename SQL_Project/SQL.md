# TPC-H Data Analysis & Report Validation

## Query 1: Validate Total Revenue

SELECT
	SUM((L_EXTENDEDPRICE) * (1 - L_DISCOUNT )) AS Total_Revenue

FROM LINEITEM;

![imagge alt](https://github.com/mannyshrestha1234-max/Project_TPC-H/blob/48478d706095dd43496c666a299a46f4f7eeff79/assets/Q1.jpg)

## Query 2: Validate Total Orders

SELECT
	COUNT(DISTINCT O_ORDERKEY) AS Total_Orders

FROM ORDERS;

![imagge alt](https://github.com/mannyshrestha1234-max/Project_TPC-H/blob/ed4b71c17ed2e71de55a6a76003acad76a826cd1/assets/q2.jpg)

## Query 3: Validate Average Order Value

WITH OrderTotals AS (
    SELECT 
        l.L_ORDERKEY,
        SUM(l.L_EXTENDEDPRICE * (1 - l.L_DISCOUNT)) AS Total_Revenue

FROM LINEITEM l

GROUP BY l.L_ORDERKEY
)

SELECT 
    SUM(TOTAL_REVENUE) / COUNT(*) AS Average_Order_Value

FROM OrderTotals;

![image alt](https://github.com/mannyshrestha1234-max/Project_TPC-H/blob/7b8534a48a667b68e0bde5cbd03f87b4d3462dbd/assets/q3.jpg)

## Query 4: Validate Top 10 Customers by Revenue

SELECT
	c.C_NAME AS Customer_Name,
	SUM((l.L_EXTENDEDPRICE) * (1 - l.L_DISCOUNT )) AS Total_Revenue

FROM LINEITEM l

JOIN ORDERS o 
	ON l.L_ORDERKEY = o.O_ORDERKEY

JOIN CUSTOMER c 
	ON c.C_CUSTKEY = o.O_CUSTKEY 

GROUP BY c.C_NAME  

ORDER BY Total_Revenue DESC 

LIMIT 10;

![image alt](https://github.com/mannyshrestha1234-max/Project_TPC-H/blob/7b8534a48a667b68e0bde5cbd03f87b4d3462dbd/assets/q4.jpg)

## Query 5: Validate Revenue by Region

SELECT
	r.R_NAME AS Region_Name,
	SUM((l.L_EXTENDEDPRICE) * (1 - l.L_DISCOUNT )) AS Total_Revenue

FROM LINEITEM l

JOIN ORDERS o 
	ON l.L_ORDERKEY = o.O_ORDERKEY

JOIN CUSTOMER c 
	ON c.C_CUSTKEY = o.O_CUSTKEY

JOIN NATION n
	ON n.N_NATIONKEY = c.C_NATIONKEY 

JOIN REGION r
	ON r.R_REGIONKEY = n.N_REGIONKEY 

GROUP BY r.R_NAME;

![image alt](https://github.com/mannyshrestha1234-max/Project_TPC-H/blob/7b8534a48a667b68e0bde5cbd03f87b4d3462dbd/assets/q5.jpg)

## Query 6: Validate Monthly Revenue Trend

SELECT
    CAST(EXTRACT(YEAR FROM o.O_ORDERDATE) AS VARCHAR) AS YEAR,
    EXTRACT(MONTH FROM o.O_ORDERDATE) AS Month,
    SUM((l.L_EXTENDEDPRICE) * (1 - l.L_DISCOUNT)) AS Total_Revenue

FROM ORDERS o

JOIN LINEITEM l ON l.L_ORDERKEY = o.O_ORDERKEY

GROUP BY EXTRACT(YEAR FROM o.O_ORDERDATE), EXTRACT(MONTH FROM o.O_ORDERDATE)

ORDER BY YEAR, Month;

![image alt](https://github.com/mannyshrestha1234-max/Project_TPC-H/blob/7b8534a48a667b68e0bde5cbd03f87b4d3462dbd/assets/q6.jpg)

## Query 7: Product Performance Summary

SELECT
	p.P_NAME AS Part_Name,
	SUM((l.L_EXTENDEDPRICE) * (1 - l.L_DISCOUNT )) AS Total_Revenue ,
	sum(l.L_QUANTITY) AS Total_Quantity ,
	(SUM((l.L_EXTENDEDPRICE) * (1 - l.L_DISCOUNT )) / sum(l.L_QUANTITY)) AS Average_Price,
	COUNT(DISTINCT O_ORDERKEY) AS Number_of_Orders

FROM LINEITEM l 

JOIN PART p
	ON p.P_PARTKEY = l.L_PARTKEY

JOIN ORDERS o
	ON o.O_ORDERKEY = l.L_ORDERKEY

GROUP BY p.P_NAME

ORDER BY TOTAL_REVENUE DESC 

LIMIT 20 ;

![image alt](https://github.com/mannyshrestha1234-max/Project_TPC-H/blob/7b8534a48a667b68e0bde5cbd03f87b4d3462dbd/assets/q7.jpg)

## Query 8: Revenue by Product Type

WITH RevenueData AS (
    SELECT
        p.P_TYPE AS Product_Type,
        SUM(l.L_EXTENDEDPRICE * (1 - l.L_DISCOUNT)) AS Total_Revenue
    FROM LINEITEM l 
    JOIN PART p ON p.P_PARTKEY = l.L_PARTKEY
    GROUP BY p.P_TYPE
)

SELECT
    Product_Type,
    Total_Revenue,
    ROUND(Total_Revenue * 100.0 / SUM(Total_Revenue) OVER(), 2) || '%' AS Revenue_Percentage

FROM RevenueData

ORDER BY Total_Revenue DESC;

![image alt](https://github.com/mannyshrestha1234-max/Project_TPC-H/blob/7b8534a48a667b68e0bde5cbd03f87b4d3462dbd/assets/q8.jpg)

## Query 9: Top 5 Products by Revenue

SELECT
	p.P_NAME AS Product_name,
	CAST(SUM(l.L_EXTENDEDPRICE * (1 - l.L_DISCOUNT)) AS int) AS Total_Revenue

FROM LINEITEM l 

JOIN PART p 
	ON p.P_PARTKEY = l.L_PARTKEY

GROUP BY p.P_NAME

ORDER BY Total_Revenue DESC 

LIMIT 5;

![image alt](https://github.com/mannyshrestha1234-max/Project_TPC-H/blob/7b8534a48a667b68e0bde5cbd03f87b4d3462dbd/assets/q9.jpg)

## Query 10: Revenue by Customer Market Segment

SELECT
	c.C_MKTSEGMENT AS Market_Segment,
	SUM((l.L_EXTENDEDPRICE) * (1 - l.L_DISCOUNT )) AS Total_Revenue

FROM LINEITEM l 

JOIN ORDERS o 
	ON o.O_ORDERKEY = l.L_ORDERKEY 

JOIN CUSTOMER c 
	ON c.C_CUSTKEY = o.O_CUSTKEY 

GROUP BY MARKET_SEGMENT ;

![image alt](https://github.com/mannyshrestha1234-max/Project_TPC-H/blob/7b8534a48a667b68e0bde5cbd03f87b4d3462dbd/assets/q10.jpg)

## Query 11: Top Suppliers Analysis

SELECT
	s.S_NAME AS Supplier_Name ,
	n.N_NAME AS Nation_Name,
	SUM((l.L_EXTENDEDPRICE) * (1 - l.L_DISCOUNT )) AS Total_Revenue,
	COUNT(DISTINCT p.P_PARTKEY ) AS Unique_parts 

FROM LINEITEM l

JOIN ORDERS o 
	ON o.O_ORDERKEY = l.L_ORDERKEY 

JOIN CUSTOMER c 
	ON c.C_CUSTKEY = o.O_CUSTKEY 

JOIN SUPPLIER s 
	ON s.S_SUPPKEY = l.L_SUPPKEY 

JOIN NATION n 
	ON n.N_NATIONKEY = c.C_NATIONKEY

JOIN PART p 
	ON p.P_PARTKEY = l.L_PARTKEY 

GROUP BY
	s.S_NAME,
	n.N_NAME

ORDER BY TOTAL_REVENUE DESC 

LIMIT 15 ;

![image alt](https://github.com/mannyshrestha1234-max/Project_TPC-H/blob/7b8534a48a667b68e0bde5cbd03f87b4d3462dbd/assets/q11.jpg)

## Query 12: Customer Count by Country

SELECT
	n.N_NAME AS Nation_Name ,
	COUNT(c.C_CUSTKEY) AS Total_Count

FROM CUSTOMER c 

JOIN NATION n 
	ON n.N_NATIONKEY = c.C_NATIONKEY

GROUP BY NATION_NAME

ORDER BY NATION_NAME ASC ;

![image alt](https://github.com/mannyshrestha1234-max/Project_TPC-H/blob/7b8534a48a667b68e0bde5cbd03f87b4d3462dbd/assets/q12.jpg)

## Query 13: Order Priority Distribution

SELECT 
    o.O_ORDERPRIORITY AS Order_Priority, 
    COUNT(*) AS Priority_Count, 
    ROUND(COUNT(*) * 100.0 / SUM(COUNT(*)) OVER(), 2) || '%' AS Percentage 

FROM ORDERS o 

GROUP BY o.O_ORDERPRIORITY 

ORDER BY Priority_Count DESC;

![image alt](https://github.com/mannyshrestha1234-max/Project_TPC-H/blob/7b8534a48a667b68e0bde5cbd03f87b4d3462dbd/assets/q13.jpg)

## Query 14: Customer Lifetime Value --

SELECT
	c.C_NAME AS Customer_Name,
	SUM((l.L_EXTENDEDPRICE) * (1 - l.L_DISCOUNT )) AS Total_Revenue,
	COUNT(o.O_ORDERKEY) AS Number_of_orders,
	ROUND(AVG((l.L_EXTENDEDPRICE) * (1 - l.L_DISCOUNT )),2) AS Average,
	MIN(o.O_ORDERDATE) AS First_Order_Date,
    MAX(o.O_ORDERDATE) AS Last_Order_Date

FROM LINEITEM l

JOIN ORDERS o 
	ON l.L_ORDERKEY = o.O_ORDERKEY

JOIN CUSTOMER c 
	ON c.C_CUSTKEY = o.O_CUSTKEY 

GROUP BY 
	c.C_NAME

ORDER BY Total_Revenue DESC 

LIMIT 25;

![image alt](https://github.com/mannyshrestha1234-max/Project_TPC-H/blob/7b8534a48a667b68e0bde5cbd03f87b4d3462dbd/assets/q14.jpg)

## Query 15: Top Products by Product Type (Using Window Functions)

WITH ProductRevenue AS (
    SELECT 
        p.P_TYPE AS Product_Type,
        p.P_NAME AS Product_Name,
        SUM(l.L_EXTENDEDPRICE * (1 - l.L_DISCOUNT)) AS Revenue,
        ROW_NUMBER() OVER (
            PARTITION BY p.P_TYPE 
            ORDER BY SUM(l.L_EXTENDEDPRICE * (1 - l.L_DISCOUNT)) DESC
        ) AS Rank_Within_Type
    FROM LINEITEM l
    JOIN PART p ON p.P_PARTKEY = l.L_PARTKEY
    GROUP BY p.P_TYPE, p.P_NAME
)

SELECT 
    Product_Type,
    Product_Name,
    Revenue,
    Rank_Within_Type

FROM ProductRevenue

WHERE Rank_Within_Type <= 3

ORDER BY Product_Type, Rank_Within_Type;

![image alt](https://github.com/mannyshrestha1234-max/Project_TPC-H/blob/1bd36cd2fcd4113e911539880a81cfbe9d6b181e/assets/q15.jpg)
