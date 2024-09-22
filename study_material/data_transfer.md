# Data Transfer

All the sub-headings here represents approaches to data transfer.

## 1. Cloud Storage transfer tools

 - Upload data directly from computer to Cloud Storage.
 - For transfers up to few TBs.
 - Methods: 
	 - [Cloud Console UI](https://cloud.google.com/storage/docs/cloud-console#_uploadingdata) (Uploading data to bucket)
	 - [JSON API](https://cloud.google.com/storage/docs/json_api)
	 - [gsutil command line interface](https://cloud.google.com/storage/docs/quickstart-gsutil#upload_an_object_into_your_bucket) (parallel/multi-processing)

**The Google Cloud CLI (Command-Line Interface)** is a powerful tool provided by Google that allows users to interact with various Google Cloud services from the command line. Here are some key differences between using the Google CLI and not using it:

- Using Google CLI:
	* Efficiency: The CLI provides a streamlined way to interact with Google Cloud services without the need to navigate through the web console. This can save time and make tasks more efficient.
	Automation: With the CLI, you can automate tasks using scripts or batch commands, which can be especially useful for repetitive tasks or complex operations.
	* Flexibility: The CLI offers a wide range of commands and options for managing Google Cloud resources, giving users more flexibility and control over their cloud environment.
	* Integration: It can be easily integrated into CI/CD pipelines, allowing for seamless automation and deployment processes.
	* Portability: The CLI can be used across different operating systems, providing a consistent interface regardless of the platform.
- Not Using Google CLI:
	* Manual Operations: Without the CLI, users may need to rely on the Google Cloud Console web interface for managing resources, which can be more time-consuming, especially for repetitive tasks.
	* Limited Automation: Without the CLI, automating tasks may require more manual effort or the use of other tools, which may not be as efficient as using a dedicated command-line tool.
	* Learning Curve: Using the web console may have a steeper learning curve for users who are more comfortable with command-line interfaces.
	* Dependency on GUI: Without the CLI, users are dependent on the graphical user interface (GUI) provided by Google Cloud, which may not be as suitable for certain use cases or workflows.
In summary, using the Google CLI provides a more efficient, flexible, and automated way to interact with Google Cloud services compared to not using it, especially for users who prefer command-line interfaces or need to automate tasks in their cloud operations.


## 2. Storage Transfer Service

 - Quickly import online data into Cloud Storage from **other clouds**, from **on-premises** sources, or from **one bucket to another** within Google Cloud. Ex: Amazon s3, Azure Blob Storage
 - Set up recurring transfer jobs.
 - A managed solution which handles retries and provides detailed transfer logging.
 - The on-premise transfer service minimizes the transfer time by utilizing the maximum available bandwidth and by applying performance optimizations
 - Compressing and combining smaller files info fewer larger files is also a best practice for speeding up transfer speeds

| Transfer Scenario | Recommendation |
|--|--|
| Transferring from another cloud storage provider | Use Storage Transfer Service |
| Transferring less than 1 TB from on-premises | Use gsutil |
| Transferring more than 1 TB from on-premises | Use Transfer Service for on-premise data |
| Transferring less than 1 TB from another Cloud Storage region | Use gsutil |
| Transferring more than 1 TB from another Cloud Storage region | Use Storage Transfer Service |


## 3. Transfer Appliances
- Great option to migrate a large dataset and don’t have lots of bandwidth to spare
- Transfer Appliance enables seamless, secure, and speedy data transfer to Google Cloud
- For example, a 1 PB data transfer can be completed in just over 40 days using the Transfer Appliance, as compared the three years it would take to complete an online data transfer over a typical network (100 Mbps)
- Transfer appliance is highly performant because it uses all solid state drives

## 4. BigQuery Data Transfer Service
- Used to lay the foundation for a BigQuery data warehouse without writing a single line of code
- It automates data movement into BigQuery on a scheduled, managed basis
- It supports several [third-party sources](https://cloud.google.com/bigquery-transfer/docs/introduction#supported_data_sources) along with transfers from Google SaaS apps, external cloud storage providers. and data warehouses such as Teradata and Amazon Redshift

![enter image description here](https://storage.googleapis.com/gweb-cloudblog-publish/images/Data-Transfer-Service_v03-30-21.max-2000x2000.jpeg)
- 
