**Basic components of Architecture:**

Driver: Lives on Master Node, declares transformations and actions on RDD. In cluster mode doesn't process data. 

Executor: Lives on Worker nodes. performs the tasks on the RDD's in a Job.

slots: unit of parallelism (normally a core) the potential for a task, in cluster mode they exist on the worker nodes only.

rdd: Resiliant distributed dataset. The smallest building block. 

dataframe: RDD's + metadata

Job: contains stages, total amount of work sent to the cluster

stage: stage is a unit of work within one shuffle boundry (group), contains tasks

task: smallest unit of work for each executor
  
  

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
  
 
**Shuffling:**
  
* moving data from one executor to another, or syncing point. spark is a bulk sync proc engine
* wide transformation: requires information from other partitions, and requires a shuffle.
* Narrow transformation: a transforamation that doesn't need to shuffle, or the data can be done in parallel on the partitions without needed sharing data across partitions. 
* Shuffle write/read
* shuffle partition configuration : ```SET spark.sql.shuffle.partitions=10``` set in notebook or clluster config
  * 200 default: after wide shuffle the number of post partitions is set by default to 200

**partitions** 
  should not have 0 , too few or too mich data idea no skew should 

**UI:**

* example of caching: http://files.training.databricks.com/images/eLearning/ucdavis/inmemorysize.png


**Braodcast Joins:**

* small table is broadcast to all executors: saves the need to shuffle.


**Plans:**

* Physical
* Logical

**Catalyst:**

**Dynamic partition pruning :**


**AQE:**


