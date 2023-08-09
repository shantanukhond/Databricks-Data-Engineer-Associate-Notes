# Spark SQL to read data from file or External sources

## CTAS:  CREATE TABLE AS

CTAS is used to query self describing formats such as json, parquet and it can even be used to read data from other sources such as csv, tsv, text, etc. But it will be less usefull as schema can not be provided using CTAS and neither there is any way to use any options.

    

        SELECT * FROM json.`folder\path_to_json.json`

    
json can be replaced with the sources such as csv, parquet, tsv, etc. 

- Do not support Manual Schema Declaration, Schema is infered. 
- Do not support additional file options.
- Creates Actual table and data is moved.


## Create Table statement with using keyword


- Table created using this is non-delta table.
- performance and features like performance, latest data, timetravel is not available
- No data movemnent actully happens.
- Supports options.
- files are kept in orignal format.


Example of create table using CSV is as below:

        CREATE TABLE table_name
        (col1,col2,col3....,coln)
        USING CSV
        OPTIONS (header="true", delimiter=";")
        LOCATION path

Example of create table using JDBC:
        
        CREATE TABLE table_name
        (col1,col2,col3....,coln)
        USING JDBC
        OPTIONS (url=jdbc:sqlite://hostname:port,
                dbtable="database.table",
                user="username",
                password="pwd"
                )

        
## Temporary view to point to external data:

Using Temporary view to point external data and it can be loaded into table.

Format for create temprory view and then data load is as shown below:

        CREATE TEMP VIEW temp_view_name (col1,col2,col3....,coln)
        USING data_source
        OPTIONS (key1=val1,key2=val3,....,keyn=valn)

and then the data from temp table can be loaded into delta table using CTAS as shown below:

        CREATE TABLE table_name
        AS select * from temp_view_name





    

