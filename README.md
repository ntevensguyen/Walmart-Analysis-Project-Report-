Title: Sales Data Analysis Project
1. Introduction:
The purpose of this project is to analyze sales data from a retail store to identify key trends and patterns. The project involves cleaning the dataset, performing exploratory data analysis (EDA), and extracting insights related to product sales, customer behavior, and revenue.

2. Data Cleaning:
The sales dataset was cleaned to make it more useful for analysis. This included:

Adding a time_of_day column to categorize transactions based on the time they occurred (Morning, Afternoon, Evening).
Adding a day_name column to show the day of the week each transaction took place.
Adding a month_name column to track transactions by the month.
sql
Copy code
ALTER TABLE sales ADD time_of_day VARCHAR(20) AFTER time;
UPDATE sales
SET time_of_day = 
CASE
    WHEN time >= '00:00:00' AND time < '12:00:00' THEN 'Morning'
    WHEN time >= '12:00:00' AND time < '18:00:00' THEN 'Afternoon'
    ELSE 'Evening'
END;
After adding the new columns, the data was updated accordingly to reflect accurate information for each transaction.

3. Exploratory Data Analysis (EDA):
A series of SQL queries were written to explore different aspects of the data:

Generic Analysis:
Number of unique cities: Found that the dataset contains several distinct cities, where transactions occur.

sql
Copy code
SELECT DISTINCT city FROM sales;
Cities with branch locations: Each city contains specific branch information, identified through this query.

sql
Copy code
SELECT DISTINCT city, branch FROM sales;
Product Analysis:
Unique product lines: The store offers a variety of products across several product lines.

sql
Copy code
SELECT DISTINCT product_line FROM sales;
Most common payment method: Identified the most frequently used payment methods by customers.

sql
Copy code
SELECT payment_method, COUNT(payment_method) AS cnt FROM sales GROUP BY payment_method ORDER BY cnt DESC;
Top-selling product line: Identified the product line that generated the most sales.

sql
Copy code
SELECT product_line, COUNT(product_line) AS num_sold FROM sales GROUP BY product_line ORDER BY num_sold DESC;
Revenue by month: Calculated total revenue per month to identify the best performing months.

sql
Copy code
SELECT month_name, SUM(total) AS total_revenue FROM sales GROUP BY month_name ORDER BY total_revenue DESC;
Sales Analysis:
Sales made per time of day on weekdays: This query highlights sales activity during different times of the day, excluding weekends.

sql
Copy code
SELECT time_of_day, day_name, COUNT(*) AS sales_made
FROM sales
GROUP BY time_of_day, day_name
HAVING day_name NOT IN ('Saturday', 'Sunday')
ORDER BY FIELD(day_name, 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday'),
FIELD(time_of_day, 'Morning', 'Afternoon', 'Evening');
Revenue by customer type: Analyzed which customer type (new or returning) contributed the most to the total revenue.

sql
Copy code
SELECT customer_type, SUM(total) AS revenue FROM sales GROUP BY customer_type ORDER BY revenue DESC;
4. Analysis & Results:
Top-selling product line: The most sold product line is the "Electronics" category.
Best-selling month: The highest sales were recorded in December, indicating a strong performance during the holiday season.
Most common payment method: The "Credit Card" was the most frequently used payment method.
Sales by time of day: Sales are highest in the Afternoon during weekdays, suggesting a peak in customer activity during that time.
5. Conclusion:
From this analysis, it’s clear that the store's strongest revenue periods align with the holiday season, and certain product lines like Electronics perform exceptionally well. The insights from customer behavior, such as peak sales times and the preference for certain payment methods, can inform targeted marketing strategies and operational planning. Additionally, the analysis of sales by branch and city can help the store identify areas of high demand and potential for expansion.

