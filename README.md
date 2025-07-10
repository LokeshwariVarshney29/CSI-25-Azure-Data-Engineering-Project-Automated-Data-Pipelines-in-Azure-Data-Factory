**🌐 Azure Data Engineering Project – Automated Data Pipelines in Azure Data Factory: REST & SQL Integration**

**📌 Project Overview** This project showcases an end-to-end data engineering workflow in Azure Data Factory (ADF). It automates the fetching of country data via a REST API, conditionally moves SQL data to Azure Data Lake Storage (ADLS), orchestrates pipeline dependencies, and integrates scheduled triggers for periodic execution.

**🚀 Objectives**

- Retrieve country information for India, US, UK, China, and Russia via REST API
- Automatically run pipelines twice daily (12:00 AM & 12:00 PM IST)
- Copy customer data to ADLS only if record count > 500
- Trigger product data pipeline conditionally if customer count > 600
- Dynamically pass parameters between parent and child pipelines

**🧩 Architecture Components**

- **Azure Data Factory** – Pipeline orchestration
- **Azure SQL Database** – Source of customer and product data
- **Azure Data Lake Storage (ADLS)** – Destination for ingested data
- **REST API Integration** – Source for country metadata
- **Pipeline Parameters** – For inter-pipeline communication
- **Schedule Trigger** – For automation (IST timezone)
- **Activities Used** – Lookup, If Condition, Copy, Execute Pipeline

**📂 Pipeline Details**

1. **Country Data Ingestion Pipeline**
    - Uses REST endpoint: <https://restcountries.com/v3.1/name/{name}>
    - Loops through India, US, UK, China, and Russia
    - Copies data using REST connector
    - Saves as {name}.json files in ADLS
    - Includes error handling and retry logic
      ![](https://github.com/LokeshwariVarshney29/CSI-25-Azure-Data-Engineering-Project-Automated-Data-Pipelines-in-Azure-Data-Factory/blob/f9aca870698d8f3c001d3971446eec426d86e77d/snapshots/AzureDataFactory/Pipelines/Pipeline%20-%20CustomerData.png)
2. **Scheduled Trigger**
    - Frequency: Twice per day
    - Timings: 12:00 AM IST and 12:00 PM IST
    - Configured using CRON expression
    - Verified against IST for regional accuracy
      ![]() ![]()
3. **Customer Data Pipeline (Parent)**
    - Lookup Activity fetches record count from customer table
    - If count > 500, Copy Activity transfers data to ADLS
    - Uses Execute Pipeline to invoke child pipeline
    - Passes customer count via pipeline parameters
      ![]()
4. **Product Data Pipeline (Child)**
    - Executes only if customer count parameter > 600
    - Copies product table data to ADLS
    - Includes parameter validation via If Condition activity
      ![]()

**🧪 Sample Data Generation**

- Created with Python’s Faker module
- Customer table: 1000 synthetic records
- Product table: 1000 realistic entries
- Fields include IDs, names, contact info, categories, prices, and more

**📊 Monitoring & Logging**

- Pipeline activity tracking via ADF monitoring
- Error alerts, retry attempts, and execution histories
- Trigger logs with duration, status, and timestamp insights
  ![]()

**🧠 Key Features**

- Conditional logic for intelligent execution
- Dynamic parameter passing between linked pipelines
- Time zone–aware scheduling
- Modular design with reusability
- Scalable structure for additional data sources

**⚙️ Configuration Checklist**

- Azure Data Factory: ✅
- SQL Database & Tables: ✅
- REST API Dataset Configured: ✅
- ADLS Linked & Writable: ✅
- Service Permissions Established: ✅
- CRON Expression Verified: ✅

**🛠️ Troubleshooting Guide**

| **Issue** | **Suggested Fix** |
| --- | --- |
| API Timeouts | Use retry policies; check endpoint status |
| SQL Connection Fails | Review firewall rules and linked services |
| Parameter Errors | Validate data types and mappings |
| Trigger Not Executing | Confirm CRON schedule and timezone alignment |

**🌱 Future Enhancements**

- Add data validation checks
- Implement incremental copy logic
- Enable email or Teams notifications
- Expand to dynamic country list ingestion
- Introduce cold storage archiving for older exports

**👩‍💻 Author**

**Lokeshwari Varshney**

Data Engineering Enthusiast
