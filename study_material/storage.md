# Storage and Databases

<details><summary>Diagram on Types of Storage</summary>
<p>

![Types of storage](https://cloud.google.com/architecture/images/data-lifecycle-3.svg)
	
</p>
</details>

Here are the approximate figures for the handling capacity of Cloud SQL, Cloud Firestore (formerly Datastore), Cloud Spanner, and Bigtable:

- Cloud SQL:
Volume Handling: Cloud SQL can handle databases ranging from a few gigabytes to several terabytes in size, depending on the instance type and configuration.
Scaling: While Cloud SQL can handle moderate data volumes, it may start to face challenges with extremely large datasets and high traffic compared to other Google Cloud database services. It is more suitable for small to medium-sized databases.
- Cloud Firestore (formerly Datastore):
Volume Handling: Cloud Firestore (Datastore) is designed for high scalability and can handle massive volumes of data. It can easily scale to handle datasets exceeding multiple terabytes.
Scaling: Cloud Firestore is well-suited for applications that require high scalability and can handle very large datasets and high request rates effectively.
- Cloud Spanner:
Volume Handling: Cloud Spanner is designed to handle very large volumes of data across multiple regions. It can handle datasets ranging from terabytes to multiple petabytes.
Scaling: Cloud Spanner is highly scalable and can handle very large volumes of data with strong consistency and high availability across regions.
- Bigtable:
Volume Handling: Bigtable is designed to handle massive amounts of data, ranging from terabytes to petabytes and beyond.
Scaling: Bigtable is a highly scalable NoSQL database that can handle very large volumes of data and high throughput, making it suitable for applications that require low-latency data access at scale.
These figures are approximate and can vary based on the specific use case, instance configurations, data structures, and other factors. It's crucial to consider the specific requirements of your application when selecting a database service to ensure it can effectively handle the expected data volume and traffic.



## Cloud Storage
 - It is a bucket, or we can call it a blob storage - similar to *Amazon S3*
 - The content is not indexed at all.
 - No capacity or planning required. Almost unlimited storage.
 - Can be accessed by http(s) or REST APIs.
 - Multi-region or Dual-region also supported
 - Access control can be *uniform* or *fine-grained*
 - Object versioning and retention policy also supported.
 - A regional Google Cloud Storage is cheaper.
 - **Cloud Storage Connector** : This allows data to be directly accessed from Cloud Storage
 - Types of cloud storage:
	 - Standard (accessed frequently)
	 - Nearline (accessed once a month)
	 - Coldline (accessed once a quarter)
	 - Archive (accessed once a year)
 - On basis of conditions and actions, lifecycle of all objects in the bucket can be controlled
 - gsutil command used in shell.
 - The data here can be commonly used by Dataproc and BigQuery
 - *Signed URL*:
	 - Temporary access for a person with or without google account.
	 - Max limit = 10 days
	 - Access can be given **for objects** using signed url.
- Cloud Storage can be used for batch historical exports. You can export data from BigQuery to Cloud Storage in batch, making it available for consumers to download.
- Huge amount of data with log network bandwidth, Transfer applicate is best for moving data over 100TB
- Like gsutil, Storage Transfer Service for on-premises data enables transfers from network file system (NFS) storage to Cloud Storage. Although gsutil can support small transfer sizes (up to 1 TB), Storage Transfer Service for on-premises data is designed for large-scale transfers (up to petabytes of data, billions of files).

## DataStore
 - NoSQL DB, serverless, highly scalable
 - AutoScale supported.
 - High availability of reads and writes.
 - Fully managed with no planned downtime
 - **It is a fully managed and serverless solution that allows for transactions and will autoscale (storage and compute) without the need to manage any infrastructure**
 - Each transaction is guaranteed to be **atomic**, meaning that transactions are never partially applied. Either all of the operations in the transaction are applied, or none of them are applied.
 - Document kind storage
 - Tightly coupled with app engine, so one project can have just one firestore/datastore
 - GQL (Google Query Language) is used which is similar to SQL
 - Support ACID (Atomicity, Consistency, Isolation, Durability) transactions
 - Replication across different regions is possible
 - Export is only available with gcloud utility only.
 - Data exported from one Datastore mode database can be imported into another Datastore mode database, **even one in another project**
 - Cloud Datastore only retrieves results using indexes, it does not scan entities checking filter conditions.

<details><summary>Comparison b/w DataStore and RDBMS</summary>
<p>

|DataStore|RDBMS|
|:-:|:-:|
|Kind|Table|
|Key|PK|
|Entity|Row|
|Property|Column|
	
</p>
</details>

## FireStore
 - Only datastore or firestore can be used in a project
 - It is next gen datastore
 - Collection and document model used
 - Native mode = Firestore mode
 - Having more indexes will lead to greater storage sizes
 - Good replacement for **MongoDB**

<details><summary>Comparison b/w FireStore and RDBMS</summary>
<p>

|FireStore|RDBMS|
|:-:|:-:|
|Collection|Table|
|Document ID|PK|
|Document|Row|
|Field|Column|
	
</p>
</details>

## Cloud SQL
- Fully managed
- Cannot be scaled globally
- Cloud SQL is fully a managed transactional DB, but only the storage grows automatically. As your user base increases, you will need to increase the CPU/memory of the instance, and to do that you must edit the instance manually (and the questions specifically says "you do not want to manage infrastructure scaling")
- Can connect to App engine, Google Kubernetes Engine or Compute Engine
- Can Store 30 TB of data
- Backups - 
	- On-Demand Backups
	- Scheduled Backups
- DB Migration Service (DMS) available
- To shift some workloads, `read replicas` can be made.
- Cloud SQL supports transactions as well as **analysis through a _BI tool_**.
- Cloud SQL supports MySQL 5.6 or 5.7, and provides up to 624 GB of RAM and 30 TB of data storage, with the option to automatically increase the storage size as needed.
- It asks for scaling up which can be done in cloud sql, horizontal scaling is not possible in cloud sql
- Automatic storage increase: If you enable this setting, Cloud SQL checks your available storage every 30 seconds. If the available storage falls below a threshold size, Cloud SQL automatically adds additional storage capacity. If the available storage repeatedly falls below the threshold size, Cloud SQL continues to add storage until it reaches the maximum of 30 TB.

## Cloud Spanner
- Can be scaled globally.
- Costly.
- Use when data is > 2TB
- Lift and Shift not recommended for this.
- Spanner = SQL + Horizontal Scalability
- Enabling stale reads in Spanner would reduce data consistency and reduce latency.
- High replication possible
- We do not have to mention storage. So we do not change number of nodes for increasing or decreasing storage
- Each node can store upto 2TB
- 65% is the recommended CPU utilization for a regional instance Cloud Spanner instance
- 45% is the recommended CPU utilization for a multi-regional Cloud Spanner instance
- **Hotspotting** - 
	-  Hot spotting can occur when sequential values are used as primary keys
	-  Introduce more variation in the sort order of primary keys generated in close proximity.  Options for keys include using the hash of a natural key; swapping the  order of columns in keys to promote  higher-cardinality attributes; using a universally unique identifier (UUID), specifically version 4 or later; and using bit-reverse  sequential values.
- **Secondary Index** -
	- In a Cloud Spanner database, Cloud Spanner automatically creates an index for each table's primary key.
	- Secondary indexes are explicitly created using  the `CREATE INDEX` command
	- Secondary indexes are useful when filtering in a query using a `WHERE` clause. If the column referenced in the WHERE clause is indexed, the index can be used for filtering rather than scanning the full table and then filtering
- Use interleaved tables with a parent-child relationship in which parent data is stored with child data. This makes retrieving data from both tables simultaneously more efficient than if the data were stored separately and is especially helpful when performing joins. Since the data from both tables is co-located, the database has to perform fewer seeks to get all the needed data
- Three types of replicas: read-write replicas, read-only replicas, and witness replicas.
  
<details><summary>Cloud SQL vs Cloud Spanner</summary>
<p>

## SQL vs Spanner
- Cloud Spanner is used when you need to handle massive amounts of data with an elevated level of consistency and with a big amount of data handling (+100,000 reads/write per second). Spanner gives much better scalability and better SLOs.
- On the other hand, Spanner is also much more expensive than Cloud SQL.
- If you just want to store some data of your customer in a cheap way but still don't want to face server configuration Cloud SQL is the right choice.
- If you are planning to create a big product or if you want to be ready for a huge increase in users for your application (viral games/applications) Spanner is the right product
	
</p>
</details>

## Bigtable
Refer to this [link](https://cloud.google.com/bigtable/docs/overview) for doc.
- A managed service.
- No transactional support (so can handle petabytes of data)
- Bigtable is a key/value store, not a relational store. 
- It does not support joins, and transactions are supported only within a single row.
- HBase and Cassandra are similar wide-column databases.
- Supports HBase API
- Bigtable tables are **sparse**. A column doesn't take up any space in a row that doesn't use the column
- When you create a Cloud Bigtable instance and cluster, your choice of SSD or HDD storage for the cluster is permanent. If you need to convert an existing HDD cluster to SSD, or vice-versa, you can export the data from the existing instance and import the data into a new instance.
- Data Replication: Replications is copying data across multiple regions to increase durability. Just add another cluster and it will be possible to replicate the data.
- No downtime for cluster resize.
- While instance creation, clusters can be configured on number of nodes, SSD or HDD, Regional or Zone etc.
- Scales linearly. Increasing no. of nodes increases performance.
- Bigtable is a NoSQL database for massive writes, and to scale (storage and CPU) you must add nodes
- Mutations or Deletions takes extra storage as mutations are stored sequentially.
- Deletions are just specialized mutations.
- Automatic read-write operations to reorganize the data or to remove deleted items.
- A Cloud Bigtable instance is mostly just a container for your clusters and nodes, which do all of the real work.
- Tables belong to instances, not to clusters or nodes. So if you have an instance with up to 2 clusters, you can't assign tables to individual clusters
- For time-series data, financial data or IOT data, **BigTable is recommended** as it is highly scalable.
- Backups are also supported.
- It does not support SQL queries, joins or multi-row transactions.
- Not good for data less than 1TB of data or items greater than 10MB.
- `cbt` is a tool for doing basic interactions with Cloud Bigtable
- [Garbage collection](https://github.com/singhgautam7/GCP-PDE-preparation---GRS/blob/main/study_material/others/definitions/garbage_collection.md) is supported.
- Supports max of 1,000 tables in each instance.
- Can use up to around 100 column families.
- Empty columns don’t take up any space. Can create large number of columns, even if most columns are empty in most rows
- Adding more nodes to a cluster (not replication) can improve the write performance
- Google recommends adding nodes when storage utilization is > 70%
- BigTable provides **lowest latency**
- Multi-cluster routing is beneficial in cases where high availability is needed
- Field promotion avoids hotspotting
- It is recommended to create your Compute Engine instance in the same zone as your Cloud Bigtable instance for the best possible performance. If it's not possible to create a instance in the same zone, you should create your instance in another zone within the same region
- The only way to achieve strong consistency in Cloud Bigtable is by having all reads routed from a single cluster and using the other replicas only for failover
- Security : Can manage security at project, instance and table levels and it can be managed via IAM. For example, you can grant the ability to: Read from, but not write to, **any table** within the project. Read from and write to **any table** within the project, but not manage instances. Read from and write to **any table** within the project, and manage instances
- For Cloud Bigtable, you can configure access control at the project level. For example, you can grant the ability to:
	- Read from, but not write to, any table within the project.
	- Read from and write to any table within the project, but not manage instances.
	- Read from and write to any table within the project, and manage instances.
- In a Cloud Bigtable architecture all client requests go through a front-end server before they are sent to a Cloud Bigtable node.
- The nodes are organized into a Cloud Bigtable cluster, which belongs to a Cloud Bigtable instance, which is a container for the cluster. Each node in the cluster handles a subset of the requests to the cluster.
When additional nodes are added to a cluster, you can increase the number of simultaneous requests that the cluster can handle, as well as the maximum throughput for the entire cluster.

<details><summary>Row Keys in BigTable</summary>
<p>

Each table has only one index, the row key, and each row key must be unique. Best Practices for creating row keys:
- Design your row key based on the queries you will use to retrieve the data.
- It's important to create a row key that makes it possible to retrieve a well-defined range of rows.
- Avoid using a single row key to identify a value that must be updated very frequently
- Hashing a row key removes your ability to take advantage of Bigtable's natural sorting order
- Keep your row keys reasonably short
- Should not be only timestamp 
- Should not have timestamp at starting.
	
</p>
</details>

<details><summary>Schema Design in BigTable</summary>
<p>

- A tall and narrow table has a small number of events per row, which could be just one event, whereas a short and wide table has a large number of events per row.
- Narrow and tall table : storing one event per row; makes it easier to run queries the data.
- Short and Wide table : for data over a month, multiple events.

</p>
</details>

## BigQuery
Refer to this [link](https://cloud.google.com/bigquery/docs/introduction) for doc.
- Fully managed Data Warehouse
- Alternative to Hadoop with Hive
- Has connectors for BigTable, GCS, Google Drive and can import from Datastore backups, CSV, JSON and ARVO
- A serverless, analytical DB
- Uses SQL
- Zero infrastructure management
- Can query TB of data in seconds and PB of data in minutes
- Columnar storage
- Not for transactional purposes
- Can also query from external data sources like SQL, Bigtable
- Supports CSV, JSON, Avro, SQL, Parquet
	- Avro format has schema evolution capabilities and efficient serialization for flight telemetry data
- Querying is very expensive here
- Command line tool = `bq`
- Tables here have schema
- Jobs are async tasks that work on the top of table
- Used for load, query, extract or query data
- No join is preferred in BigQuery
- The data should be denormalized
- Denormalizing in BigQuery can be done with **nested and repeated columns**
- Security can be applied at a project level or dataset or at table level.
- _Authorized views_ allows to share query results without giving access to the underlying data
- Caching time = 24 hrs
- No prices from data fetched from cache.
- Can directly run query on cloud storage. No need for dataflow.
- BQ is optimised for reads
- **BigQuery Data Transfer Service** can only transfer data into BigQuery, not out of it
- You can load data into BigQuery via two options: batch loading (free) and streaming (costly). Both Batch and Streaming: BigQuery supports data ingestion in both batch and streaming modes. Batch mode is used for large, periodic data loads, while streaming mode allows for continuous data updates in real time.
- When using the Cloud Console, files loaded from a local data source cannot exceed 10 MB.
- BigQuery maintains a 7 day history of changes so that you can query a point-in time snapshot of data
- Wildcard tables - Used if you want to union all similar tables with similar names. ’*’ (e.g. project.dataset.Table*)
- **Partitioning > Table Sharding**: When you have multiple wildcard tables, best option is to shard it into single partitioned table. Time and cost efficient
- Types of queries - 
	- Interactive: query is executed immediately
	- Batch: Batches of queries are queued and the query starts when idle resources are available
- [Link](https://cloud.google.com/architecture/dw2bq/dw-bq-migration-overview) for Migrating data warehouses to BigQuery
- [Link](https://cloud.google.com/bigquery/docs/best-practices-performance-patterns) for Best practices for performance
- BigQuery supports ANSI SQL queries, making it suitable for both real-time and historical data analysis. You can stream data into BigQuery tables from Pub/Sub and provide ANSI SQL access to consumers.
- Before loading the data into BigQuery, use Cloud Data Loss Prevention (DLP) to replace input values with a cryptographic format-preserving encryption token.
	The key reasons are:
	- DLP allows redacting sensitive PII like SSNs before loading into BigQuery. This provides security by default for the raw SSN values.
	- Using format-preserving encryption keeps the column format intact while still encrypting, allowing business logic relying on SSN format to continue functioning.
	- The encrypted tokens can be reversed to view original SSNs when required, meeting the access requirement for customer service reps.
 - **TABLE_DATE_RANGE**: Legacy sql uses table date range whereas standard sql uses table_sufix for wildcard
<details><summary>Partitioning in BQ</summary>
<p>

- Dividing a table into **segments** to make it easier to manage and query data. This saves cost and time. 
- Partition is nothing but a newly created table. 
- You can partition on hourly or daily.
- Once table is created, you cannot change it partitioned

</p>
</details>

<details><summary>Clustering in BQ</summary>
<p>

- Data in clustered tables are **sorted** based on values in one or more columns
- Clustering is supported only on partitioned tables
- Clustered tables can improve performance of aggregate queries.

</p>
</details>

<details><summary>BigQuery Hierarchy</summary>
<p>

```
├── Project
│   ├── Datasets
│   │   ├── Tables
│   │   │   ├── Data
│   │   │   ├── Jobs
```

</p>
</details>

<details><summary>Types of Tables in BQ</summary>
<p>

- Native tables: 
	- *Permanent tables* are those that are created in a dataset and linked to an external source. Dataset-level access controls can be applied to these tables.
	- *Temporary tables* are created in a special dataset and will be available for approximately 24 hours. Temporary tables are useful for one-time operations or caching,  such as loading data into a data warehouse. It is not sharable. 
- External tables (from external sources, also know as **federated** sources). Used when tables are small. As an external data source, the frequently changing data does not need to be reloaded every time it is updated.
- Views

</p>
</details>

<details><summary>Use Cases of BQ</summary>
<p>

- When workload is analytical
- When the data does not change much in DB, since caching is also used in BigQuery
- When complex queries needs to be run
- Offload some work from primary DB to run time taking/complex queries

</p>
</details>

<details><summary>Import/Export in BQ</summary>
<p>

- Data Import -
	- Batch import - web console (local files), GCS, GDS
	- Stream - data with CDF, Cloud logging or POST calls. This is a paid service
	- Raw files - federated data source, CSV/JSON/Avro on GCS, Google sheets. Default file format is csv
	- By default, the BigQuery service expects all source data to be UTF-8 encoded. BQ also supports ISO-8859-1
	- To support (occasionally) schema changing we can use 'Automatically detect' for schema changes. Automatically detect is not default selected
- Data Export - 
	- Data can only be exported in JSON / CSV / Avro
	- To export more than 1 GB of data, you need to put a wildcard in the destination filename. (up to 1 GB of table data to a single file)

</p>
</details>

<details><summary>Controlling Cost in BigQuery</summary>
<p>

- Avoid SELECT * (full scan), select only columns needed (SELECT * EXCEPT)
- Sample data using preview options for free
- Preview queries to estimate costs (dryrun)
- Use max bytes billed to limit query costs
- Don’t use LIMIT clause to limit costs (still full scan)
- Monitor costs using dashboards and audit logs
- Partition data by date
- Break query results into stages
- Use default table expiration to delete unneeded data
- Use streaming inserts wisely
- Set hard limit on bytes (members) processed per day
	
</p>
</details>

<details><summary>Query Performance in BigQuery</summary>
<p>
	
- Generally, queries that do less work perform better
- Input Data/Data Sources
	- Avoid SELECT *
	- Prune partitioned queries (for time-partitioned table, use PARTITIONTIME pseudo column to filter partitions)
	- Denormalize data (use nested and repeated fields)
	- Use external data sources appropriately
	- Avoid excessive wildcard tables
- SQL Anti-Patterns
	- Avoid self-joins., use window functions (perform calculations across many table rows related to current row)
	- Partition/Skew: avoid unequally sized partitions, or when a value occurs more often than any other value
	- Cross-Join: avoid joins that generate more outputs than inputs (pre-aggregate data or use window function) Update/Insert Single Row/Column: avoid point-specific DML, instead batch updates and inserts.
- Optimizing Query Computation
	- Avoid repeatedly transforming data via SQL queries
	- Avoid JavaScript user-defined functions
	- Use approximate aggregation functions (approx count)
	- Order query operations to maximize performance. Use ORDER BY only in outermost query, push complex operations to end of the query.
	- For queries that join data from multiple tables, optimize join patterns. Start with the largest table.
	
</p>
</details>

<details><summary>Pricing in BigQuery</summary>
<p>

BigQuery offers a choice of two pricing models for running queries - 
1. **On-demand pricing**: With this pricing model, you are **charged for the number of bytes processed** by each query. The first 1 TB of query data processed per month is free.
2. **Flat-rate pricing**. With this pricing model, you purchase slots, which are** virtual CPUs**. When you buy slots, you are buying dedicated processing capacity that you can use to run queries. Slots are available in the following commitment plans:
	- _Flex slots_: You commit to an initial 60 seconds.
	- _Monthly_: You commit to an initial 30 days.
	- _Annual_: You commit to 365 days.
	
</p>
</details>
**Clustering**
In general, there are two typical usage patterns for clustering within a data warehouse:
- Clustering on columns that have a very high number of distinct values, like userId or transactionId.

- Clustering on multiple columns that are frequently used together. When clustering by multiple columns, the order of columns you specify is important. The order of the specified columns determines the sort order of the data. You can filter by any prefix of the clustering columns and get the benefits of clustering, like regionId, shopId and productId together; or regionId and shopId; or just regionId.

## Choosing a Database
- If there is a requirement to search terabytes or petabytes of data relatively quickly it will make more sense to simply store in BigQuery.
- If the data set is relatively small < 10TB then DataStore will be preferred.
- If the data set is > 10TB and/or there is no requirement for multiple indexes then BigTable will be better.
- If searching for objects by attribute value is required, then Datastore is preferred.
- If high throughput writes of wide column data then Bigtable is preferred.
- If there is a need of data warehousing then BigQuery is preferred.
- Bigtable is best suited to the following scenarios: time-series data (e.g. CPU and memory usage over time for multiple servers), financial data (e.g. transaction histories, stock prices, and currency exchange rates), and IoT (Internet of Things) use cases
---
![Storage Comparison](https://juanignaciosl.github.io/img/deogcp-storage.png)
---
![Which Storage Should I Use](https://storage.googleapis.com/gweb-cloudblog-publish/images/Storage-to-Use_v04-23-21.max-1600x1600.jpeg)
---
![Which DB Should I Use](https://storage.googleapis.com/gweb-cloudblog-publish/images/Which-Database_v07-10-21_1.max-2000x2000.jpeg)
