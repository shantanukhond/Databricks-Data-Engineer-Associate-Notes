# Auto Loader vs Copy Into

Auto Loader and COPY INTO are two methods of ingesting data into a Delta Lake table from a folder in a data lake. Both features are especially useful for data engineers, as they make it possible to ingest data directly from a data lake folder incrementally, in an idempotent way, without needing a distributed real-time streaming data system like Kafka.

COPY INTO is a SQL command that loads data from a folder location into a Delta Lake table. It can be used in Databricks SQL, notebooks, and Databricks Jobs.

Auto Loader incrementally and efficiently processes new data files as they arrive in cloud storage without additional setup.


- If you’re going to ingest files in the order of thousands, you can use COPY INTO. If you are expecting files in the order of millions or more over time, use Auto Loader.
- Auto Loader requires fewer total operations to discover files compared to COPY INTO and can split the processing into multiple batches, meaning that Auto Loader is less expensive and more efficient at scale.
- If your data schema is going to evolve frequently, Auto Loader provides better primitives around schema inference and evolution.

#### Key points
1. use auto loader with schema inferance and evolution is frequent.
2. use copy into when file are less or in thousands.
