# Sales Data Analysis Project

## 1. Introduction:
The purpose of this project is to analyze sales data from a retail store to identify key trends and patterns. The project involves cleaning the dataset, performing exploratory data analysis (EDA), and extracting insights related to product sales, customer behavior, and revenue.

## 2. Data Cleaning:
The sales dataset was cleaned to make it more useful for analysis. This included:

- Adding a `time_of_day` column to categorize transactions based on the time they occurred (Morning, Afternoon, Evening).
- Adding a `day_name` column to show the day of the week each transaction took place.
- Adding a `month_name` column to track transactions by the month.

```sql
ALTER TABLE sales ADD time_of_day VARCHAR(20) AFTER time;

UPDATE sales
SET time_of_day = 
CASE
    WHEN time >= '00:00:00' AND time < '12:00:00' THEN 'Morning'
    WHEN time >= '12:00:00' AND time < '18:00:00' THEN 'Afternoon'
    ELSE 'Evening'
END;
