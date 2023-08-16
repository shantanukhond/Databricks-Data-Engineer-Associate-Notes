# Databricks Data Engineer Associate

### Databricks Architecture

Following diagram shows the architecture of databricks.

![Databricks Storage Architecture](assets/databricks_storage_architecture.png)

### The control plane 
The control plane is set of backend services that is controlled by databricks inline with the cloud provider that customer chooses (AWS, Azure or GCP). 
1. Workspace configuration 
2. Web application
3. Repo/Notebook
4. Jobs
5. Cluster Management
Are Stored in control plane and encrypted at rest.

### The Data Plane
Data Plane where are the data is stored. It hosts compute aka clusters. connects to backing dbfs and can be connected to external storage such as s3, sql etc. 


1. Cluster:
    1. is a set of computation resources to run notebook or job or instruction.
    2. lives in data plan but managed by control plane. 
    3. have driver node and one or more executer node.
    4. Also have option to create single node cluster for smaller needs.
    5. Workloads are distributed across executors by the driver

    ![The Cluster](assets/cluster.png)

    Databricks makes a distinction between job and all-purpose cluster

    1.  All Purpose Cluster
        -   Analyse data collaboratively using this.
        -   Can be created using Workspace or API.
        -   Configuration information retained for up to **70 clusters** or **30 Days**

    2.  Job Cluster
        -   Run Automated jobs.
        -   Databricks job scheduler creates job cluster while running job.
        -   Configuration information retained up to 30 most recently terminated clusters. (Can be retained after this but administrator must pin the cluster).
        -   Can not be restarted


2. Databricks Repos
    Notebooks have basic revision control (No centralized history maintained, History can be manipulated or deleted).
    -   Review change history but only basic ops are supported.
    -   Can not merge changes, create branches or tags. 

    Databricks support following git provider
    1.  Azure devops
    2.  bitbucket
    3.  github
    4.  gitlab

    ![Git Best Practices](assets/git-best-practices.png)


Data Objects in Lakehouse
1.  MetaStore -> Stores Metadata 
2.  CatLog-> Group of database
3.  Database/Schema -> Grouping of objects
    -   Table    -  Collection of row and column stored as data file
    -   View     -  Collection of queries to point one or more table or view
    -   Function -  Saved logic which returns scaler value or set of rows

    Tables can be classified as
    1.  Managed Tables.
        Based on files stored in managed storage. 
        metadata is stored in Metastore.
        Deletes table and underlying data when deleted.

    2.  External Table 
        Datafiles are stored in external cloud storage outside managed storage location.
        Only table metadata is managed.
        when dropped only metadata is deleted keeping the data as it is.

### Complex Transformation

1.  Json:
    -   **":"** Syntax can be used to query child or sub items in json. 
    -   **schema_of_json** can be used to retrieve schema of the json.
    -   **from_json** parses a column into json to struct type using json schema.
    -     


2.  Struct types:
    -   **"."** Syntax can be used to query child items in Struct types.
    -   **".*"** can be used to pull subfield of json into own columns.

3. Arrays
    -   **explode** separates items into separate new rows. 
    -   **size** returns count of items in array.
    -   **flattens** combine multiple arrays into one.
    -   **array_distinct** removes duplicate values from array.  

4.  Field
    -   **collect_set** collects unique value for the field.

5. Joins
    -   supports inner, outer, left, right, anti, cross, semi

6. Pivot
    -   Supports pivot using aggregate function for the values described in the column in the list provided.


### User Defined Function (UDFs)

   **SQL UDF**
    
   -   Must have usage and select permission on function 
   -   describe and describe extended can be used
   
   for sql udf example:

        
        CREATE FUNCTION to_hex(x INT COMMENT 'Any number between 0 - 255')
        RETURNS STRING
        COMMENT 'Converts a decimal to a hexadecimal'
        CONTAINS SQL DETERMINISTIC
        RETURN lpad(hex(least(greatest(0, x), 255)), 2, 0)

    
  **Python UDF**
    
   -   can be registered using spark.udf.register("udf_name",python_function_name)
   -   can also registered using python decorators i.e. @udf("")
   -   pandas udf are available. uses apache arrow. 




### 1. [Delta Lake](DeltaLake\README.md)
### 2. [Reading External Data](ReadingExternalData/README.md)
### 3. [Reading External Data Sources](ReadingExternalData/README.md)
### 4. [Auto Loader vs Copy into](Auto%20Loader%20Vs%20Copy%20Into/Readme.md)




## Anonymous Key Points

1.  What is the difference between Pivot_longer and pivot_wider?
    pivot_wider() is the opposite of pivot_longer() : it makes a dataset wider by increasing the number of columns and decreasing the number of rows. It's relatively rare to need pivot_wider() to make tidy data, but it's often useful for creating summary tables for presentation, or data in a format needed by other tools.

1.  What are magic commands?
    Magic commands in Databricks are special commands that start with a percentage sign (%) and allow you to execute code snippets in different languages or perform various actions within a notebook. For example, you can use magic commands to run SQL queries, switch the notebook context to Python, Scala, or R, display images or mathematical equations, or access the Databricks file system. Magic commands can make your notebook more interactive and versatile, as well as save you time and effort. 


    -   **%run** :  runs a Python file or a notebook.
    -   **%sh** :  executes shell commands on the cluster nodes.
    -   **%fs** :  allows you to interact with the Databricks file system.
    -   **%sql** :  allows you to run SQL queries.
    -   **%scala** :  switches the notebook context to Scala.
    -   **%python** :  switches the notebook context to Python.
    -   **%md** :  allows you to write markdown text.
    -   **%r** :  switches the notebook context to R.
    -   **%lsmagic** :  lists all the available magic commands.
    -   **%jobs** :  lists all the running jobs.
    -   **%config** :  allows you to set configuration options for the notebook.
    -   **%reload** :  reloads the contents of a module.
    -   **%pip** :  allows you to install Python packages.
    -   **%load** :  loads the contents of a file into a cell.
    -   **%matplotlib** :  sets up the matplotlib backend.
    -   **%who** :  lists all the variables in the current scope.
    -   **%env** :  allows you to set environment variables.
    [ref](https://medium.com/@shuklaprashant9264/databricks-magic-command-list-ebe0269934f6)



## To be added.....

### End to end data load and fault tolerance

### Identifying the arrival of new files

### SQL Endpoints

### Maximum bond vs vm size vs serverless

### check points vs write ahead logging vs idempotent sinks

