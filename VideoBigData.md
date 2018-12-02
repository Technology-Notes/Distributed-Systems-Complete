# Hadoop Intro

## Evolution of Big Data
- Before 2000 : <strong>Complex computation and Processor bound</strong>
- Year 2000 : <strong>Bigger computers, larger memory, and fster processors</strong>
- After 2000: <strong>The solution could no longer help</strong>
> 40,000 search queries on Google every second.<br>
> 300 hours of video uploaded to YouTube every minute.<br>
> 31.25 million messages sent and 2.77 milion videos viewed by Facebook users every minute.<br>
> By 2017, nearly 80% of photos will be taken on smartphones.<br>
> By 2020, at least a third of all dat will pass through Cloud.<br>
> By 2020, about 1.7 megabytes of new information for every human.<br>

## How Does a Distributed System Work?
- Using multiple computers to resolve problem.
- The Distributed System Problems:
> High changes of system faliture.<br>
> Limit on bandwith.<br>
> Hight programming complexity.<br>

## What is Hadoop?
>>Hadoop is a frame work that allows for distributed processing of large data sets across clusters of commodity computers using simple 
programming models.
### Hadoop Key Characteristics
- Economical
> Ordinary compputers can be used for data processing.
- Reliable 
> Stroes copies of the data on different machines and is resistant to hardware failure.
- Scalable
> Can follow both horizontal and vertical scaling.
- Flexible
> Can store as much of the decide to use it later.

### Hadoop Ecosystem
- HDFS
> - A storage layer for Haoop.
> - Suitable for the distributed storage and processing.
> - Hadoop provides a command line interface to interact with HDFS.
> - Streaming access to file system data.
> - Provides file permissions and authentication.
- HBase
> - Stores data in HDFS.
> - A NoSQL database or non-relational database.
> - Manly used when you need random, real-time, read/write access to your Big Daata.
> - Provides support to high volume of data and high throughup.
> - The table can have thousands of columns.
- Sqoop
> - Sqoop is a tool designed to transfer data between Hadoop and relational database serves.
> - It is used to import data from relational databased such as, Oracle and MySQL to HDFS and MySQL to HDFS and export data from HDFS to relational datbases.
- Flume
> - A distributed service for ingesting streaming data.
> - Ideally suited for event data from multiple systems.
- Spark 
> - An open-source cluster computing framework.
> - Supports Machine learning, Business intelligence, Streaming, and Batch processing.
> - Provides 100 times faster perfromance as compared to MapReduce.
> ### Apache Spark
>> - Spark Core and Resilient Distributed Datasets(RDDs).
>> - Spark SQL.
>> - Spark Streaming.
>> - Machine Learning Library(Mlib).
>> - GraphX.
- MapReduce
> - The original Hadoop processing engine which is primarily Java based.
> - Based on the map and reduce programming model.
> - An extensive and mature fault tolerance framework.
> - Commonly used.
- Pig
> - An open-source dataflow system.
> - COnverts pig script to Map-Reduce code.
> - An alternate to writing Map-Reduce code.
> - Best for ad-hoc queries like join and filter.
- Impala
> - High performance SQL engine which runs on Hadoop cluster.
> - Ideal for interactive analysis
> - Very low latency - measured in milliseconds.
> - Supports a dialect of SQL(Impala SQL).
- Hive
> - Similar to Impala.
> - Best for data processing and ETL.
> - Executed queries using MapReduce.
- Cloudera Search
> - One of Cloudera's near-real-time access products.
> - Enables non-technical users to search and explore data stored in or ingested into Hadoop and HBase.
> - A fully integrated data processing platform.
> - Users do not need SQL or programming skills to use Cloudera Search.
- Guzzi
- Hue
> - Hue is an open source Web interface for analyzing data with Hadoop.
> - It provdes SQL editors for Hive, Impala, MySQL, Oracle, PostgreSQL, Spark SQL, and SolrSQL.
## Big Data Processing
- Ingest : Oqoop, Flume
- Processing : HDFS, HBASE, MapReduce, SPARK
- Analyze : Hive, Impala, Pig
- Access : Hue, Cloudera Search



