# Data Quality Assessment

## 1. Dataset Overview

- Source: Brazilian E-Commerce Public Dataset by Olist
- Format: CSV
- Inspection tool: Python and Pandas
- Status: Initial profiling completed

## 2. Issues Identified

### Geolocation
- Duplicate rows were identified.
- Further investigation is required before removing duplicates.

### Orders
- Some timestamp fields contain missing values.
- Missing delivery timestamps must be evaluated against order status.

### Order Reviews
- Missing values were identified.
- Affected columns and percentages will be documented.

### Products
- Missing product attributes were identified.
- Missing-value percentages will be used to prioritize further investigation.

### Date and Time Columns
- Some timestamp columns were loaded as `object` (text-like) data types.
- Relevant columns will be converted to datetime during the cleaning phase.

## 3. Cleaning Principles

- Preserve the original raw data.
- Investigate before removing duplicates.
- Do not automatically remove canceled or undelivered orders.
- Handle missing values according to the business meaning of each column.
- Validate changes after cleaning.

## 4. Next Steps

1. Complete missing-value and duplicate analysis.
2. Convert relevant date columns to datetime.
3. Investigate data-quality issues.
4. Validate the cleaned datasets.

### Delivered Orders with Missing Customer Delivery Timestamps

- **Records affected:** 8 orders
- **Observed issue:** Orders marked as `delivered` have a missing `order_delivered_customer_date`.
- **Additional finding:** 7 records have a carrier delivery timestamp, while 1 record is also missing that timestamp.
- **Impact:** Actual delivery duration and on-time delivery status cannot be calculated reliably for these 8 orders using the missing customer delivery date.
- **Planned treatment:** Preserve the records in the raw dataset. Exclude them only from metrics that require an actual customer delivery timestamp, and disclose the exclusion count.
- **Limitation:** The reason for the missing timestamps cannot be established from these fields alone.

### Datetime Conversion

- Converted the relevant order timestamp columns to Pandas datetime format in a separate DataFrame named `orders_clean`.
- Preserved the original `orders` DataFrame.
- Compared missing-value counts before and after conversion.
- Result: Missing-value counts remained unchanged, indicating that the conversion did not introduce additional missing values in the selected columns.
- Remaining issue: Missing timestamps require further investigation based on order status and analytical purpose.

### Geolocation Data Quality

**Issue identified:** The geolocation dataset contains 261,831 completely duplicated rows. It also contains multiple coordinate pairs for many ZIP-code prefixes.

**Key findings:**
- 19,015 unique ZIP-code prefixes were identified.
- 17,781 prefixes (approximately 93.5%) have multiple coordinate pairs.
- The median number of coordinate pairs per prefix is 22.
- One ZIP-code prefix has as many as 746 distinct coordinate pairs.

**Decision:** Preserve the original geolocation data and remove only completely identical rows in a separate cleaned DataFrame. Do not arbitrarily retain one coordinate per ZIP prefix, because this may discard geographic information. If a single representative point is needed for mapping, aggregate coordinates by prefix and document that the resulting location is approximate.

**Business relevance:** This assessment helps prevent inaccurate geographic analysis when comparing customer locations, order distribution, or regional performance.

### Customer Reviews Data Quality

**Dataset size:** 99,224 rows and 7 columns.

**Issues identified:**
- 87,656 missing review titles (approximately 88.34%).
- 58,247 missing review messages (approximately 58.70%).
- No completely duplicated rows.
- 547 orders have multiple review records.

**Review score distribution:**
- 1 star: 11,424 reviews (11.51%).
- 2 stars: 3,151 reviews (3.18%).
- 3 stars: 8,179 reviews (8.24%).
- 4 stars: 19,142 reviews (19.29%).
- 5 stars: 57,328 reviews (57.78%).

**Decision:** Preserve missing review titles and messages because written feedback is optional. Retain all review records and investigate orders with multiple reviews before aggregating scores.

**Business relevance:** Review scores can support customer satisfaction analysis. They can later be compared with delivery delays and other order characteristics to investigate possible relationships with customer experience.

### Order Payments Data Quality

**Dataset size:** 103,886 rows and 5 columns.

**Quality checks:**
- No missing values were found.
- No completely duplicated rows were found.
- Three records use the `not_defined` payment type.
- The minimum payment value is 0.00.

**Payment method distribution:**
- Credit card: 76,795 records (73.92%).
- Boleto: 19,784 records (19.04%).
- Voucher: 5,775 records (5.56%).
- Debit card: 1,529 records (1.47%).
- Not defined: 3 records (0.003%).

**Payment value summary:**
- Mean: 154.10.
- Median: 100.00.
- Minimum: 0.00.

**Decision:** Preserve the original payment data. Investigate the three `not_defined` records and zero-value payments before deciding how to handle them in specific analyses. Do not remove payment records merely because their values or categories appear unusual.

**Business relevance:** Payment data can be used to analyze payment-method preferences and order payment values. Payment records must be aggregated carefully because an order may have multiple payment entries.

### Order Items Data Quality

**Dataset size:** 112,650 rows and 7 columns.

**Quality checks:**
- No missing values were found.
- No completely duplicated rows were found.
- No zero or negative item prices were found.
- No negative freight values were found.
- 9,803 orders contain multiple item records.

**Price summary:**
- Mean item price: 120.65.
- Median item price: 74.99.
- Minimum item price: 0.85.
- Maximum item price: 6,735.00.

**Freight summary:**
- Mean freight value: 19.99.
- Median freight value: 16.26.
- Minimum freight value: 0.00.
- Maximum freight value: 409.68.

**Decision:** No immediate row removal is necessary based on these checks. Preserve the original data and investigate extreme prices and freight charges during exploratory data analysis. Aggregate item prices at the correct order level to avoid double-counting.

**Business relevance:** The dataset supports product performance, seller performance, item price, and freight analysis. Item price and freight should be treated as separate measures, and neither should automatically be interpreted as profit.

### Customers Data Quality

**Dataset size:** 99,441 rows and 5 columns.

**Quality checks:**
- No missing values were found.
- No completely duplicated rows were found.
- All 99,441 `customer_id` values are unique.
- There are 96,096 distinct `customer_unique_id` values.

**Geographic distribution:** São Paulo (SP) has the highest number of customer records, followed by Rio de Janeiro (RJ) and Minas Gerais (MG).

**Decision:** No immediate cleaning is required based on these checks. Preserve both customer identifiers because they serve different purposes. Use `customer_unique_id` when identifying underlying customers and investigating repeat purchases.

**Business relevance:** Customer and location data can support customer retention, repeat-purchase, and regional sales analysis. Repeat purchasing should be measured by linking customer records to orders rather than inferred from customer counts alone.

### Orders Data Quality

**Dataset size:** 99,441 rows and 8 columns.

**Quality checks:**
- No completely duplicated rows were found.
- 160 missing order approval timestamps.
- 1,783 missing carrier delivery timestamps.
- 2,965 missing customer delivery timestamps.
- Purchase and estimated delivery timestamps have no missing values.

**Order status distribution:**
- Delivered: 96,478.
- Shipped: 1,107.
- Canceled: 625.
- Unavailable: 609.
- Invoiced: 314.
- Processing: 301.
- Created: 5.
- Approved: 2.

**Decision:** Preserve orders with missing timestamps. Missing delivery events can be expected for orders that have not reached the relevant stage. Investigate inconsistencies such as delivered orders without a customer delivery timestamp. Exclude records only from calculations that require unavailable timestamps, and document those exclusions.

**Business relevance:** The order table supports order status analysis, delivery-time calculations, cancellation analysis, and time-based trends. The percentage of orders marked delivered should not be confused with the on-time delivery rate.

### Sellers Data Quality

**Dataset size:** 3,095 rows and 4 columns.

**Quality checks:**
- No missing values were found.
- No completely duplicated rows were found.
- All 3,095 seller IDs are unique.

**Decision:** No immediate cleaning is required based on these checks. Retain the seller table for joining with order-item data.

**Business relevance:** Seller information can support seller-level sales comparisons and geographic analysis.

### Product Category Translation Data Quality

**Dataset size:** 71 rows and 2 columns.

**Quality checks:**
- No missing values were found.
- No completely duplicated rows were found.
- There are 71 unique Portuguese category names.

**Decision:** Preserve the translation table and use it to display category names in English. During integration, verify which product categories have matching translations.

**Business relevance:** English category labels make product performance reports and dashboards easier to understand.