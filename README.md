# 🏥 Healthcare OLTP to Data Warehouse Project

## 📚 Table of Contents

- [Overview](#overview)
- [Dataset](#dataset)
- [Dataset Sources](#dataset-sources)
- [Entity Relationship Diagram (ERD)](#entity-relationship-diagram-erd)
- [High-level DW & BI Solution Architecture](#high-level-dw--bi-solution-architecture)
- [Data Warehouse Dimensional Model](#data-warehouse-dimensional-model)
- [ETL Process](#etl-process)
  - [Extraction](#️extraction)
  - [Transformation & Loading](#transformation--loading)
  - [Patient Dimension Example](#patient-dimension-example)
  - [Fact Table: Encounters](#fact-table-encounters)
- [Author](#author)

---

## 📘 Overview

This project involves designing and implementing a Data Warehousing and Business Intelligence (DW & BI) solution using a healthcare-related OLTP dataset. The aim is to enable efficient analytics and reporting by transforming transactional healthcare data into a star schema model through a structured ETL process.

---

## 📂 Dataset

📥 Source: [Synthea Healthcare Dataset](https://synthea.mitre.org/downloads)

This dataset represents synthetic healthcare records and includes the following 18 entities:

1. Allergies  
2. Patients  
3. Claims  
4. Claims Transactions  
5. Care Plans  
6. Conditions  
7. Devices  
8. Encounters  
9. Imaging Studies  
10. Immunizations  
11. Medications  
12. Observations  
13. Organizations  
14. Payer Transitions  
15. Payers  
16. Procedures  
17. Providers  
18. Supplies

---

## 🗃️ Dataset Sources

- `.csv`: All entities except `Allergies`
- `.txt`: `Allergies`

---

## 🧩 Entity Relationship Diagram (ERD)

![ER Diagram](https://drive.google.com/uc?export=view&id=1WohbTvUpQ5sgv4fczP7dBMf1sdwMdI_6)

---

## 🏗️ High-level DW & BI Solution Architecture

This architecture outlines the flow of data from source systems into the data warehouse via SSIS.

![High-level DW & BI solution architecture](https://drive.google.com/uc?export=view&id=1scnqqerQ3plLR1PPxo6Ij0tUCGdJFi3W)

---

## 🗄️ Data Warehouse Dimensional Model

A **Star Schema** dimensional model is used, containing one fact table and five dimension tables.

### 📐 Dimension Tables

- **Dim Providers** – Details about healthcare professionals  
- **Dim Organizations** – Information on healthcare institutions  
- **Dim Patients** – Demographic and personal details of patients  
- **Dim Payers** – Insurance providers, coverage statistics, and revenue  
- **Dim Date** – A surrogate-key-based date dimension

### 🔢 Fact Table

- **Fact Encounters** – Stores metrics related to healthcare interactions such as base cost, claim cost, coverage, and derived measures.

### 📝 Design Assumptions

- `Encounters` is used as the fact table due to its multiple foreign key relationships and valuable measures.
- `Patients`, `Providers`, `Organizations`, and `Payers` are treated as **Slowly Changing Dimensions (SCDs)**.
- The `Date` dimension uses surrogate keys instead of raw dates.

---

## 🔄 ETL Process

The ETL process was implemented using **SQL Server Integration Services (SSIS)**.

### 🛠️ Extraction

- Flat File Source: Used to extract data from `.txt` and `.csv` files (e.g., `Allergies.txt`).
- Excel Source: Extracted data from Excel files (where applicable).
- All extracted data was loaded into the **staging area** via **OLE DB Destinations**.
- **Data profiling** was performed to assess data quality and structure.

---

### 🔁 Transformation & Loading

Data transformation ensured consistency and referential integrity before final loading.

#### 🗓️ Load Order

1. **Dim Date**
2. **Dim Patients**
3. **Dim Organizations**
4. **Dim Providers**
5. **Dim Payers**
6. **Fact Encounters**

> 🔄 Slowly Changing Dimensions (SCD) were implemented for key dimensions to manage historical changes.

---

### 👤 Patient Dimension Example

1. **Data Conversion**: Standardized column formats.
2. **Derived Column**:
   - Replaced `NULL` values in the `prefix` column.
   - Created `InsertDate` and `ModifiedDate`.
3. **SCD Transformation**:
   - Mapped keys and attributes.
   - Defined historical, fixed, and changing fields.
4. **Load**: Records loaded into the final destination table via OLE DB.

➡️ The same workflow was applied to **Organizations**, **Providers**, and **Payers** dimensions.

---

### 📊 Fact Table: Encounters

1. **Data Conversion**: Converted dates (`NVARCHAR` ➝ `DT_DBTIMESTAMP`).
2. **Lookups**: Fetched surrogate keys for dimensions.
3. **Derived Columns**:
   - `InsertDate`, `ModifiedDate`
   - `RemainingClaimAmount`
   - `AdditionalCharge`
   - `TotalCoverageRatio`
   - `txn_process_time_hours`
4. **Load**: Final load to the fact table after lookups and transformations.

---

## 👨‍💻 Author

- **Student ID:** IT22107978  
- **Institution:** Sri Lanka Institute of Information Technology  
- **Course:** Information Technology Project – Year 3 Semester 2 (2025)

