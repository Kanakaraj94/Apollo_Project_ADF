# Apollo Healthcare Data Engineering Project

## Project Overview

The Apollo Healthcare Data Engineering Project is an end-to-end Azure Data Engineering solution that ingests healthcare data from multiple source systems, performs data cleansing and transformations using the Medallion Architecture (Bronze, Silver, Gold), and delivers a unified data warehouse for reporting and analytics.

The project is built using Azure Data Factory (ADF), Azure Data Lake Storage Gen2 (ADLS Gen2), and Azure SQL Database.

---

# Architecture

```
        Source Systems
              |
              v
      Azure Data Factory
              |
              v
      ADLS Gen2 - Bronze
              |
     (Raw Data Storage)
              |
              v
      ADLS Gen2 - Silver
   (Cleaned & Standardized)
              |
              v
      ADLS Gen2 - Gold
 (Business Ready Data Warehouse)
              |
              v
     Azure SQL Database
              |
              v
         Power BI Reports
```

---

# Technology Stack

- Azure Data Factory (ADF)
- Azure Data Lake Storage Gen2
- Azure SQL Database
- Azure Blob Storage
- Mapping Data Flow
- Azure Integration Runtime
- GitHub Integration
- SQL
- Power Query
- Power BI

---

# Source Tables

The project processes healthcare-related datasets including:

- Patient Data
- Encounter
- Encounter Diagnosis
- Pregnancy Diagnosis
- Provider
- Primary Care Provider (PCP)
- Location

---

# Medallion Architecture

## Bronze Layer

### Objective

Store raw data exactly as received from the source systems.

### Activities

- Copy Activity
- Metadata Driven Pipeline
- Incremental File Loading
- Raw CSV/Parquet Storage

### Output

Raw healthcare datasets stored in ADLS Gen2 Bronze container.

---

## Silver Layer

### Objective

Clean and standardize the healthcare data.

### Transformations

- Remove duplicate records
- Handle null values
- Standardize date formats
- Rename columns
- Convert data types
- Trim spaces
- Validate mandatory fields
- Data quality checks

### Output

Validated and standardized healthcare datasets.

---

## Gold Layer

### Objective

Create a Single Source of Truth (SSOT) for analytics.

### Business Model

The Gold layer uses the Encounter table as the central fact table and joins it with supporting dimension tables.

### Fact Table

Fact_Encounter

Contains

- Encounter ID
- Patient ID
- Provider ID
- PCP ID
- Location ID
- Diagnosis ID
- Encounter Date

### Dimension Tables

- Dim Patient
- Dim Provider
- Dim PCP
- Dim Location
- Dim Diagnosis

### Gold Output

A denormalized healthcare data warehouse ready for reporting.

---

# Data Flow

```
Patient Data
        \
Provider \
          \
Location -----> Lookup
               |
PCP ---------->|
               |
Encounter DX ->|
               |
Pregnancy DX ->|
               |
Encounter ------> Join
                    |
             Derived Columns
                    |
                Select Columns
                    |
             Gold Data Warehouse
```

---

# Pipeline Workflow

1. Read healthcare source files.
2. Load raw data into Bronze layer.
3. Validate and cleanse data in Silver layer.
4. Join healthcare entities in Gold layer.
5. Load business-ready data into Azure SQL Database.
6. Consume data in Power BI.

---

# Business Rules

- Every encounter belongs to one patient.
- Every encounter is associated with one provider.
- Every encounter occurs at one location.
- Every patient may have a primary care provider.
- A patient can have multiple encounters.
- A patient can have multiple diagnoses.
- Pregnancy diagnosis is identified using diagnosis codes.

---

# Data Quality Checks

- Duplicate removal
- Null validation
- Invalid date validation
- Mandatory field validation
- Data type validation
- Record count validation
- Business rule validation

---

# Key Features

- Medallion Architecture
- Metadata-driven pipelines
- Automated data ingestion
- Reusable ADF pipelines
- Incremental data loading
- Data quality validation
- Centralized healthcare data warehouse
- GitHub version control
- Scalable Azure architecture

---

# Benefits

- Single Source of Truth
- Improved reporting performance
- Simplified analytics
- High-quality healthcare data
- Reduced duplicate records
- Standardized business reporting
- Easy integration with Power BI

---

# Future Enhancements

- Slowly Changing Dimensions (SCD Type 2)
- Delta Lake implementation
- Azure Databricks integration
- Automated monitoring and alerting
- CI/CD using Azure DevOps
- Real-time data ingestion
- Incremental watermark loading

---

# Repository Structure

```
Apollo-Healthcare-ADF/
│
├── pipelines/
├── datasets/
├── linkedServices/
├── dataflows/
├── triggers/
├── integrationRuntime/
├── bronze/
├── silver/
├── gold/
├── sql/
├── architecture/
├── screenshots/
└── README.md
```

---

# Author

Kanakaraj M

**Technologies:** Azure Data Factory | ADLS Gen2 | Azure SQL Database | Power BI | SQL | GitHub

---
