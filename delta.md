1. Added layer to parquet based data.
2. OSS (with some extra when using Databricks, Bin packing and zorder, opt caching , flex serialzable, opt joins , opt UDF)
3. Data lake focused
4. adds support for ACID , so concurrency safe ect..
5. Batch and streaming support in spark
6. transaction log
7. supports schema evolution
8. Time travel , access ALL versions of the data.

dataframe.write.format("delta").save("...")


CREATE TABLE events USING DELT LOCATION '...'


Suggested ETL DELTA PROCESS

1st job read in the data an ingestion Delta table (Bronze)
2nd job use clean data , and update table. (Silver)
3rd create features, agg , summary ect.. (Gold)
