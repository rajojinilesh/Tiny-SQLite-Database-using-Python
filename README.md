# Tiny-SQLite-Database-using-Python
📌 Overview

This project is part of my Data Analyst role at Elevate Labs.
The goal was to connect to a SQLite database, run basic SQL aggregation queries, and generate a sales summary report along with a visualization.

The dataset used is a Superstore sales dataset stored in a CSV file, which was loaded into SQLite for querying.

🛠 Tools & Technologies

Python 3

SQLite (via sqlite3)

Pandas (data handling)

Matplotlib (visualization)

Jupyter Notebook / Google Colab

📂 Dataset

File Name: Superstore.csv

Rows: 9,994

Columns: 21

Key Fields Used:

Product Name

Sales

Quantity

📊 Steps Implemented
1️⃣ Load Data into SQLite
import sqlite3
import pandas as pd

df = pd.read_csv("Superstore.csv", encoding='latin1')
conn = sqlite3.connect("sales_data.db")
df.to_sql("sales", conn, if_exists="replace", index=False)

2️⃣ Run SQL Query to Get Sales Summary
query = """
SELECT "Product Name" AS product,
       SUM(Quantity) AS total_qty,
       SUM(Quantity * Sales) AS revenue
FROM sales
GROUP BY "Product Name"
"""
summary_df = pd.read_sql_query(query, conn)

3️⃣ Print Results
print("Sales Summary:")
print(summary_df)

4️⃣ Plot Revenue by Product
import matplotlib.pyplot as plt

summary_df.plot(kind='bar', x='product', y='revenue', figsize=(10,5), legend=False)
plt.xlabel("Product")
plt.ylabel("Revenue")
plt.title("Revenue by Product")
plt.tight_layout()
plt.savefig("sales_chart.png")
plt.show()

📈 Key Insights

Shows total quantity sold and total revenue for each product.

Helps identify top-performing products in terms of revenue.

Demonstrates the combination of SQL + Python for quick business analytics.




🚀 How to Run

Clone this repository:

git clone https://github.com/yourusername/task7-sales-summary.git
cd task7-sales-summary


Install required libraries:

pip install pandas matplotlib


Run the script or open the notebook in Jupyter/Colab.

