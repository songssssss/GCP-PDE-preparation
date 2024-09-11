
# Data Processing and Pipelines

## Dataflow
You can refer to [this](https://cloud.google.com/dataflow) for docs.
 - Cloud version for *Apache Beam*. Apache Beam connectors avoid having to write much code to integrate proprietary data sources
 - Preferred for new Hadoop or Spark infrastructure development
 - Process batch or stream data. Dataflow provides managed resource scaling for efficient stream processing
 - Serverless, fast, scalable, fault-tolerant.
 - Multi-Step processing data. Eg: Wordcount.
 - Cloud dataflow executed as jobs where one or more worker carry out specific tasks
 - Supports SQL, Java, Python
 - When you run a job on Cloud Dataflow, it spins up a cluster of virtual machines, distributes the tasks in your job to the VMs, and dynamically scales the cluster based on how the job is performing.
 - Stackdriver integration for logging and monitoring
 - Used for data processing, ELT(Extract Transform Load), filter, group for data sets.
 - Can read data from multiple sources, can kick off multiple cloud functions in parallel and can also writer to multiple sinks (like BigQuery, BigTable etc.)
 - When you update a job on the Dataflow service, you replace the existing job with a new job that runs your updated pipeline code
 - Jobs can be created with inbuilt templates, or notebook instances(write jobs in Java/Python/SQL)
 - Dataflow pipelines can also run on alternate runtimes like Spark and Flink, as they are built using the Apache Beam SDKs
 - The Dataflow SDK provides a **transform** component. It is responsible for the data processing operation. You can use conditional, for loops, and other complex programming structure to create a branching pipeline.
 - Can apply [windowing](https://github.com/singhgautam7/GCP-PDE-preparation---GRS/blob/main/study_material/others/definitions/windowing.md) to streams for rolling average for the window, max in a window etc.
 - You can stop a Dataflow job in the following two ways:
	- Canceling a job. This method applies to both streaming and batch pipelines. Canceling a job stops the Dataflow service from processing any data, including buffered data
	- Draining a job. This method applies only to streaming pipelines. Draining a job enables the Dataflow service to finish processing the buffered data while simultaneously ceasing the ingestion of new data. Using the Drain option to stop your job tells the Dataflow service to finish your job in its current state. Your job will immediately stop ingesting new data from input sources, but the Dataflow service will preserve any existing resources (such as worker instances) to finish processing and writing any buffered data in your pipeline.
 - Updating the pipeline: 
 	- If any major change to windowing transformation (like completely changing window fn from fixed to sliding) in Beam/Dataflow/you want to stop pipeline but want inflight data --> use Drain option.
	- For all other use cases and Minor changing to windowing fn (like just changing window time of sliding window) --> Use Update with Json mapping.
 - Important IAM roles - 
	 - **dataflow.developer** role enable the developer interacting with the Cloud Dataflow job , with data privacy. It allows you to create and manage Dataflow jobs. It includes permissions to run jobs and view job details.
	 - **dataflow.worker** role provides the permissions necessary for a *Compute Engine service account* to execute work units for a Dataflow pipeline. It allows you to run Dataflow jobs.


 <details><summary>Common Concepts in Dataflow</summary>
<p>

- **Pipeline**: encapsulates series of computations that accepts input data from external sources, transforms data to provide some useful intelligence, and produce output. In the Dataflow SDKs, a pipeline represents a data processing job. You build a pipeline by writing a program using a Dataflow SDK. A pipeline consists of a set of operations that can read a source of input data, transform that data, and write out the resulting output. The data and transforms in a pipeline are unique to, and owned by, that pipeline. While your program can create multiple pipelines, pipelines cannot share data or transforms.
- **PCollections**: abstraction that represents a potentially distributed, multi-element data set, that acts as the pipeline’s data. PCollection objects represent input, intermediate, and output data. The edges of the pipeline.
- **Transforms**: operations in pipeline. A transform takes a PCollection(s) as input, performs an operation that you specify on each element in that collection, and produces a new output PCollection. Composite transforms are multiple transforms: combining, mapping, shuffling, reducing, or statistical analysis.
- **Pipeline I/O**: the source/sink, where the data flows in and out. Supports read and write transforms for a number of common data storage types, as well as custom.
- **Windowing**: Windowing a PCollection divides the elements into windows based on the associated event time for each element. Dataflow's default windowing behavior is to assign all elements of a PCollection to a single, global window, even for unbounded PCollections. Global Window: By default, Dataflow applies a Global Window to unbounded data sets. This means that all the data is treated as a single, continuous window. This default behavior is useful for scenarios where you need to process all incoming data together without explicit time-based or event-based partitioning.
- Key Points About Global Windowing:
	- **Unified Data View: All elements of the unbounded data stream are included in one global window, which simplifies processing if no specific windowing or time-based logic is needed.
	- **Custom Windowing: While the global window is the default, Apache Beam (and thus Dataflow) provides flexibility to define custom windowing strategies. For example, you can specify:
		- Fixed Windows: Divide data into fixed-size time intervals.
		- Sliding Windows: Overlap time intervals with configurable slide durations.
		- Session Windows: Group data based on periods of activity or inactivity.
	- Triggers and Accumulation: In conjunction with windowing, you can define triggers that determine when to emit results from the window. With global windowing, you might not use triggers extensively unless you have specific needs for processing and output.
	- Customizable: You can override the default global windowing behavior by specifying your own windowing strategy in your Apache Beam pipeline if you need more granular control over how data is partitioned and processed.
- **Triggers**: Allows specifying a trigger to control when (in processing time) results for the given window can be produced. Triggers determines when a Window's contents should be output based on certain criteria being met. Types of triggers are :  
	 - Time based triggers
	 - Data Driven triggers
	 - Composite triggers
- **Watermark**: It is a threshold that indicates when Dataflow expects all of the data in a window to have arrived. If new data arrives with a timestamp that's in the window but older than the watermark, the data is considered **late data**.
- **ParDo**: It is a parallel processing function which can transform elements of an input PCollection to an output PCollection.
- **DoFn**: It is a template which is used to create user defined functions that are referenced by ParDo
</p>
</details>

## DataProc
You can refer to [this](https://cloud.google.com/dataproc/) for docs.
 - Provides access to Hadoop cluster on GCP and Hadoop-ecosystem tools (Pig, Hive, and Spark).
 - Lift and Shift existing Spark/Hadoop jobs is possible
 - Automated cluster management
 - Dataproc automation helps you create clusters quickly, manage them easily, and save money by turning clusters off when not needed
 - Cluster types - 
	 - Standard (1 master, N workers)
	 - Single Node (1 master, 0 workers)
	 - High Availability (3 master, N workers)
 - After creating a Cloud Dataproc cluster, you can scale the cluster by increasing or decreasing the number of worker nodes in the cluster at any time, even when jobs are running on the cluster. Cloud Dataproc clusters are typically scaled to: 1) increase the number of workers to make a job run faster 2) decrease the number of workers to save money 3) increase the number of nodes to expand available Hadoop Distributed Filesystem (HDFS) storage
 - Worker node can be a regular VM or a Preemptible VM.
- The following rules will apply when you use *preemptible workers* with a Cloud Dataproc cluster:
	- Processing only: Since preemptibles can be reclaimed at any time, preemptible workers do not store data. Preemptibles added to a Cloud Dataproc cluster only function as processing nodes.
 	- No preemptible-only clusters: To ensure clusters do not lose all workers, Cloud Dataproc cannot create preemptible-only clusters.
  	- Persistent disk size: As a default, all preemptible workers are created with the smaller of 100GB or the primary worker boot disk size. This disk space is used for local caching of data and is not available through HDFS.
  	- The managed group automatically re-adds workers lost due to reclamation as capacity permits.

 - No. of master nodes cannot be changed.
 - Job Supported - Hadoop, SparkR, Spark, SparkSQL, Hive, Pig, PySpark
 - Can store data on disk (HDFS) or can use GCS
 - Google recommends using Cloud Storage instead of HDFS as it is much more cost effective especially when jobs aren’t running.
 - Cloud Dataproc is the better option when migrating and existing Spark/Hadoop cluster to GCP. **New data pipelines should prefer Cloud Dataflow**.
 - Hadoop/Spark jobs are run on Dataproc, and the **pre-emptible machines cost 80% less**.
 - Dataproc **Graceful Decommissioning** incorporates Graceful Decommission of YARN Nodes to finish work in progress on a worker before it is removed from the Cloud Dataproc cluster. By default this is disabled. 
	- This make sures that the work in progress is not lost while scaling.
 - If you create a Dataproc cluster with internal IP addresses only, attempts to access the Internet in an initialization action will fail unless you have configured routes to direct the traffic through a NAT or a VPN gateway. Without access to the Internet, you can enable Private Google Access, and **place job dependencies in Cloud Storage**; cluster nodes can download the dependencies from Cloud Storage from internal IPs.
 - Outputs can be automatically pushed to big query, big table, or gcs
 - IAM - 
	 - Service accounts used with Cloud Dataproc must have Dataproc/Dataproc Worker role (or have all the permissions granted by Dataproc Worker role).
		 - Need permissions to read and write to Google Cloud Storage, and to write to Google Cloud Logging
- The YARN ResourceManager and the HDFS NameNode interfaces are available on a Cloud Dataproc cluster master node. The cluster master-host-name is the name of your Cloud Dataproc cluster followed by an -m suffixfor example, if your cluster is named "my-cluster", the master-host-name would be "my-cluster-m".
- A Cloud Dataproc Viewer is limited in its actions based on its role. A viewer can only list clusters, get cluster details, list jobs, get job details, list operations, and get operation details.
- When using Cloud Dataproc clusters, configure your browser to use the SOCKS proxy. The SOCKS proxy routes data intended for the Cloud Dataproc cluster through an SSH tunnel.
- Although the pricing formula is expressed as an hourly rate, Dataproc is billed by the second, and all Dataproc clusters are billed in one-second clock-time increments, subject to a 1-minute minimum billing. Usage is stated in fractional hours (for example, 30 minutes is expressed as 0.5 hours) in order to apply hourly pricing to second-by-second use.
- start using Hive in Cloud Dataproc:
	C. Run the gsutil utility to transfer all ORC files from the Cloud Storage bucket to the master node of the Dataproc cluster. Then run the Hadoop utility to copy them do HDFS. Mount the Hive tables from HDFS.
	D. Leverage Cloud Storage connector for Hadoop to mount the ORC files as external Hive tables. Replicate external Hive tables to the native ones.
	
	I know it says to transfer all the files but with the options provided c is the best choice.
	Explaination
	A and B cannot be true as gsutil can copy data to master node and the to hdfs from master node.
	C -> works
	D->works Recommended by google. You can use the Cloud Storage connector for Hadoop to mount the ORC files stored in Cloud Storage as external Hive tables. This allows you to query the data without copying it to HDFS. You can replicate these external Hive tables to native Hive tables in Cloud Dataproc if needed.
	E-> Will work but as the question says maximize performance this is not a case. As bigquery hadoop connecter stores all the BQ data to GCS as temp and then processes it to HDFS. As data is already in GCS we donot need to load it to bq and use a connector then unloads it back to GCS and then processes it.

## Pub/Sub
You can refer to [this](https://cloud.google.com/pubsub/docs/overview) for docs.
 - Replacement for **Kafka**
 - Serverless messaging
 - Order of message not guaranteed
 - Async processing
 - Messages are persisted in message store until they are delivered and acknowledged by subscribers
 - When message is ack, it is removed from subscription's message queue
 - The only scenario for real-time(stream) is the use of pub/sub with push.
 - If messages exceed the 10MB maximum, they cannot be published.
 - If in exam it is writtern: "Delivery of confimed atleast 1 message" or "message must be delivered/processed atleast once" then go with the Pub/Sub option.
 - Pub sub can retain message only for 7 days maximum
 - It also integrates well with Cloud Dataflow
 - How to Deduplicate: 
	 - Duplicates can happen when endpoint is not acknowledging messages.
	 - Maintain a DB to store hash value for each entry.
	 - Pub/Sub assigns a unique `message_id` to each message which can be used to detect duplicates.
- Real-time Event Stream: Cloud Pub/Sub is a managed messaging service that can handle real-time event streams efficiently. You can use Pub/Sub to ingest and publish real-time market data to consumers.
- Pub/sub will be used to streaming data between application
- Use Google Stackdriver Monitoring on Cloud Pub/Sub: Check monitoring and logs to determine if there are any issues with message delivery or processing in Cloud Pub/Sub. This step can help identify problems with message consumption or delivery.

<details><summary>Use Cases of PubSub</summary>
<p>

1. Gather events from many clients simultaneously and use stream processing (like dataflow to deliver it to BigQuery, BigTable, CloudStorage on other DBs.
2. Replicating data among DBs
3. Parallel processing by Pub/Sub messages to connect to cloud functions.
4. Data streaming for  various processes or devices(ex- IOT devices).
5. Cache invalidation for distributed cashes by publishing events, i.e. refreshing caches.
6. Load balancing for reliability.
7. Implementing asynchronous workflows.
8. Distributing event notifications.
9. Logging to multiple systems.


</p>
</details>

## Data Fusion
You can refer to [this](https://cloud.google.com/data-fusion) for docs.
 - Code-free, drag and drop tool to quickly build data pipelines.

## DataPrep
You can refer to [this](https://cloud.google.com/dataprep/docs/how-to) for docs.
 - Service for visually exploring, cleaning, and preparing data for analysis. can transform data of any size stored in CSV, JSON, or relational table formats
 - Build by Trifacta – Third Party tool, not cloud native one
 - Dataprep is serverless and works at any scale
 - No code required
 - No infrastructure to deploy or manage
 - Automatically detect schema, anomalies
 - Dataprep can be run on Dataflow using template and cloud composer
 - Dataprep is used by non developers

## Cloud Composer
You can refer to [this](https://cloud.google.com/composer/docs) for docs.
 - Fully managed *Apache Airflow* in google cloud
 - Helps you create, schedule, monitor and manage workflows
 - Workflows are defined as DAG (Direct Acyclic Graphs) which are written in Python 3.x
 - This also has built-in support for other GCP services like Pub/sub, Cloud Storage, DataFlow, DataProc
 - It serves well when orchestrating interdependent pipelines
 - Cloud Composer should be used when there is inter-dependencies between the job, e.g. we need the output of a job to start another whenever the first finished, and use dependencies coming from first job
 - All interdependent tasks need to be run through cloud composer whereas small/adhoc tasks need to be run via **cloud scheduler**.
 - It also empowers you to author, schedule, and monitor **pipelines** that span across clouds and on-premises data centers.

## DataProc vs DataFlow vs DataPrep

| Workload | Dataproc | Dataflow |
|--|:-:|:-:|
|Stream processing (ETL)| No | Yes |
|Batch processing (ETL)| Yes | Yes |
|Iterative processing and notebooks| Yes | No |
|Machine learning with Spark ML| Yes | No |
|Preprocessing for Machine learning| No | Yes |

![enter image description here](https://cloud.google.com/architecture/images/data-lifecycle-4.svg)

## Apache Kafka
- Ability to Seek to a Particular Offset: Kafka allows consumers to seek to a specific offset in a topic, enabling you to read data from a specific point, including back to the start of all data ever captured. This is a fundamental capability of Kafka.
- Support for Publish/Subscribe Semantics: Kafka supports publish/subscribe semantics through topics. You can have hundreds of topics in Kafka, and consumers can subscribe to these topics to receive messages in a publish/subscribe fashion.
- Retain Per-Key Ordering: Kafka retains the order of messages within a partition. If you have a key associated with your messages, you can ensure per-key ordering by sending messages with the same key to the same partition.
- Scalability: Kafka is designed to handle high-throughput data streaming and is capable of scaling to meet your needs.
- Apache Kafka aligns well with the requirements you've outlined for centralized data ingestion and delivery. It's a robust choice for scenarios that involve data streaming, publish/subscribe, and retaining message ordering.
