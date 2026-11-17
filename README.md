# E-commerce Analysis with Python and SQL

A small project that answers business questions about an e-commerce dataset by writing SQL queries in MySQL and running them from Python. Results are loaded into pandas DataFrames and visualised with matplotlib.

## Overview

The notebook connects to a local MySQL database (`ecommers`), runs seven analytical queries, and presents the results as tables and charts. The data is Brazilian e-commerce order data: customer cities include São Paulo, Campinas and Franca.

## Questions Answered

| # | Question | Technique | Result |
|---|---|---|---|
| 1 | List all unique cities where customers are located | `SELECT DISTINCT` | Table of cities (São Paulo, Campinas, Franca, ...) |
| 2 | Count the orders placed in 2017 | `COUNT` with a `YEAR()` filter | **45,101 orders** |
| 3 | Total sales per product category | Three-table `JOIN`, `SUM`, `GROUP BY` | e.g. Bed Table Bath 1.71M, Furniture Decoration 1.43M, Automotive 852K, Perfumery 507K, Telephony 487K |
| 4 | Percentage of orders paid in instalments | `CASE WHEN` inside `SUM` | **99.998%** of payment records have 1 or more instalments |
| 5 | Number of customers in each state | `GROUP BY`, bar chart | Chart sorted from most to fewest customers |
| 6 | Number of orders per month in 2018 | `MONTHNAME()`, `GROUP BY`, bar chart | Monthly order chart |
| 7 | Average number of products per order, by customer city | CTE, `JOIN`, `AVG` | Padre Carvalho (7.0), Celso Ramos (6.5), Datas (6.0), Candido Godoi (6.0) |

Note on Q4: a payment with 1 instalment counts as "paid in instalments" in this query, which is why the result is almost 100%. Filtering on `payment_installments > 1` would give a more useful split.

Note on Q7: the top cities are very small, so a handful of large orders pushes their averages up.

## Database Tables Used

| Table | Used for |
|---|---|
| `customers` | Customer city and state |
| `orders` | Order purchase timestamps |
| `order_items` | Products in each order |
| `products` | Product categories |
| `payments` | Payment value and instalments |

## Tools and Libraries

- Python
- MySQL and `mysql-connector-python`
- pandas
- matplotlib
- seaborn
- Jupyter Notebook

## How to Run

1. Install MySQL and create a database named `ecommers`, then load the dataset tables into it.
2. Install the requirements:
   ```bash
   pip install pandas matplotlib seaborn mysql-connector-python jupyter
   ```
3. Set your MySQL password as an environment variable instead of writing it in the notebook:
   ```powershell
   $env:MYSQL_PASSWORD = "your_password"
   ```
4. Open `python_sql_ecommerce.ipynb` in Jupyter or VS Code and run the cells from top to bottom.

The notebook connects to a MySQL server on your own computer, so it cannot run on Google Colab as it is.

## Viewing the Notebook

GitHub displays the saved outputs and charts directly. Open `python_sql_ecommerce.ipynb` above to see them without running anything.

## Files

| File | Description |
|---|---|
| `python_sql_ecommerce.ipynb` | Notebook with the queries, tables and charts |

## Author

Rakshit ([@Rakshiii365](https://github.com/Rakshiii365))
