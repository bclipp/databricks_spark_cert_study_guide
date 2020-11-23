**Basic components of Architecture:**

Driver

Exectuore

slots: unit of parallelism (normally a core) the potential for a task.

rdd

dataframe: RDD's + metadata

**Caching:**

* In memory and/or on Disk

* can be set for lazy cache

* can be serialized or deseralized, handled for you. Ser is smaller but slower.

Dataframes: 

Tables

 Tungsten Optimizer:



**Partitioning:**

Partition: a portion of a dataset, each partition has the potential to be distibuted.

Ways to partition data: 
  A. Larger size, more partitions
  B. Partitioning on a column,Ie days of the week.
  C. Configuration of the cluster

**UI:**

* example of caching: http://files.training.databricks.com/images/eLearning/ucdavis/inmemorysize.png


Braodcast Joins:


Plans:


Catalyst:


AQE:


