# Microsoft Fabric End-to-End E-Commerce Lakehouse & Analytics Pipeline

An end-to-end cloud data engineering and business intelligence solution built using **Microsoft Fabric**[cite: 10]. This project automates the ingestion of raw e-commerce files, performs scalable data cleaning and feature engineering using PySpark, establishes ACID-compliant Delta tables, models a star schema relationship, and orchestrates automated pipelines feeding into Power BI analytical reports[cite: 10, 11, 12, 13, 14, 15].

---

## Architecture & End-to-End Workflow

The workspace orchestrates a modern Lakehouse architecture across OneLake storage, compute notebooks, and BI reporting layers[cite: 10]:

```text
+-----------------------+      +------------------------+      +------------------------+      +-------------------------+
|    Raw Files (CSV)    | ---> | PySpark Data Cleaning  | ---> |   Delta Lake Tables    | ---> |    Star Schema Model    |
| (OneLake Files/raw/)  |      |      (Notebook 1)      |      | (fact & dim tables)    |      | (Semantic Model / DAX)  |
+-----------------------+      +------------------------+      +------------------------+      +-------------------------+
                                                                                                            |
                                                                                                            v
                                                                                               +-------------------------+
                                                                                               |   Power BI Reports &    |
                                                                                               |   Automated Pipelines   |
                                                                                               +-------------------------+

```

### Implementation Steps

1. **Workspace & Storage Setup**: Provisioned a dedicated workspace (`Fabric_Project`) containing OneLake storage (`Products` Lakehouse) to centralize enterprise assets.


2. **Raw Data Ingestion**: Loaded raw product (`dummyjson_products.csv`) and category lookup (`category_product.txt`) files into OneLake under structured raw directories.


3. **Data Transformation & Cleansing (`Notebook 1`)**:
* Applied missing value imputation (`.na.fill()`) to handle null attributes for textual fields (e.g., brand, warranty info) and numerical boundaries (e.g., price, stock, ratings).


* Performed feature engineering to calculate discounted prices, total inventory valuations, and segmented rating tiers.


* Persisted processed outputs into managed Delta Lake tables (`fact_products` and `dim_category_details`).




4. **Dimensional Modeling**: Designed a star schema in the semantic model layer, establishing a one-to-many relationship on the category key between the fact and dimension tables.


5. **Business Intelligence Reporting**: Built an interactive Power BI report (`products report`) displaying key business metrics including Total Inventory Value, Average Ratings by Category, and Stock Distribution across Supplier Regions.


6. **Pipeline Orchestration (`Pipeline 1`)**: Automated end-to-end workflow execution by chaining the PySpark data transformation notebook directly to a downstream semantic model refresh activity.



---

## Repository Structure

```text
.
├── notebooks/
│   └── data_transformation.ipynb   # PySpark notebook for cleaning and delta table creation
├── data/
│   ├── dummyjson_products.csv      # Raw product input dataset
│   └── category_product.txt        # Raw category lookup dataset
├── pipeline/
│   └── pipeline_orchestration.json # Fabric pipeline definition and execution flow
└── README.md

```

---
