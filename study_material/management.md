# Management

## Identity and Access Management (IAM)
- Types of accounts - 
	- *Service Accounts* are for non human users such as applications
	- *Google Accounts* are for single users
	- *Google groups* are for multi users
- Billing - 
	- Billing access can be provided to a project or set of projects without granting access to the content
	- This is useful for separation of duties between finance/developers etc.
- Roles - 
```
TYPES OF ROLES
├── Primitive
│   ├── Owner
│   ├── Editor
│   ├── Viewer
│
├── Pre-defined (Examples below)
│   ├── Compute Admin
│   ├── Storage Viewer
│
├── Custom
│   ├── Combined collection of permissions
```
In Google Cloud IAM (Identity and Access Management), roles are used to grant specific permissions to users, groups, or service accounts. Roles can be broadly categorized into three types:

### 1. **Basic Roles**
These roles are predefined and apply to all Google Cloud services. They include:

- **Viewer (`roles/viewer`)**: Grants read-only access to all resources.
- **Editor (`roles/editor`)**: Grants read and write access to all resources, including the ability to modify them.
- **Owner (`roles/owner`)**: Grants full control over all resources, including the ability to manage roles and permissions.

### 2. **Predefined Roles**
These roles are specific to certain services and provide granular permissions. For example:

- **BigQuery Roles**:
  - **BigQuery Data Viewer (`roles/bigquery.dataViewer`)**: Read access to BigQuery datasets and tables.
  - **BigQuery Data Editor (`roles/bigquery.dataEditor`)**: Read and write access to BigQuery datasets and tables.
  - **BigQuery Admin (`roles/bigquery.admin`)**: Full control over BigQuery resources.

- **Compute Engine Roles**:
  - **Compute Instance Admin (`roles/compute.instanceAdmin`)**: Manage VM instances.
  - **Compute Network Admin (`roles/compute.networkAdmin`)**: Manage networking resources.

### 3. **Custom Roles**
Custom roles allow you to create roles tailored to your specific needs by combining various permissions. This provides flexibility in granting access based on the specific actions a user or service account needs to perform.
- **Authorized Viewer Role**: roles/iam.authorizedViewer
	- Purpose: View metadata and resources without accessing sensitive data.
	- Use Case: Data governance, compliance, and controlled access scenarios.

### Additional Categories
- **Service Accounts**: Roles can also be assigned to service accounts, allowing applications to perform actions on Google Cloud resources.
- **Organization and Folder Roles**: Roles can be applied at the organization or folder level to manage access across multiple projects.

### Summary of Roles
- **Basic Roles**: Viewer, Editor, Owner.
- **Predefined Roles**: Service-specific roles (e.g., BigQuery Data Viewer, Compute Instance Admin).
- **Custom Roles**: Tailored roles based on specific permissions.

## Stackdriver
[Link](https://cloud.google.com/products/operations) to docs
- Now know as *Google Cloud's operations suite*
- For storing, searching, analyzing, monitoring, and alerts on log data and events.
- **Audit Logs to review data access** (e.g. BigQuery)
- Application Performance Management (APM) combines the monitoring and troubleshooting capabilities of Cloud Logging and Cloud Monitoring without aggregated sink this will be required to be done for each project individually which will be cumbersome.
- Monitoring does not only provide you with access to Dataflow-related metrics, but also lets you to create alerting policies and dashboards so you can chart time series of metrics and choose to be notified when these metrics reach specified values.
- Stack driver could tell us about performance **but NOT logging of missing data**.
- Use cases - 
	- **Debugger**: inspect state of app in real time without stopping/slowing down e.g. code behavior
	- **Error Reporting**: counts, analyzes, aggregates crashes in cloud services
	- **Monitoring**: overview of performance, uptime and heath of cloud services (metrics, events, metadata)
	- **Alerting**: create policies to notify you when health and uptime check results exceed a certain limit
	- **Tracing**: tracks how requests propagate through applications/receive near real-time performance results, latency reports of VMs
	- **Logging**: store, search, monitor and analyze log data and events from GCP
#### Cloud Logging
- Stores log for 30 days
- Bigtable is not a sink option here.
- There is no way to create an alert on Cloud Logging not receiving data from a service

#### Cloud Monitoring
- Create dashboards and visualizations
- Collect metrics from GCP, AWS and hybrid resources
- **Alerting** and Anamoly reporting

#### Components Use-Cases
| Component | Used for |
|--|--|
| Stackdriver Logging | Collect semi-structured data about events |
| Stackdriver Debugger | Inspect the state of running code |
| Stackdriver Monitoring | Collects performance metrics |
| Stackdriver Trace | Collect information about the time required to execute functions in a call stack |

## Cloud Deployment Manager
- Allows you to specify all the resources needed for your application in a declarative format using yaml

## Data Catalog
- Cloud Catalog is designed to help data consumers understand what data is available, what it means, and how it can be used
- A fully managed and highly scalable data discovery and metadata management service
- Single place to discover all data, asset across all project
- Use cases - Search and tag data
- Data Catalog will collect metadata automatically from several GCP sources. These sources include Cloud Storage, Cloud Bigtable, Google Sheets, BigQuery, and Cloud Pub/Sub.
- In addition to native metadata, Data Catalog can collect custom  metadata through the use of tags
  


#### **Service Account**
A **service account** in Google Cloud is a special type of account that is used to perform automated tasks or run applications without human intervention. Unlike regular user accounts, service accounts are intended for machine-to-machine communication and provide a way for your applications to authenticate and interact with Google Cloud services securely.

### Key Features of Service Accounts

1. **Authentication**:
   - Service accounts use key files (JSON or P12 format) to authenticate API requests. This allows applications to authenticate programmatically without user interaction.

2. **Roles and Permissions**:
   - You can assign IAM roles to service accounts, defining what resources they can access and what actions they can perform. This ensures that service accounts have only the permissions they need, adhering to the principle of least privilege.

3. **Use Cases**:
   - Commonly used for applications running on Google Cloud (like Google App Engine, Cloud Functions, or Compute Engine) that need to access other Google Cloud services.
   - Can also be used in CI/CD pipelines, where automated processes require access to Google Cloud resources.

4. **Service Account Email**:
   - Each service account has a unique email address (e.g., `service-account-name@project-id.iam.gserviceaccount.com`) that is used to identify the service account in IAM policies.

5. **Impersonation**:
   - Other users or applications can impersonate a service account to gain its permissions temporarily, which is useful for delegating access without sharing keys.

### Creating a Service Account

1. **In the Google Cloud Console**:
   - Go to the **IAM & Admin** section.
   - Click on **Service accounts**.
   - Click **Create Service Account** and follow the prompts to set up the account and assign roles.

2. **Using the gcloud CLI**:
   ```bash
   gcloud iam service-accounts create [SERVICE_ACCOUNT_NAME] --description "[DESCRIPTION]" --display-name "[DISPLAY_NAME]"
   ```

### Best Practices

- **Limit Permissions**: Assign only the necessary roles to service accounts to minimize security risks.
- **Rotate Keys**: Regularly rotate service account keys and avoid hardcoding keys in your application code.
- **Monitor Usage**: Use logging and monitoring to track the usage of service accounts and identify any unauthorized access.

### Summary
Service accounts are crucial for enabling secure and automated interactions with Google Cloud services, providing a way for applications to authenticate and access resources without human intervention. By following best practices, you can effectively manage service accounts to enhance your security posture.

If you have more questions or need additional information, feel free to ask!
