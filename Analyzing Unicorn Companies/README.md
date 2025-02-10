# Unicorn Companies Dashboard Project 

## Project Overview
This project involves building a comprehensive **Unicorn Companies Dashboard** using SQL for data querying and Power BI for visualization. The dashboard provides insights into unicorn companies' valuations, countries, industries, and trends. Below are the details of the process, including the SQL queries used and the steps taken to build the dashboard.

---

## Dashboard Preview

Below is a snapshot of the interactive dashboard: ![Dashboard](https://github.com/CodeVistaPro/SQL-Projects/blob/main/Analyzing%20Unicorn%20Companies/Unicorn%20Companies%20Analysis.png)

---

## Dataset Details
The dataset, `unicorn_df`, contains information about unicorn companies, including the following columns:
- `Company`: Name of the company.
- `Valuation`: Valuation in billions.
- `Country`: The country where the company is based.
- `City`: The city where the company is headquartered.
- `Industry`: The industry to which the company belongs.
- `Date Joined`: The date the company joined the unicorn list.
- `Year`: The year the company joined the unicorn list.
- `Month`: The month the company joined the unicorn list.

---

## SQL Queries Used
Below are the SQL queries used for creating KPIs, charts, and slicers:

### **KPI Queries for Dashboard Cards**

#### 1. Total Number of Unicorn Companies
```sql
SELECT COUNT(DISTINCT Company) AS Total_Unicorns FROM unicorn_df;
```

#### 2. Total Valuation of All Unicorns (in Billion)
```sql
SELECT SUM(Valuation) AS Total_Valuation FROM unicorn_df;
```

#### 3. Average Valuation of a Unicorn (in Billion)
```sql
SELECT AVG(Valuation) AS Avg_Valuation FROM unicorn_df;
```

#### 4. Most Valuable Unicorn Company
```sql
SELECT Company, Valuation 
FROM unicorn_df 
ORDER BY Valuation DESC 
LIMIT 1;
```

#### 5. Country with the Most Unicorns
```sql
SELECT Country, COUNT(*) AS Unicorn_Count 
FROM unicorn_df 
GROUP BY Country 
ORDER BY Unicorn_Count DESC 
LIMIT 1;
```

#### 6. Industry with the Most Unicorns
```sql
SELECT Industry, COUNT(*) AS Industry_Count 
FROM unicorn_df 
GROUP BY Industry 
ORDER BY Industry_Count DESC 
LIMIT 1;
```

#### 7. Year with the Highest Number of New Unicorns
```sql
SELECT Year, COUNT(*) AS New_Unicorns 
FROM unicorn_df 
GROUP BY Year 
ORDER BY New_Unicorns DESC 
LIMIT 1;
```

---

### **Chart Queries**

#### 1. Unicorn Count by Country (Top 10) - Bar Chart
```sql
SELECT Country, COUNT(*) AS Unicorn_Count 
FROM unicorn_df 
GROUP BY Country 
ORDER BY Unicorn_Count DESC 
LIMIT 10;
```

#### 2. Unicorn Valuation by Industry - Pie Chart
```sql
SELECT Industry, SUM(Valuation) AS Total_Valuation 
FROM unicorn_df 
GROUP BY Industry 
ORDER BY Total_Valuation DESC;
```

#### 3. New Unicorns Over the Years - Line Chart
```sql
SELECT Year, COUNT(*) AS New_Unicorns 
FROM unicorn_df 
GROUP BY Year 
ORDER BY Year ASC;
```

#### 4. Monthly Trend of New Unicorns - Area Chart
```sql
SELECT Month, COUNT(*) AS New_Unicorns 
FROM unicorn_df 
GROUP BY Month 
ORDER BY FIELD(Month, 'January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December');
```

#### 5. Top Cities with Most Unicorns - Horizontal Bar Chart
```sql
SELECT City, COUNT(*) AS Unicorn_Count 
FROM unicorn_df 
GROUP BY City 
ORDER BY Unicorn_Count DESC 
LIMIT 10;
```

---

### **Slicer Queries**

#### 1. Unique Country List for Slicer
```sql
SELECT DISTINCT Country FROM unicorn_df ORDER BY Country;
```

#### 2. Unique Industry List for Slicer
```sql
SELECT DISTINCT Industry FROM unicorn_df ORDER BY Industry;
```

#### 3. Unique Years for Slicer
```sql
SELECT DISTINCT Year FROM unicorn_df ORDER BY Year;
```

---

## Dashboard Features

### **KPI Cards**
- **Total Unicorns**: Displays the total number of unique unicorn companies.
- **Total Valuation**: Displays the total valuation of all unicorn companies.
- **Most Valuable Company**: Shows the unicorn company with the highest valuation.
- **Top Country**: Displays the country with the most unicorn companies.
- **Top Year**: Shows the year with the highest number of unicorn companies added.

### **Charts & Insights**

1. **Top Countries by Unicorn Count**:
   - **Chart Type**: Horizontal Bar Chart
   - **Insight**: Highlights the countries with the most unicorn companies. For example, the United States leads with the highest number of unicorns, followed by China and India.

2. **Unicorn Valuation by Industry**:
   - **Chart Type**: Pie Chart
   - **Insight**: Shows the distribution of total unicorn valuations across industries. It reveals which industries dominate unicorn company valuations, such as Enterprise Tech and Financial Services.

3. **New Unicorns Over the Years**:
   - **Chart Type**: Line Chart
   - **Insight**: Tracks the trend of unicorn companies over the years, helping to understand the growth pattern of unicorn startups.

4. **Monthly Trend of New Unicorns**:
   - **Chart Type**: Area Chart
   - **Insight**: Displays the trend of unicorn companies added each month, highlighting the most active months for new unicorns.

5. **Top Cities by Unicorn Count**:
   - **Chart Type**: Horizontal Bar Chart
   - **Insight**: Identifies cities with the highest concentration of unicorn companies, such as San Francisco and New York.

---

### **Slicers**
- **Industry**: Filter the visuals by industry.
- **Country**: Filter the visuals by country.
- **Year**: Filter the visuals by year.

---

## Tools Used
- **SQL**: Used for data querying and transformation.
- **Power BI**: Used for building the interactive dashboard.

---

This project demonstrates the effective use of SQL for querying data and Power BI for creating visually appealing and insightful dashboards. Let me know if you need further assistance!


