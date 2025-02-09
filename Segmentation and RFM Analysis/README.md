# RFM Analysis Project

## Overview
This project implements **RFM (Recency, Frequency, Monetary)** analysis on a retail dataset to segment customers based on their purchasing behavior. The analysis involves SQL for data preparation and Power BI for visualization, providing business insights about customer segments.

---

## Dashboard Preview

Below is a snapshot of the interactive dashboard: ![Dashboard](https://github.com/CodeVistaPro/SQL-Projects/blob/main/Segmentation%20and%20RFM%20Analysis/RFM%20Analysis.png)

---

## What is RFM Analysis?
RFM Analysis is a marketing technique used to analyze and segment customers based on their transactional behavior. It is based on three metrics:
1. **Recency**: How recently a customer made a purchase.
2. **Frequency**: How often a customer makes a purchase.
3. **Monetary**: How much money a customer spends.

By calculating scores for these metrics, businesses can identify high-value customers and tailor marketing strategies effectively.

---

## SQL Implementation
The following steps outline how the RFM analysis was implemented using SQL:

### Step 1: Preparing the RFM Metrics Table
```sql
ALTER TABLE rfm_metrics
ADD COLUMN R_score INT,
ADD COLUMN F_score INT,
ADD COLUMN M_score INT;
```
This step adds columns to store RFM scores in the dataset.

### Step 2: Calculating Recency (R Score)
1. Create a table sorted by recency:
   ```sql
   CREATE TABLE recency_sorted (
       id INT AUTO_INCREMENT PRIMARY KEY,
       CustomerID INT,
       Recency INT
   ) ENGINE=InnoDB
   SELECT 
       CustomerID, 
       Recency 
   FROM rfm_metrics
   ORDER BY Recency ASC;
   ```

2. Calculate percentile rank and assign R scores:
   ```sql
   SET @total_count = (SELECT COUNT(*) FROM recency_sorted);

   ALTER TABLE recency_sorted ADD COLUMN percentile_rank FLOAT;

   UPDATE recency_sorted
   SET percentile_rank = id / @total_count;

   UPDATE rfm_metrics AS r
   JOIN recency_sorted AS s ON r.CustomerID = s.CustomerID
   SET r.R_Score = CASE
       WHEN s.percentile_rank <= 0.2 THEN 5
       WHEN s.percentile_rank <= 0.4 THEN 4
       WHEN s.percentile_rank <= 0.6 THEN 3
       WHEN s.percentile_rank <= 0.8 THEN 2
       ELSE 1
   END;
   ```

### Step 3: Calculating Frequency (F Score)
```sql
CREATE TABLE frequency_sorted (
    id INT AUTO_INCREMENT PRIMARY KEY,
    CustomerID INT,
    Frequency INT
) ENGINE=InnoDB
SELECT 
    CustomerID, 
    Frequency 
FROM rfm_metrics
ORDER BY Frequency DESC;

SET @total_count = (SELECT COUNT(*) FROM frequency_sorted);

ALTER TABLE frequency_sorted ADD COLUMN percentile_rank FLOAT;

UPDATE frequency_sorted
SET percentile_rank = id / @total_count;

UPDATE rfm_metrics AS r
JOIN frequency_sorted AS f ON r.CustomerID = f.CustomerID
SET r.F_Score = CASE
    WHEN f.percentile_rank <= 0.2 THEN 5
    WHEN f.percentile_rank <= 0.4 THEN 4
    WHEN f.percentile_rank <= 0.6 THEN 3
    WHEN f.percentile_rank <= 0.8 THEN 2
    ELSE 1
END;
```

### Step 4: Calculating Monetary (M Score)
```sql
CREATE TABLE monetary_sorted (
    id INT AUTO_INCREMENT PRIMARY KEY,
    CustomerID INT,
    Monetary DECIMAL(10, 2)
) ENGINE=InnoDB
SELECT 
    CustomerID, 
    Monetary 
FROM rfm_metrics
ORDER BY Monetary DESC;

SET @total_count = (SELECT COUNT(*) FROM monetary_sorted);

ALTER TABLE monetary_sorted ADD COLUMN percentile_rank FLOAT;

UPDATE monetary_sorted
SET percentile_rank = id / @total_count;

UPDATE rfm_metrics AS r
JOIN monetary_sorted AS m ON r.CustomerID = m.CustomerID
SET r.M_Score = CASE
    WHEN m.percentile_rank <= 0.2 THEN 5
    WHEN m.percentile_rank <= 0.4 THEN 4
    WHEN m.percentile_rank <= 0.6 THEN 3
    WHEN m.percentile_rank <= 0.8 THEN 2
    ELSE 1
END;
```

### Step 5: Final Table for RFM Analysis
```sql
CREATE TABLE rfm_table AS
SELECT 
    CustomerID, 
    Recency, 
    Frequency, 
    Monetary, 
    R_score, 
    F_score, 
    M_score
FROM rfm_metrics;
```
This table consolidates all metrics and scores for Power BI analysis.

---

## Power BI Implementation

### Data Connection
The `rfm_table` was connected to Power BI using the MySQL connector.

### Visualizations
1. **KPI Cards**:
   - Total Monetary Value
   - Average Recency
   - Total Frequency
   - Top Customer Spending

2. **Recency Distribution**:
   - Histogram showing the distribution of recency values across customers.

3. **Frequency Analysis**:
   - Bar chart displaying customer categories based on F_score.

4. **Monetary Analysis**:
   - Tree map showing customer segmentation by M_score.

5. **Top Customers by Spending**:
   - Bar chart showcasing the highest-spending customers.

6. **Monetary vs. Frequency Relationship**:
   - Scatter plot visualizing the correlation between frequency and monetary value.

7. **Segmented RFM Heatmap**:
   - Visualizing the interaction between R, F, and M scores.

---

## Insights
- **Top Customers**: Identified the highest-spending customers, enabling targeted marketing campaigns.
- **Customer Segments**: Segmentation based on R, F, and M scores helps prioritize efforts towards high-value customers.
- **Spending Patterns**: The Monetary vs. Frequency plot highlighted spending trends and anomalies.
- **Behavioral Insights**: Recency distribution revealed customer retention rates and potential churn risks.

---

This project demonstrates how to use RFM analysis to derive actionable insights, enhancing customer segmentation and improving business strategies.


