# Chick-fil-A Sales Data Analysis

## Project Overview
This project provides insights into Chick-fil-A sales data by cleaning and analyzing the dataset to explore sales patterns, customer behavior, and product performance. Using SQL, I demonstrate data cleaning techniques and conduct exploratory data analysis (EDA) to address various business questions. The insights from this project can support data-driven decisions for improving customer satisfaction and operational efficiency.

## Dataset
The dataset contains:
- **Sales transactions**: Detailed information on transaction times, product lines, and total amounts.
- **Customer demographics**: Basic demographic information such as gender and customer type.
- **Branch and city information**: Identifies the location of each transaction.
  
### Project Structure

- **data/**: Contains raw or sample data files.
    - `sample_sales_data.csv`: Sample dataset with select rows to provide a glimpse of the data.

- **queries/**: Holds SQL scripts for different parts of the analysis.
    - `01_data_cleaning.sql`: Script for cleaning and preparing the data.
    - `02_exploratory_analysis.sql`: Script for analyzing sales trends, popular items, revenue, etc.

- **results/**: A folder for storing outputs of queries.
    - `example_output.csv`: Example of output data from a specific query.

- **README.md**: Documentation of the project, including:
    - Overview of the project and purpose.
    - Instructions for running the queries.
    - Descriptions of the data and the queries used in analysis.



## Data Cleaning and Preparation
The data cleaning steps standardize date and time fields to create more usable categories and remove redundant information. Key steps include:

- **Creating `time_of_day` column**: Assigns each transaction a period of the day (Morning, Afternoon, Evening) based on the time of sale.
- **Adding `day_name` and `month_name` columns**: These fields display the weekday and month of each transaction, making it easier to analyze temporal patterns.

**Example Query**:
```sql
UPDATE sales
SET time_of_day = 
    CASE
        WHEN time >= '00:00:00' AND time < '12:00:00' THEN 'Morning'
        WHEN time >= '12:00:00' AND time < '18:00:00' THEN 'Afternoon'
        WHEN time >= '18:00:00' AND time <= '23:59:59' THEN 'Evening'
    END;
```
## Exploratory Data Analysis (EDA)
With the cleaned data, I explored questions about sales performance, customer preferences, and product demand. 
Some examples include:

1. Number of sales made in each time of the day per weekday
```sql
select time_of_day, day_name, count(*) sales_made
from sales
group by time_of_day, day_name
having day_name not in('Saturday','Sunday')
order by field(day_name,'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday'), 
field(time_of_day,'Morning', 'Afternoon','Evening')
;
```

2. The most common product line by gender
```sql
select gender, product_line, count(gender) as total_count
from sales
group by gender, product_line
order by 3 desc
;
```

3. Which branch sold more products than average product sold?
```sql
select branch, sum(quantity)
from sales
group by branch
having sum(quantity)>(select avg(quantity)from sales)
;
```
## Conclusion
This analysis of Chick-fil-A sales data revealed key insights into customer behavior, product popularity, and sales patterns. Through SQL data cleaning and categorization, I structured raw transaction data to enable clearer trend analysis.

Notable findings include:

- **Peak Sales Times:**
  - Afternoon hours show the highest sales, providing guidance for staffing and resource allocation.
Customer and Product Trends: Preferences vary by demographic, offering opportunities for targeted promotions.
Branch Performance: Identifying branches that outperform the average can guide best practices across locations.
This project refined my SQL skills and demonstrated how structured data analysis can drive smarter business decisions.
