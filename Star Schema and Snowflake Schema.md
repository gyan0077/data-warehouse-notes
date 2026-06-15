# 📦  Star Schema

A Star Schema is a dimensional model where:

A central Fact Table is connected directly to multiple Dimension Tables.
Dimension tables are denormalized (all attributes stored in a single table).
The structure resembles(look like) a star.

'
A Star Schema consists of a central Fact Table connected directly to denormalized Dimension Tables. It is simple, requires fewer joins, and provides better query performance, making it ideal for reporting and analytics.
'

# Banking Example
Suppose the bank wants to analyze customer transactions.

# Fact Transaction

| Transaction_ID | Customer_Key | Branch_Key | Date_Key | Amount |
| -------------- | ------------ | ---------- | -------- | ------ |
| 1001           | 101          | 21         | 20240615 | 10000  |
| 1002           | 102          | 22         | 20240615 | 5000   |

# Dim Customer

| Customer_Key | Customer_Name | Gender | City   | State       |
| ------------ | ------------- | ------ | ------ | ----------- |
| 101          | Amit Sharma   | Male   | Pune   | Maharashtra |
| 102          | Priya Patel   | Female | Mumbai | Maharashtra |

# Dim Branch

| Branch_Key | Branch_Name    | City   | State       |
| ---------- | -------------- | ------ | ----------- |
| 21         | Pune Main      | Pune   | Maharashtra |
| 22         | Mumbai Central | Mumbai | Maharashtra |


# Dim Date

| Date_Key | Date        | Month | Quarter | Year |
| -------- | ----------- | ----- | ------- | ---- |
| 20240615 | 15-Jun-2024 | Jun   | Q2      | 2024 |


# 📦  Structure


                Dim_Customer
                     |
                     |
Dim_Date ---- Fact_Transaction ---- Dim_Branch




# 📦  Why Denormalized?

Customer Dimension contains:
Customer Name
Gender
City
State

All attributes exist in one table.

No separate City or State tables.

# 📦  Advantages of Star Schema

| Advantage              | Explanation               |
| ---------------------- | ------------------------- |
| Simple design          | Easy for business users   |
| Fewer joins            | Better query performance  |
| Easy reporting         | BI tools work efficiently |
| Easy understanding     | Faster onboarding         |
| Preferred in analytics | Most common DW design     |

# 📦  Disadvantages of Star Schema

| Disadvantage      | Explanation                    |
| ----------------- | ------------------------------ |
| Data redundancy   | City/State repeated many times |
| More storage      | Duplicate values consume space |
| Update complexity | Changes may affect many rows   |


# 📦 Snowflake Schema
A Snowflake Schema is a dimensional model where:

Fact Table remains at the center.
Dimension tables are normalized into multiple related tables.
Resembles(look like) a snowflake structure.


'
A Snowflake Schema is an extension of the Star Schema where Dimension Tables are normalized into multiple related tables. It reduces redundancy and improves data integrity but requires more joins and increases query complexity.
'

# Banking Example

Instead of storing everything in Customer Dimension:

# Customer Dimension

| Customer_Key | Customer_Name | Gender | City_Key |
| ------------ | ------------- | ------ | -------- |
| 101          | Amit Sharma   | Male   | 11       |
| 102          | Priya Patel   | Female | 12       |


# City Dimension

| City_Key | City_Name | State_Key |
| -------- | --------- | --------- |
| 11       | Pune      | 1         |
| 12       | Mumbai    | 1         |


# State Dimension

| State_Key | State_Name  |
| --------- | ----------- |
| 1         | Maharashtra |


# 📦 Structure

                   Dim_State
                        |
                        |
                   Dim_City
                        |
                        |
                Dim_Customer
                        |
                        |
Fact_Transaction ---- Dim_Branch
                        |
                        |
                    Dim_Date





Dimensions are broken into multiple related tables.

# 📦 Why Normalize?

Instead of repeating:
Maharashtra
Maharashtra
Maharashtra
Maharashtra

Store it once in State Dimension.

This reduces redundancy.

# 📦 Advantages of Snowflake Schema

| Advantage             | Explanation                |
| --------------------- | -------------------------- |
| Less redundancy       | Reduced duplicate data     |
| Better data integrity | Single source of truth     |
| Lower storage         | Saves space                |
| Easier maintenance    | Master data updates easier |

# 📦 Disadvantages of Snowflake Schema

| Disadvantage     | Explanation                   |
| ---------------- | ----------------------------- |
| More joins       | Slower queries                |
| Complex design   | Harder to understand          |
| Complex ETL      | More relationships            |
| Less BI-friendly | Reporting becomes complicated |


# 📦 Star Schema vs Snowflake Schema

| Feature           | Star Schema    | Snowflake Schema |
| ----------------- | -------------- | ---------------- |
| Dimension Design  | Denormalized   | Normalized       |
| Number of Joins   | Fewer          | More             |
| Query Performance | Faster         | Slightly slower  |
| Storage Usage     | More           | Less             |
| Complexity        | Simple         | Complex          |
| Readability       | High           | Medium           |
| Reporting         | Easier         | More difficult   |
| ETL Complexity    | Lower          | Higher           |
| Data Redundancy   | Higher         | Lower            |
| Preferred For     | Analytics & BI | Data Integrity   |




