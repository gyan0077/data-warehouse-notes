# Star Schema

A Star Schema is a dimensional model where:

A central Fact Table is connected directly to multiple Dimension Tables.
Dimension tables are denormalized (all attributes stored in a single table).
The structure resembles(look like) a star.

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


# Structure

                Dim_Customer
                     |
                     |
Dim_Date ---- Fact_Transaction ---- Dim_Branch


# Why Denormalized?

Customer Dimension contains:
Customer Name
Gender
City
State

All attributes exist in one table.

No separate City or State tables.

# Advantages of Star Schema

| Advantage              | Explanation               |
| ---------------------- | ------------------------- |
| Simple design          | Easy for business users   |
| Fewer joins            | Better query performance  |
| Easy reporting         | BI tools work efficiently |
| Easy understanding     | Faster onboarding         |
| Preferred in analytics | Most common DW design     |

# Disadvantages of Star Schema

| Disadvantage      | Explanation                    |
| ----------------- | ------------------------------ |
| Data redundancy   | City/State repeated many times |
| More storage      | Duplicate values consume space |
| Update complexity | Changes may affect many rows   |




