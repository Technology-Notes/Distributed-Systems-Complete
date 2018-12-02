# Distributed Systems Practice
Notes from learning about distributed systems in [GW CS 6421](https://gwdistsys18.github.io/) with [Prof. Wood](https://faculty.cs.gwu.edu/timwood/)

- Big  Data and Machine Learning
    - [x] Beginner Level
    - [x] Intermediate Level
    
- Docker and Containers
    - [x] Beginner Level
    - [ ] Intermediate Level

## Big Data and Machine Learning


### Hadoop

Hadoop is a framework that allows for distributed processing of large data sets across clusters of commodity computers using simple
programming models. Hadoop has an ecosystem that has evolved from three components, processing resource management and storage. Its ecosystem consists of
several components.

![Alt text](https://github.com/dongyh1995/dist-sys-practice/raw/master/Screenshots/hadoop.png)

- HDFS
    - A storage layer for Hadoop
    - Suitable for distributed storage and processing
    - Hadoop provides a command line interface to interact with HDFS
    - Streaming access to file system data
    - Provides file permissions and authentication
- HBASE
    - Stores data in HDFS
    - A NoSQL database or non-relational database
    - Provides support to high volume data and high throughput
- Sqoop
    - Designed to transfer data between HDFS and relational database servers
- Hadoop MapReduce
    - Based on map and reduce programming model
    - An extensive and fault tolerance framework
- Pig
    - An open-source dataflow system
    - Converts pig scripts to Map-Reduce code
- ClouderaSearch
    - A fully integrated data processing platform
    - One of Cloudera's near-real-time access products
- Oozie
    - A workflow or coordination system used to manage the Hadoop jobs

Components of the Hadoop ecosystem work together to process Big Data.

![Alt text](https://github.com/dongyh1995/dist-sys-practice/raw/master/Screenshots/workflow.png)

### Amazon Machine Learning

Amazon Machine Learning (Amazon ML) is a robust, cloud-based service that makes it easy for developers of all skill levels to use machine learning technology. 
With Amazon ML, you can build and train predictive models and host your applications in a scalable cloud solution.

In Amazon ML, dataset is actually stored in S3. In order to avoid changing or moving data in S3, we need to define
 a datasource that contains the data location of out input data. Amazon ML uses the datasource for operations like ML model
  training and evaluation.

Amazon provides a great user interface to evaluate results. It also interprets the [AUC metric](https://docs.aws.amazon.com/machine-learning/latest/dg/binary-model-insights.html#measuring-ml-model-accuracy) to tell you if the quality of the ML model is adequate for most machine
learning applications. You can change threshold to make model meet some specific requirement.

![Alt text](https://github.com/dongyh1995/dist-sys-practice/raw/master/Screenshots/ML_Evaluation.png)

### Projects: Bring it all together

- Build a Serverless Real-Time Data Processing App
    - Build a data stream. Create a stream in Kinesis and write to and read from the stream.
    - Aggregate data. Build a Kinesis Data Analytics application to read from the stream and aggregate metrics using existing data.
    - Process streaming data. Transfer aggregrated data from application to DynamoDB database.
    - Store & Query data. Use Kinesis Data Firehose to flush the raw sensor data to an S3 bucket for archival purposes. Using Athena, you'll run SQL queries against the raw data for ad-hoc analyses.

- Compute Mean and Variance on massive data using Hadoop
    - Mapper. Write Mapper program to take input file and output number of instances, mean and variance values.
    - Reducer. Take output of several Mappers as input and compute global mean and variance values.
    - Process data. Use EMR services of AWS to create a job flow using our own Mapper and Reducer.

### Summary

Hadoop can help us process massive data across clusters of commodity computers very easily. Its core component MapReduce uses Map step to divide whole work into
several pieces and Reduce step to combine different results as final output. As for machine learning, in order to imporve efficiency, we
need to find the most time-consuming part and use that as our Mapper. Then the hardest work will be distributed to several clusters and time efficiency
will get increased.


## Docker and Containers

### Docker
- Docker is a software that can package code and its dependencies together so the application can run on different
environments very easily.
- Docker can run container images inside of it. Each container image is isolated from each other so it is very helpful for security and testing.
- Docker Store is a registry of container images. It stores all available container images in it. Users can pull image they need and runs it in their own container.
- Compared to VM, each VM has its own memory and OS while containers all share the same kernal with each other. Container
only focus on the OS and application, not so much about the hardware. So it is much faster to start up a container than VM.
### Container
- Runtime definition. Container is like a sandbox for process. It provides isolation between different containers  running on one machine. Container process and container's lifecycle are tightly coupled.
- Container image. Image is a binary representation. Containr image is layered in a tree strcuture, which starts from most basic(scratch/OS) to most specific(application). Container is like a template that allows you to create specific container.
- Docker file. Docker file is used to create image file. Each line in docker file represents a layer in image tree. Use this way to create container image, then use this image to instantiate specific container.
- Combine these together. When you type the command 'docker container run my_app', first it pulls the container image you need from the registry to your image cache running inside your docker host. Then it configures networking and storage you need to run containers. Networking allows different containers communicate with each other while storage is used to store persistant states. After setting up the process namespace and cgroups, then your container is finally running inside docker host.
