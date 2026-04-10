# OLTP (Online Transaction Processing)

OLTP systems handle real-time transactional operations like inserts, updates, and deletes.

# OLAP (Online Analytical Processing)

OLAP systems handle complex analytical queries on large historical datasets for reporting and decision-making.

Example:
OLTP → placing an order : Insert order record

OLAP → analyzing yearly revenue trends:
SELECT city, SUM(revenue)
FROM fact_sales
GROUP BY city;






