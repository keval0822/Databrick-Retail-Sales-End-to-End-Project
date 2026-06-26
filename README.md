**Source Files** ---->  **Bronze**  ( Raw Data + Metadata )  ----->  **Silver**   (Data Cleaning + Validation + Standardize )  -----> **Gold**   ( Fact Tables + Aggregations  + Business KPIs ) 


**Project Architecture**

**Bronze Layer (Raw Ingestion)**

The Bronze layer stores raw data exactly as received from the source systems with minimal transformation.

Activities Performed:

 * Ingest raw retail order and customer datasets from source files.
 * Preserve original schema and data for auditing and traceability.

Add ingestion metadata:
 * ingestion_date
 * ingestion_timestamp
 * Maintain historical raw records without modification.

Purpose:

 * Acts as the single source of truth and enables data lineage and reprocessing.



**Silver Layer (Data Cleansing & Standardization)**

The Silver layer focuses on improving data quality and preparing data for analytics.

Transformations Performed: 

  ✔ Fixed inconsistent date formats.

✔ Standardized category values.

✔ Removed duplicate records.

✔ Handled missing/null values.

✔ Converted discount values:
  * "5%" → 0.05
  * "10%" → 0.10

✔ Removed invalid records with negative quantities.

✔ Standardized text casing:
  * Customer names
  * Cities
  * States
  * Categories


✔ Cast unit_price to Decimal datatype.

✔ Validated customer email addresses.

✔ Recalculated total_amount using:

Purpose:
 * Provides clean, validated, and standardized datasets for downstream consumption.


**Gold Layer (Business Aggregation Layer)**

The Gold layer contains curated business-ready datasets optimized for reporting and analytics.

Fact Table Creation

Created a fact_sales dataset by joining:

 * Orders dataset
 * Customers dataset

Additional date dimensions generated:

 * Year
 * Month
 * Day

Business Metrics Generated:
 * Total Revenue
 * Total Quantity Sold
 * Total Orders
 * Average Revenue
 * Average Quantity
 * Average Loyalty Points
 * Minimum Product Price
 * Maximum Product Price


Aggregation Dimensions:
 * Product
 * Customer
 * Category
 * Order Date
 * Gender
 * City
 * State
 * Year
 * Month


Purpose:
  * Supports BI dashboards, reporting, and business analysis.


Tech Stack
  * Azure Databricks
  * PySpark
  * Delta Lake
  * SQL
  * Medallion Architecture
  * GitHub


