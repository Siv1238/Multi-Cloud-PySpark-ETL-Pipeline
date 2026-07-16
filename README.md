# Multi-Cloud Insurance Claims Data Pipeline 🚀

## Project Overview
This project demonstrates an end-to-end Data Engineering ETL pipeline built across a multi-cloud architecture. It processes realistic insurance claims data using **Azure Databricks (PySpark)** for compute and writes the final optimized analytical reports to **AWS S3 Data Lake** for storage.

## Tech Stack
* **Compute Engine:** Azure Databricks
* **Storage:** AWS S3
* **Language & Framework:** Python, PySpark, Spark SQL

## Key Technical Implementations
1. **Data Ingestion & Mocking:** Generated synthetic policy and claims datasets, intentionally introducing **Data Skew** (e.g., massive COVID-19 claims) to simulate real-world data engineering challenges.
2. **Transformations & Optimizations:**
   * Applied both Narrow (`filter`, `withColumn`) and Wide (`groupBy`) transformations.
   * Addressed the Data Skew bottleneck by implementing **Broadcast Hash Joins** for dimension tables, bypassing heavy network shuffles.
   * Managed cluster resources and data partitioning using `repartition()` for parallelism and `coalesce()` for optimal output file sizing.
3. **Advanced Spark SQL:** Leveraged Common Table Expressions (CTEs) and Window Functions (`ROW_NUMBER`, `RANK`, `DENSE_RANK`) to perform complex ranking logic on partitioned policy data.
4. **Multi-Cloud Integration:** Configured Hadoop AWS S3a connectors securely within Databricks to write the final processed DataFrames directly into an AWS S3 bucket.

## File Structure
* `Insurance_Claims_Project.py` : Contains the complete PySpark execution code.
* `_SUCCESS` / `part-0000.csv` : (Located in AWS S3) The final analytical report outputs.

## How to Run
1. Import the provided `.py` or `.ipynb` file into an Azure Databricks workspace.
2. Attach to a standard compute cluster (Note: Serverless compute restricts direct S3 credential configs).
3. Update the AWS IAM Access Keys and S3 bucket details in the final export cell.
4. Execute the notebook sequentially to generate the output in S3.
