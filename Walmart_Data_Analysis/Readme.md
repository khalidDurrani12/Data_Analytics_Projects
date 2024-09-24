# Walmart Sales Data Analysis

## Project Overview
This project aims to explore Walmart Sales data to identify top-performing branches and products, analyze sales trends of various products, and understand customer behavior. The objective is to study how Walmart can improve and optimize its sales strategies based on data-driven insights. The dataset was obtained from the [Kaggle Walmart Sales Forecasting Competition](https://www.kaggle.com/c/walmart-recruiting-store-sales-forecasting).

The competition provided historical sales data from 45 Walmart stores across different regions, each containing various departments. The dataset includes markdowns and promotions that affect sales, particularly during holidays, making it a challenge to predict sales trends accurately.

## Purposes of the Project
The key objectives of this project are:
- To gain insights into Walmart's sales data to understand the various factors influencing sales at different branches.
- To perform in-depth analysis of sales performance, customer segmentation, and product line performance.
- To identify sales strategies that could be improved and optimized.

## Data Overview
The dataset contains sales data from three Walmart branches located in Mandalay, Yangon, and Naypyitaw. It consists of 17 columns and 1000 rows.

### Data Columns:
| Column                | Description                          | Data Type         |
|-----------------------|--------------------------------------|-------------------|
| `invoice_id`           | Invoice of the sales made            | VARCHAR(30)       |
| `branch`               | Branch at which sales were made      | VARCHAR(5)        |
| `city`                 | Location of the branch               | VARCHAR(30)       |
| `customer_type`        | Type of customer                     | VARCHAR(30)       |
| `gender`               | Customer gender                      | VARCHAR(10)       |
| `product_line`         | Product line sold                    | VARCHAR(100)      |
| `unit_price`           | Price per product                    | DECIMAL(10, 2)    |
| `quantity`             | Quantity sold                        | INT               |
| `VAT`                  | Tax amount on purchase               | FLOAT(6, 4)       |
| `total`                | Total cost of purchase               | DECIMAL(10, 2)    |
| `date`                 | Date of purchase                     | DATE              |
| `time`                 | Time of purchase                     | TIMESTAMP         |
| `payment_method`       | Payment method used                  | VARCHAR(15)       |
| `cogs`                 | Cost of Goods Sold (COGS)            | DECIMAL(10, 2)    |
| `gross_margin_percentage` | Gross margin percentage           | FLOAT(11, 9)      |
| `gross_income`         | Gross income from sales              | DECIMAL(10, 2)    |
| `rating`               | Customer rating                      | FLOAT(2, 1)       |

## Analysis List
### Product Analysis:
- Identify and analyze different product lines.
- Determine the best-performing product lines and those requiring improvement.

### Sales Analysis:
- Analyze sales trends and their effectiveness.
- Identify seasonal or promotional periods influencing sales.

### Customer Analysis:
- Study customer segmentation, behavior, and profitability.

## Approach Used
### Data Wrangling:
- Inspection of data to detect NULL values.
- Data replacement techniques applied to handle missing or NULL values (using `NOT NULL` constraints during table creation).

### Feature Engineering:
- **Time of Day**: Created a new column to categorize sales by Morning, Afternoon, and Evening.
- **Day Name**: Extracted the day of the week (Mon, Tue, Wed, etc.) to determine busiest days.
- **Month Name**: Extracted the month to find out which months have the highest sales.

### Exploratory Data Analysis (EDA):
- Performed EDA to answer business questions such as sales trends by product line, branch performance, customer segments, and revenue distribution.

## Business Questions Answered
### General:
- How many unique cities are in the data?
- Which city hosts each branch?

### Product:
- What are the most common product lines and payment methods?
- Which product lines and months generate the most revenue?
- What branch has the largest revenue and VAT?
- Which product line has the highest ratings and sales performance?

### Customer:
- What is the gender distribution of customers by branch?
- Which customer type brings in the most revenue?
- Which customer type has the highest VAT contribution?

## Revenue and Profit Calculations
**COGS (Cost of Goods Sold)**:  
$COGS = unit\_price \times quantity$

**VAT Calculation (5% of COGS)**:  
$VAT = 0.05 \times COGS$

**Total Revenue Calculation**:  
$total = VAT + COGS$

**Gross Profit Calculation**:  
$gross\_profit = total\_revenue - COGS$

**Gross Margin Percentage**:  
$gross\_margin\_pct = \frac{gross\_income}{total\_revenue}$

### Example Calculation for the First Row:
Given the data:
- Unit Price = 45.79
- Quantity = 7

The calculations are as follows:
- **COGS**:  
  $COGS = 45.79 \times 7 = 320.53$
- **VAT**:  
  $VAT = 0.05 \times 320.53 = 16.0265$
- **Total**:  
  $total = VAT + COGS = 16.0265 + 320.53 = 336.5565$
- **Gross Margin Percentage**:  
  $gross\_margin\_pct = \frac{16.0265}{336.5565} \approx 4.76\%$

## Code Snippet
For the full SQL code, refer to the `SQL_queries.sql` file.

### Create Database:
```sql
CREATE DATABASE IF NOT EXISTS walmartSales;
CREATE TABLE IF NOT EXISTS sales(
  invoice_id VARCHAR(30) NOT NULL PRIMARY KEY,
  branch VARCHAR(5) NOT NULL,
  city VARCHAR(30) NOT NULL,
  customer_type VARCHAR(30) NOT NULL,
  gender VARCHAR(30) NOT NULL,
  product_line VARCHAR(100) NOT NULL,
  unit_price DECIMAL(10, 2) NOT NULL,
  quantity INT NOT NULL,
  tax_pct FLOAT(6, 4) NOT NULL,
  total DECIMAL(12, 4) NOT NULL,
  date DATETIME NOT NULL,
  time TIME NOT NULL,
  payment VARCHAR(15) NOT NULL,
  cogs DECIMAL(10, 2) NOT NULL,
  gross_margin_pct FLOAT(11, 9),
  gross_income DECIMAL(12, 4),
  rating FLOAT(2, 1)
);
