# Spark SQL to read data from file or External sources

## CTAS:  CREATE TABLE AS

CTAS is used to query self describing formats such as json, parquet and it can even be used to read data from other sources such as csv, tsv, text, etc. But it will be less usefull as schema can not be provided using CTAS and neither there is any way to use any options.

    

        SELECT * FROM json.`folder\path_to_json.json`

    

