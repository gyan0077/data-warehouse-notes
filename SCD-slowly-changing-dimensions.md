# Slowly Changing Dimensions (SCD)

A Slowly Changing Dimension (SCD) is a technique used to manage changes in Dimension Tables over time.

In real-world systems, dimension attributes change:

Customer changes address
Employee changes department
Account holder changes mobile number
Branch changes region

SCD provides different strategies to manage historical data.

# Banking Example
Consider a Customer Dimension.

# Initial Data

| Customer_Key | Customer_ID | Customer_Name | City |
| ------------ | ----------- | ------------- | ---- |
| 101          | C1001       | Amit Sharma   | Pune |


Later Amit moves from Pune to Mumbai.

Different SCD types handle this change differently.


# Why SCD is Important?

Business users often ask:
What was the customer's city when the transaction occurred?
Show customer distribution by city last year.

Without history management, such reporting becomes inaccurate.


# SCD Type 0 – Fixed Dimension
No changes are allowed.
'
SCD Type 0 preserves original values permanently and ignores all future updates.
'

Once data is loaded, it never changes.

# Example
| Customer_ID | Customer_Name | DOB        |
| ----------- | ------------- | ---------- |
| C1001       | Amit Sharma   | 1995-05-10 |

DOB should never change.


# Use Cases
Attribute
| Attribute              |
| ---------------------- |
| Date of Birth          |
| PAN Number             |
| Account Opening Date   |
| Customer Creation Date |


# SCD Type 1 – Overwrite
Old value is overwritten.

'
SCD Type 1 overwrites existing values and does not preserve history.
'

No history is maintained.

# Before Update

| Customer_ID | Customer_Name | City |
| ----------- | ------------- | ---- |
| C1001       | Amit Sharma   | Pune |


# After Update

| Customer_ID | Customer_Name | City   |
| ----------- | ------------- | ------ |
| C1001       | Amit Sharma   | Mumbai |

Pune is lost forever. 

# Advantages

| Advantage        |
| ---------------- |
| Simple           |
| Less storage     |
| Easy maintenance |

# Disadvantages

| Disadvantage             |
| ------------------------ |
| History lost permanently |



# Banking Use Cases

| Attribute      |
| -------------- |
| Mobile Number  |
| Email Address  |
| Marital Status |

Current value is usually sufficient.


# SCD Type 2 – Full History Tracking
Instead of updating the existing row:

Expire old row
Insert new row
Maintain complete history

'
SCD Type 2 maintains complete history by inserting a new record whenever a change occurs. The old record is expired using end dates or flags, while a new surrogate key is generated for the updated record.
'

# Before Update

| Customer_Key | Customer_ID | Customer_Name | City | Start_Date | End_Date | Current_Flag |
| ------------ | ----------- | ------------- | ---- | ---------- | -------- | ------------ |
| 101          | C1001       | Amit Sharma   | Pune | 2024-01-01 | NULL     | Y            |


**When Customer Moves to Mumbai**

# After Update

| Customer_Key | Customer_ID | Customer_Name | City   | Start_Date | End_Date   | Current_Flag |
| ------------ | ----------- | ------------- | ------ | ---------- | ---------- | ------------ |
| 101          | C1001       | Amit Sharma   | Pune   | 2024-01-01 | 2024-06-30 | N            |
| 102          | C1001       | Amit Sharma   | Mumbai | 2024-07-01 | NULL       | Y            |


# Key Points
New Surrogate Key Generated

Old Key = 101
New Key = 102

Business Key remains same:

Customer_ID = C1001

# Common Columns

| Column         | Purpose                   |
| -------------- | ------------------------- |
| Start_Date     | Record effective start    |
| End_Date       | Record effective end      |
| Current_Flag   | Y/N indicator             |
| Version_Number | Optional version tracking |

# Banking Use Cases

| Attribute            |
| -------------------- |
| Customer Address     |
| Customer City        |
| Branch Region        |
| Relationship Manager |

History is required for regulatory and analytical reporting.


# SCD Type 3 – Limited History

Store current value and previous value in the same row.

'
SCD Type 3 stores limited history by adding additional columns such as Previous_City and Current_City.
'

# Example

| Customer_ID | Current_City | Previous_City |
| ----------- | ------------ | ------------- |
| C1001       | Mumbai       | Pune          |

If customer moves again:

| Customer_ID | Current_City | Previous_City |
| ----------- | ------------ | ------------- |
| C1001       | Delhi        | Mumbai        |

Pune is Lost


# Characteristics

| Feature       | Value   |
| ------------- | ------- |
| History Depth | Limited |
| Storage       | Low     |
| Complexity    | Low     |


# SCD Type 4 – History Table

Current data and historical data are stored separately.

# Current Customer Table

| Customer_ID | Customer_Name | City   |
| ----------- | ------------- | ------ |
| C1001       | Amit Sharma   | Mumbai |


# Customer History Table

| Customer_ID | Customer_Name | City | Change_Date |
| ----------- | ------------- | ---- | ----------- |
| C1001       | Amit Sharma   | Pune | 2024-01-01  |


# Advantages

| Advantage                   |
| --------------------------- |
| Current table remains small |
| Historical data separated   |




# SCD Type 6 (1+2+3 Hybrid)

Combination of:

Type 1

Type 2

Type 3

# Maintains:

Current value

Previous value

Full history


# Example

| Customer_Key | Customer_ID | Current_City | Previous_City | Start_Date | End_Date   |
| ------------ | ----------- | ------------ | ------------- | ---------- | ---------- |
| 101          | C1001       | Pune         | NULL          | 2024-01-01 | 2024-06-30 |
| 102          | C1001       | Mumbai       | Pune          | 2024-07-01 | NULL       |

Rarely implemented but commonly asked theoretically.


# SCD Type Comparison

| Feature           | Type 0            | Type 1      | Type 2      | Type 3  | Type 4        |
| ----------------- | ----------------- | ----------- | ----------- | ------- | ------------- |
| History Preserved | No Change Allowed | No          | Full        | Limited | Full          |
| New Row Inserted  | No                | No          | Yes         | No      | History Table |
| Storage Usage     | Low               | Low         | High        | Medium  | High          |
| Complexity        | Low               | Low         | Medium      | Medium  | Medium        |
| Most Used         | Rare              | Very Common | Very Common | Rare    | Rare          |


# How Fact Tables Work with SCD Type 2
Suppose:  Customer lives in Pune

| Customer_Key | Customer_ID | City |
| ------------ | ----------- | ---- |
| 101          | C1001       | Pune |


# Transaction occurs:

| Transaction_ID | Customer_Key | Amount |
| -------------- | ------------ | ------ |
| T001           | 101          | 10000  |


# Customer moves to Mumbai.

# New dimension row:

| Customer_Key | Customer_ID | City   |
| ------------ | ----------- | ------ |
| 102          | C1001       | Mumbai |


# New transaction:

| Transaction_ID | Customer_Key | Amount |
| -------------- | ------------ | ------ |
| T002           | 102          | 5000   |


# Result

Historical reports remain accurate because transactions point to the correct version of the customer.

# Interview Answer (2-Minute Version)

Slowly Changing Dimensions are techniques used to manage changes in dimension data over time.

SCD Type 1 overwrites existing values and does not maintain history.
SCD Type 2 preserves complete history by expiring old records and inserting new records with new surrogate keys. 

SCD Type 3 maintains limited history using additional columns. 

In banking projects, SCD Type 2 is most commonly used because historical customer information is required for regulatory reporting, auditing, and trend analysis.






























