# 📦 Fact Table

A Fact Table stores business events or transactions and contains measurable metrics (facts)

Facts are typically numeric values that can be aggregated (SUM, AVG, COUNT, MIN, MAX).

A Fact Table sits at the center of a Star Schema and is connected to multiple Dimension Tables through foreign keys.

For example, in a banking transaction warehouse, Transaction Amount is stored in the Fact Table, while Customer, Branch, Account, and Date details are stored in Dimension Tables. Facts are used for calculations and aggregations, whereas dimensions are used for filtering, grouping, and reporting.




# Banking Example
Suppose a customer performs a fund transfer.
| Transaction_ID | Customer_Key | Account_Key | Date_Key | Branch_Key | Amount |
| -------------- | ------------ | ----------- | -------- | ---------- | ------ |
| 10001          | 101          | 501         | 20240615 | 21         | 10000  |


This record represents a business event (transaction).

# Measures (Facts)
Amount = 10000
Transaction Count = 1
These values can be aggregated.

# Characteristics of Fact Table
| ------------------------ | ------------------------------ |
| Characteristic           | Description                    |
| ------------------------ | ------------------------------ |
| Contains business events | Transactions, Orders, Payments |
| Contains measures        | Amount, Quantity, Balance      |
| Very large table         | Millions/Billions of rows      |
| Connected to dimensions  | Via foreign keys               |
| Used for analytics       | Reporting and dashboards       |
| Frequently loaded        | Daily, hourly, near real-time  |

# Common Measures in Banking
| Fact Table       | Measures                       |
| ---------------- | ------------------------------ |
| Transaction Fact | Amount, Fee, Transaction Count |
| Loan Fact        | Loan Amount, Interest Amount   |
| Credit Card Fact | Spend Amount, Cashback         |
| Deposit Fact     | Deposit Amount, Balance        |


# 📦 Dimension Table
A Dimension Table stores descriptive information (context) about business entities.

Dimensions answer questions such as:
Who?

What?

When?

Where?

Which?

# Banking Example
# Customer Dimension

| Customer_Key | Customer_ID | Customer_Name | Gender | City   |
| ------------ | ----------- | ------------- | ------ | ------ |
| 101          | C1001       | Amit Sharma   | Male   | Mumbai |
| 102          | C1002       | Priya Patel   | Female | Pune   |

This table describes the customer.

# Branch Dimension

| Branch_Key | Branch_Code | Branch_Name | State       |
| ---------- | ----------- | ----------- | ----------- |
| 21         | BR001       | Nagpur Main | Maharashtra |

This table describes branch information.

# Characteristics of Dimension Table

| Characteristic                  | Description                   |
| ------------------------------- | ----------------------------- |
| Contains descriptive attributes | Name, City, Product           |
| Usually smaller than Fact table | Thousands or millions of rows |
| Provides business context       | Customer, Product, Branch     |
| Used in filtering and grouping  | WHERE, GROUP BY               |
| Contains surrogate keys         | Usually primary key           |


# 📦 Fact vs Dimension Table
| Feature     | Fact Table            | Dimension Table               |
| ----------- | --------------------- | ----------------------------- |
| Purpose     | Store business events | Store descriptive information |
| Data Type   | Numeric measures      | Textual attributes            |
| Size        | Very large            | Relatively small              |
| Growth Rate | Rapid                 | Slow                          |
| Aggregation | Yes                   | No                            |
| Example     | Transaction Amount    | Customer Name                 |
| Keys        | Foreign Keys          | Primary Key                   |
| Usage       | Calculations          | Filtering & Grouping          |





