
# Business Requirements

## 1. Business Context

Olist is an e-commerce marketplace in Brazil. Marketplace performance depends on sales, product availability, customer purchasing behavior, payment processing, and successful delivery.

This project uses the public Olist dataset to investigate business performance and identify opportunities for improvement.

## 2. Problem Statement

The objective is to transform raw marketplace data into reliable business metrics and actionable insights that help stakeholders understand sales performance, customer retention, product demand, and delivery experience.

## 3. Stakeholders

- Business and sales managers
- Marketing teams
- Customer experience teams
- Logistics and operations teams
- Marketplace leadership

## 4. Business Questions

### Sales Performance
- How does sales value change over time?
- Which months show the highest and lowest sales?
- How many orders are placed and how does order value vary?

### Product Performance
- Which product categories contribute the most to sales?
- Which categories have high order volume but weaker review scores?
- How do product prices and freight charges vary across categories?

### Customer Behavior
- How many distinct customers place orders?
- What proportion of customers place more than one order?
- How does customer purchasing behavior vary over time?

### Geographic Performance
- Which Brazilian states contribute the most to sales?
- How do order volumes and delivery outcomes vary by state?

### Payment Analysis
- Which payment methods are most commonly used?
- How does order value vary by payment method?
- How frequently are installment payments used?

### Delivery and Customer Experience
- What proportion of delivered orders arrive on or before the estimated delivery date?
- How long does delivery take?
- Are late deliveries associated with lower review scores?

## 5. KPI Definitions

### Total Orders
Count of distinct valid order IDs included in the analysis. Excluded statuses and cancellations will be documented.

### Gross Merchandise Value (GMV)
Sum of item prices for eligible orders. Freight will be reported separately unless a metric is explicitly defined to include it.

### Average Order Value (AOV)
GMV divided by the number of eligible orders, using the same order population in both calculations.

### Repeat-Customer Rate
Percentage of distinct customers with more than one qualifying order divided by all distinct customers with at least one qualifying order in the selected population.

Use the customer_unique_id field to identify customers across orders, rather than customer_id, which can represent separate order-specific customer records.

### On-Time Delivery Rate
Percentage of eligible delivered orders delivered on or before their estimated delivery date.

Orders without the required delivery timestamps will be excluded from this KPI and reported separately.

### Average Review Score
Arithmetic mean of available review scores for the defined order population. The review population and treatment of multiple reviews will be documented.

## 6. Analytical Approach

1. Inspect source tables and data types.
2. Validate identifiers, missing values, duplicates, and relationships.
3. Define analysis populations and KPI calculation rules.
4. Clean and analyze data using Python.
5. Reproduce relevant business metrics using SQL.
6. Build interactive Power BI views.
7. Summarize findings, limitations, and recommendations.

## 7. Assumptions and Limitations

- The dataset primarily covers 2016–2018 and does not represent current marketplace performance.
- Sales value does not equal profit.
- Correlation between delivery delays and review scores does not establish causation.
- Missing values and excluded records will be documented before KPI reporting.
- Analysis will distinguish order-level, item-level, payment-level, and customer-level metrics.
- Findings will be reported only after validation against the underlying data.

## 8. Success Criteria

- Data quality checks are documented and reproducible.
- KPI definitions are explicit and consistently applied.
- Python and SQL results agree where their populations and calculations match.
- The dashboard communicates business performance clearly.
- Recommendations are supported by measured evidence.
- The repository contains understandable documentation and reproducible analytical assets.
