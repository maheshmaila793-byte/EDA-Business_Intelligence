# 📊 Task 2: Exploratory Data Analysis & Business Intelligence

## 🔹 Objective
Perform EDA on the cleaned dataset, answer business questions using SQL, and prepare a static dashboard mock‑up for Power BI.

---

## 🔹 Dataset
- **File:** `cleaned_dataset (2).xlsx`
- **Columns:** ID, CustomerName, Gender, DOB, Email, Product, Category, Quantity, Price, Date, Age
- **Derived Column:** Revenue = Quantity × Price

---

## 🔹 Code Workflow
1. **Data Cleaning**
   - Standardized gender labels
   - Filled missing ages with median
   - Removed duplicates
   - Converted `Date` to datetime format

2. **Descriptive Statistics**
   - Summary of Quantity, Price, Age
   - Frequency counts for Product, Gender, Category

3. **Univariate Analysis**
   - Histogram of Age
   - Bar chart of Category distribution
   - Pie chart of Gender split

4. **SQL Queries (Business Questions)**
   - Top 5 Products by Revenue (Overall)
   - Top 5 Products by Revenue (Last 6 Months)
   - Monthly Sales Trend
   - Average Spend by Gender
   - Category‑wise Revenue
   - Monthly User Acquisition Trend

5. **Multivariate Analysis**
   - Scatter plot: Age vs Revenue
   - Scatter plot: Quantity vs Revenue by Gender
   - Correlation heatmap
   - Pair plot of Age, Quantity, Price, Revenue

6. **KPI Calculations**
   - Total Revenue
   - Average Age of Customers
   - Top Product (Last 6 Months)
   - Monthly New Users (Latest Month)

7. **Export**
   - `dataset_for_dashboard.xlsx` for Power BI
   - SQL outputs as CSV
   - Plots as PNG

---

## 🔹 Dashboard (Static Mock‑Up)
- **KPIs:**
  - Total Revenue
  - Average Age of Customers
  - Top Product (Last 6 Months)
  - Monthly New Users (Latest Month)

- **Visuals:**
  - Age distribution histogram
  - Revenue by product/category/gender bar charts
  - Scatter plots (Age vs Revenue, Quantity vs Revenue)
  - Correlation heatmap

---

## 🔹 SQL Queries
```sql
-- Top 5 Products by Revenue (Overall)
SELECT Product, SUM(Revenue) AS TotalRevenue
FROM sales_data
GROUP BY Product
ORDER BY TotalRevenue DESC
LIMIT 5;

-- Top 5 Products by Revenue (Last 6 Months)
SELECT Product, SUM(Revenue) AS TotalRevenue
FROM sales_data
WHERE Date >= DATE('now','-6 months')
GROUP BY Product
ORDER BY TotalRevenue DESC
LIMIT 5;

-- Monthly Sales Trend
SELECT substr(Date,1,7) AS Month, SUM(Revenue) AS Revenue
FROM sales_data
GROUP BY Month
ORDER BY Month;

-- Average Spend by Gender
SELECT Gender, AVG(Revenue) AS AvgSpend
FROM sales_data
GROUP BY Gender;

-- Category-wise Revenue
SELECT Category, SUM(Revenue) AS Revenue
FROM sales_data
GROUP BY Category;

-- Monthly User Acquisition Trend
SELECT substr(Date,1,7) AS Month, COUNT(DISTINCT CustomerName) AS NewUsers
FROM sales_data
GROUP BY Month
ORDER BY Month;
