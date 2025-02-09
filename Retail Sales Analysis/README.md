# Retail Sales Analysis Project

This project focuses on analyzing retail sales data to uncover meaningful insights through visualizations and key performance indicators (KPIs). The analysis was conducted using data loaded from SQL through an ODBC connection, and the final visualizations and dashboard were created in Excel.

## **Project Overview**

The primary objective of this project was to:

- Analyze retail sales data from multiple perspectives.
- Build an interactive dashboard to summarize key metrics and trends.
- Use SQL queries for data preparation and extract actionable insights.
- Export the SQL results as a CSV and visualize them in Excel.

  
## Dashboard Preview

Below is a snapshot of the interactive dashboard: ![Banking Churn Dashboard](https://github.com/CodeVistaPro/SQL-Projects/blob/main/Retail%20Sales%20Analysis/retail%20sales%20analysis.png)

---
## **Steps Undertaken**

### **1️⃣ Data Loading**

- The dataset was initially loaded from an SQL database via ODBC.
- The data was exported as a CSV file to work with in Excel for visualization purposes.

### **2️⃣ Data Preparation**

- **SQL Queries Used for Cleaning and Insights:**
  - Calculated key metrics like Total Revenue, Total Transactions, and Average Order Value.
  - Transformed raw data fields (e.g., converting dates into months).
  - Grouped data for specific analyses like monthly trends, customer demographics, and product performance.

### **3️⃣ Key Performance Indicators (KPIs)**

The following KPIs were calculated and displayed prominently on the dashboard:

- **Total Revenue:**

  - SQL Query:
    ```sql
    SELECT FORMAT(SUM(Total_Amount), 0) AS Total_Revenue FROM sales;
    ```
  - Result: `$456K`.

- **Total Customers:**

  - SQL Query:
    ```sql
    SELECT COUNT(DISTINCT Customer_ID) AS Total_Customers FROM sales;
    ```
  - Result: `1000`.

- **Avg Items per Order:**

  - SQL Query:
    ```sql
    SELECT ROUND(SUM(Quantity) / COUNT(DISTINCT Transaction_ID), 2) AS Avg_Items_per_Order FROM sales;
    ```
  - Result: `3`.

- **Average Order Value (AOV):**

  - SQL Query:
    ```sql
    SELECT ROUND(SUM(Total_Amount) / COUNT(Transaction_ID), 2) AS Avg_Order_Value FROM sales;
    ```
  - Result: `$456`.

### **4️⃣ Visualizations**

The following charts and visuals were created to summarize insights:

#### **Monthly Sales (Line Chart)**

- **Purpose:** Analyze sales trends over months to identify peaks and dips.
- **SQL Query:**
  ```sql
  SELECT DATE_FORMAT(Date, '%m') AS Transaction_Month, SUM(Total_Amount) AS Monthly_Sales
  FROM sales
  WHERE Date IS NOT NULL
  GROUP BY Transaction_Month
  ORDER BY Transaction_Month;
  ```
- **Visualization:** The line chart shows monthly trends with peaks in May and October.

#### **Total Revenue by Category (Bar Chart)**

- **Purpose:** Identify which product categories generate the most revenue.
- **SQL Query:**
  ```sql
  SELECT Product_Category, SUM(Total_Amount) AS Total_Revenue
  FROM sales
  GROUP BY Product_Category
  ORDER BY Total_Revenue DESC;
  ```
- **Result:** Electronics leads, followed by Clothing and Beauty.

#### **Total Quantity by Category (Bar Chart)**

- **Purpose:** Determine the most sold product categories in terms of quantity.
- **SQL Query:**
  ```sql
  SELECT Product_Category, SUM(Quantity) AS Total_Quantity_Sold
  FROM sales
  GROUP BY Product_Category
  ORDER BY Total_Quantity_Sold DESC;
  ```

#### **Gender-wise Revenue Contribution (Pie Chart)**

- **Purpose:** Understand how sales are distributed across genders.
- **SQL Query:**
  ```sql
  SELECT Gender, SUM(Total_Amount) AS Total_Revenue
  FROM sales
  GROUP BY Gender;
  ```
- **Result:** Male customers contributed 51% and females contributed 49%.

#### **Customer Age Distribution (Bar Chart)**

- **Purpose:** Highlight the distribution of customers across age groups.
- **SQL Query:**
  ```sql
  SELECT CASE
           WHEN Age BETWEEN 18 AND 25 THEN '18-25'
           WHEN Age BETWEEN 26 AND 35 THEN '26-35'
           WHEN Age BETWEEN 36 AND 45 THEN '36-45'
           WHEN Age BETWEEN 46 AND 55 THEN '46-55'
           ELSE '56+'
         END AS Age_Group, COUNT(*) AS Customers_Count
  FROM sales
  WHERE Age IS NOT NULL
  GROUP BY Age_Group
  ORDER BY Age_Group;
  ```
- **Result:** Most customers fall into the 26-35 age group.

### **5️⃣ Dashboard Design**

The dashboard was designed in Excel with the following features:

- **Color Scheme:** Warm, reddish tones for a consistent look.
- **KPI Cards:** Placed prominently to summarize key metrics at a glance.
- **Charts:**
  - Line chart for monthly trends.
  - Bar charts for category-wise revenue and quantity.
  - Pie chart for gender-wise contributions.
  - Bar chart for customer age distribution.

### **6️⃣ Limitations**

- **Slicers Omitted:** Although initially planned, slicers were excluded from this project and will be included in future projects.

### **7️⃣ Key Learnings**

- Gained hands-on experience in SQL for data analysis.
- Created effective visualizations in Excel to represent insights.
- Learned to handle challenges with data formats and transformations.

### **8️⃣ Tools Used**

- **SQL:** For querying and data preparation.
- **Excel:** For dashboard creation and visualization.
- **ODBC Connection:** To fetch data from the SQL database.

###

