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

