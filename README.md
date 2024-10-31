# Chick-fil-A Sales Data Analysis

## Project Overview
This project provides insights into Chick-fil-A sales data by cleaning and analyzing the dataset to explore sales patterns, customer behavior, and product performance. Using SQL, I demonstrate data cleaning techniques and conduct exploratory data analysis (EDA) to address various business questions. The insights from this project can support data-driven decisions for improving customer satisfaction and operational efficiency.

## Dataset
The dataset contains:
- **Sales transactions**: Detailed information on transaction times, product lines, and total amounts.
- **Customer demographics**: Basic demographic information such as gender and customer type.
- **Branch and city information**: Identifies the location of each transaction.
  
### Project Structure
chickfila-sales-analysis/
├── data/
│   └── sample_sales_data.csv     # Sample data with select rows
├── queries/
│   ├── 01_data_cleaning.sql      # SQL file for data cleaning operations
│   ├── 02_exploratory_analysis.sql  # SQL file for exploratory data analysis
├── results/
│   └── example_output.csv        # Example output for select queries
└── README.md                     # Project README (this file)


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

