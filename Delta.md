https://delta.io/

https://docs.databricks.com/delta/quick-start.html

Basic Notes:

ACID Transactions
Scalable Metadata Handling
Time Travel (data versioning)
Open Format
Unified Batch and Streaming Source and Sink
Schema Enforcement

Delta Architecture multitable:
A. Bronze
  * Raw Data little to no processing
  * Data will be stored in delta format
B. Silver
  * refined view
  * agg tables for BI
  * feature tables for data scientsits
  * schema enforcement, dedup
C. Gold
  * data is queryable and read for insignts
  * all cleaning has been done

Delta Architecture single table SSOT:
A. Bronze step
  * Raw Data little to no processing
  * Data will be stored in delta format
B. Silver step
  * filtered
  * cleaned 
C. Gold step
  * BI Agg

Basic Commands:

Convert the files to Delta files:
from delta.tables import DeltaTable

parquet_table = f"parquet.`{health_tracker}processed`"
partitioning_scheme = "p_device_id int"

DeltaTable.convertToDelta(spark, parquet_table, partitioning_scheme)


