# Retail Orders Data Analysis

![System Overview](https://github.com/rohitaragde/OrderDataSQL-ETL-Analysis/blob/master/system_overview.png)

This project demonstrates the process of downloading, cleaning, processing, and analyzing retail order data using Python and SQL. The dataset used is from Kaggle, and the analysis is performed on SQL Server.

## Project Objectives
- **Sales Trends Analysis:** Identify top-selling products and regions, and analyze revenue generation across different periods.
- **Profitability Insights:** Determine the most profitable product subcategories and analyze profit growth trends.
- **Month-Over-Month Sales Comparison:** Compare sales performance between 2022 and 2023 to assess growth trends.
- **Product Performance Analysis:** Evaluate the highest revenue-generating products and regions to inform inventory and marketing strategies.

## Deliverables
- **SQL Scripts:** A set of SQL scripts designed to extract insights from the retail orders dataset.
- **Data Analysis Report:** A detailed report summarizing the findings and insights derived from the data analysis.
- **System Overview Image:** Visual representation of the data flow from extraction to analysis.

## Technologies Used
- Python
- Pandas
- SQL Server
- SQLAlchemy
- pyODBC

## Project Overview

The project involves:
1. **Data Extraction**: Downloading a dataset from Kaggle using Kaggle API.
2. **Data Cleaning & Processing**: Using Pandas to clean and transform the data.
3. **Data Loading**: Importing the processed data into SQL Server.
4. **Data Analysis**: Performing SQL queries to derive meaningful insights.

## Dataset

- **Source**: [Kaggle - Retail Orders](https://www.kaggle.com/datasets/ankitbansal06/retail-orders)
- **File**: `orders.csv`

## Project Structure

- **Python Script**: Handles data download, cleaning, processing, and loading into SQL Server.
- **SQL Script**: Contains queries to perform ETL analysis on the loaded data.

## Setup and Usage

### 1. Install and Import Required Libraries

```python
!pip install kaggle pandas sqlalchemy pyodbc
import kaggle
import zipfile
import pandas as pd
import sqlalchemy as sal

### 2. Download and Extract Dataset
!kaggle datasets download ankitbansal06/retail-orders -f orders.csv

# Extract the dataset
zip_ref = zipfile.ZipFile('orders.csv.zip')
zip_ref.extractall()
zip_ref.close()

### 3. Data Cleaning and Processing
df = pd.read_csv('orders.csv', na_values=['Not Available', 'unknown'])

# Rename columns
df.columns = df.columns.str.lower().str.replace(' ', '_')

# Derive new columns
df['profit_margin'] = (df['sales'] - df['profit']) / df['sales']
df['order_month'] = pd.to_datetime(df['order_date']).dt.to_period('M')

### 4. Load Data into SQL Server

# Define SQL Server connection details
engine = sal.create_engine('mssql+pyodbc://username:password@server/database?driver=ODBC+Driver+17+for+SQL+Server')

# Load the dataframe into SQL Server
df.to_sql('retail_orders', engine, if_exists='replace', index=False)



