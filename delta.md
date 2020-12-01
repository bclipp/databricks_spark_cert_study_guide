1. Added layer to parquet based data.
2. OSS (with some extra when using Databricks, Bin packing and zorder, opt caching , flex serialzable, opt joins , opt UDF)
3. Data lake focused
4. adds support for ACID , so concurrency safe ect..
5. Batch and streaming support in spark
6. transaction log
7. supports schema evolution
8. Time travel , access ALL versions of the data.


Suggested ETL DELTA PROCESS

1st job read in the data an ingestion Delta table (Bronze)
2nd job use clean data , and update table. (Silver)
3rd create features, agg , summary ect.. (Gold)


events = spark.read.json("/databricks-datasets/structured-streaming/events/")
events.write.format("delta").save("/mnt/delta/events")
spark.sql("CREATE TABLE events USING DELTA LOCATION '/mnt/delta/events/'")
These operations create a new unmanaged table using the schema that was inferred from the JSON data.

convert to delta a parquet
SQL: CONVERT TO DELTA parquet.`/mnt/delta/events`

add partitioning:
events.write.partitionBy("date").format("delta").save("/mnt/delta/events")

Batch updates:
MERGE INTO events
USING updates
ON events.eventId = updates.eventId
WHEN MATCHED THEN
  UPDATE SET
    events.data = updates.data
WHEN NOT MATCHED
  THEN INSERT (date, eventId, data) VALUES (date, eventId, data)
  

Time travel:
to query an older version of a table, specify a version or timestamp in a SELECT statement. For example, to query version 0 from the history above, use:
SQL
Copy to clipboardCopy
SELECT * FROM events VERSION AS OF 0
or
SQL
dataframe from version
SELECT * FROM events TIMESTAMP AS OF '2019-01-29 00:37:58'
df1 = spark.read.format("delta").option("timestampAsOf", timestamp_string).load("/mnt/delta/events")
df2 = spark.read.format("delta").option("versionAsOf", version).load("/mnt/delta/events")

Optimize a table
Once you have performed multiple changes to a table, you might have a lot of small files. To improve the speed of read queries, you can use OPTIMIZE to collapse small files into larger ones:
SQL
OPTIMIZE delta.`/mnt/delta/events`
or
SQL
OPTIMIZE events

Z-order by columns
To improve read performance further, you can co-locate related information in the same set of files by Z-Ordering. This co-locality is automatically used by Delta Lake data-skipping algorithms to dramatically reduce the amount of data that needs to be read. To Z-Order data, you specify the columns to order on in the ZORDER BY clause. For example, to co-locate by eventType, run:
SQL
OPTIMIZE events
  ZORDER BY (eventType)


Clean up snapshots
Delta Lake provides snapshot isolation for reads, which means that it is safe to run OPTIMIZE even while other users or jobs are querying the table. Eventually however, you should clean up old snapshots. You can do this by running the VACUUM command:
SQL
VACUUM events
You control the age of the latest retained snapshot by using the RETAIN <N> HOURS option:
SQL
Copy to clipboardCopy
VACUUM events RETAIN 24 HOURS
