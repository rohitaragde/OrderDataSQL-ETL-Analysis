# Retail Orders Data Analysis

![System Overview](https://github.com/rohitaragde/OrderDataSQL-ETL-Analysis/blob/master/system_overview.png)

This project demonstrates the process of downloading, cleaning, processing, and analyzing retail order data using Python and SQL. The dataset used is from Kaggle, and the analysis is performed on SQL Server.

## Project Overview

The project involves:
1. **Data Extraction**: Downloading a dataset from Kaggle using Kaggle API.
2. **Data Cleaning & Processing**: Using Pandas to clean and transform the data.
3. **Data Loading**: Importing the processed data into SQL Server.
4. **Data Analysis**: Performing SQL queries to derive meaningful insights.

## Dataset

- **Source**: [Kaggle - Retail Orders](https://www.kaggle.com/datasets/ankitbansal06/retail-orders)
- **File**: `orders.csv`
- **License**: CC0-1.0

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
