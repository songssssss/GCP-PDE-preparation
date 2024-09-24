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
























