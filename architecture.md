# 📦 What is a Data Warehouse?
A Data Warehouse (DWH) is a centralized repository designed to store integrated, historical, and structured data from multiple sources for analytical reporting and business intelligence (BI).

# 🧠 Why Data Warehouse Exists:
Organizations typically have many systems:
| System         | Stores           |
| -------------- | ---------------- |
| CRM            | customer info    |
| ERP            | orders           |
| Payment system | transactions     |
| Website        | clickstream logs |

If management asks:

“Show total revenue by customer region for last 5 years”

You cannot efficiently query multiple OLTP systems directly ❌

So we: Extract → Transform → Load → Store in Data Warehouse

Now analytics becomes fast and consistent ✅

# 🧱 Core Characteristics of a Data Warehouse
1️⃣ Subject-Oriented: Data is organized around business subjects:
Ex: 
Customers
Sales
Products
Revenue

2️⃣ Integrated: Data comes from multiple sources but stored in consistent format

Source systems:
System A → gender = M/F
System B → gender = Male/Female

Warehouse stores:
gender = Male/Female

3️⃣ Time-Variant: Stores historical data

4️⃣ Non-Volatile: Data is not frequently updated or deleted. It will be INSERT and SELECT.









