# Distributed Systems Practice
Notes from learning about distributed systems in [GW CS 6421](https://gwdistsys18.github.io/) with [Prof. Wood](https://faculty.cs.gwu.edu/timwood/)

# Cloud Web Applications

## CLOUD BEGINNER
----------------
### AWS Tutorial: Launch a VM 
>** Following are the main processes done after entering the amazon EC2 console**

![launched instance](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/L1.PNG)
![pair key ](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/l2.PNG)
![connection through putty](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/l3.PNG)
---------------------------------
### Introduction to Amazon Simple Storage Service S3
new to S3? watch this [intro to S3](https://www.youtube.com/watch?v=77lMCiiMilo).
---------------------------------
>**Use cases** of S3
1. Frequently accessed data
2. S3 Standard-*Infrequent Access*
3. S3 One Zone-*Infrequent Access* for long-lived, but less frequently accessed data.
4. Amazon Glacier for *long-term archive*.

>**reliable**- use ssl and management policies

>**flexibility**- to use as much storage as required

#### Hands-On practice on [awseducate-qwiklabs](https://awseducate.qwiklabs.com/focuses/30?parent=catalog) 
>**create a bucket in Amazon S3**

>**Add an object to your bucket**

>**Manage access permissions on an object**

>**Create a bucket policy**
{
    "Version": "2012-10-17",
    "Id": "Policy1540400907130",
    "Statement": [
        {
            "Sid": "Stmt1540400902968",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObjectVersion",
            "Resource": "arn:aws:s3:::(mybucket223344)/*"
        }
    ]
}
so that each object inside the bucket can publicly shared.

>**Use bucket versioning**
Save multiple versions of a same object
"Action": "s3:GetObjectVersion" -- different versions of the same object can be accessed through this policy.

## CLOUD Intermediate

### Virtual Machines, Websites, and Databases:
(https://www.youtube.com/watch?v=GIdVRB5yNsk)describes virtualization and  why it needs more and more implimentation everyday.
>This video talks about the growing demand of distributed environment and the evolution of vartulization.
======================
### Install a Lamp Web Server on Amazon Linux2

** This tutorial guided me to install lamp i.e apache web server with PHP and MariaDB on amazon linux 2 instance.**

The main parts of the procedure are described below:

> ran linux instance

>establisihing connection through putty

>*ID instance*- i-093bd0ab14b25df00

>*public DNS name*-(ipv4) 54.202.153.202

>C:\Users\akshay\.ssh\mykeypair.pem(personal)

>ec2-user 

>Connect to your instance. 

>ensure that all of your software packages are up to date *sudo yum update -y*

>Install the lamp-mariadb10.2-php7.2 and php7.2 *sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2*

>install the Apache web server, MariaDB, and PHP software packages. *sudo yum install -y httpd mariadb-server*

>Start the Apache web server*Start the Apache web server*

>Use the systemctl command to configure the Apache web server to start at each system boot. *sudo systemctl enable httpd*

>*sudo systemctl is-enabled httpd* (**enable verification**)

>added inbound rules

>sudo usermod -a -G apache ec2-user- *Add your user (in this case, ec2-user) to the apache group. *

>exit

>verify membership *groups*

**USE CASES**
> to host static website
> Depoly dynamic PHP application that reads and writes information to database.

 
### On your own: Compare the performance, functionality, and price when serving web content from S3 versus an EC2 VM 

**S3 vs EC2**

>Only Static web content can be served through S3. S3 is a object based storage system.

>It is highly available and by defaults it is duplicated across availability zone.

>Also S3 storage is much cheaper than EBS- block storage. By serving the static contents from S3, one can save on IOPs of the EC2 as the request for S3 static links isnt served through EC2.

>Also it create a highly available environment, the static content which often are media files which consumes much higher storage need not be stored in all the EC2 instances

>Thus EC2 EBS storage requirement is reduced considerably

>Price wise S3 is 4-5 times less cheaper.

### Intro to DynamoDB

> **Amazon DynamoDB** is a fast and flexible NoSQL database service for all applications that need consistent,single-digit
 millisecond latency at any scale.
> It is fully managed database and supports both document and key-value data models.

Following things were learned in this tutorial:

> Create Amazon DynamoDB table:
1. Here, I crreated a table named music. The table make use of Primary key and Sort Key to uniquely identify each item in a Dynamo DB table.
2. After adding table name, primary key*e.g. artist which is string* with the usage of add sort key to finally create a table.

> Enter data into an Amazon DynamoDB table:
1. we can add unlimited data into dynamoDB where attribute(*has a field/value*) is the fundamental or smallest entity.
2. The entry of data is only dependent on primary/sort keys.
3. Using **items** tab we can create items and append required attributes.

> Modifying Existing data
1. Using **Psy**, we can change field values.

> Query an Amazon DynamoDB table:

1. Query can be done by using **query** or **scan**.
2. query is a faster option as it is based on priary eeys and is fully indexed.

> Delete an Amazon DynamoDB table:
1. Simply click Delete table to delete it.


## Deploy a Node.js Web App

> **GOALS**:
1. learn how to deploy a high-availability Node.js web app using AWS Elastic Beanstalk and Amazon DynamoDB.
2. Use Amazon Simple Notification Service (SNS) to configure push notifications for the app.
![M1](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/unh_vs_h.PNG)
![M2](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/ins.PNG)
![M3](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/Mon.PNG)
![M4](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/S3.PNG)


## Serverless and Edge Computing:

### Intro to AWS lambda

>![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/AWS_lambda.PNG)

## QwikLab: Intro to Amazon API Gateway - 35 min
*https://developer.spotify.com/documentation/web-api/*  was good example to understand RESTFUL API.


## Build a serverless web App

# Host a static website
	http://wildrydes-akshay-gupta.s3-website-us-west-2.amazonaws.com(s3 stattic host end point)

	![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/app_arch.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/static_web_hosting_S3.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/static_bp.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/2.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/3.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/webapp_awslambda.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/lambdalog_webapp.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/authentication.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/APcognito_verification.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/api_method.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/lambda_requestunicorn.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/method_requestcard.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/authorized.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/unicorn%20arrived.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/cognito_usergroup.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/unicorn_dynamo.PNG)

# Manage users

Pool Id us-west-2_QwfIuQsvA
607gktk0nr9leupbrn5c6nhsiu

# Serverless Service Backend
Amazon Resource Name (ARN)
	arn:aws:dynamodb:us-west-2:566965401352:table/Rides
## Deploy Rest API

auth token: eyJraWQiOiJuTnA4NUVcL2tnS1Q3VmkxZ0kyRW5xVjlaZEdpTEFSYW5KenV0N01nNzd0ST0iLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiIxMGRkZWM3Ni0xOWU3LTQ1YjctYmNjNC1jOTlmYmZjMjA3ZjYiLCJhdWQiOiI2MDdna3RrMG5yOWxldXBicm41YzZuaHNpdSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJldmVudF9pZCI6ImY3ZmQxMDE2LWRiMDAtMTFlOC1iNWIyLTc5YzdiNTZkMjQ1ZiIsInRva2VuX3VzZSI6ImlkIiwiYXV0aF90aW1lIjoxNTQwNzY1Nzg0LCJpc3MiOiJodHRwczpcL1wvY29nbml0by1pZHAudXMtd2VzdC0yLmFtYXpvbmF3cy5jb21cL3VzLXdlc3QtMl9Rd2ZJdVFzdkEiLCJjb2duaXRvOnVzZXJuYW1lIjoiYWtzaGF5Lmd1cHRhMDcxMkBnbWFpbC5jb20iLCJleHAiOjE1NDA3NjkzODQsImlhdCI6MTU0MDc2NTc4NCwiZW1haWwiOiJha3NoYXkuZ3VwdGEwNzEyQGdtYWlsLmNvbSJ9.Wf8mpVtwtbODlFQA8tQyhGC0yz6I-z4xD8yFmrfSggs30s5mJL8YiiRxWg03ZuOmsjBco5XMMduIqu0va7T4FpTYSrCAq9m1uAoCrOfUbuBD3MQFFGuJ2geJgi8tMoEmWtaLz32LBHBNERMq3-6MmMqkT3tRqLyb7GI0_FyNIvHvQok_gZUWquR98Ny9FKn4pkYf7ApbZgw9jqWlIHDZAT8EKVQYslTk32dkuvYgugO1lj-aHWDY5zl7Q0D-TLPHOLSI2CarNi7e4VhwcliiXktYCmZnI_qieCBFOcq8HndBVpgSkPXOkAK4AUvujBdUK3SekGZcXMyDjgYDyGMfdA

>arn:aws:lambda:us-west-2:566965401352:function:RequestUnicorn

>https://2x01cqllu1.execute-api.us-west-2.amazonaws.com/prod(deployed api)

# Build a Modern Web Application in python

**Goal:**
: *To create a website that enables visitors to a adopt a fantasy creature.*(www.mythicalmysfits.com)

>*host the weapp on a front-end web server*

>*connnect to backend database*

>*user authentication*

>*collect and analyze user behavior*

>*gathers insight for fututre analysis*

## Application architecture

![Application Architecture](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/P1.PNG)

## Modules

>Create Static website-*building static website i.e storing static objects in S3 *

>Build Dynamic Website-*hosting application logic on a web server-using API backend microservice deployed(as a container)--aws fargate*

>Store Mysfit Data-*manage via NoSQl databse i.e. Amazon DynamoDB*

>Add User Registration-*API Gateway/Amazon Cognito*

>Capture User Clicks-*capture user analysi using AWS lambda/kenesis Firehose*

>create the required infrastructure components, which includes a fully managed CI/CD stack utilizing AWS CodeCommit, CodeBuild, and CodePipeline. Finally, you will complete the development tasks required all within your own browser using the cloud-based IDE, AWS Cloud9.


>Modue1-(static hosting)
![architecture](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/F2.1.PNG)

>>Cloud 9 created
mythical-mysfits-bucket01(S3 bucket creaated)
aws s3 mb s3://mythical-mysfits-bucket-02

>>basic static site created
---------------
>module 2(host your app on web server)
![]()
*creating microservice hosted with aws fargatevto integrate website with backend*
**Fargate** is reliable for long running process for web/mobile and PaaS platform

>>Module 2a *Setup Core Infrastructure*

>>>Deploy Cloud Formation Templates

    An Amazon VPC - a network environment that contains four subnets (two public and two private) in the 10.0.0.0/16 private IP space, as well as all the needed Route Table configurations.
    Two NAT Gateways (one for each public subnet) - allows the containers we will eventually deploy into our private subnets to communicate out to the Internet to download necessary packages, etc.
    A DynamoDB Endpoint - our microservice backend will eventually integrate with Amazon DynamoDB for persistence (as part of module 3).
    A Security Group - Allows your Docker containers to receive traffic on port 8080 from the Internet through the Network Load Balancer.
    IAM Roles - Identity and Access Management Roles are created. These will be used throughout the workshop to give AWS services or resources you create access to other AWS services like DynamoDB, S3, and more.
	cloud finished provisioning all of the core networking and security resources as described above.


	>>Module 2B: Deploy A Service With AWS Fargate
![]()
*creating Docker image that will contain all of the code and configuration required to run mythical mysts backend as a microservice API created with Flask*
--creating Docker image using cloud 9 and pushing it in Elastic Container Registery(to make it available when we create our service using Fargate).
cd ~/environment/aws-modern-application-workshop/module-2/app *create docker image *
getting
{
    "Account": "566965401352", 
    "UserId": "566965401352", 
    "Arn": "arn:aws:iam::566965401352:root"
}
after bulding docker image 
we get(image tags that are required later) 
Successfully built 18bcefda98c8
Successfully tagged 566965401352.dkr.ecr.us-west-2.amazonaws.com/mythicalmysfits/service:latest

>>>test the service locally

>>>Push the Docker Image to Amazon ECR 

>>>Replace the API Endpoint

>>Module 2C: Automate Deployments using AWS Code Services*will automatically deliver all of the code changes that you make to your code base to the service you created during the last module.*
![architecture](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/F2.PNG)

>>>creating and testing  CI/CD Pipeline
---------------

>Module 3: Store Mysfit Information*will create a table in Amazon DynamoDB, a managed and scalable NoSQL database service on AWS with super fast performance*
![architecture](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/f3.PNG)

>>adding a No SQ Databasee To Mythical Mysfits

>>commiting real code change

>>updating website content in S3
----------------

>Module 4: Setup User Registration*To enable registration and authentication of website users, we will create a User Pool in AWS Cognito - a fully managed user identity management service. *
![architecture](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/F4.PNG)
**To make sure that only registered users are authorized to like or adopt mysfits on the website, we will deploy an REST API with Amazon API Gateway to sit in front of our NLB. Amazon API Gateway is also a managed service, and provides commonly required REST API capabilities out of the box like SSL termination, request authorization, throttling, API stages and versioning, and much more.**

>>added user poool for website Users

>>added a new rest api with amazon API gateway

>>Updated the Mythical Mysfits Website
-------------------

>Module 5: Capture User Behavior *in order to make use of the site it is a ggod practice to analyze user response*
![architecture](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/F5.PNG)
**following instructions are required to implement it**

1. create streaming service code
2. update the lambda function package and code
3. create the streaming Service Stack
4. sending mysfit profile clicks to the created microervice

**Conclusion**: Using AWS CLI, A serverless system with multiple modules was managed.

============================================

# Big Data and Machine Learning

## Beginner
---------------------------------------------
### Intro to Hadoop
![traditional vs Hadoop](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/hadoop1.PNG)

>Hadoop is the solution to complexities arised due to use of distributed systems.

>Four Key characteristics are:
1.Economical(any computer can be used)
2.Reliable(reistant to hard ware failure )
3.Scalable(follows both horizontal and vertical scaling) 
4.Flexible(slexibilty to use of structured/unstructured data)
![Hadoop Environment](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/Hadoop2.PNG)

>here program goes into data instead of vice versa(conventional approach(rdbms)-overloadig)

>hadoop ecosystem comprises of 12 components(which can be classified under Data Ingestion, Data Analysis, Data Processing,Data Exploration,Workflow System, No SQl)
![Hadoop Stages](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/Hadoop3.PNG)

### analyze BigData With Hadoop
*launching functional Hadoop cluster using Amazon EMR*


>added a S3 bucket in config file of the cluster
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/hadoop2.1.PNG)

>added necessary steps to be executed *defining schema and table for sample log data in S3*
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/hadoop2.2.PNG)
![macro instances](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/hadoop2.3.PNG)

>OS_request *analyzed data using a HiveQl script and wrote results back to S3*
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/hadoop2.4.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/hadoop2.5.PNG)
![Terminating](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/hadoop2.7.PNG)
![]()


