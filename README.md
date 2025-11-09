Shopify Analytics Power BI Dashboard

Overview
This project presents a Power BI Shopify Analytics Dashboard designed to help eCommerce businesses monitor, analyse, and optimise store performance in real time.
The dashboard offers interactive visualisations for KPIs such as Total Sales, Conversion Rate, Average Order Value (AOV), Customer Retention, and Sales by Channel — empowering Shopify merchants to make data-driven decisions that improve profitability and customer engagement.

Dataset
Imported CSV and API data sources:

shopify_orders.csv

shopify_customers.csv

shopify_products.csv

shopify_transactions.csv

Fields Used
OrderID, CustomerID, OrderDate, ProductType, Channel
TotalSales, Quantity, PaymentMethod, DeviceType
ReturningCustomer, ConversionRate, Region, GrossMargin

 Data Transformation
All cleaning and transformations were performed in Power Query:

Removed duplicate orders and null values

Standardised categorical fields (e.g., “paypal” vs “PayPal”)

Created calculated columns for:

CustomerType → New / Returning

SalesBand → Low / Medium / High

DeviceGroup → Desktop / Mobile / Tablet

Converted date fields into Year-Month format for trend analysis

Merged order and product tables to create a unified sales dataset

  Data Model
Tables:

Orders (Primary Key: OrderID)

Customers (Linked via CustomerID)

Products (Linked via ProductID)

Payments (Linked via PaymentID)

Relationships: One-to-many between Customers → Orders and Products → Orders tables.
 
  DAX Measures

Total Sales = SUM(Orders[TotalAmount])

Total Orders = COUNT(Orders[OrderID])

Average Order Value (AOV) = DIVIDE([Total Sales], [Total Orders])

Conversion Rate (%) =
DIVIDE([Total Orders], [Total Sessions]) * 100

Repeat Purchase Rate (%) =
DIVIDE([Returning Customers], [Total Customers]) * 100

Customer Lifetime Value (CLV) =
AVERAGEX(Customers, [Average Order Value] * [Repeat Purchase Rate])

Sales by Channel =
CALCULATE([Total Sales], VALUES(Orders[Channel]))

Sales by Product Type =
CALCULATE([Total Sales], VALUES(Products[ProductType]))
