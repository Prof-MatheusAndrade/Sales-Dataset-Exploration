# Data Modeling and Preprocessing

The data modeling process plays a crucial role in deriving meaningful insights from the original dataset provided by Company Holding. Utilizing the information contained in the CSV file, a data model structured in a snowflake schema has been created. This schema offers distinct advantages, providing a normalized and efficient way to organize data relationships. The resulting data model is visually represented in the figure below, crafted with precision using the draw.io tool:

<p align="center">
<img src="https://drive.google.com/uc?export=view&id=10WqmVpm5Bk6mWB7xePgdqqZOifSpR4q0"  width="60%" height="30%">
</p>

The draw.io files can be found in the repository folder: ["1_Data_Modeling"](https://github.com/Prof-MatheusAndrade/Sales-Dataset-Exploration/tree/main/0_Materials/1_Data_Modeling).

The adoption of a snowflake schema facilitates the entire process forward, especially in the context of time series analysis. By normalizing the data, efficiency is enhanced in handling large datasets, and consistency in the relationships between entities over time is ensured.

Moreover, leveraging Power BI for dashboard creation enhances the accessibility and visualization of the analytical results. Power BI's robust features allow for dynamic and interactive representations of the data model, empowering stakeholders to explore trends, anomalies, and key performance indicators efficiently.

## Data preprocessing in Databricks

Utilizing Databricks Community to implement and apply the data model to the current CSV file, a configured cluster with the provided JSON file was leveraged:
```json
{
    "num_workers": 0,
    "cluster_name": "My Cluster",
    "spark_version": "12.2.x-scala2.12",
    "spark_conf": {
        "spark.databricks.rocksDB.fileManager.useCommitService": "false"
    },
    "aws_attributes": {
        "first_on_demand": 0,
        "availability": "ON_DEMAND",
        "zone_id": "us-west-2c",
        "spot_bid_price_percent": 100,
        "ebs_volume_count": 0
    },
    "node_type_id": "dev-tier-node",
    "driver_node_type_id": "dev-tier-node",
    "ssh_public_keys": [],
    "custom_tags": {},
    "spark_env_vars": {
        "PYSPARK_PYTHON": "/databricks/python3/bin/python3"
    },
    "autotermination_minutes": 60,
    "enable_elastic_disk": false,
    "cluster_source": "UI",
    "init_scripts": [],
    "enable_local_disk_encryption": false,
    "runtime_engine": "STANDARD",
    "cluster_id": "1229-120843-ssdgcig8"
}
```


The decision to choose Databricks was based on its integration with the Delta Lakehouse environment, offering features such as ACID transactions, efficient schema evolution, and time travel capabilities. Additionally, Databricks simplifies the process of consuming data in external tools like Power BI, ensuring accessibility and usability for stakeholders throughout the organization.

Following the cluster configuration, the next crucial step involved uploading the original dataset from the CSV file to the Databricks DBFS (Databricks File System). The original dataset can be found in the repository folder ["0_Original_Dataset"](https://github.com/Prof-MatheusAndrade/Sales-Dataset-Exploration/tree/main/0_Materials/0_Original_Dataset), or in this link [here](https://www.kaggle.com/datasets/fatihilhan/global-superstore-dataset).

For a comprehensive understanding of the processes involved in implementing data preprocessing to achieve the data modeling, detailed information can be found in the notebook ["0_Data_Modeling.ipynb"](https://github.com/Prof-MatheusAndrade/Sales-Dataset-Exploration/blob/main/0_Materials/2_Databricks_Notebooks/0_Data_Modeling.ipynb). The input to this notebook is the CSV file with the original dataset, and the outputs include the creation of a database named "company" with a Delta table for the fact table, and other Delta tables for each dimension tables derived from the data model. 

To ensure data quality and integrity, a dedicated notebook, named ["1_Data_Quality.ipynb"](https://github.com/Prof-MatheusAndrade/Sales-Dataset-Exploration/blob/main/0_Materials/2_Databricks_Notebooks/1_Data_Quality.ipynb) was developed. This notebook incorporates various data quality checks, including statistical results such as minimum, maximum, and average values. Additionally, the notebook validates the presence of duplicate values in primary keys and their corresponding subjects. This meticulous data quality assurance process contributes to the reliability of the dataset, instilling confidence in the subsequent analysis and decision-making processes. 

## Relevant results in data preprocessing and quality check

In the pursuit of refining the dataset for analysis, thorough data preprocessing and quality checks were conducted. The outcomes of these efforts yielded valuable insights and improvements in data quality. Here are the relevant results identified during the preprocessing and quality checks:

### 1. Data Completeness and Numerical Results
During the data preprocessing phase, no issues related to missing values were identified. Numerical columns, such as "Shipping Cost" and "Sales," exhibited sound results without negative values or unusual outliers. Categorical columns across all tables demonstrated meaningful subjects, and the date column posed no issues, providing a solid foundation for subsequent analysis.

### 2. Fact Table - Order
In the fact table "Order," duplicates were identified in the "Order_ID" column. To resolve this, an incremental column was introduced to serve as the primary key for the fact table, and the original "Order_ID" column was renamed to "Order_local_ID." This approach ensures the uniqueness of each record in the fact table.

### 3. Dimension Table - Product
Within the dimension table "Product," discrepancies were observed in different features (e.g., product name) for the same "Product_ID." To maintain a one-to-many relationship in the snowflake model, the last content based on the last order date was considered during preprocessing. This ensures consistency and relevance in the dimension table.

### 4. Dimension Tables - Product_Category and Customer
The dimension tables "Product_Category" and "Customer" exhibited duplicates in content but with different primary keys. In these cases, the decision was made to consider only the primary key for identifying "Product_Category" and "Customers." This ensures data integrity and avoids redundancy in the snowflake model.

These identified results underscore the importance of rigorous data preprocessing and quality checks, ensuring the reliability and accuracy of the dataset. The proactive measures taken during this phase contribute to a robust foundation for subsequent analytical tasks, providing stakeholders with confidence in the validity of the derived insights.
