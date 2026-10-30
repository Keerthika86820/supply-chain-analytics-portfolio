Supply Chain Operations & Commercial Performance Analysis
An end-to-end analytics portfolio project using SQL, Python (Pandas/Matplotlib), and Power BI to examine revenue, product mix, regional performance, order fulfilment, supplier activity, shipping, and inventory status.

Business objective
Evaluate the commercial and operational profile of the supplied supply-chain order dataset. The analysis is organized around questions a business operations or supply-chain analytics team could use to understand sales contribution, fulfilment status, inventory exposure, and supplier/logistics performance.

Dataset overview

| Attribute | Details |
|---|---|
| Records | 30,000 rows |
| Fields | 26 columns |
| Date coverage (Order_Date) | 01 Jan 2023 to 09 Aug 2026 |
| Business entities | Orders, customers, products, categories, suppliers, warehouses, carriers |
| Measures | Quantity, unit/total cost, unit price, total revenue, lead time, inventory on hand, reorder point |
| Currency | USD, as represented in source column names |
| File | `data/supply_chain_management.csv` |

Main fields
- Order & customer: Order_ID, Order_Date, Customer, Region, Order_Status, Payment_Terms
- Product & supplier: Product_ID, Product_Name, Category, Supplier, Supplier_Country
- Warehouse & inventory: Warehouse_Code, Warehouse_Location, Inventory_On_Hand, Reorder_Point, Stock_Status
- Cost & revenue: Quantity, Unit_Cost_USD, Unit_Price_USD, Total_Cost_USD, Total_Revenue_USD
- Logistics: Shipping_Method, Carrier, Ship_Date, Delivery_Date, Lead_Time_Days
Data provenance: The uploaded CSV was used as supplied. Its original publisher, generation method, and reuse licence were not included with the files; verify usage rights before public redistribution.
Questions addressed
1. What are total revenue, total cost, and gross profit?
2. Which products and categories contribute the most revenue?
3. Which regions and customers contribute the most revenue?
4. How does revenue change month over month?
5. Which products have the highest sales quantity and gross profit?
6. What is the distribution of order statuses, including delayed, backordered, and cancelled orders?
7. What inventory statuses are present, and how many records fall into each status?
8. How do suppliers compare on order volume, revenue, and recorded lead time?
9. How do shipping methods and carriers compare on order volume and recorded lead time?
10. How do warehouse locations compare on revenue and recorded lead time?
11. How do payment terms relate to order volume and associated revenue?
Tools and analytical workflow
Tool	Work performed
MySQL 8.0+	Table definition, aggregation, ranking, date grouping, supplier/logistics/inventory analysis
Python	Data loading, profiling, descriptive analysis, grouped summaries, Matplotlib charts
Power BI	Three report pages: Dashboard, Revenue Report, Inventory Report; KPI cards, trend and category/region visuals, stock-status visuals, and slicers


Workflow
1. Load the CSV and inspect dimensions, data types, missing values, and duplicate identifiers.
2. Import the CSV into the MySQL table defined in sql/supply_chain_analysis.sql.
3. Run the business analysis queries in the same SQL file.
4. Reproduce exploratory summaries and charts in notebooks/supply_chain_analysis.ipynb.
5. Open powerbi/supply_chain_dashboard.pbix in Power BI Desktop and explore the report pages and slicers.
Selected findings from the supplied dataset
These figures are independently recalculated from the uploaded CSV; they are not estimates.
Metric	Result
Total order records	30,000
Distinct Order_ID values	30,000
Total revenue	$796,190,010.27
Total cost	$332,234,174.75
Gross profit (revenue − cost)	$463,955,835.52
Average recorded lead time	23.58 days
Delivered order records	16,347 (54.5%)
Cancelled order records	1,203 (4.0%)


Revenue leaders
- Top revenue category: Protective Gear — $80,696,058.08.
- Top revenue region: Europe — $162,416,051.63.
- Top gross-profit category: Hoodies — $47,218,286.52.
- The five regional revenue totals are relatively close; Europe ranks first in this dataset.
Inventory profile
- Overstock: 19,768 records (65.9%).
- In Stock: 7,639 records (25.5%).
- Low Stock: 2,589 records (8.6%).
- Out of Stock: 4 records (0.0%).
Interpretation caution: These are row-level counts in the supplied file. The data does not establish whether each row is a unique SKU-level inventory snapshot, so do not describe these percentages as the share of unique products without further modelling.
Data quality and analytical limitations
- Order_ID is unique across all 30,000 rows; the CSV has no fully duplicated rows.
- Delivery_Date is missing in 6,687 rows (22.3%). Missing values occur in Backordered, Cancelled, and Processing statuses. Treat these records as having no recorded delivery date; do not impute a delivery date.
- Lead_Time_Days is populated even for rows with no Delivery_Date. Therefore, the source does not establish that this field is actual elapsed ship-to-delivery time for every record. The SQL and dashboard label it as recorded lead time; validate its definition with the data owner before using it for SLA or on-time-delivery claims.
- The supplied notebook uses descriptive aggregation and visualisation; no forecasting, classification, causal analysis, or machine-learning model is implemented.
- Revenue and cost arithmetic reconcile exactly to Quantity × Unit_Price_USD and Quantity × Unit_Cost_USD in the supplied CSV (to cent precision).
- Dataset provenance and licence are unknown from the supplied materials.
