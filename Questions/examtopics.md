Question #21
Topic 1
Your company uses a proprietary system to send inventory data every 6 hours to a data ingestion service in the cloud. Transmitted data includes a payload of several fields and the timestamp of the transmission. If there are any concerns about a transmission, the system re-transmits the data. How should you deduplicate the data most efficiency?
A. Assign global unique identifiers (GUID) to each data entry. Most Voted
B. Compute the hash value of each data entry, and compare it with all historical data.
C. Store each data entry as the primary key in a separate database and apply an index.
D. Maintain a database table to store the hash value and other metadata for each data entry. Most Voted
 
To deduplicate the data efficiently in this scenario, the best approach would be:

### **A. Assign global unique identifiers (GUID) to each data entry.**

### Explanation:
Using GUIDs (or UUIDs) ensures that each entry is uniquely identifiable, making it easy to track and manage individual data entries. This method allows you to quickly check if an entry already exists in your database by simply comparing the GUIDs, which is efficient and avoids the overhead of computing hashes or managing separate hash tables.

### Other Options Considered:
- **B. Compute the hash value of each data entry**: This could work, but it requires comparing the hash against all historical data, which can be computationally expensive as the data grows.
  
- **C. Store each data entry as the primary key in a separate database**: While this might prevent duplicates, it doesn’t inherently resolve the issue of managing deduplication efficiently.

- **D. Maintain a database table to store the hash value and other metadata**: This is a viable option, but it still involves additional overhead for managing the hash values and checking against them.

### Conclusion:
While options B and D have their merits, option A stands out as the most straightforward and efficient method for deduplication in this scenario. If you have more questions or need further clarification, feel free to ask!



---
## Q41

For READ operation it's is correct. i.e. Date#Device (so that data read from single node) -
For write operation it should be DeviceID#Date (so that data write via multiple nodes)

The strategy you've outlined for optimizing read and write operations in Google Cloud Bigtable by structuring the row key differently for reads and writes is a common and effective approach known as "time series data modeling." This approach aims to improve read and write performance by considering the access patterns of the data.

### Read Operation - Date#Device:

- **Row Key Format: Date#Device**
  - When designing the row key for read operations, you've chosen to structure it as Date#Device.
  - This design allows you to efficiently retrieve data for a specific date and device together.
  - By combining the date and device in the row key, you can read data from a single node, enhancing read performance for queries that require data related to a specific date and device.

### Write Operation - DeviceID#Date:

- **Row Key Format: DeviceID#Date**
  - For write operations, you've chosen to structure the row key as DeviceID#Date.
  - This design aims to distribute writes across multiple nodes by including DeviceID first in the row key.
  - By starting with DeviceID in the row key, you can achieve better write scalability as writes related to different devices are spread across partitions, allowing for concurrent writes to different devices without creating hotspots.

### Benefits of this Approach:

1. **Optimized Read Performance:**
   - The Date#Device row key structure facilitates efficient retrieval of data for a specific date and device, enhancing read performance by reading from a single node.

2. **Improved Write Scalability:**
   - The DeviceID#Date row key structure helps distribute write operations across multiple nodes, improving write scalability by avoiding hotspots and allowing for concurrent writes to different devices.

3. **Balanced Data Distribution:**
   - By considering the access patterns for reads and writes, this approach balances data distribution and optimizes performance for both operations.

4. **Query Flexibility:**
   - The chosen row key formats provide flexibility for querying data based on either date or device, supporting different types of queries efficiently.

By structuring the row key differently for read and write operations in Google Cloud Bigtable based on the specific requirements of your application, you can optimize performance, scalability, and overall efficiency when reading and writing time series data.

---
## Q42
**Does Spark support MapReduce?**  
Apache Spark is a fast and general-purpose cluster computing system that provides high-level APIs in Java, Scala, Python, and R. While Spark does not directly use MapReduce for its processing, it can run on top of Hadoop YARN clusters and can also process data stored in HDFS. Spark provides its own distributed computing framework that is faster than traditional MapReduce due to its in-memory processing capabilities and DAG (Directed Acyclic Graph) execution engine.

**Differences between Pig and Spark:**

1. **Processing Model:**
   - **Pig:** Apache Pig is a data flow language that converts high-level Pig Latin scripts into MapReduce jobs for execution on Hadoop clusters. It is primarily designed for batch processing.
   - **Spark:** Apache Spark is a unified analytics engine for big data processing that provides support for batch processing, real-time processing, machine learning, and interactive queries. It uses an in-memory computation model and can process data faster than MapReduce.

2. **Execution Speed:**
   - **Pig:** Pig scripts are translated into MapReduce jobs, which can lead to slower processing times due to disk I/O involved in each MapReduce job.
   - **Spark:** Spark processes data in-memory and uses lazy evaluation and transformations through its RDD (Resilient Distributed Dataset) abstraction, leading to faster processing times compared to MapReduce and Pig.

3. **Programming Model:**
   - **Pig:** Pig Latin is a data flow language that is SQL-like and provides a high-level abstraction for data processing tasks.
   - **Spark:** Spark provides high-level APIs in Java, Scala, Python, and R. It supports a variety of programming languages and APIs, including DataFrames, Datasets, and Spark SQL.

4. **Fault Tolerance:**
   - **Pig:** Apache Pig relies on Hadoop's fault tolerance mechanisms built into the MapReduce framework.
   - **Spark:** Spark provides fault tolerance through lineage information stored for RDDs, enabling efficient recovery in case of node failures.

5. **Ease of Use:**
   - **Pig:** Pig is relatively easy to learn for those familiar with SQL-like languages. It abstracts the complexity of MapReduce programming.
   - **Spark:** Spark offers a more versatile and flexible programming model, but it may have a steeper learning curve compared to Pig.

In summary, while both Apache Pig and Apache Spark are tools for data processing on Hadoop clusters, they differ in their processing models, execution speed, fault tolerance mechanisms, programming languages, and ease of use. Spark is known for its speed and versatility, especially for in-memory processing, while Pig provides a simpler abstraction layer for data processing tasks.

---
## Q44
Excluding the time component when indexing a datetime field or timestamp can be a strategic decision based on the specific requirements of your application. Here are some reasons why you might choose to exclude the time component from indexing:

1. **Query Simplicity**: If your queries typically do not involve the time component or do not require precise time comparisons, excluding the time component can simplify your queries and indexing strategy.

2. **Reduced Index Size**: Excluding the time component can reduce the size of the index data structure, potentially saving storage space and improving query performance by making the index more compact.

3. **Aggregation Queries**: For scenarios where you need to aggregate data based on dates (e.g., daily, monthly), excluding the time component can make these aggregation queries easier and more efficient.

4. **Query Consistency**: Excluding the time component can help ensure that queries based on dates are consistent, especially if time precision is not necessary for your use case.

5. **Index Efficiency**: If queries primarily focus on date-based comparisons and ordering, excluding the time component can make the index more efficient and better optimized for those types of queries.

6. **Query Flexibility**: By excluding the time component, you can focus on date-based queries and potentially handle different time zones or date ranges more effectively.

7. **Simplified Logic**: Excluding the time component can simplify the logic for date-based queries, making it easier to work with and reducing the complexity of query construction.

However, it's essential to consider your specific use case and query patterns when deciding whether to exclude the time component from indexing. If your application requires precise time-based queries or if the time component is crucial for your data analysis, excluding the time component may not be appropriate.

Ultimately, the decision to exclude the time component from indexing should be based on a careful evaluation of your application's requirements, query patterns, and the trade-offs between query simplicity, index efficiency, and data accuracy.

---
## Q45
C. Create a cron job with Google App Engine Cron Service to run the Cloud Dataflow job.
Using the Google App Engine Cron Service to run the Cloud Dataflow job allows you to automate the execution of the job. By creating a cron job, you can ensure that the Dataflow job is triggered exactly once per day at a specified time. This approach is automated, reliable, and fits the requirement of processing the log file once per day.
Actually, google recommends Dataflow over Dataproc for both batch and streaming. Dataproc is only recommended if you are coming from
hadoop, spark, ....

The App Engine Cron Service allows you to configure regularly scheduled tasks that operate at defined times or regular intervals. These tasks are commonly known as cron jobs. These cron jobs are automatically triggered by the App Engine Cron Service. For instance, you might use this to send out a report email on a daily basis, to update some cached data every 10 minutes, or to update some summary information once an hour.

A cron job makes a scheduled HTTP GET request to the specified endpoint in the same app where the cron job is configured. The handler for that endpoint executes the logic when it is called.

The App Engine Cron Service cannot be used to call web endpoints outside the App Engine host app. It cannot be used to call App Engine endpoints from other apps besides the host app.

Cron job requests are subject to the same limits as other HTTP requests . Free applications can have up to 20 scheduled tasks. Paid applications can have up to 250 scheduled tasks.

---
## Q47
optimize the data schema + Machine Learning --> Bigquery
transactions 
--
## Q48
Bigquery understands UTF-8 encoding anything other than that will result in data issues with schema

If you don't specify an encoding, or if you specify UTF-8 encoding when the CSV file is not UTF-8 encoded, BigQuery attempts to convert the data to UTF-8. Generally, your data will be loaded successfully, but it may not match byte-for-byte what you expect
--
## Q49
Transfer Service is recommended for bandwidth 300mbps or faster

Follow these rules of thumb when deciding whether to use gsutil or Storage Transfer Service:
- Transfer scenario Recommendation
- Transferring from another cloud storage provider Use Storage Transfer Service.
- Transferring less than 1 TB from on-premises Use gsutil.
- Transferring more than 1 TB from on-premises Use Transfer service for on-premises data.
- Transferring less than 1 TB from another Cloud Storage region Use gsutil.
- Transferring more than 1 TB from another Cloud Storage region Use Storage Transfer Service.

C: gsutil parallel ingestion will reduce time
E: Storage Transfer service needs good internet and used for large size of data and for on premises storage, this one is regular ingestion.

---
## Q50
NoSQL: HBase, Cassandra, MongDB, Redis
Redis is limited to 1 TB capacity quota per region. So it doesn't satisfy the requirement.

NoSQL, telemetry data, IoT, high availability and low latency, not require ACID 
HBase, Cassandra, MongDB

A. Redis - Redis is an in-memory non-relational key-value store. Redis is a great choice for implementing a highly available in-memory cache to decrease data access latency, increase throughput, and ease the load off your relational or NoSQL database and application. Since the question does not ask cache,
E. Cassandra - Apache Cassandra is an open source NoSQL distributed database trusted by thousands of companies for scalability and high availability without compromising performance. Linear scalability and proven fault-tolerance on commodity hardware or cloud infrastructure make it the perfect platform for mission-critical data.
F. HDFS with Hive - Hive allows users to read, write, and manage petabytes of data using SQL. Hive is built on top of Apache Hadoop, which is an open-source framework used to efficiently store and process large datasets. As a result, Hive is closely integrated with Hadoop, and is designed to work quickly on petabytes of data. HIVE IS NOT A DATABSE.

Hive: data warehouse infrastructure
Apache Hadoop is an open-source framework designed for distributed storage and processing of large datasets across clusters of commodity hardware. 
---
## Q52
**DataProc Roles**
viewer role will not be able to submit dataproc jobs
---
## Q53
BigQuery query plan: 
Purple is reading, Blue is writing

Group by queries in BigQuery can run slowly when there is significant data skew on the grouped columns. Since the query is grouping by country, if most rows have the same country value, all that data will need to be shuffled to a single reducer to perform the aggregation. This can cause a data skew slowdown.
---
## Q54
Auction application. Bid
It has pub/sub push, more real time than pub/sub pull. You need to aware at some point, something has to be pulled which adds a latency.
Push: near real-time
Pull: add latency
---
#Q55
ODBC connections require standard SQL, not legacy SQL.

Legacy SQL vs Standard, BQ supports legacy SQL but ODBC or Most RDBMS connection doesn't support Legacy SQL, so in this case we need to create a new view on existing view or replace the existing one by changing syntax.
For ODBC, you just need a service account to authenticate as its external service connection. 
---
## Q56
`TABLE_DATE_RANGE()` : Queries multiple daily tables that span a date range.
 TABLE DATE RANGE function in legacy SQL
---
## Q57

For unbound collection, this will fail if any aggregation function is done

Beam’s default windowing behavior is to assign all elements of a PCollection to a single, global window and discard late data
even for unbounded PCollections. Before you use a grouping transform such as GroupByKey on an unbounded PCollection, you must do at least
one of the following:
—->>>>>>Set a non-global windowing function. See Setting your PCollection’s windowing function.
Set a non-default trigger. This allows the global window to emit results under other conditions, since the default windowing behavior (waiting for
all data to arrive) will never occur.
—->>>>If you don’t set a non-global windowing function or a non-default trigger for your unbounded PCollection and subsequently use a
grouping transform such as GroupByKey or Combine, your pipeline will generate an error upon construction and your job will fail. Global windowing is the default behavior,

---
## Q58
Cloud SQL would be the most appropriate choice for the online retailer in this scenario. Cloud SQL is a fully-managed relational database service that allows for easy management and analysis of data using SQL. It is well-suited for applications built on Google App Engine and can handle the transactional workload of an e-commerce application, as well as the analytical workload of a BI tool.

BigQuery is good for the analysis part but it's not good for managing transactions. If the question needed a database just to store the data for analysis it would be ok. But if we want to update single transactions or add them row by row, then it's not good. BigQuery is not made to support an application. It's a DW.

---
## Q82
Streaming ingestion -> Partitioned table rather than sharded tables

---
## Q85
Flat-rate service: a certain number of slots are dedicated to your projects. It is suitable for large enterprises with multiple business units and workloads with varying priorities and budgets.

---
## Q87
# By default, preemptible node disk sizes are limited to 100GB or the size of the non-preemptible node disk sizes, whichever is smaller.
However you can override the default preemptible disk size to any requested size. Since the majority of our cluster is using preemptible nodes,
the size of the disk used for caching operations will see a noticeable performance improvement using a larger disk. Also, SSD's will perform
better than HDD. This will increase costs slightly, but is the best option available while maintaining costs.

IF your work involves a lot of shuffling job, Aim for around 1GB per file (spark partition) (1). So by making parquet files larger, row groups can still be the same

---
## Q88
Adding a try-catch block to the DoFn that transforms the data would allow you to catch and handle errors within the pipeline. However, storing erroneous rows in Pub/Sub directly from the DoFn (Option C) could potentially create a bottleneck in the pipeline, as it adds additional I/O operations to the data processing.
Better use sideoutput as it doesn't make the workload heavier.

---
## Q89
use L1 regularization becuase we know the feature is a strong feature. L2 will evenly distribute weights
Use L1 regularization when you need to assign greater importance to more influential features. It shrinks less important feature to 0.
L2 regularization performs better when all input features influence the output & all with the weights are of equal size.

---
## Q90
MariaDB is a community-developed, commercially supported fork of the MySQL relational database management system (RDBMS). To collect logs and metrics for MariaDB, use the mysql receivers.
The mysql receiver connects by default to a local MariaDB server using a Unix socket and Unix authentication as the root user.

---
## Q92
- Cloud SQL is cheap and relational DB.
- Cloud SQL: max storage for shared core = 3TB and for dedicated core = up to 64TB
- Only use Spanner if we need autoscale (Note that Cloud SQL could scale too but not automatic yet) or the size is too big (as above > 10TB) or 4/5 9s HA (Cloud SQL is only 99.95)
- 
---
## Q93
### Bigtable for a real-time application, and you have a heavy load that is a mix of read and writes.

In the context of databases and cloud services, a **"live-traffic app profile"** refers to a configuration or set of parameters tailored for handling real-time, interactive workloads. This profile optimizes the database for low latency and high throughput, making it suitable for applications that require immediate data access and quick response times.

### Key Features of a Live-Traffic App Profile

1. **Low Latency**: The profile is designed to minimize response times, ensuring that user interactions (like API calls, web requests, etc.) are processed quickly.

2. **High Throughput**: It can handle a large number of concurrent requests, which is crucial for applications with many users or frequent updates.

3. **Optimized Resource Allocation**: Resources (such as CPU and memory) may be allocated specifically for real-time processing to ensure consistent performance under load.

4. **Read and Write Optimization**: The profile may optimize read and write operations to ensure that data can be quickly accessed and updated, crucial for applications like e-commerce sites, social media, or live data dashboards.

5. **Connection Management**: It may include settings for managing a high number of simultaneous connections, which is often necessary for applications with a large user base.

6. **Monitoring and Scaling**: The profile might have built-in monitoring tools to track performance and trigger automatic scaling when needed, ensuring that the application remains responsive.

### Use Case Examples
- **E-Commerce**: Handling transactions and user queries in real-time.
- **Social Media**: Displaying live feeds and processing user interactions immediately.
- **Gaming**: Managing real-time updates and interactions among players.

By utilizing a live-traffic app profile, organizations can ensure that their applications meet the demands of users in real-time, providing a smooth and responsive experience.

---
## Q95
Adding more nodes to a cluster (not replication) can improve the write performance
Key visualizer is Metrics for Performance issues. The key visualizer metrics options, suggest other things other than increase the cluster size. 
s Key Visualizer, it means the row key needs re-design again.

Storage utilization (% max)
- The percentage of the cluster's storage capacity that is being used. The capacity is based on the number of nodes in your cluster.
In general, do not use more than 70% of the hard limit on total storage, so you have room to add more data.

---
## Q98
The security rules **don't allow access from external IPs to their on-premises resources**. After an initial upload, they will add new data from existing on-premises applications every day. W

The gsutil tool is the standard tool for small- to medium-sized transfers (less than 1 TB) over a typical enterprise-scale network, from a private data center to Google Cloud. We recommend that you include gsutil in your default path when you use Cloud Shell. It's also available by default when you install the Google Cloud CLI. It's a reliable tool that provides all the basic features you need to manage your Cloud Storage instances, including copying your data to and from the local file system and Cloud Storage. It can also move and rename objects and perform real-time incremental syncs, like rsync, to a Cloud Storage bucket.

--- 
## Q100
need the data to be available within 1 minute of ingestion for real-time analysis” → low latency requirement → Dataflow streaming
---
## Q101
Without knowing the bandwidth, it is not possible to determine whether the upload can be completed within 7 days using gsutil.
gsutil has a limit of 1TBaccording to Google documentation,if data is morethan 1TBthen we have to use Transfer Appliance.

---
## Q103
BigQuery table snapshot preserves the contents of a table (called the base table) at a particular time. You can save a snapshot of a current table, or create a snapshot of a table as it was at any time in the past seven days. A table snapshot can have an expiration; when the configured amount of time has passed since the table snapshot was created, BigQuery deletes the table snapshot. You can query a table snapshot as you would a standard table. Table snapshots are read-only, but you can create (restore) a standard table from a table snapshot, and then you can modify the restored table.

Point-in-time snapshots only have data from the past 7 days at their creation. They can be stored for as long as desired
---
## Q104
The reasons:
A scheduler like Cloud Scheduler won't handle the dependency on the BigQuery load completion time
Using Composer allows creating a DAG workflow that can:
Trigger the BigQuery load
Wait for BigQuery load to complete
Trigger the Dataprep Dataflow job
Dataflow template allows easy reuse of the Dataprep transformation logic
Composer coordinates everything based on the dependencies in an automated workflow

---
## Q106
Graceful decommissioning: to finish work in progress on a worker before it is removed from the Cloud Dataproc cluster
Use Graceful Decommissioning for don't lose any data and add more(increase the cluster) preemptible workers because there are more cost-effective .
Increase the cluster size with preemptible worker nodes, and configure them to use graceful decommissioning.

---
## 129
If the corruption is caught within 7 days, query the table to a point in time in the past to recover the table prior to the corruption using snapshot decorators.

---
## Q130
Avoid updates in Datawarehousing environment instead use merge to create a new table.

---
## Q131
"Google Cloud Deployment Manager is an infrastructure deployment service that automates the creation and management of Google Cloud
resources. Write flexible template and configuration files and use them to create deployments that have a variety of Google Cloud services"

---
## Q132
A - NO - BigQuery with must have a selected regional or multi-regional file storage
B - YES - Spanner is specifically designed for this high and consistent throughput
C - NO - I am not sure about what many said in this discussion as Cloud SQL can store this amount of records if u have just a few columns. Anyway
for sure Spanner is better and it is a GCP product.
D - Bigtable - it's a NoSQL solution, no ANSI

Cloud Spanner is the first scalable, enterprise-grade, globally-distributed, and strongly consistent database service built for the cloud specifically to combine the benefits of relational database structure with non-relational horizontal scale.
Cloud Spanner is a fully managed, mission-critical, relational database service that offers transactional consistency at global scale, schemas, SQL
(ANSI 2011 with extensions), and automatic, synchronous replication for high availability.

---
## Q133
Bigtable provides lowest latency

---
# Q137
You have a data pipeline with a Dataflow job that aggregates and writes time series metrics to Bigtable. You notice that data is slow to update in Bigtable. This data feeds a dashboard used by thousands of users across the organization. You need to support additional concurrent users and reduce the amount of time required to write the data.
- Increase max num of workers increases pipeline performance in Dataflow
- Increase number of nodes in Bigtable increases write throughput

B. Increase the maximum number of Dataflow workers by setting maxNumWorkers in PipelineOptions:
Increasing the number of Dataflow workers can help parallelize the processing of your data, which can result in faster data updates to Bigtable and improved concurrency. You can set maxNumWorkers to a higher value to achieve this.
C. Increase the number of nodes in the Bigtable cluster:
Increasing the number of nodes in your Bigtable cluster can improve the overall throughput and reduce latency when writing data. It allows Bigtable to handle a higher rate of data ingestion and queries, which is essential for supporting additional concurrent users.

---
## Q139
You are building a new data pipeline to share data between two different types of applications: jobs generators and job runners. Your solution must scale to accommodate increases in usage and must accommodate the addition of new applications without negatively affecting the performance of existing ones.

- Job generators (they would be the publishers).
- Job runners = subscribers
Question mentions that it must scale (of which push subscription has automatic scaling) and can accommodate additional new applications (this can be solved by having multiple subscriptions, with each relating to a unique application) to a central topic

App Engine API: While scalable, it introduces a central point of failure and might not be as performant as Pub/Sub for high-volume data.

---
## Q140
You need to create a new transaction table in Cloud Spanner that stores product sales data. You are deciding what to use as a primary key. From a performance perspective, which strategy should you choose?
A random universally unique identifier number (version 4 UUID)

### For a transaction table in Cloud Spanner that stores product sales data, from a performance perspective, it is generally recommended to choose a primary key that allows for even distribution of data across nodes and minimizes hotspots. Therefore, option C, which suggests using a random universally unique identifier number (version 4 UUID), is the preferred choice.

---
## Q141
Answer D is correct. Aggregated log sink will create a single sink for all projects, the destination can be a google cloud storage, pub/sub topic, bigquery table or a cloud logging bucket. without aggregated sink this will be required to be done for each project individually which will be cumbersome

---
## Q142
Create a Cloud Monitoring dashboard based on the BigQuery metric slots/allocated_for_project
This metric represents the number of BigQuery slots allocated for a project. By creating a Cloud Monitoring dashboard based on this metric, you can monitor the slot usage within each project in your organization. This will allow each team to monitor their own slot usage and ensure that they are not exceeding their allocated quota.

---
## Q144
Description: Huge amount of data with log network bandwidth, Transfer applicate is best for moving data over 100TB

---
## Q148
AutoML is used to train model and do damage detection
Auto Vision is used is a pre trained model used to detect objects in images

AutoML:
Custom Model Training: AutoML allows users to train custom machine learning models tailored to specific datasets and use cases. It's designed for users who may not have extensive machine learning expertise but want to create specialized models.
Cloud Vision API:
Pre-trained Models: The Cloud Vision API provides access to pre-trained machine learning models for common tasks such as image labeling, text detection, face detection, and object localization. It’s ready to use without the need for additional training.


Answer is B. Train an AutoML model on your corpus of images, and build an API around that model to integrate with the package tracking applications.

For this scenario, where you need to automate the detection of damaged packages in real time while they are in transit, the most suitable solution among the provided options would be B.

Here's why this option is the most appropriate:

Real-Time Analysis: AutoML provides the capability to train a custom model specifically tailored to recognize patterns of damage in packages. This model can process images in real-time, which is essential in your scenario.

Integration with Existing Systems: By building an API around the AutoML model, you can seamlessly integrate this solution with your existing package tracking applications. This ensures that the system can flag damaged packages for human review efficiently.

Customization and Accuracy: Since the model is trained on your specific corpus of images, it can be more accurate in detecting damages relevant to your use case compared to pre-trained models.

Let's briefly consider why the other options are less suitable:
A. Use BigQuery machine learning: BigQuery is great for handling large-scale data analytics but is not optimized for real-time image processing or complex image recognition tasks like damage detection on packages.

C. Use the Cloud Vision API: While the Cloud Vision API is powerful for general image analysis, it might not be as effective for the specific task of detecting damage on packages, which requires a more customized approach.

D. Use TensorFlow in Cloud Datalab: While this is a viable option for creating a custom model, it might be more complex and time-consuming compared to using AutoML. Additionally, setting up a real-time analysis system through a Python notebook might not be as straightforward as an API integration.

---
## Q150
Sufficient Disk Capacity: Increasing the disk space ensures that there is enough room for all intermediate data, which is crucial for disk I/O intensive jobs. However, it’s important to note that simply increasing capacity does not directly improve speed; the combination of using HDFS for I/O-intensive operations and having sufficient space to avoid bottlenecks is key.


---
## Q154
Cloud SQL using MySQL. You need to ensure high availability in the event of a zone failure
Failover Replica: By creating a failover replica in another zone within the same region, you establish a high-availability configuration. The failover replica is kept in sync with the primary instance, and it can quickly take over in case of a failure of the primary instance.
Same Region: Placing the failover replica in the same region ensures minimal latency and data consistency. In the event of a zone failure, the failover can happen within the same region, reducing potential downtime.
Zone Resilience: Google Cloud's regional design ensures that zones within a region are independent of each other, which adds resilience to zone failures.
Automatic Failover: In case of a primary instance failure, Cloud SQL will automatically promote the failover replica to become the new primary instance, minimizing downtime.








