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
- Create an Amazon S3 Bucket
![avatar](/Image/lab41.png)
- Create an Amazon EC2 Key Pair
![avatar](/Image/lab42.png)
- Open the Amazon EMR console and Choose <strong>Create cluster</strong>
![avatar](/Image/lab43.png)
- On the <strong>Create Cluster - Quick Options</strong> page, accept the default values.
![avatar](/Image/lab44.png)
![avatar](/Image/lab45.png)
- Choose <strong>Create</strong>
![avatar](/Image/lab46.png)
- Open the Amazon EMR console
- Choose <strong>Clusters</strong>
- Choose the <strong>Name</strong> of the cluster.
![avatar](/Image/lab47.png)
- User <strong>Security and access</strong> choose the <strong>Security groups for Master</strong> link.
- Choose <strong>ElasticMapReduce-master</strong> from the list.
- Choose <strong>Inbound, Edit</strong> to add a new inbound rule.
- Scroll down through the listing of default rultes and choose <strong>Add Rule</strong> at the bottom of the list.
- For <strong>Type</strong>, select <strong>SSH</strong>. For source, select <strong>My IP</strong
- Choose <strong>Save</strong>
- Click <strong>Step</strong>.
![avatar](/Image/lab49.png)
- Choose <strong>Add</strong>. The step apears in the console with as status of Pending.
![avatar](/Image/lab48.png)
- Open the Amazon S3 console.
- Choose the <strong>Bucket name</strong> and then the folder that set up earlier.
- Choose the file, and the choose <strong>Download</strong> to save it locally.
- Open the file.
![avatar](/Image/lab411.png)



