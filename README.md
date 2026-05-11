# Laboratory-Work-3-Merged-Data-DAX-and-DAX-Function-Insights-Completion-requirements

Part 1: Review the Merged Dataset – Guide Questions
1. Is the dataset in flat-table format?
Yes. All customer attributes and transaction details are stored in a single, denormalized table without separation between descriptive and transactional data.
2. Which columns describe customers?
CustomerName, City, Region, and CustomerID are customer attributes (descriptive fields that define who the customer is).
3. Which columns represent transactions?
OrderID, OrderDate, and SalesAmount are transactional fields (measurable events that record business activity).
Part 2: Identify Fact and Dimension Tables – Guide Questions
1. Why must dimension tables contain unique keys?
Dimension tables require unique keys to ensure each entity (e.g., one customer) is represented by exactly one row. This guarantees that relationships resolve unambiguously and that filters aggregate facts correctly.
2. What problems occur if duplicates exist in DimCustomer?
Duplicates in a dimension table create ambiguous relationships (a single fact row may match multiple dimension rows), leading to inflated counts, incorrect aggregations, and unreliable analysis results.
Part 3: Define Primary & Foreign Keys – Guide Questions
1. What is a primary key?
A primary key is a column (or combination of columns) that uniquely identifies each row in a table, enforcing entity integrity and enabling reliable table relationships.
2. Why is CustomerID a foreign key in FactSales?
CustomerID in FactSales is a foreign key that establishes a relationship to DimCustomer, enabling the model to link each transaction to the corresponding customer for filtering and aggregation.
Part 4: Create Relationships – Guide Questions
1. Why should relationships flow from dimension to fact?
Relationships should flow from dimension to fact (one-to-many) because dimension tables filter and group the fact table. This direction ensures that slicers and filters on customer or date attributes correctly summarize transactional metrics.
2. What happens if the relationship is Many-to-Many?
Many-to-many relationships can produce ambiguous or inflated results because a single fact may relate to multiple dimension members, complicating aggregation logic and often requiring bridge tables or bidirectional filtering to resolve properly.
Part 5: Validate the Data Model – Guide Questions
1. Did sales aggregate correctly per customer?
Yes. SalesAmount was properly grouped by CustomerID and summed, confirming that the relationship between DimCustomer and FactSales is functioning correctly.
2. What would happen if relationships were missing?
Without relationships, tables operate in isolation. Filters would not propagate across tables, and measures would fail to calculate correctly—producing blank values, cartesian products, or misleading totals.
Part 6: Introduction to DAX – Guide Questions
1. What is a DAX measure?
A DAX measure is a dynamic calculation written in Data Analysis Expressions that computes aggregations (such as sums, averages, or ratios) based on the current filter context in a report or visualization.
2. Difference between SUM and AVERAGE?
SUM adds all values in a column, returning a total. AVERAGE calculates the arithmetic mean by dividing the sum of values by the count of non-blank rows.
3. Why use measures instead of calculated columns?
Measures calculate on-the-fly in response to user interactions and report filters, consuming less memory and adapting to context. Calculated columns compute at refresh time and consume storage for every row, regardless of what is visible.

Part 7: DAX Time Intelligence – Formulas & Guide Questions
DAX Formulas

Measure,Formula
Total Sales,`Total Sales = SUM(FactSales[SalesAmount])`
Total Quantity,`Total Quantity = SUM(FactSales[Quantity])`
Average Sales,`Average Sales = AVERAGE(FactSales[SalesAmount])`

Guide Questions
1. What is time intelligence in DAX?
Time intelligence is a set of DAX functions that enable period-over-period analysis, enabling comparisons across dates, months, quarters, and years using a dedicated date table.
2. Why is a date table required?
A contiguous, unique date table is required because time intelligence functions depend on an unbroken sequence of dates to correctly identify boundaries (e.g., month start/end) and calculate periods like YTD or MTD.
3. How does PREVIOUSMONTH help analyze trends?
PREVIOUSMONTH shifts the current filter context back one month, enabling direct month-over-month comparisons to identify growth, decline, or seasonal patterns.
4. What insights can YTD Sales provide?
Year-to-Date (YTD) Sales shows the cumulative sales total from January 1 through the current date, revealing overall annual progress and performance trajectory against targets.


Structure Summary:
DimCustomer → One side of the relationship (unique CustomerID)
FactSales → Many side (contains foreign keys: CustomerID, OrderDate)
DimDate → One side of the relationship (unique Date/OrderDate)









