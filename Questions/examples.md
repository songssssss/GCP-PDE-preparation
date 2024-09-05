## Question 22

Your financial services company is moving to cloud technology and wants to store 50 TB of financial time-series data in the cloud. This data is updated frequently and new data will be streaming in all the time. Your company also wants to move their existing Apache Hadoop jobs to the cloud to get insights into this data.

Which product should they use to store the data?
Cloud Bigtable
Google BigQuery
Google Cloud Storage
Google Cloud Datastore
Explain the above produects on their functions

---
For storing 50 TB of frequently updated financial time-series data and supporting Apache Hadoop jobs for insights, **Cloud Bigtable** is the most appropriate choice. Here’s an overview of each of the mentioned products and why Cloud Bigtable stands out for this use case:

### 1. **Cloud Bigtable**

- **Function**: Cloud Bigtable is a fully managed, scalable NoSQL database service designed for large analytical and operational workloads. It is optimized for time-series data, real-time analytics, and large-scale data storage.
- **Use Case**: It is ideal for storing large amounts of time-series data, such as financial data, because it efficiently handles high write throughput and large read volumes. Cloud Bigtable is well-suited for applications that require low-latency access to data and can scale horizontally to handle high data ingestion rates.
- **Features**: 
  - Handles large volumes of data and high request rates.
  - Suitable for time-series data, where data is continuously updated and needs to be queried efficiently.
  - Integrates with Apache Hadoop and other data processing frameworks.
  - Provides high availability and reliability.

### 2. **Google BigQuery**

- **Function**: Google BigQuery is a fully managed, serverless data warehouse designed for large-scale data analytics. It enables fast SQL queries using the processing power of Google's infrastructure.
- **Use Case**: BigQuery is excellent for running complex queries and performing analytics on large datasets. However, it is more suited for analytical workloads rather than real-time, frequently updated data ingestion.
- **Features**: 
  - Designed for interactive analysis and querying of large datasets.
  - Supports SQL queries and integrates well with data visualization tools.
  - Best for running analytical queries rather than serving as a primary store for continuously streaming data.

### 3. **Google Cloud Storage**

- **Function**: Google Cloud Storage is a scalable object storage service for storing and accessing any amount of data. It is designed for high durability and availability.
- **Use Case**: Ideal for storing large volumes of unstructured data, such as backups, data archives, and media. It is not optimized for high-frequency updates or low-latency access for time-series data.
- **Features**: 
  - Provides high durability and availability.
  - Suitable for archiving and backup rather than real-time data ingestion and analytics.
  - Data retrieval can be slower compared to specialized databases for real-time use cases.

### 4. **Google Cloud Datastore**

- **Function**: Google Cloud Datastore is a fully managed NoSQL document database designed for web and mobile applications. It provides a hierarchical data model and is suitable for applications requiring flexible schema and high availability.
- **Use Case**: Datastore is ideal for applications with flexible schema requirements and those needing automatic scaling. However, it is not optimized for handling large volumes of time-series data or high-throughput scenarios.
- **Features**: 
  - Supports hierarchical data and flexible schema.
  - Better suited for transactional data rather than large-scale time-series data.

### Recommendation

**Cloud Bigtable** is the best fit for your requirements because:

- It efficiently handles large volumes of time-series data with high write throughput and low-latency read access.
- It scales horizontally to accommodate increasing data volumes and ingestion rates.
- It integrates well with Apache Hadoop for running analytical jobs and gaining insights from your data.

While **Google BigQuery** and **Google Cloud Storage** are powerful tools for data analytics and storage, respectively, they are not as optimized for real-time data ingestion and frequent updates as Cloud Bigtable. **Google Cloud Datastore** is more suited for applications requiring flexible schema and hierarchical data rather than high-frequency time-series data.


---
## Question 33

You decided to use Cloud Datastore to ingest vehicle telemetry data in real time. You want to build a storage system that will account for the long-term data growth, while keeping the costs low. You also want to create snapshots of the data periodically, so that you can make a point-in-time (PIT) recovery, or clone a copy of the data for Cloud Datastore in a different environment. You want to archive these snapshots for a long time.

Which two methods can accomplish this?
(Choose two.)
Use managed export, and store the data in a Cloud Storage bucket using Nearline or Coldline class.
Use managed export, and then import to Cloud Datastore in a separate project under a unique namespace reserved for that export.
Use managed export, and then import the data into a BigQuery table created just for that export, and delete temporary export files.
Write an application that uses Cloud Datastore client libraries to read all the entities. Treat each entity as a BigQuery table row via BigQuery streaming insert. Assign an export timestamp for each export, and attach it as an extra column for each row. Make sure that the BigQuery table is partitioned using the export timestamp column.
Write an application that uses Cloud Datastore client libraries to read all the entities. Format the exported data into a JSON file. Apply compression before storing the data in Cloud Source Repositories.

---
Question 35

Your United States-based company has created an application for assessing and responding to user actions. The primary table's data volume grows by 250,000 records per second. Many third parties use your application's APIs to build the functionality into their own frontend applications. Your application's APIs should comply with the following requirements:
- Single global endpoint
- ANSI SQL support
- Consistent access to the most up-to-date data

What should you do?
Implement BigQuery with no region selected for storage or processing.
Implement Cloud Spanner with the leader in North America and read-only replicas in Asia and Europe.
Implement Cloud SQL for PostgreSQL with the master in Norht America and read replicas in Asia and Europe.
Implement Cloud Bigtable with the primary cluster in North America and secondary clusters in Asia and Europe.




Answer is Implement Cloud Spanner with the leader in North America and read-only replicas in Asia and Europe.

Cloud Spanner has three types of replicas: read-write replicas, read-only replicas, and witness replicas. Bigquery cannot support 250K data ingestion/second , as ANSI SQL support is required , no other options left except Spanner.

---







