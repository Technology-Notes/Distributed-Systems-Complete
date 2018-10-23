# Amazon EMR
>>https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-gs.html

## What is Amazon EMR?
Amazon EMR is a managed cluster platform that simplifies running big data frameworks, such as Apache Hadoop and Apache Spark,
on AWS to process and analyze vast amounts of data. By using these frameworks and related open-source projects, such as Apache 
Hive and Apache Pig, you can process data for analytics purposes and business intelligence workloads. Additionally, you can use
Amazon EMR to transform and move large amounts of data into and out of other AWS data stores and databases, such as Amazon Simple
Storage Service (Amazon S3) and Amazon DynamoDB. 

## Cluster and Nodes

- <strong>Master node</strong>:A node that manages the cluster by running software components to coordinate the distribution of
data and tasks among other nodes for processing. The master node tracks the status of tasks and monitors the health of the
cluster. Every cluster has a master node, and it's possible to create a single-node cluster with only the master node.
- <strong>Core node</strong>: A node with software components that run tasks and store data in the Hadoop Distributed
File System (HDFS) on your cluster. Multi-node clusters have at least one core node.
- <strong>Task node</strong>: A node with software components that only runs tasks and does not store data in HDFS. 
Task nodes are optional.

## Analyzing Big Data with Amazon EMR
- C

