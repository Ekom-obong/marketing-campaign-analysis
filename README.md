# Superstore Sales Analysis

## Project Overview

This project analyzes sales data from a sample superstore dataset using Python. 
The dataset includes details on customer segments, shipping modes, geographical distribution, product categories, and financial metrics such as sales, profit, and quantity.

## Dataset

Source: SampleSuperstore.csv

Number of Records: 9994

Number of Columns: 13

Key Columns: Ship Mode, Segment, Country, City, State, Postal Code, Region, Category, Sub-Category, Sales, Quantity, Discount, Profit

## Tool and library Used

Python: Tool used for this analysis

Pandas

Matplotlib

Seaborn

NumPy

# Data Cleaning and Preparation
Loading of data
```Python
import pandas as pd 
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
data_df = pd.read_csv(r"C:\Users\essie\Desktop\HNG\SampleSuperstore.csv")
data_df.head()
```
Data Overview
```python
print(data_df.info())
print(data_df.describe())
```
Handling Duplicates
```python
if data_df.duplicated().sum() > 0:
    print('Duplicates found')
    data_df = data_df.drop_duplicates()
print(f"Number of rows after removing duplicates: {len(data_df)}")
````
## Exploratory Data Analysis

Customer segmentation
```python
no_customers = data_df['Segment'].value_counts().reset_index()
no_customers.columns = ['Customer Type', 'Total Customers']
print(no_customers)
plt.pie(no_customers['Total Customers'], labels=no_customers['Customer Type'], autopct='%1.1f%%')
plt.title('Customer Distribution by Segment')
plt.show()
```
Sales by Customer Type
```pthon
sales_by_category = data_df.groupby('Segment')['Sales'].sum().reset_index()
sales_by_category.columns = ['Customer Type', 'Total Sales']
plt.bar(sales_by_category['Customer Type'], sales_by_category['Total Sales'])
plt.xlabel('Customer Type')
plt.ylabel('Total Sales')
plt.title('Sales by Customer Segment')
plt.show()
```
Geographic Analysis
```python
state_sales = data_df.groupby('State')['Sales'].sum().reset_index()
top_states_sales = state_sales.sort_values(by='Sales', ascending=False).head(5)
sns.barplot(x='Sales', y='State', data=top_states_sales, palette='viridis')
plt.title('Top 5 States by Sales')
plt.show()
```
Product Analysis
```python
sales_per_category = data_df.groupby('Category')['Sales'].sum().reset_index()
sales_per_category.columns = ['Category', 'Total Sales']
plt.pie(sales_per_category['Total Sales'], labels=sales_per_category['Category'], autopct='%1.1f%%')
plt.title('Sales per Product Category')
plt.show()
```
Profit Analysis
```python
product_profit = data_df.groupby('Sub-Category')['Profit'].sum().reset_index()
top_profit_subcategories = product_profit.sort_values(by='Profit', ascending=False).head(5)
sns.barplot(x='Profit', y='Sub-Category', data=top_profit_subcategories, palette='bwr')
plt.title('Top 5 Most Profitable Product Subcategories')
plt.show()
```
## Summary/insights
- Top Customer Segment: Consumers

- Most Used Shipping Mode: Standard Class

- Top State for Sales: California

- Top Product Category: Technology

- Most Profitable Product Subcategory: Copiers

## Conclusion

This analysis provides valuable insights into customer behavior, sales performance, and product profitability, which can help improve business strategies.
