<p align="center">
  <img src="https://img.shields.io/badge/SQL_Server-CC2927?style=for-the-badge&logo=microsoft-sql-server&logoColor=white" alt="SQL Server"/>
  <img src="https://img.shields.io/badge/Data_Warehouse-4169E1?style=for-the-badge&logo=databricks&logoColor=white" alt="Data Warehouse"/>
  <img src="https://img.shields.io/badge/ETL_Pipeline-FF6F00?style=for-the-badge&logo=apache-airflow&logoColor=white" alt="ETL"/>
  <img src="https://img.shields.io/badge/Star_Schema-2E86AB?style=for-the-badge&logo=snowflake&logoColor=white" alt="Star Schema"/>
</p>

<h1 align="center">🏢 SQL Data Warehouse Project</h1>

<p align="center">
  <strong>A Production-Ready Data Warehouse Solution with Medallion Architecture</strong>
</p>

<p align="center">
  <em>Transform raw data into actionable business intelligence through a structured Bronze → Silver → Gold data pipeline</em>
</p>

---

## 📋 Table of Contents

- [Project Overview](#-project-overview)
- [Architecture](#️-architecture)
- [Data Flow](#-data-flow)
- [ETL Pipeline](#-etl-pipeline)
- [Project Structure](#-project-structure)
- [Data Model](#️-data-model)
- [Getting Started](#-getting-started)
- [Documentation](#-documentation)
- [Quality Assurance](#-quality-assurance)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 Project Overview

This project implements a **modern data warehouse** using SQL Server, following the **Medallion Architecture** pattern (Bronze → Silver → Gold). It demonstrates industry best practices for:

| Feature | Description |
|---------|-------------|
| 🥉 **Bronze Layer** | Raw data ingestion from multiple source systems |
| 🥈 **Silver Layer** | Data cleansing, standardization, and transformation |
| 🥇 **Gold Layer** | Business-ready dimensional model (Star Schema) |
| 🔍 **Data Quality** | Comprehensive quality checks at each layer |
| 📊 **Analytics Ready** | Optimized for reporting and business intelligence |

### Key Technologies

- **Database**: Microsoft SQL Server
- **Architecture**: Medallion Architecture (Multi-Layered)
- **Data Modeling**: Star Schema (Dimension & Fact Tables)
- **Source Systems**: CRM & ERP Data Integration

---

## 🏗️ Architecture

The data warehouse follows the **Medallion Architecture** pattern, organizing data into three distinct layers for progressive refinement:

<p align="center">
  <img src="docs/data_architecture.png" alt="Data Architecture" width="90%"/>
</p>

### Layer Details

| Layer | Schema | Purpose | Data Quality |
|-------|--------|---------|--------------|
| 🥉 **Bronze** | `bronze` | Raw data store - exact copy from source systems | As-is from source |
| 🥈 **Silver** | `silver` | Cleansed, standardized, and deduplicated data | Validated & Cleaned |
| 🥇 **Gold** | `gold` | Business-level aggregations and dimensional models | Business-Ready |

---

## 📊 Data Flow

Understanding how data flows through the warehouse is crucial for maintaining data lineage and ensuring quality:

<p align="center">
  <img src="docs/data_flow.png" alt="Data Flow" width="90%"/>
</p>

### Source Systems Integration

Our data warehouse ingests data from two primary source systems:

<p align="center">
  <img src="docs/data_integration.png" alt="Data Integration" width="90%"/>
</p>

| Source System | Data Type | Tables |
|---------------|-----------|--------|
| **CRM** | Customer & Sales Data | `cust_info`, `prd_info`, `sales_details` |
| **ERP** | Enterprise Data | `CUST_AZ12`, `LOC_A101`, `PX_CAT_G1V2` |

---

## 🔄 ETL Pipeline

The ETL (Extract, Transform, Load) pipeline is the backbone of this data warehouse, ensuring data is properly processed at each layer:

<p align="center">
  <img src="docs/ETL.png" alt="ETL Pipeline" width="90%"/>
</p>

### Pipeline Stages

```
📥 EXTRACT          📦 TRANSFORM         📤 LOAD
    │                    │                  │
    ▼                    ▼                  ▼
┌─────────┐        ┌───────────┐      ┌──────────┐
│  CSV    │   ──►  │  Cleanse  │  ──► │  Bronze  │
│  Files  │        │  Validate │      │  Tables  │
└─────────┘        └───────────┘      └──────────┘
                         │
                         ▼
                   ┌───────────┐      ┌──────────┐
                   │ Normalize │  ──► │  Silver  │
                   │ Standardize      │  Tables  │
                   └───────────┘      └──────────┘
                         │
                         ▼
                   ┌───────────┐      ┌──────────┐
                   │ Aggregate │  ──► │   Gold   │
                   │ Enrich    │      │   Views  │
                   └───────────┘      └──────────┘
```

---

## 📁 Project Structure

```
sql-data-warehouse-project/
│
├── 📂 datasets/                    # Source data files
│   ├── 📂 source_crm/              # CRM system data
│   │   ├── cust_info.csv           # Customer information
│   │   ├── prd_info.csv            # Product information
│   │   └── sales_details.csv       # Sales transactions
│   │
│   └── 📂 source_erp/              # ERP system data
│       ├── CUST_AZ12.csv           # Customer demographics
│       ├── LOC_A101.csv            # Location data
│       └── PX_CAT_G1V2.csv         # Product categories
│
├── 📂 scripts/                     # SQL scripts
│   ├── init_database.sql           # Database & schema setup
│   │
│   ├── 📂 bronze/                  # Bronze layer scripts
│   │   ├── ddl_bronze.sql          # Table definitions
│   │   └── proc_load_bronze.sql    # Data loading procedures
│   │
│   ├── 📂 silver/                  # Silver layer scripts
│   │   ├── ddl_silver.sql          # Table definitions
│   │   └── proc_load_silver.sql    # Transformation procedures
│   │
│   └── 📂 gold/                    # Gold layer scripts
│       └── ddl_gold.sql            # Dimension & Fact views
│
├── 📂 tests/                       # Quality assurance
│   ├── quality_checks_silver.sql   # Silver layer validation
│   └── quality_checks_gold.sql     # Gold layer validation
│
└── 📂 docs/                        # Documentation & diagrams
    ├── data_architecture.png       # Architecture overview
    ├── data_flow.png               # Data flow diagram
    ├── data_integration.png        # Integration diagram
    ├── data_model.png              # Star schema model
    ├── ETL.png                     # ETL pipeline diagram
    ├── data_catalog.md             # Data dictionary
    └── naming_conventions.md       # Naming standards
```

---

## 🗃️ Data Model

The Gold Layer implements a **Star Schema** optimized for analytical queries:

<p align="center">
  <img src="docs/data_model.png" alt="Data Model - Star Schema" width="90%"/>
</p>

### Dimensional Model

#### 📊 Fact Table: `gold.fact_sales`

| Column | Type | Description |
|--------|------|-------------|
| `order_number` | NVARCHAR(50) | Unique order identifier |
| `product_key` | INT | FK to dim_products |
| `customer_key` | INT | FK to dim_customers |
| `order_date` | DATE | Order placement date |
| `shipping_date` | DATE | Order shipping date |
| `due_date` | DATE | Payment due date |
| `sales_amount` | INT | Total sale value |
| `quantity` | INT | Units ordered |
| `price` | INT | Unit price |

#### 👥 Dimension: `gold.dim_customers`

| Column | Type | Description |
|--------|------|-------------|
| `customer_key` | INT | Surrogate key (PK) |
| `customer_id` | INT | Natural key |
| `customer_number` | NVARCHAR(50) | Business identifier |
| `first_name` | NVARCHAR(50) | Customer first name |
| `last_name` | NVARCHAR(50) | Customer last name |
| `country` | NVARCHAR(50) | Country of residence |
| `marital_status` | NVARCHAR(50) | Marital status |
| `gender` | NVARCHAR(50) | Gender |
| `birthdate` | DATE | Date of birth |
| `create_date` | DATE | Record creation date |

#### 📦 Dimension: `gold.dim_products`

| Column | Type | Description |
|--------|------|-------------|
| `product_key` | INT | Surrogate key (PK) |
| `product_id` | INT | Natural key |
| `product_number` | NVARCHAR(50) | Product code |
| `product_name` | NVARCHAR(50) | Product description |
| `category_id` | NVARCHAR(50) | Category identifier |
| `category` | NVARCHAR(50) | Product category |
| `subcategory` | NVARCHAR(50) | Product subcategory |
| `maintenance` | NVARCHAR(50) | Maintenance requirement |
| `cost` | INT | Product cost |
| `product_line` | NVARCHAR(50) | Product line |
| `start_date` | DATE | Availability start date |

---

## 🚀 Getting Started

### Prerequisites

- **SQL Server** 2019 or later (or Azure SQL Database)
- **SQL Server Management Studio (SSMS)** or Azure Data Studio
- **Git** for version control

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/PrithamBhosale/sql-data-warehouse-project.git
   cd sql-data-warehouse-project
   ```

2. **Initialize the database**
   ```sql
   -- Run the initialization script
   -- ⚠️ WARNING: This will drop existing 'DataWarehouse' database
   :r scripts/init_database.sql
   ```

3. **Create Bronze layer objects**
   ```sql
   :r scripts/bronze/ddl_bronze.sql
   :r scripts/bronze/proc_load_bronze.sql
   ```

4. **Create Silver layer objects**
   ```sql
   :r scripts/silver/ddl_silver.sql
   :r scripts/silver/proc_load_silver.sql
   ```

5. **Create Gold layer views**
   ```sql
   :r scripts/gold/ddl_gold.sql
   ```

6. **Load data and run quality checks**
   ```sql
   EXEC load_bronze;
   EXEC load_silver;
   
   -- Validate data quality
   :r tests/quality_checks_silver.sql
   :r tests/quality_checks_gold.sql
   ```

---

## 📖 Documentation

| Document | Description |
|----------|-------------|
| [📚 Data Catalog](docs/data_catalog.md) | Complete data dictionary for Gold layer tables |
| [📝 Naming Conventions](docs/naming_conventions.md) | Standards for object and column naming |

---

## 🧪 Quality Assurance

This project includes comprehensive quality checks:

### Silver Layer Checks
- ✅ Data type validation
- ✅ Null value handling
- ✅ Duplicate detection
- ✅ Referential integrity

### Gold Layer Checks
- ✅ Surrogate key uniqueness
- ✅ Dimension-Fact relationships
- ✅ Data model connectivity
- ✅ Business rule validation

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

---

## 📜 License

This project is open source and available under the [MIT License](LICENSE).

---

<p align="center">
  <strong>⭐ If you found this project helpful, please give it a star!</strong>
</p>

<p align="center">
  Made with ❤️ by <a href="https://github.com/PrithamBhosale">Pritham Bhosale</a>
</p>

---

<p align="center">
  <sub>🏗️ Building Data Warehouses, One Query at a Time</sub>
</p>
