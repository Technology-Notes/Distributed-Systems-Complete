##Data Storage

### Intro to S3

This is similar to what was done in cloud web section.
Which helped learn following things
1.  Create a S3 bucket
2.  Add an S3 object in the S3 bucket
3.  Manage access permission of the object
4.  Create a bucket Policy
5.  Use bucket versioning

### Intro to Amazon Redshift
> It is a data warehouse used for analyzing and reporting data of petascale category.

> It should be used when source of data is numerous

> group of computer nodes are called clusters.

>> cluster properties

>>> each cluster has one or more database that runs on redshift engine

> Use SQL client to query data inside redshift:

> Here I used PGweb to load data into tables from client as well as by connecting Amazon S3.

**Redshift pros**:

> MPP - Masive parallel processing makes everything very fast

> columnar storage- reduce i/o operation on disk
way ahead than Bigquery, snowflake

https://hevodata.com/blog/amazon-redshift-pros-and-cons/

## Big data Analytics:

### Aws machine learning overview

>Three layers in machine learning stack:

1. Framework and interfaces:

> Deep learning AMI e.g. TensorFlow, pytorch, chainer are available ou there to anyone who is comfortable at building and training their own machine learning models.

2. ML Platforms:

> Amazon sage maker(build, train, deploy) e.g. is useful to ease things by managing all the process envolved in machine learning process i.e. labelling, training using appropriate algorithm, everything until making predictions.

3. Application Services:

> For developers who want use machine learning services by making API calls not concerning about the machine learning model design.

> Thse services includes voice, speech, text, vision recognition and many more.

### Analyze Bigdata with Hadoop

> Uses EMR manages every node in cluster by adding task specific softwares depending whether the nodes in the cluster is master, task, or a core.

**Controlling EMR to specify work**

> creating clusters that may be required to terminante soon after they are done with processing.

> creating long running cluster that may use EMR console, API.

> creating cluster to connect different types of node that uses SSH and interfaces to interact with different services as described.

**processing data**

> While cluster are launched, we need to mention the frameworks and softwares that would be required for data processing needs.

> three ways of processing data in amazon EMR cluster:
1. submitting jobs
2. querying directly
3. or, running steps 

here each step is a unit of work that contains instruction to manipulate data for processing by software’s installed on the cluster.

**USE CASE:**

> To run heavy distributed frameworks kike Apache Hive,Spark..

> To transform and transfer large amount of data from/into S3 and other data store services in AWS.

## Machine learning models

Amazon ML help data scientists to focus on the efficiency of their ML models rather thn worrying about resources required to trin a model.

Amazon Machine Learning (Amazon ML) can solve business problems by finding and learning the patterns in your historical data and using the patterns to generate predictions. To get started, you provide Amazon ML with your data.

> **What is a datasource?**
A datasource is an Amazon ML object that contains information about your input data, including its location, attribute names and types, and descriptive statistics for each attribute. Note that a data source does not contain your input data, it only points to its location. Operations such as ML model training and evaluation use the datasource ID to locate and access their input data.

> **Garbage in, Garbage out ?**
Amazon ML performs statistical analyses on your training and evaluation data sources to help you identify and fix any data anomalies. In order for Amazon ML to produce the best results, your data must be as clean and consistent as possible. For example, Amazon ML can't tell that NY, ny, New York, and new York mean the same thing, so the more consistent your data source, the more accurate your results.

>Amazon Machine Learning (Amazon ML) can solve business problems by finding and learning the patterns in your historical data and using the patterns to generate predictions. To get started, you provide Amazon ML with your data.

>**What is an evaluation?**

Amazon ML evaluates the ML model to gauge its performance before using it to generate predictions. If you create a binary classification ML model, Amazon ML provides Area Under a Curve (AUC) metrics and allows you to adjust the ML model's score threshold

> Generate predictions
In Amazon ML, there are two ways to generate predictions: enabling the ML model for real-time predictions or using batch predictions. You can use either approach, depending on your application's requirements.

> Configuring model, data and identifiers (i.e. target variable.)
We need to specify input data file and its location and what schema would it take. And, what is our target e.g. Here it is rating which is Multiclass Classification.

> Creating model by using the configuration(datasource)

> Here, In AWS we can see that the ML model is evaluated automatically, and AWS also creates confusion matrix for us for visualization of the classification that we need to do.
*It is important to split data into train/test ratio that can be 80/20 or 70/30(e.g. here which is default setting in AWS). Since, the model would give 100% accuracy on evaluation if we train and evaluate the model on same figures. *
>As we can see that the F1 score has gradually increases, finally reaching to 0.8 so we can say that our model is good.

**Evaluating our model**
> Batch vs Real time prediction
batch prediction is used to predict group of prediction using multiple data sets and real time involves interactivity where focus is only one prediction at a time.

> Using real time prediction to evaluate our model

> Results of ML model for a male who is under 20 and have to spend more than 50 bucks on continental food.

### Build a Machine Learning Model

>use uci bank repository for data source
>create model
>evaluating using real time setting threshold to restrict target area 
>using batch.csv and evaluating batch results

### Amazon Sage maker
> Scalable platform to host, train, evaluate and decide end points for a ML model.

Three basic hosting is generally used which are:
> train using off the shelf algorithm e.g. XGBoost Algorithm

>> can be single instance or distributed

> train with sframeworks in sage maker (MXnet/Tensorflow) with your own training code

> hosting your own pretrained model in sage maker and then use it (requires conversion through sagemaker standards)

> In advanced cases when a user has own algorithm, custom set of libraries. The user can bring in custom algorithm i.e. by setting up a docker image and registering it with the sage maker.

**it's advisible to use custom containers incase the code is complex and requires better synching with ML libraries even though sagemaker would provide those frameworks**

> The custom container needs to adhere to the requirements of the sagemaker in order to synch with container at every point. 

> After training we can use persistent prediction for single prediction or batch prediction for multiple prediction.

### practical
> We create S3 buckets so to have an entry point in order to fetch data an also, endppoints where er can store results at any stage we want through the ML modelling process.
> Here, in this practical we picked MNSIT datasets of images of handwritten, single digit numbers. And, we use the K-means algorithm that is provided by the sage maker itself.
> A preconfigured t2 instance that gives us enough resources to deploy our code, creating sagemaker notebook instance, here, we use jupyter notebook to execute our script.

> We create a training job-- We specify registary path of the traing code, specify quality of the model. And define where the training data and saved result should be stored in S3.

> Deploying our model involves three processes:

>> Creation of model-- *providing S3 location to use necessary model artifacts and the registery path of the image* 

>> Creation of endpoint configuration-- *to identify how many ML compute instances would be required to launch our model*

>> Creation of endpoint-- *after deploying, we get an endpoint with which applications can interact to get the inference about our model*

> Through batch transform we can get inferences from our model by setting up S3 bucket paths.

> Now we have deployed our model successfully which can be used to get inference. So, we will use sample data to validate our model.

## Bring it all together:

### Build a Serverless Real-Time Data Processing App

#Use points:
Serverless applications don’t require you to provision, scale, and manage any servers. You can build them for nearly any type of application or backend service, and everything required to run and scale your application with high availability is handled for you.

#Where to use this app?
Serverless architectures can be used for many types of applications. For example, you can process transaction orders, analyze click streams, clean data, generate metrics, filter logs, analyze social media, or perform IoT device data telemetry and metering.

#anticipated learning
In this project, you’ll learn how to build a serverless app to process real-time data streams. You’ll build infrastructure for a fictional ride-sharing company. In this case, you will enable operations personnel at a fictional Wild Rydes headquarters to monitor the health and status of their unicorn fleet. Each unicorn is equipped with a sensor that reports its location and vital signs.

#learning outcomes from four different modules

1. Build a data stream
    Create a stream in Kinesis and write to and read from the stream to track
    Wild Rydes unicorns on the live map. In this module you'll also create an
    Amazon Cognito identity pool to grant live map access to your stream.
> This portion involves the usage of Amazon kinesis stream, a producer and consumer.

> **Role of these services**

>> *Producer* is a sensor attached to the unicorn which is taking passengers on the ride. The passenger transmits data at intervals of time i.e. distance covered, current location and more to the operation team to keep the track. 

>> *Amazon Kinesis stream* stores the data sent by the *producer* and provides interface to the *consumer* to analyze and process the data.

> Kinesis stream make use of shard which is a unit of throughput capacity. Each shard ingests up to 1MB/sec and 1000 records/sec and emits up to 2MB/sec and the number of shards can be modified as per requirement once we have setup the kinesis.

> Use ./producer to produce messages into the stream and ./consumer to read messages from the stream created.

1. **Kinesis Stream**
*Now that the stream is being produced and read, we need to grant user access to read the Kinesis stream through the AWS Cognito services by creating an Identity Pool and referencing our Kinesis stream created. Once the AWS Cognito Identity Pool is created, we need to create an IAM Role in Kinesis service by creating a policy that gives read and list permissions to the kinesis stream created. 
Now that we have stream which is generating data and access have been given to read the data, we have viewed the stream online via the Unicorn Dashboard by linking it with the Coginto Identity Pool ID. Once done, we will be able to see the Unicorn on the map originating from New York. 
We can add more Unicorns/streams by adding another producer stream through AWS Cloud9 environment. 
Thus we have successfully created the Amazon Kinesis stream and have visualized it through the fleets of unicorns.*

2. **Aggregate data**

> Create a data stream in Amazon Kinesis Service by naming it and keeping sharding minimum to 1 for testing and evaluation basis. 

> We need to read the messages form the stream. Make sure that in Amazon Cloud9 environment, consumer is reading senor data. We can produce multiple producer which will lead to multiple unicorns and rows being captured.

3. **Process streaming data**

> We use AWS Lambda to process data from the wildrydes Amazon Kinesis stream created earlier. 

> Amazon DynamoDB table with a String as Sort Key and another string as Partion Key. Make a note of the ARN end point of the DynamoDB table created.

> IAM Role so that Amazon Lambda can have read access to Amazon Kinesis created earlier and log into Amaozn Cloudwatch Logs.

> Thus, we have created a Lambda function that reads from the Kinesis stream of summary unicorn data and saves each row to DynamoDB.

4. **Store & query Data**

> For the Amazon Kinesis Data Firehose to archive the data in Amazon S3 bucket, we first need to create a Amazon S3 bucket

> T Kinesis Data Firehose delivery stream to deliver data from the Kinesis stream to an Amazon S3 bucket and using Athena, we ran queries against this data on S3.
