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

Question 77

You need to give new website users a globally unique identifier (GUID) using a service that takes in data points and returns a GUID. This data is sourced from both internal and external systems via HTTP calls that you will make via microservices within your pipeline.
There will be tens of thousands of messages per second and that can be multi-threaded. and you worry about the backpressure on the system.

How should you design your pipeline to minimize that backpressure?
Call out to the service via HTTP.
Create the pipeline statically in the class definition.
Create a new object in the startBundle method of DoFn.
Batch the job into ten-second increments.


Answer is Batch the job into ten-second increments.

Option D is the best approach to minimize backpressure in this scenario. By batching the jobs into 10-second increments, you can throttle the rate at which requests are made to the external GUID service. This prevents too many simultaneous requests from overloading the service.

Option A would not help with backpressure since it just makes synchronous HTTP requests as messages arrive. Similarly, options B and C don't provide any inherent batching or throttling mechanism.

Batching into time windows is a common strategy in stream processing to deal with high velocity data. The 10-second windows allow some buffering to happen, rather than making a call immediately for each message. This provides a natural throttling that can be tuned based on the external service's capacity.

To design a pipeline that minimizes backpressure, especially when dealing with tens of thousands of messages per second in a multi-threaded environment, it's important to consider how each option affects system performance and scalability. Let's examine each of your options:

A. Call out to the service via HTTP: Making HTTP calls to an external service for each message can introduce significant latency and backpressure, especially at high throughput. This is due to the overhead of establishing a connection, waiting for the response, and handling potential network delays or failures.

B. Create the pipeline statically in the class definition: While this approach can improve initialization time and reduce overhead during execution, it doesn't directly address the issue of backpressure caused by high message throughput.

C. Create a new object in the startBundle method of DoFn: This approach is typically used in Apache Beam to initialize resources before processing a bundle of elements. While it can optimize resource usage and performance within each bundle, it doesn't inherently solve the backpressure issue caused by high message rates.

D. Batch the job into ten-second increments: Batching messages can be an effective way to reduce backpressure. By grouping multiple messages into larger batches, you can reduce the frequency of external calls and distribute the processing load more evenly over time. This can lead to more efficient use of resources and potentially lower latency, as the system spends less time waiting on external services.

Given these considerations, option D (Batch the job into ten-second increments) seems to be the most effective strategy for minimizing backpressure in your scenario. By batching messages, you can reduce the strain on your pipeline and external services, making the system more resilient and scalable under high load. However, the exact batch size and interval should be fine-tuned based on the specific characteristics of your workload and the capabilities of the external systems you are interacting with.

Additionally, it's important to consider other strategies in conjunction with batching, such as implementing efficient error handling, load balancing, and potentially using asynchronous I/O for external HTTP calls to further optimize performance and minimize backpressure.

---
Question 100

You launched a new gaming app almost three years ago. You have been uploading log files from the previous day to a separate Google BigQuery table with the table name format LOGS_yyyymmdd. You have been using table wildcard functions to generate daily and monthly reports for all time ranges. Recently, you discovered that some queries that cover long date ranges are exceeding the limit of 1,000 tables and failing.

How can you resolve this issue?
Convert all daily log tables into date-partitioned tables
Convert the sharded tables into a single partitioned table
Enable query caching so you can cache data from previous months
Create separate views to cover each month, and query from these views


Google says that when you have multiple wildcard tables, best option is to shard it into single partitioned table. Time and cost efficient
To address the issue of exceeding the limit of 1,000 tables due to your current sharded table structure in Google BigQuery, the most effective solution is to **convert the sharded tables into a single partitioned table**. Here’s why this approach works best and how it compares to the other options:

### 1. **Convert the Sharded Tables into a Single Partitioned Table**

**Description:**
- **Partitioned Tables**: In BigQuery, partitioned tables allow you to store large amounts of data in a single table while still being able to query efficiently across specific date ranges. You can partition tables by date, which will let you query data efficiently without hitting the 1,000-table limit.

**Advantages:**
- **Efficiency**: Queries on a partitioned table are often more efficient than those using table wildcards, especially for large date ranges.
- **Cost-Effective**: Reduces the need to scan multiple tables and simplifies the query logic, potentially lowering costs.
- **Scalability**: Avoids the issue of hitting table limits and scales better with large datasets over time.

**Implementation Steps:**
1. **Create a Partitioned Table**:
   ```sql
   CREATE TABLE `your_project.your_dataset.logs_partitioned` (
     log_date DATE,
     -- other columns
   )
   PARTITION BY log_date;
   ```

2. **Migrate Data**:
   - Load your existing sharded data into this new partitioned table. You can use a Data Transfer Service or write a script to handle the migration.

3. **Update Queries**:
   - Modify your queries to work with the new partitioned table. You can use date filters to specify the desired range.

   ```sql
   SELECT *
   FROM `your_project.your_dataset.logs_partitioned`
   WHERE log_date BETWEEN '2023-01-01' AND '2023-01-31';
   ```

### 2. **Convert All Daily Log Tables into Date-Partitioned Tables**

**Description:**
- This would involve creating multiple partitioned tables, each corresponding to a specific date range or period.

**Disadvantages:**
- **Over-Complexity**: Managing multiple partitioned tables can become cumbersome and does not solve the fundamental issue of exceeding the table limit.

### 3. **Enable Query Caching**

**Description:**
- Query caching in BigQuery is used to speed up query execution by reusing the results of previously run queries.

**Disadvantages:**
- **Not a Solution for Table Limits**: Caching helps with performance but does not address the issue of exceeding the table limit or manage large datasets effectively.

### 4. **Create Separate Views for Each Month**

**Description:**
- This involves creating views that aggregate data by month from the existing sharded tables.

**Disadvantages:**
- **Still Exceeds Table Limits**: Although views can simplify querying, you are still dealing with the original sharded tables and will eventually hit the 1,000-table limit.

### **Summary**

**Converting the sharded tables into a single partitioned table** is the best solution because it efficiently manages large datasets, avoids the 1,000-table limit, and improves query performance. It provides a scalable and manageable way to handle historical and ongoing data without running into limitations imposed by the sharded table approach.

Question 110

Your company needs to upload their historic data to Cloud Storage. The security rules don't allow access from external IPs to their on-premises resources. After an initial upload, they will add new data from existing on-premises applications every day.

What should they do?
Execute gsutil rsync from the on-premises servers.
Use Cloud Dataflow and write the data to Cloud Storage.
Write a job template in Cloud Dataproc to perform the data transfer.
Install an FTP server on a Compute Engine VM to receive the files and move them to Cloud Storage.

---
Question 108

You're using Bigtable for a real-time application, and you have a heavy load that is a mix of read and writes. You've recently identified an additional use case and need to perform hourly an analytical job to calculate certain statistics across the whole database. You need to ensure both the reliability of your production application as well as the analytical workload.

What should you do?
Export Bigtable dump to GCS and run your analytical job on top of the exported files.
Add a second cluster to an existing instance with a multi-cluster routing, use live-traffic app profile for your regular workload and batch-analytics profile for the analytics workload.
Add a second cluster to an existing instance with a single-cluster routing, use live-traffic app profile for your regular workload and batch-analytics profile for the analytics workload.
Increase the size of your existing cluster twice and execute your analytics workload on your new resized cluster.

Answer is Add a second cluster to an existing instance with a single-cluster routing, use live-traffic app profile for your regular workload and batch-analytics profile for the analytics workload.

You need to perform an hourly batch job on the cluster that already has high workload. in such cases, the best option is to replicate the cluster with single cluster routing. The original cluster can continue its read and writes. the replicated cluster can be used for analytical workload without impacting original cluster. Multi cluster routing is beneficial in cases where high availability is needed but requirement is only to isolate analytical workload from existing cluster.

---
Question 107

Your team is responsible for developing and maintaining ETLs in your company. One of your Dataflow jobs is failing because of some errors in the input data, and you need to improve reliability of the pipeline (incl. being able to reprocess all failing data).

What should you do?
Add a filtering step to skip these types of errors in the future, extract erroneous rows from logs.
Add a try... catch block to your DoFn that transforms the data, extract erroneous rows from logs.
Add a try... catch block to your DoFn that transforms the data, write erroneous rows to PubSub directly from the DoFn.
Add a try... catch block to your DoFn that transforms the data, use a sideOutput to create a PCollection that can be stored to PubSub later.


When dealing with data pipeline failures in Google Cloud Dataflow due to errors in input data, it’s important to ensure that your pipeline is resilient and can handle and reprocess errors effectively. Here's a breakdown of the options:

### 1. **Add a Filtering Step to Skip These Types of Errors in the Future, Extract Erroneous Rows from Logs**

**Description:**
- This approach involves modifying the pipeline to filter out problematic records that cause errors, and then extracting these errors from logs for further analysis.

**Advantages:**
- **Prevention**: Prevents the pipeline from failing on future errors of the same type.

**Disadvantages:**
- **Limited Reprocessing**: This does not directly address reprocessing or managing the erroneous data. It focuses on preventing failures but does not handle the errors that have already occurred.

### 2. **Add a Try... Catch Block to Your `DoFn` That Transforms the Data, Extract Erroneous Rows from Logs**

**Description:**
- This involves adding error handling within your `DoFn` to catch exceptions and then extract erroneous rows from logs.

**Advantages:**
- **Error Handling**: Catches and logs errors within the `DoFn`.

**Disadvantages:**
- **Reactive Approach**: This approach focuses on extracting errors after the fact, and it does not provide a mechanism for reprocessing or handling erroneous rows dynamically.

### 3. **Add a Try... Catch Block to Your `DoFn` That Transforms the Data, Write Erroneous Rows to Pub/Sub Directly from the `DoFn`**

**Description:**
- This approach involves handling errors in your `DoFn` and sending erroneous rows to Pub/Sub for further analysis or reprocessing.

**Advantages:**
- **Immediate Action**: Allows you to handle errors in real-time and forward erroneous rows for further processing or monitoring.

**Disadvantages:**
- **Potential Overhead**: Directly writing to Pub/Sub from `DoFn` can introduce overhead and complexity. The handling of erroneous rows needs to be carefully managed.

### 4. **Add a Try... Catch Block to Your `DoFn` That Transforms the Data, Use a SideOutput to Create a PCollection That Can Be Stored to Pub/Sub Later**

**Description:**
- This involves adding error handling within the `DoFn` and using a `SideOutput` to capture erroneous rows into a separate `PCollection`, which can then be written to Pub/Sub or another sink for later processing.

**Advantages:**
- **Structured Error Handling**: This method allows you to separately handle and reprocess erroneous data without affecting the main pipeline. 
- **Flexibility**: Enables reprocessing of erroneous data later, and keeps the main pipeline clean and focused on processing valid data.

**Disadvantages:**
- **Complexity**: Introduces additional steps and complexity in managing side outputs and ensuring that the erroneous data is properly handled and reprocessed.

### **Recommendation**

**Add a Try... Catch Block to Your `DoFn` That Transforms the Data, Use a SideOutput to Create a PCollection That Can Be Stored to Pub/Sub Later**

**Rationale:**
- This approach provides a robust way to handle errors and ensures that erroneous data can be captured, stored, and reprocessed separately from the main data pipeline. Using `SideOutput` allows for a clean separation of error handling and main data processing, which improves reliability and maintainability.

**Implementation Steps:**
1. **Add Error Handling**: Implement a `try... catch` block within your `DoFn` to handle and catch exceptions that occur during data transformation.
   
2. **Use SideOutput**: Create a `PCollection` for erroneous rows using `SideOutput`.

   ```python
   class MyDoFn(DoFn):
       def process(self, element, context):
           try:
               # Transformation logic
               yield transformed_element
           except Exception as e:
               # Capture erroneous rows in a side output
               context.side_output(erroneous_rows, element)
   
   p = Pipeline()
   main_data = p | 'Read' >> ReadFromSource()
   erroneous_data = main_data | 'Transform' >> ParDo(MyDoFn()).with_outputs('erroneous_rows', main='main_data')
   erroneous_data.erroneous_rows | 'WriteErrorsToPubSub' >> WriteToPubSub(...)
   main_data.main | 'WriteToBigQuery' >> WriteToBigQuery(...)
   ```

3. **Process SideOutput Data**: Set up a separate process or pipeline to handle and reprocess the erroneous data stored in Pub/Sub or another sink.

This approach ensures that your pipeline remains reliable and that errors are effectively managed and reprocessed, enhancing the overall robustness of your data processing workflows.





