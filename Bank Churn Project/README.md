# Banking Churn Analysis

## Overview

This repository contains the Banking Churn Analysis project, designed to understand customer churn behavior in the banking industry. By leveraging SQL queries and DAX calculations, we visualized key metrics and trends in Power BI to identify actionable insights.

---

## Dashboard Preview

Below is a snapshot of the interactive dashboard: ![Banking Churn Dashboard](https://github.com/CodeVistaPro/SQL-Projects/blob/main/Bank%20Churn%20Project/Banking%20Churn%20Analysis.png))




---

## Features

1. **Key Metrics**:
   - Total Customers
   - Churned Customers
   - Churn Rate
   - Average Credit Score
   - Average Customer Balance
2. **Interactive Visuals**:
   - Churn by Customer Segment
   - Churn by State
   - Distribution of Credit Scores
   - Customers by Occupation
   - Balance by Education Level
   - Products Purchased by Churn Status
3. **Filters**:
   - Gender
   - Education Level
   - State

---

## SQL Queries Used

### Key Metrics Queries

1. **Total Customers**:
   ```sql
   SELECT COUNT(*) AS Total_Customers FROM clean_churn;
   ```
2. **Churned Customers**:
   ```sql
   SELECT COUNT(*) AS Churned_Customers FROM clean_churn WHERE `Churn Flag` = 1;
   ```
3. **Churn Rate**:
   ```sql
   SELECT
       ROUND((COUNT(*) * 100.0 / (SELECT COUNT(*) FROM clean_churn)), 2) AS Churn_Rate
   FROM clean_churn
   WHERE `Churn Flag` = 1;
   ```
4. **Average Customer Balance**:
   ```sql
   SELECT ROUND(AVG(Balance), 2) AS Avg_Customer_Balance FROM clean_churn;
   ```
5. **Average Credit Score**:
   ```sql
   SELECT ROUND(AVG(`Credit Score`), 2) AS Avg_Credit_Score FROM clean_churn;
   ```

### Visual Queries

1. **Churn Rate by Customer Segment**:
   ```sql
   SELECT `Customer Segment`,
          COUNT(*) AS Total_Customers,
          SUM(`Churn Flag`) AS Churned_Customers,
          ROUND((SUM(`Churn Flag`) * 100.0 / COUNT(*)), 2) AS Churn_Rate
   FROM clean_churn
   GROUP BY `Customer Segment`
   ORDER BY Churn_Rate DESC;
   ```
2. **Churn Rate by State**:
   ```sql
   SELECT State,
          COUNT(*) AS Total_Customers,
          SUM(`Churn Flag`) AS Churned_Customers,
          ROUND((SUM(`Churn Flag`) * 100.0 / COUNT(*)), 2) AS Churn_Rate
   FROM clean_churn
   GROUP BY State
   ORDER BY Churn_Rate DESC;
   ```
3. **Distribution of Credit Scores**:
   ```sql
   SELECT FLOOR(`Credit Score` / 50) * 50 AS Credit_Score_Range,
          COUNT(*) AS Customer_Count
   FROM clean_churn
   GROUP BY Credit_Score_Range
   ORDER BY Credit_Score_Range;
   ```
4. **Number of Products Purchased by Churn Status**:
   ```sql
   SELECT `NumOfProducts`,
          COUNT(*) AS Total_Customers,
          SUM(`Churn Flag`) AS Churned_Customers,
          COUNT(*) - SUM(`Churn Flag`) AS Active_Customers
   FROM clean_churn
   GROUP BY `NumOfProducts`
   ORDER BY `NumOfProducts`;
   ```

---

## DAX Measures Used

### Key Metrics

1. **Churn Rate**:
   ```DAX
   Churn Rate =
   DIVIDE(
       CALCULATE(COUNTROWS(clean_churn), clean_churn[Churn Flag] = 1),
       COUNTROWS(clean_churn),
       0
   ) * 100
   ```
2. **Total Customers**:
   ```DAX
   Total Customers = COUNTROWS(clean_churn)
   ```
3. **Churned Customers**:
   ```DAX
   Churned Customers =
   CALCULATE(
       COUNTROWS(clean_churn),
       clean_churn[Churn Flag] = 1
   )
   ```

### Visual-Specific Measures

1. **Credit Score Range** (Calculated Column):
   ```DAX
   Credit Score Range =
   FLOOR(clean_churn[Credit Score] / 50, 1) * 50
   ```
2. **Customer Count by Range**:
   ```DAX
   Customer Count = COUNTROWS(clean_churn)
   ```

---

## How to Use

1. **SQL Setup**:
   - Load the provided `clean_churn` dataset into your SQL database.
   - Run the SQL queries to extract the required metrics and datasets.
2. **Power BI Setup**:
   - Import the processed data into Power BI.
   - Use the DAX measures to create interactive visuals.
   - Customize slicers for a more dynamic dashboard experience.

---

## Next Steps

- Explore the insights from the dashboard to drive business decisions.
- Enhance the analysis with additional metrics or visuals based on business needs.


