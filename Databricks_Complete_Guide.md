# Complete Databricks Learning Guide: From Scratch to Production

## Table of Contents
1. [Introduction to Databricks](#introduction-to-databricks)
2. [Why Databricks?](#why-databricks)
3. [Core Concepts](#core-concepts)
4. [Getting Started](#getting-started)
5. [Databricks Workspace](#databricks-workspace)
6. [Working with Data](#working-with-data)
7. [Spark SQL for SQL Users](#spark-sql-for-sql-users)
8. [Python and PySpark](#python-and-pyspark)
9. [Working with AWS Integration](#working-with-aws-integration)
10. [Advanced Topics](#advanced-topics)
11. [Best Practices](#best-practices)
12. [Real-World Projects](#real-world-projects)
13. [Resources and Next Steps](#resources-and-next-steps)

---

## Introduction to Databricks

### What is Databricks?

Databricks is a unified analytics platform built on top of Apache Spark. It provides a collaborative environment for data engineers, data scientists, and analysts to work together on big data processing, machine learning, and analytics workloads.

Think of Databricks as:
- **For Data Engineers**: A platform to build and manage data pipelines at scale
- **For Data Scientists**: An environment for machine learning experiments and model deployment
- **For Analysts**: A way to query massive datasets using familiar SQL syntax

### Key Components

1. **Databricks Workspace**: Web-based collaborative environment
2. **Databricks Runtime**: Optimized Apache Spark runtime with additional features
3. **Delta Lake**: Open-source storage layer with ACID transactions
4. **MLflow**: Machine learning lifecycle management
5. **Databricks SQL**: Serverless SQL analytics

---

## Why Databricks?

### Problems It Solves

1. **Scale**: Process petabytes of data efficiently
2. **Speed**: Distributed computing across clusters
3. **Collaboration**: Shared notebooks and workspaces
4. **Cost**: Optimized infrastructure management
5. **Integration**: Works seamlessly with AWS, Azure, GCP

### When to Use Databricks

- Processing large datasets (TB+)
- Real-time streaming analytics
- Machine learning at scale
- Data warehousing needs
- Collaborative data teams

---

## Core Concepts

### 1. Apache Spark

Spark is the underlying engine that powers Databricks. Key concepts:

- **Resilient Distributed Dataset (RDD)**: Fundamental data structure
- **DataFrame**: Distributed collection of data organized in named columns (similar to SQL tables)
- **Dataset**: Type-safe, object-oriented API (available in Scala/Java)
- **Partitioning**: Data split across nodes for parallel processing

**For SQL users**: A DataFrame is like a SQL table, but it's distributed across multiple machines.

### 2. Clusters

- **Driver Node**: Coordinates the job execution
- **Worker Nodes**: Execute tasks in parallel
- **Cluster Types**:
  - **Interactive Clusters**: For ad-hoc analysis and notebooks
  - **Job Clusters**: For scheduled/automated jobs

### 3. Delta Lake

Delta Lake adds reliability to data lakes:
- **ACID Transactions**: Ensures data consistency
- **Time Travel**: Query historical versions of data
- **Schema Evolution**: Handle schema changes gracefully
- **Upserts/Merges**: Update and insert operations

**For MySQL users**: Think of Delta Lake as giving you MySQL-like reliability in a data lake environment.

### 4. Notebooks

- Interactive coding environment (like Jupyter notebooks)
- Support multiple languages: Python, SQL, Scala, R
- Can share code cells and results
- Built-in visualizations

---

## Getting Started

### Prerequisites Check

You mentioned you have:
- ✅ **SQL/MySQL**: You'll use this extensively in Spark SQL
- ✅ **Python**: Essential for PySpark
- ✅ **AWS**: We'll integrate with S3, EC2, IAM

### Step 1: Account Setup

1. Go to [databricks.com](https://databricks.com)
2. Sign up for **Databricks Community Edition** (free) or **Azure Databricks Trial**
3. For production, you'll typically use **AWS Databricks** (we'll cover this later)

### Step 2: Understanding the Interface

Once logged in, you'll see:
- **Workspace**: Your folder structure
- **Clusters**: Compute resources
- **Jobs**: Scheduled tasks
- **SQL Warehouses**: For SQL queries
- **Repos**: Git integration

---

## Databricks Workspace

### Creating Your First Notebook

1. Click **Workspace** → **Create** → **Notebook**
2. Choose language: **Python** or **SQL**
3. Attach to a cluster (or create one)

### Notebook Basics

```python
# Cell 1: Display Spark version
print(spark.version)

# Cell 2: Create a simple DataFrame
data = [(1, "Alice", 25), (2, "Bob", 30), (3, "Charlie", 35)]
df = spark.createDataFrame(data, ["id", "name", "age"])
df.show()
```

### Creating a Cluster

1. Go to **Compute** → **Create Cluster**
2. Choose cluster type: **Standard** or **Single Node** (for learning)
3. Select Databricks Runtime version (latest stable)
4. Configure:
   - **Cluster name**: `learning-cluster`
   - **Cluster mode**: Single Node (cheaper) or Standard
   - **Worker type**: Small instance for learning
5. Click **Create Cluster**

**Note**: Clusters auto-terminate after inactivity (configurable). You only pay for compute time.

---

## Working with Data

### Data Sources in Databricks

Databricks can read from:
- **Files**: CSV, JSON, Parquet, Delta
- **Databases**: MySQL, PostgreSQL, Oracle, etc.
- **Cloud Storage**: S3, ADLS, GCS
- **Data Warehouses**: Snowflake, Redshift, BigQuery
- **Streaming Sources**: Kafka, Kinesis

### Reading Data

#### Example 1: Reading CSV (Similar to MySQL LOAD DATA)

```python
# Read CSV file
df = spark.read.format("csv") \
    .option("header", "true") \
    .option("inferSchema", "true") \
    .load("/path/to/file.csv")

# Or using SQL
df.createOrReplaceTempView("my_table")
spark.sql("SELECT * FROM my_table LIMIT 10").show()
```

#### Example 2: Reading from S3 (AWS Integration)

```python
# Configure AWS credentials (or use IAM roles)
spark.conf.set("spark.hadoop.fs.s3a.access.key", "your-access-key")
spark.conf.set("spark.hadoop.fs.s3a.secret.key", "your-secret-key")

# Read from S3
df = spark.read.format("csv") \
    .option("header", "true") \
    .load("s3a://your-bucket/path/to/file.csv")
```

#### Example 3: Reading from MySQL (Your Existing Database)

```python
# Read from MySQL database
df = spark.read \
    .format("jdbc") \
    .option("url", "jdbc:mysql://your-mysql-host:3306/your_database") \
    .option("dbtable", "your_table") \
    .option("user", "your_username") \
    .option("password", "your_password") \
    .load()

df.show()
```

### Writing Data

```python
# Write to CSV
df.write.format("csv") \
    .option("header", "true") \
    .mode("overwrite") \
    .save("/path/to/output.csv")

# Write to Parquet (columnar format, better performance)
df.write.format("parquet") \
    .mode("overwrite") \
    .save("/path/to/output.parquet")

# Write to S3
df.write.format("parquet") \
    .mode("overwrite") \
    .save("s3a://your-bucket/output/")
```

---

## Spark SQL for SQL Users

If you know SQL, Spark SQL will feel very familiar!

### Basic SQL Operations

```sql
-- Create a temporary view (like a MySQL view)
CREATE OR REPLACE TEMPORARY VIEW employees AS
SELECT * FROM csv.`/path/to/employees.csv`

-- Basic SELECT (same as MySQL)
SELECT 
    department,
    COUNT(*) as emp_count,
    AVG(salary) as avg_salary
FROM employees
WHERE salary > 50000
GROUP BY department
ORDER BY avg_salary DESC;
```

### Key Differences from MySQL

| MySQL | Spark SQL |
|-------|-----------|
| Single machine | Distributed across cluster |
| Immediate execution | Lazy evaluation (optimization) |
| Limited to table size | Handles petabytes |
| ACID by default | ACID with Delta Lake |

### Common SQL Patterns in Spark SQL

#### 1. Joins (Same as MySQL)

```sql
-- Inner Join
SELECT a.*, b.*
FROM table_a a
INNER JOIN table_b b ON a.id = b.id;

-- Left Join
SELECT a.*, b.*
FROM table_a a
LEFT JOIN table_b b ON a.id = b.id;
```

#### 2. Window Functions (Same as MySQL 8.0+)

```sql
-- ROW_NUMBER, RANK, DENSE_RANK
SELECT 
    employee_id,
    salary,
    department,
    ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) as dept_rank,
    AVG(salary) OVER (PARTITION BY department) as dept_avg_salary
FROM employees;
```

#### 3. CTEs (Common Table Expressions)

```sql
WITH high_earners AS (
    SELECT * FROM employees WHERE salary > 100000
),
dept_stats AS (
    SELECT 
        department,
        COUNT(*) as count,
        AVG(salary) as avg_sal
    FROM high_earners
    GROUP BY department
)
SELECT * FROM dept_stats WHERE count > 10;
```

### Advanced Spark SQL Features

#### 1. Array Functions

```sql
-- Working with arrays
SELECT 
    id,
    collect_list(name) as all_names,  -- Collect values into array
    array_contains(collect_list(name), 'John') as has_john
FROM employees
GROUP BY id;
```

#### 2. JSON Functions

```sql
-- Parse JSON data
SELECT 
    get_json_object(json_column, '$.name') as name,
    get_json_object(json_column, '$.age') as age
FROM json_table;
```

#### 3. Date Functions

```sql
-- Date operations (similar to MySQL)
SELECT 
    CURRENT_DATE() as today,
    DATE_ADD(CURRENT_DATE(), 7) as next_week,
    DATEDIFF('2024-12-31', CURRENT_DATE()) as days_remaining,
    YEAR(hire_date) as hire_year,
    MONTH(hire_date) as hire_month
FROM employees;
```

---

## Python and PySpark

### PySpark vs Regular Python

PySpark allows you to use Python syntax with Spark's distributed computing:

```python
# Regular Python (single machine)
data = [1, 2, 3, 4, 5]
result = [x * 2 for x in data]  # Runs on one machine

# PySpark (distributed)
rdd = spark.sparkContext.parallelize([1, 2, 3, 4, 5])
result = rdd.map(lambda x: x * 2).collect()  # Runs on multiple machines
```

### Working with DataFrames (PySpark Style)

#### Creating DataFrames

```python
# Method 1: From list of tuples
data = [(1, "Alice", 25), (2, "Bob", 30), (3, "Charlie", 35)]
columns = ["id", "name", "age"]
df = spark.createDataFrame(data, columns)

# Method 2: From Pandas DataFrame (if you know Pandas)
import pandas as pd
pandas_df = pd.DataFrame(data, columns=columns)
df = spark.createDataFrame(pandas_df)

# Method 3: From JSON
df = spark.read.json("/path/to/data.json")
```

#### DataFrame Operations

```python
# Select columns (like SQL SELECT)
df.select("name", "age").show()

# Filter (like SQL WHERE)
df.filter(df.age > 30).show()
# Or
df.filter("age > 30").show()

# Group by and aggregate
df.groupBy("department") \
  .agg({"salary": "avg", "salary": "max", "id": "count"}) \
  .show()

# Order by (like SQL ORDER BY)
df.orderBy(df.age.desc()).show()

# Joins
df1.join(df2, df1.id == df2.id, "inner").show()
```

#### Column Operations

```python
from pyspark.sql import functions as F
from pyspark.sql.types import *

# Add new column
df = df.withColumn("age_plus_10", df.age + 10)

# Conditional logic (like SQL CASE WHEN)
df = df.withColumn("age_group", 
    F.when(df.age < 30, "Young")
     .when(df.age < 50, "Middle")
     .otherwise("Senior"))

# String operations
df = df.withColumn("name_upper", F.upper(df.name))
df = df.withColumn("name_length", F.length(df.name))

# Date operations
df = df.withColumn("current_date", F.current_date())
df = df.withColumn("days_diff", F.datediff(F.current_date(), df.hire_date))
```

### Converting Between SQL and DataFrame API

You can use both approaches interchangeably:

```python
# DataFrame API
df.filter(df.age > 30).select("name", "age").show()

# SQL (same result)
df.createOrReplaceTempView("people")
spark.sql("SELECT name, age FROM people WHERE age > 30").show()
```

### User-Defined Functions (UDFs)

When built-in functions aren't enough:

```python
from pyspark.sql.types import StringType

# Define a Python function
def categorize_age(age):
    if age < 30:
        return "Young"
    elif age < 50:
        return "Middle"
    else:
        return "Senior"

# Register as UDF
categorize_age_udf = F.udf(categorize_age, StringType())

# Use it
df = df.withColumn("age_category", categorize_age_udf(df.age))
```

---

## Working with AWS Integration

### Setting Up Databricks on AWS

1. **Launch Databricks on AWS**:
   - Use AWS Marketplace or Databricks website
   - Choose VPC, subnets, security groups
   - Configure IAM roles for access

2. **IAM Roles** (Best Practice):
   ```json
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "s3:GetObject",
           "s3:PutObject",
           "s3:DeleteObject",
           "s3:ListBucket"
         ],
         "Resource": [
           "arn:aws:s3:::your-bucket/*",
           "arn:aws:s3:::your-bucket"
         ]
       }
     ]
   }
   ```

### Reading from S3

```python
# Method 1: Using s3a:// (recommended)
df = spark.read.format("csv") \
    .option("header", "true") \
    .load("s3a://your-bucket/path/to/file.csv")

# Method 2: Using s3:// (slower)
df = spark.read.format("csv") \
    .option("header", "true") \
    .load("s3://your-bucket/path/to/file.csv")
```

### Writing to S3

```python
# Write to S3
df.write.format("parquet") \
    .mode("overwrite") \
    .option("compression", "snappy") \
    .save("s3a://your-bucket/output/")

# Partitioned write (improves query performance)
df.write.format("parquet") \
    .partitionBy("year", "month") \
    .mode("overwrite") \
    .save("s3a://your-bucket/output/")
```

### Accessing AWS Services

#### Reading from RDS (MySQL/PostgreSQL)

```python
# Read from RDS MySQL
df = spark.read \
    .format("jdbc") \
    .option("url", "jdbc:mysql://your-rds-endpoint:3306/dbname") \
    .option("dbtable", "table_name") \
    .option("user", "username") \
    .option("password", "password") \
    .load()
```

#### Reading from Redshift

```python
df = spark.read \
    .format("jdbc") \
    .option("url", "jdbc:redshift://cluster.region.redshift.amazonaws.com:5439/dbname") \
    .option("dbtable", "table_name") \
    .option("user", "username") \
    .option("password", "password") \
    .load()
```

### EC2 Integration

Databricks runs on EC2 instances. You can:
- Choose instance types for clusters
- Use Spot instances for cost savings
- Configure auto-scaling

---

## Advanced Topics

### Delta Lake

Delta Lake is crucial for production workloads:

#### Creating Delta Tables

```python
# Write as Delta format
df.write.format("delta") \
    .mode("overwrite") \
    .save("/delta/table_path")

# Or using SQL
df.write.format("delta").saveAsTable("my_delta_table")
```

#### Delta Operations

```sql
-- Upsert (INSERT + UPDATE)
MERGE INTO target_table t
USING source_table s
ON t.id = s.id
WHEN MATCHED THEN UPDATE SET *
WHEN NOT MATCHED THEN INSERT *
```

```python
# Python equivalent
from delta.tables import DeltaTable

deltaTable = DeltaTable.forPath(spark, "/delta/table_path")

deltaTable.alias("target") \
    .merge(
        source_df.alias("source"),
        "target.id = source.id"
    ) \
    .whenMatchedUpdateAll() \
    .whenNotMatchedInsertAll() \
    .execute()
```

#### Time Travel

```sql
-- Query previous version
SELECT * FROM delta.`/path/to/delta` VERSION AS OF 0;

-- Query by timestamp
SELECT * FROM delta.`/path/to/delta` TIMESTAMP AS OF '2024-01-01';
```

### Streaming Data

#### Structured Streaming

```python
# Read streaming data from Kafka
stream_df = spark.readStream \
    .format("kafka") \
    .option("kafka.bootstrap.servers", "host1:port1,host2:port2") \
    .option("subscribe", "topic_name") \
    .load()

# Process stream
processed_stream = stream_df.selectExpr("CAST(key AS STRING)", "CAST(value AS STRING)")

# Write to output
query = processed_stream.writeStream \
    .format("delta") \
    .outputMode("append") \
    .option("checkpointLocation", "/checkpoint/path") \
    .start("/output/path")
```

#### Reading from Kinesis (AWS)

```python
stream_df = spark.readStream \
    .format("kinesis") \
    .option("streamName", "your-stream") \
    .option("region", "us-east-1") \
    .option("awsAccessKeyId", "your-key") \
    .option("awsSecretKey", "your-secret") \
    .load()
```

### Performance Optimization

#### 1. Partitioning

```python
# Partition data when writing
df.write.format("delta") \
    .partitionBy("country", "year") \
    .save("/delta/partitioned_table")

# Partition existing table
spark.sql("""
    OPTIMIZE delta.`/path/to/table`
    ZORDER BY (user_id, event_date)
""")
```

#### 2. Caching

```python
# Cache DataFrame in memory
df.cache()  # or df.persist()

# Unpersist when done
df.unpersist()
```

#### 3. Broadcast Joins (for small tables)

```python
# Broadcast small DataFrame for efficient joins
from pyspark.sql.functions import broadcast

large_df.join(broadcast(small_df), "id")
```

#### 4. Repartitioning

```python
# Repartition for better parallelism
df = df.repartition(200)  # 200 partitions

# Coalesce to reduce partitions
df = df.coalesce(10)  # Reduce to 10 partitions
```

### Machine Learning with MLlib

```python
from pyspark.ml import Pipeline
from pyspark.ml.feature import VectorAssembler, StandardScaler
from pyspark.ml.regression import LinearRegression
from pyspark.ml.evaluation import RegressionEvaluator

# Prepare features
assembler = VectorAssembler(inputCols=["feature1", "feature2"], outputCol="features")
scaler = StandardScaler(inputCol="features", outputCol="scaled_features")

# Model
lr = LinearRegression(featuresCol="scaled_features", labelCol="label")

# Pipeline
pipeline = Pipeline(stages=[assembler, scaler, lr])

# Train
model = pipeline.fit(training_data)

# Predict
predictions = model.transform(test_data)

# Evaluate
evaluator = RegressionEvaluator(labelCol="label", predictionCol="prediction")
rmse = evaluator.evaluate(predictions)
```

### Job Scheduling

#### Creating Jobs

1. Go to **Jobs** → **Create Job**
2. Configure:
   - **Task name**
   - **Type**: Notebook, JAR, Python script
   - **Source**: Notebook path
   - **Cluster**: New cluster or existing
   - **Schedule**: Cron expression

Example cron schedule:
- `0 0 * * *` - Daily at midnight
- `0 */6 * * *` - Every 6 hours
- `0 9 * * 1` - Every Monday at 9 AM

---

## Best Practices

### 1. Data Organization

```
/databricks-datasets/          # Sample datasets
/user/hive/warehouse/          # Hive tables
/delta/                        # Delta tables
/tmp/                          # Temporary data
/prod/raw/                     # Raw data
/prod/processed/               # Processed data
/prod/curated/                 # Final curated data
```

### 2. Cluster Management

- ✅ Use **single node clusters** for small datasets
- ✅ **Auto-terminate** clusters after inactivity
- ✅ Use **Spot instances** for non-critical jobs
- ✅ **Right-size** clusters (don't over-provision)

### 3. Code Organization

```python
# Good: Modular code
def extract_data(source_path):
    return spark.read.format("csv").load(source_path)

def transform_data(df):
    return df.filter(df.age > 18)

def load_data(df, target_path):
    df.write.format("delta").save(target_path)

# Main pipeline
raw_df = extract_data("/source")
clean_df = transform_data(raw_df)
load_data(clean_df, "/target")
```

### 4. Error Handling

```python
try:
    df = spark.read.format("csv").load("/path/to/file.csv")
    df.show()
except Exception as e:
    print(f"Error reading file: {e}")
    # Handle error appropriately
```

### 5. Data Quality

```python
# Validate data
assert df.count() > 0, "DataFrame is empty"
assert "required_column" in df.columns, "Required column missing"

# Check for nulls
null_counts = df.select([F.count(F.when(F.col(c).isNull(), c)).alias(c) for c in df.columns])
null_counts.show()
```

---

## Real-World Projects

### Project 1: ETL Pipeline (Extract, Transform, Load)

**Goal**: Build an ETL pipeline from MySQL to S3

```python
# Step 1: Extract from MySQL
mysql_df = spark.read \
    .format("jdbc") \
    .option("url", "jdbc:mysql://host:3306/db") \
    .option("dbtable", "orders") \
    .option("user", "user") \
    .option("password", "pass") \
    .load()

# Step 2: Transform
transformed_df = mysql_df \
    .filter(mysql_df.order_date >= "2024-01-01") \
    .withColumn("order_year", F.year(mysql_df.order_date)) \
    .withColumn("order_month", F.month(mysql_df.order_date)) \
    .groupBy("order_year", "order_month") \
    .agg(F.sum("total_amount").alias("monthly_revenue"))

# Step 3: Load to S3 as Delta
transformed_df.write.format("delta") \
    .partitionBy("order_year", "order_month") \
    .mode("overwrite") \
    .save("s3a://your-bucket/analytics/monthly_revenue")
```

### Project 2: Data Lake Analytics

**Goal**: Analyze large CSV files stored in S3

```sql
-- Create external table pointing to S3
CREATE TABLE IF NOT EXISTS sales_data
USING DELTA
LOCATION 's3a://your-bucket/sales-data/'

-- Analyze data
SELECT 
    region,
    product_category,
    SUM(revenue) as total_revenue,
    AVG(revenue) as avg_revenue,
    COUNT(*) as transaction_count
FROM sales_data
WHERE transaction_date >= '2024-01-01'
GROUP BY region, product_category
ORDER BY total_revenue DESC
LIMIT 20;
```

### Project 3: Real-time Streaming Analytics

**Goal**: Process streaming data from Kinesis

```python
# Read from Kinesis
stream_df = spark.readStream \
    .format("kinesis") \
    .option("streamName", "sales-stream") \
    .option("region", "us-east-1") \
    .load()

# Parse JSON and process
from pyspark.sql.functions import from_json, col
from pyspark.sql.types import StructType, StructField, StringType, DoubleType

schema = StructType([
    StructField("product_id", StringType()),
    StructField("amount", DoubleType()),
    StructField("timestamp", StringType())
])

parsed_df = stream_df.select(
    from_json(col("data").cast("string"), schema).alias("parsed_data")
).select("parsed_data.*")

# Aggregate in windows
from pyspark.sql.functions import window

windowed_df = parsed_df \
    .withColumn("timestamp", F.to_timestamp("timestamp")) \
    .withWatermark("timestamp", "10 minutes") \
    .groupBy(
        window("timestamp", "5 minutes"),
        "product_id"
    ) \
    .agg(F.sum("amount").alias("total_amount"))

# Write to Delta table
query = windowed_df.writeStream \
    .format("delta") \
    .outputMode("update") \
    .option("checkpointLocation", "/checkpoint/kinesis") \
    .table("real_time_sales_metrics")

query.awaitTermination()
```

---

## Resources and Next Steps

### Official Resources

1. **Databricks Documentation**: [docs.databricks.com](https://docs.databricks.com)
2. **Databricks Academy**: Free courses and certifications
3. **Apache Spark Documentation**: [spark.apache.org](https://spark.apache.org/docs/latest/)
4. **Delta Lake Documentation**: [delta.io](https://delta.io)

### Learning Path

1. **Week 1-2**: Basics
   - Set up account and workspace
   - Create notebooks and clusters
   - Learn DataFrame operations
   - Practice with sample datasets

2. **Week 3-4**: SQL and Data Processing
   - Master Spark SQL
   - Work with different data formats
   - Practice joins, aggregations, window functions

3. **Week 5-6**: AWS Integration
   - Connect to S3
   - Read from RDS/Redshift
   - Set up IAM roles
   - Optimize S3 reads/writes

4. **Week 7-8**: Advanced Topics
   - Delta Lake operations
   - Streaming with Structured Streaming
   - Performance optimization
   - Machine learning basics

5. **Week 9-10**: Production
   - Build end-to-end pipelines
   - Schedule jobs
   - Error handling and monitoring
   - Best practices

### Practice Datasets

- **Databricks Sample Datasets**: Built into workspace
- **Kaggle**: Download datasets and practice
- **AWS Public Datasets**: Free large datasets on S3
- **Your own data**: Start with small datasets from your work

### Common Commands Cheat Sheet

```python
# Initialize Spark
spark = SparkSession.builder.appName("MyApp").getOrCreate()

# Read data
df = spark.read.format("csv").option("header", "true").load("path")

# Write data
df.write.format("delta").mode("overwrite").save("path")

# SQL
df.createOrReplaceTempView("table_name")
spark.sql("SELECT * FROM table_name").show()

# Useful DataFrame operations
df.show()                    # Display data
df.printSchema()             # Show schema
df.describe().show()         # Statistics
df.count()                   # Row count
df.columns                   # List columns
df.distinct().count()        # Unique rows
```

### Getting Help

- **Databricks Community Forum**: Community support
- **Stack Overflow**: Tag `apache-spark` and `databricks`
- **GitHub**: Apache Spark and Delta Lake repos
- **Databricks Support**: If you have a paid account

---

## Conclusion

You now have a comprehensive guide to learn Databricks from scratch! Remember:

1. **Start Simple**: Begin with small datasets and basic operations
2. **Practice Regularly**: Build small projects to reinforce concepts
3. **Use Your Existing Skills**: Your SQL and Python knowledge transfers directly
4. **Experiment**: Try different approaches and learn from mistakes
5. **Read Documentation**: Databricks docs are excellent and constantly updated

### Key Takeaways

- Databricks = Apache Spark + Collaborative Workspace + Optimizations
- Spark SQL is very similar to MySQL SQL
- PySpark combines Python with distributed computing
- Delta Lake adds reliability to data lakes
- AWS integration is straightforward with proper IAM setup

### Next Steps

1. ✅ Create a Databricks account
2. ✅ Complete the first notebook tutorial
3. ✅ Try the examples in this guide
4. ✅ Build your first ETL pipeline
5. ✅ Join the Databricks community

Happy learning! 🚀

