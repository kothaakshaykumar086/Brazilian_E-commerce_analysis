
# Brazilian E-Commerce Business Intelligence

## Project Overview

An end-to-end data analytics project using the Brazilian E-Commerce Public Dataset by Olist. The objective is to analyze marketplace sales, customer purchasing behavior, product performance, payment patterns, and delivery operations to develop actionable business recommendations.

This project demonstrates a practical analytics workflow using Python, SQL, and Power BI.

## Business Problem

E-commerce businesses need to understand what drives sales, which products and regions contribute to performance, whether customers return to purchase again, and how delivery experiences relate to customer satisfaction.

This project investigates these questions using transaction and operational data from Olist.

## Business Objectives

- Analyze sales and order trends over time.
- Identify high-performing product categories and geographic markets.
- Understand customer purchasing and repeat-purchase behavior.
- Evaluate payment methods and order values.
- Measure delivery performance and investigate its association with review scores.
- Translate analytical findings into evidence-based business recommendations.

## Tools and Technologies

- Python
- Pandas and NumPy
- Matplotlib and Seaborn
- MySQL
- Power BI
- Git and GitHub

## Project Phases

1. Business understanding and project planning
2. Data acquisition and quality assessment
3. Data cleaning and exploratory data analysis with Python
4. SQL-based business analysis
5. Interactive Power BI dashboard development
6. Business insights, recommendations, and documentation

## Key Performance Indicators

- Total orders
- Gross merchandise value (GMV)
- Average order value
- Monthly sales trends
- Repeat-customer rate
- On-time delivery rate
- Average review score

KPI definitions, calculation rules, and exclusions will be documented before analysis.

## Dataset

Source: [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

The dataset contains related tables covering orders, customers, order items, products, sellers, payments, reviews, and geographic information.

The available data primarily covers 2016–2018. All findings will be interpreted within this period and the dataset's limitations.

## Repository Structure

```text
docs/       Business requirements and project roadmap
notebooks/  Python analysis notebooks
sql/        Database schema and analytical queries
reports/    Analysis outputs and dashboard screenshots
powerbi/    Power BI report files
```

## Current Status

Phase 1: Business requirements and project planning.

Analytical findings and dashboard deliverables will be added as the project progresses.

## Data and Methodology Notes

- Sales value and profit are different measures. Profit will not be reported without reliable cost data.
- Repeat-customer analysis will use the dataset's customer identifier that represents a unique customer across orders.
- Delivery performance and review-score relationships will be treated as associations, not proof of causation.
- Data quality issues, assumptions, and metric definitions will be documented.

## Author
KOTHA AKSHAY KUMAR
Data Analytics Portfolio Project
