# ATLIQ HARDWARE: Finance and Supply Chain Analytics

## Project Overview

Atliq Hardware, a leading provider of computer hardware such as PCs, printers, and mice, faced significant challenges in analyzing its growing sales and market data. The reliance on large Excel files for data processing resulted in performance bottlenecks, limiting the ability to derive actionable insights and make timely decisions.

This project was designed to overcome these challenges by utilizing MySQL for efficient data transformation and analysis. The objective was to generate meaningful insights into sales performance, market dynamics, customer behavior, and supply chain forecasting. This comprehensive analytics project not only addressed Atliq Hardware's existing reporting inefficiencies but also provided advanced tools for decision-making across finance and supply chain operations.

#### Product Division
| Product Division | Products                              |
|------------------|---------------------------------------|
| **PC**           | Personal Laptop, Gaming Laptop       |
| **P&A**          | Keyboard, Processor, Motherboard, Mouse |
| **N&S**          | Wifi Extenders, USB Flash Drives     |

#### Product Segments
The products fall into the following major segments:
- Storage
- Peripherals
- Notebook
- Desktop
- Accessories


## Database Overview

#### Tables

| Table Name                   | Description                                                                 |
|------------------------------|-----------------------------------------------------------------------------|
| **dim_customer**             | Contains customer details such as customer ID, name, market, and region.   |
| **dim_product**              | Includes product details like product ID, name, and division information.  |
| **dim_date**                 | Provides calendar dates, fiscal year, and fiscal quarter information.      |
| **fact_sales_monthly**       | Stores monthly sales data including quantity sold and revenue.             |
| **fact_forecast_monthly**    | Contains forecasted sales data for each product and customer.              |
| **fact_gross_price**         | Details the gross price of products before any deductions.                 |
| **fact_freight_cost**        | Captures freight costs associated with product delivery.                   |
| **fact_manufacturing_cost**  | Holds manufacturing cost data for each product.                            |
| **fact_pre_invoice_deductions** | Tracks pre-invoice deductions applied to sales.                        |
| **fact_post_invoice_deductions** | Tracks post-invoice deductions affecting net sales.                    |

#### Views

| View Name                   | Description                                                                 |
|-----------------------------|-----------------------------------------------------------------------------|
| **Gross Sales**             | Provides the total gross sales for all products and customers.             |
| **Net Sales**               | Calculates net sales after applying all deductions.                        |
| **sales_pre_invoice_discount** | Captures pre-invoice discount details for analysis.                     |
| **sales_post_invoice_discount** | Tracks post-invoice deductions for calculating net sales.              |

#### Stored Procedures

| Procedure Name                                   | Description                                                                 |
|-------------------------------------------------|-----------------------------------------------------------------------------|
| **top n markets by net sales**                  | Retrieves the top `n` markets by net sales for a given fiscal year.         |
| **top n products by net sales**                 | Fetches the top `n` products by net sales for a specific fiscal year.       |
| **top n products by division by quantity sold** | Identifies the top `n` products per division based on quantity sold.        |
| **top n customers by net sales**                | Retrieves the top `n` customers by net sales for a specified market and year.|
| **get monthly gross sales for customer**        | Generates a gross sales report for a specific customer.                     |
| **get market badge**                            | Assigns a performance badge to markets based on sales thresholds.           |
| **get forecast accuracy**                       | Generates a forecast accuracy report for a given fiscal year.               |

#### Functions

| Function Name                | Description                                                                 |
|------------------------------|-----------------------------------------------------------------------------|
| **get_fiscal_year**          | Determines the fiscal year for a given date.                               |
| **get_fiscal_quarter**       | Determines the fiscal quarter for a given date.                            |


## Key Highlights

#### 1. Revenue Analysis
- Monthly Gross Sales Reports: Enabled clear tracking of revenue trends to support better financial planning.
- Product-Level Insights: Highlighted revenue contributions at the product and variant levels, identifying top-performing products.
#### 2. Customer and Market Insights
- Customer Segmentation: Provided dynamic customer-specific financial analysis, scalable across various customers and markets.
- Market Classification: Implemented a systematic approach for assessing market performance and prioritizing high-value regions.
#### 3. Streamlined Reporting
Stored Procedures: Automated dynamic report generation, reducing manual efforts and improving reporting efficiency.

#### Finance Analytics
##### Pre-Invoice Discount Reports
- Specific Customer Query: Retrieves pre-invoice discount data for a particular customer (e.g., customer 90002002) in FY 2021.
- All Customers Query: Extends the logic to include all customers in the same fiscal year.
##### Performance Improvements
- Optimization 1: Introduced dim_date to avoid calling functions repeatedly, enhancing query performance.
- Optimization 2: Added fiscal_year directly to the fact_sales_monthly table to streamline joins.
##### Net Sales Calculation
- Common Table Expressions (CTEs): Simplified logic for calculating net_invoice_sales.
- Reusable View (sales_preinv_discount): Encapsulated pre-invoice discount logic for better reusability.
- Post-Invoice Deductions and Net Sales
  - Post-Invoice Deductions View (sales_postinv_discount): Adds post-invoice deductions to the pre-invoice discount data.
  - Final Net Sales View (net_sales): Combines all deductions to calculate the final net sales value.

#### Top Markets and Customers
- Top Markets Query: Identifies the top 5 markets by net sales in FY 2021.
- Stored Procedures: Enables parameterized retrieval of top markets or customers by net sales for specific markets and fiscal years.
- Advanced Analytics with Window Functions
  - Customer Contribution Analysis: Calculates each customer's percentage contribution to total net sales.
  - Regional Sales Distribution: Analyzes net sales distribution for customers within their regions.

#### Product Analytics
- Top Products by Division: Highlights the most sold products within each division.
- Generalized Product Analytics Procedure: Retrieves the top n products per division.

#### Supply Chain Analytics
The supply chain analytics module focuses on creating a robust dataset and analyzing forecast accuracy to optimize inventory management and improve customer satisfaction.
##### Key Focus Areas
- Helper Table (fact_act_est): Consolidates actual sales and forecasted quantities for all products and customers, ensuring missing data is addressed by setting null values to zero.
- Forecast Accuracy Reporting: Measures forecast reliability with metrics such as net error, absolute error, and accuracy percentage.

