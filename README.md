# Databricks Data Engineer Associate

### Databricks Architecture

Following digram shows the architecture of databricks.

![Databricks Storage Architecture](assets/databricks_storage_architecture.png)

### The control plane 
The control plane is set of backend services that is controlled by databricks inlined with the cloud provider that customer chooses (AWS, Azure or GCP). 
1. Workspace configuration 
2. Web application
3. Repo/Notebook
4. Jobs
5. Cluster Management
Are Stored in control plane and encrypted at rest.

### The Data Plane
Data Plane where are the data is stored. It hosts compute aka clusters. connects to backing dbfs and can be connected to external storage such as s3, sql etc. 


1. Cluster:
    1. is a set of computation resources to run notebook or job or instrucations.
    2. lives in data plan but managed by control plane. 
    3. have driver node and one or more executer node.
    4. Also have option to create single node cluster for smaller needs.
    5. Workloads are destributed accross executors by the driver

    ![The Cluster](assets/cluster.png)

    Datebricks makes a distinction between job and all puprose cluster

    1.  All Purpose Cluster
        -   Analyze data colabarativly using this.
        -   Can be created using Workspace or API.
        -   Configuration information reatiend for upto **70 clusters** or **30 Days**

    2.  Job Cluster
        -   Run Automated jobs.
        -   Databricks job scheduler creates job cluster while running job.
        -   Configuration information retained upto 30 most resently terminted clusters. (Can be retained after this but administrator must pin the cluster).
        -   Can not be restarted


2. 




### 1. [Delta Lake](DeltaLake\README.md)
### 2. [Reading External Data](ReadingExternalData/README.md)
### 3. [Reading External Data Sources](ReadingExternalData/README.md)
### 4. [Auto Loader vs Copy into](Auto%20Loader%20Vs%20Copy%20Into/Readme.md)


##### End to end data load and fault taularance

##### Identifying the arrival of new files



### SQL Endpoints

### Maximum bond vs vm size vs serverless

### check points vs write ahead logging vs idempotent sinks