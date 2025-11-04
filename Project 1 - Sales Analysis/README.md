# 🍕 Sales Insights Dashboard using PySpark in Databricks

## 📘 Project Overview
This project demonstrates how to perform **data analysis and KPI generation** using **PySpark** in **Databricks**.  
Two datasets — `sales.csv` and `menu.csv` — are used to analyze customer spending patterns, sales trends, and top-performing food items.  

It’s an end-to-end **data processing workflow** starting from reading raw CSV files to generating meaningful business KPIs.

---

## 🗂️ Datasets Used

### 1️⃣ sales.csv
| Column Name   | Description                | Example          |
|----------------|----------------------------|------------------|
| Product_ID     | Unique ID for each product | 1                |
| Customer_ID    | Unique ID for each customer | A                |
| Order_Date     | Date of purchase           | 2023-01-01       |
| Location       | Country of purchase        | India            |
| Source_Order   | Platform of order          | Swiggy           |

---

### 2️⃣ menu.csv
| Column Name   | Description                | Example   |
|----------------|----------------------------|-----------|
| Product_ID     | Unique ID for each product | 1         |
| Product_Name   | Name of the food item      | PIZZA     |
| Price          | Price of the item (₹)      | 100       |

---

## ⚙️ Tech Stack

- **Language:** Python 🐍  
- **Framework:** PySpark  
- **Platform:** Databricks (Free Edition)  
- **Libraries Used:**
  - `pyspark.sql.functions`
  - `pyspark.sql.types`

---

## 🧩 Project Workflow

### 1️⃣ Data Loading
- Defined **custom schemas** for both datasets using `StructType`.
- Loaded the CSV files into PySpark DataFrames using `spark.read.csv()`.

### 2️⃣ Data Preparation
- Extracted **Year**, **Quarter**, and **Month** from `Order_Date` column.
- Cast the `Price` column from string to **DecimalType(10,2)** for accurate numeric calculations.

### 3️⃣ Data Analysis & KPIs
Below are the key performance indicators derived from the datasets 👇

| KPI | Description |
|------|--------------|
| 💰 **Total Amount Spent by Each Customer** | Total spending per customer by joining `sales_df` and `menu_df`. |
| 🍽️ **Total Amount Spent by Each Food Category** | Aggregates total sales by each `Product_Name`. |
| 📆 **Total Sales by Month** | Calculates total sales for each month. |
| 📅 **Yearly Sales** | Aggregates sales by `Order_Year`. |
| 🕓 **Quarterly Sales** | Aggregates total sales by quarter. |
| 📊 **Total Orders by Each Category** | Counts total number of orders placed for each product. |
| 🏆 **Top 3 Ordered Items** | Identifies the top 3 most frequently ordered food items. |
| 🔝 **Most Ordered Item** | Finds the single most ordered item overall. |
| 👥 **Frequency of Customers Visiting the Restaurant** | Counts distinct visits (based on `Order_Date`) for each customer who ordered from a restaurant. |
| 🌍 **Total Sales by Country** | Groups total sales by customer `Location`. |
| 🛵 **Total Sales by Order Source** | Groups total sales by `Source_Order` (e.g., Swiggy, Zomato, Restaurant). |

---

## 📈 Sample Snippet

```python
# Total Amount Spent by Each Customer
from pyspark.sql import functions as F

total_amount_spent_by_customer = (
    sales_df.join(menu_df, on='Product_ID', how='inner')
        .groupBy('Customer_ID')
        .agg(F.sum('Price').alias('Total_Amount'))
        .orderBy('Customer_ID')
)

display(total_amount_spent_by_customer)

```
---

## 💡 Key Learnings

- Working with PySpark DataFrames and Schema Definition.

- Performing joins, aggregations, and groupBy operations.

- Creating new columns using PySpark functions (year, month, quarter).

- Practicing KPI generation using Databricks SQL API.

- Hands-on experience with data analysis in distributed environments


---

## 🚀 Future Enhancements

- Add visualizations using Databricks SQL or Power BI.

- Implement window functions for advanced analysis.

- Automate data ingestion from cloud storage (Azure / AWS).

- Store processed data as Delta Tables for performance optimization.


---

## 🏁 Project Structure
📂 sales_insights_project/
 ├── 📄 sales.csv

 ├── 📄 menu.csv

 ├── 📓 sales_insights_notebook.dbc

 ├── 📄 README.md


---

## 🪶 Author
Chanush KR

🔗 [LinkedIn](https://www.linkedin.com/in/chanush-kr)  
🌐 [Portfolio Website](https://sites.google.com/view/chanushkr/home)  
📌 [LinkedIn Post about this Project](https://www.linkedin.com/posts/chanush-kr_azuredatafactory-dataengineering-azuredatalake-activity-7378763608350179328-RKsp?utm_source=share&utm_medium=member_desktop&rcm=ACoAAD0Tw64BmW6pg1qf8-1ow9qOM-2tCEyFJRw)
