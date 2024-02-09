# Lab 5

## Student information

* Full name: Owen Sugiarto
* E-mail: osugi001@ucr.edu
* UCR NetID: osugi001
* Student ID: 8632296300

## Answers

* Q1. Yes, it will use your cluster if the spark-submit command specifies a cluster manager (like YARN, Mesos, or Spark's standalone cluster manager) and if the input data is in HDFS, allowing Spark to distribute the work across multiple nodes in the cluster.

* Q2.yes the application ran on the cluster I started because it looks like there is one completed applications. In the spark web interface and there is one under the worker node under the finished executors.

* Q3. Using Spark master ‘local[*]’
Number of lines in the log file 30970

* Q4. Using Spark master ‘spark://class-225:7077’
Using Spark’s default log4j2 profile:  org/apache/spark/log4j2-defaults.properties
Number of lines in the log file 30970

* Q5.

24/02/08 21:28:32 INFO HadoopRDD: Input split: C:/Users/owens/CS167/workspace/osugi001_lab5/nasa_19950801.tsv:0+1169610

24/02/08 21:28:32 INFO HadoopRDD: Input split: C:/Users/owens/CS167/workspace/osugi001_lab5/nasa_19950801.tsv:1169610+1169610

* Q6. splits :  
24/02/08 21:29:42 INFO HadoopRDD: Input split: C:/Users/owens/CS167/workspace/osugi001_lab5/nasa_19950801.tsv:0+1169610

24/02/08 21:29:42 INFO HadoopRDD: Input split: C:/Users/owens/CS167/workspace/osugi001_lab5/nasa_19950801.tsv:1169610+1169610

24/02/08 21:30:11 INFO HadoopRDD: Input split: C:/Users/owens/CS167/workspace/osugi001_lab5/nasa_19950801.tsv:0+1169610

24/02/08 21:30:12 INFO HadoopRDD: Input split: C:/Users/owens/CS167/workspace/osugi001_lab5/nasa_19950801.tsv:1169610+1169610

* (Q7) Compare this number to the one you got earlier.
Q5 we get two input file splits while question 6 we get 4 input files.

* Q8.) I think the reason why we got this number because the increase in the number of input splits from Q5 to Q6 likely reflects a change in the parallelism level or the execution of multiple actions that caused Spark to partition the input data differently or log the partitioning multiple times.

* Q9.)To make the file is read only once, cache the data in memory after loading it by adding logFile.persist(StorageLevel.MEMORY_ONLY()); to your code. This way, subsequent operations use the cached data instead of re-reading the file.

* Q10.)The program will likely have two stages because of the transformations and actions you've applied. The stages are divided as follows:

Stage involves reading the data and mapping each line to a pair of using mapToPair. This is a transformation step.

Stage 2, involves the countByKey action, which triggers the shuffle of data across the cluster to count all keys (response codes) together. Shuffling data requires Spark to write intermediate results to disk, marking the end of the first stage and the beginning of the second stage.


* Q11.) program has two stages because the first part processes the data (turning lines into pairs), and the second part counts these pairs across all data. Counting requires gathering information from across the cluster, which splits the job into two stages at this "shuffling" point where data gets rearranged.




