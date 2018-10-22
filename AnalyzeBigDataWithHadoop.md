## Create an Amazon S3 bucket
- In the <strong>AWS Management Console</strong>, on the Service menu, click <strong>S3</strong>.
![avatar](/Image/lab11.png)
- Click <strong>Create bucket</strong>
![avatar](/Image/lab12.png)
- For <strong>Bucket name</strong>, enter <strong>hadoop-</strong> followed by a random number.
- Click <strong>Create</strong>

## Launch an Amazon EMR cluster
- On the <strong>Service</strong> menu, click<strong>emr</strong>
- Click <strong>Create cluster</strong>.
- In the General Conifiguration section, configure the following:
> - Cluster name: My cluster
> - Click the hadoop-bucket that I created.
> - Click <strong>Select</strong>.
- In the <strong>Hardware configuration</strong> section,configure:
> - <strong>Instance type</strong>: m4.large
> - Number of instances: 2
> ![avatar](/Image/lab13.png)
- In the <strong> Security and access</strong> section, configure:
> - <strong>EC2 key pair</strong>: Proceed without an EC2 key pair
> - <strong>Permissions</strong>: Custom
> - <strong>EMR role</strong>: EMR_DefaultRole
> - <strong>EC2 instance profile</strong>: EMR_EC2_DefaultRole
> ![avatar](/Image/lab14.png)
- Click <strong>Create cluster</strong> to lauch your EMR cluster.
![avatar](/Image/lab15.png)

## Process Your Sample Dat by Running a Hive Script
- Wait until cluster is showing a status of Waiting
- Click the <strong>Step</strong> tab.
- Click <strong>Add step</strong>.
![avatar](/Image/lab16.png)
- In the <strong>Add step</strong> dialog, configure the following settings:
> - <strong>Step type</strong>: Hive program
> - <strong>Name</strong>: Process logs
> - <strong>Script S3 location</strong>: s3://us-west-2.elasticmapreduce.samples/cloudfront/code/Hive_CloudFront.q
> - <strong>Input S3 location</strong>: s3://us-west-2.elasticmapreduce.samples
> - <strong>Output S3 location</strong>: s3://hadoop-1995/
> - <strong>Arguments</strong>: -hiveconf hive.support.sql11.reserved.keywords=false
> - ![avatar](/Image/lab17.png)
