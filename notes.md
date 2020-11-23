**Basic components of Architecture:**

Driver

Exectuore

slots: unit of parallelism (normally a core) the potential for a task.

rdd

dataframe: RDD's + metadata

task

stage: stage is a unit of work within one shuffle boundry (group)

**Caching:**

* In memory and/or on Disk

* can be set for lazy cache: cache partitions as they are used.

* can be serialized or deseralized, handled for you. Ser is smaller but slower.

Dataframes: 

Tables

 **Tungsten Optimizer:**
* optimizes how data is stored on disk


**Partitioning:**

Partition: a portion of a dataset, each partition has the potential to be distibuted.

Ways to partition data: 
  A. Larger size, more partitions
  B. Partitioning on a column,Ie days of the week.
  C. Configuration of the cluster


Shuffling:

* moving data from one executor to another
* wide transformation: requires information from other partitions, and requires a shuffle.
* Narrow transformation: a transforamation that doesn't need to shuffle, or the data can be done in parallel on the partitions without needed sharing data across partitions. 
* Shuffle write:
* shuffle partition configuration : ```SET spark.sql.shuffle.partitions=10```
  * 200 default: after wide shuffle the number of post partitions is set by default to 200

**UI:**

* example of caching: http://files.training.databricks.com/images/eLearning/ucdavis/inmemorysize.png


Braodcast Joins:


Plans:


Catalyst:


AQE:


