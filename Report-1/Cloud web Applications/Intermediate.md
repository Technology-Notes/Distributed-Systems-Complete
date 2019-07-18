
## ********************** CLOUD INTERMEDIATE **********************

### Virtual Machines, Websites, and Databases:
(https://www.youtube.com/watch?v=GIdVRB5yNsk)describes virtualization and  why it needs more and more implementation everyday.
>This video talks about the growing demand of distributed environment and the evolution of virtualization.
======================
### Install a Lamp Web Server on Amazon Linux2

** This tutorial guided me to install lamp i.e. apache web server with PHP and MariaDB on amazon linux 2 instance.**

The main parts of the procedure are described below:

>ran linux instance

>establishing connection through putty

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
>To host static website

>Deploy dynamic PHP application that reads and writes information to database.

 
### On your own: Compare the performance, functionality, and price when serving web content from S3 versus an EC2 VM 

**S3 vs EC2**

>Only Static web content can be served through S3. S3 is a object based storage system.

>It is highly available and by defaults it is duplicated across availability zone.

>Also S3 storage is much cheaper than EBS- block storage. By serving the static contents from S3, one can save on IOPs of the EC2 as the request for S3 static links is not served through EC2.

>Also it create a highly available environment, the static content which often are media files which consumes much higher storage need not be stored in all the EC2 instances

>Thus EC2 EBS storage requirement is reduced considerably

>Price wise S3 is 4-5 times less cheap.

### Intro to DynamoDB

> **Amazon DynamoDB** is a fast and flexible NoSQL database service for all applications that need consistent, single-digit
 millisecond latency at any scale.

> It is fully managed database and supports both document and key-value data models.

Following things were learned in this tutorial:

> Create Amazon DynamoDB table:

1. Here, I created a table named music. The table make use of Primary key and Sort Key to uniquely identify each item in a Dynamo DB table.
2. After adding table name, primary key*e.g. artist which is string* with the usage of add sort key to finally create a table.

> Enter data into an Amazon DynamoDB table:
1. we can add unlimited data into dynamoDB where attribute(*has a field/value*) is the fundamental or smallest entity.
2. The entry of data is only dependent on primary/sort keys.
3. Using **items** tab we can create items and append required attributes.

> Modifying Existing data
1. Using **Psy**, we can change field values.

> Query an Amazon DynamoDB table:

1. Query can be done by using **query** or **scan**.
2. query is a faster option as it is based on primary keys and is fully indexed.

> Delete an Amazon DynamoDB table:
1. Simply click Delete table to delete it.


## Deploy a Node.js Web App

> **GOALS**:
1. learn how to deploy a high-availability Node.js web app using AWS Elastic Beanstalk and Amazon DynamoDB.
2. Use Amazon Simple Notification Service (SNS) to configure push notifications for the app.

Main learning:
> use of Elastic Beanstalk console to launch Elastic Beanstalk Environment and configuring the environment permissions(AmazonDynamoDBFullAccess, AmazonSNSFullAccess).

>  Deploy source bundle gathered from github.

> Update application configuration files in the appliation source by changing values of NewSignupEmail & STARTUP_SIGNUP_TABLE in .ebextensions/options.config file.

> Modified capacity of the environment using auto scaling group.

> Hosting static resources in S3
![M4](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/S3.PNG)

>Running instance states of two linux t2

![M2](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/ins.PNG)

> Monitoring
![M3](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/Mon.PNG)

> Using Multiple servers for reliability
![M1](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/unh_vs_h.PNG)

## Serverless and Edge Computing:

### Intro to AWS lambda

> AWS lambda that is called every time it is needed make the network serverless. It runs code only according to the response of the user and automatically manages the resources.

> It is used as a back-end service where computing resources are automatically triggered based on custom request.

> **Following image shows the successfull deployment of AWS Lambda.**
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/AWS_lambda.PNG)

##  Intro to Amazon API Gateway

Amazon API gateway is an interface between multiple backend services to multiple client request.

**Main learning:**
> create a simple FAQ micro-service which returns a JSON object containing a random question and answer pair using Amazon API Gateway endpoint that invokes an AWS Lambda function.

> That would involve-- * creating aws lambda function, api gateway endpoints, debugging api gateway and lambda  function with amazon cloud watch*

> **MICROSERVICE - ARCHITECTURE**
![img](https://github.com/agsrc/dist-sys-practice/blob/master/images/app_arch.PNG)

*https://developer.spotify.com/documentation/web-api/*  was good example to understand RESTFUL API.


# Build a serverless web App

> **GOAL:**
Create a simple serverless web application that enables users to request unicorn rides from the WIld Rydes(*http://www.wildrydes.com/*) fleet.

> **User interface:**
1. Indicate user the location where they would be like to be picked up.
2. The application will provide user the facility to register with services and log in before requesting rides.

> 1
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/app_arch.PNG)

### Manage users
> Create an Amazon Cognito user pool to manage your users' accounts. 

> Deploy pages that enable customers to register as a new user, verify their email address, and sign into the site.

Pool Id: us-west-2_QwfIuQsvA
607gktk0nr9leupbrn5c6nhsiu

### Serverless Service Backend

> use AWS Lambda and Amazon DynamoDB to build a backend process for handling requests for your web application.

> To request a unicorn to be sent to location to user choice we need to invoke a service in the cloud i.e javascript which triggers aws lambda.

> Create dynamo table to keep the record of rides information.

> IAM roles for lambda- *to define with which servies aws lambda can interact*.

> Finally creating AWS lambda function that will process API requests from web application to dispatch a unicorn

Amazon Resource Name (ARN)
	arn:aws:dynamodb:us-west-2:566965401352:table/Rides

### Deploy Rest API

> Using Amazon API Gateway to expose lambda function.

> Using (RESTful API -- *which would be public* & Amazon Cognito user pool) will then turn your statically hosted website into a dynamic web application by adding client-side JavaScript that makes AJAX calls to the exposed APIs.

auth token: eyJraWQiOiJuTnA4NUVcL2tnS1Q3VmkxZ0kyRW5xVjlaZEdpTEFSYW5KenV0N01nNzd0ST0iLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiIxMGRkZWM3Ni0xOWU3LTQ1YjctYmNjNC1jOTlmYmZjMjA3ZjYiLCJhdWQiOiI2MDdna3RrMG5yOWxldXBicm41YzZuaHNpdSIsImVtYWlsX3ZlcmlmaWVkIjp0cnVlLCJldmVudF9pZCI6ImY3ZmQxMDE2LWRiMDAtMTFlOC1iNWIyLTc5YzdiNTZkMjQ1ZiIsInRva2VuX3VzZSI6ImlkIiwiYXV0aF90aW1lIjoxNTQwNzY1Nzg0LCJpc3MiOiJodHRwczpcL1wvY29nbml0by1pZHAudXMtd2VzdC0yLmFtYXpvbmF3cy5jb21cL3VzLXdlc3QtMl9Rd2ZJdVFzdkEiLCJjb2duaXRvOnVzZXJuYW1lIjoiYWtzaGF5Lmd1cHRhMDcxMkBnbWFpbC5jb20iLCJleHAiOjE1NDA3NjkzODQsImlhdCI6MTU0MDc2NTc4NCwiZW1haWwiOiJha3NoYXkuZ3VwdGEwNzEyQGdtYWlsLmNvbSJ9.Wf8mpVtwtbODlFQA8tQyhGC0yz6I-z4xD8yFmrfSggs30s5mJL8YiiRxWg03ZuOmsjBco5XMMduIqu0va7T4FpTYSrCAq9m1uAoCrOfUbuBD3MQFFGuJ2geJgi8tMoEmWtaLz32LBHBNERMq3-6MmMqkT3tRqLyb7GI0_FyNIvHvQok_gZUWquR98Ny9FKn4pkYf7ApbZgw9jqWlIHDZAT8EKVQYslTk32dkuvYgugO1lj-aHWDY5zl7Q0D-TLPHOLSI2CarNi7e4VhwcliiXktYCmZnI_qieCBFOcq8HndBVpgSkPXOkAK4AUvujBdUK3SekGZcXMyDjgYDyGMfdA

>arn:aws:lambda:us-west-2:566965401352:function:RequestUnicorn

>https://2x01cqllu1.execute-api.us-west-2.amazonaws.com/prod(deployed api)

**Whole process is described through the series of screenshots**

> 2
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/static_web_hosting_S3.PNG)
> 3
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/static_bp.PNG)
> 4
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/2.PNG)
> 5 
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/3.PNG)
> 6 
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/webapp_awslambda.PNG)
> 7
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/lambdalog_webapp.PNG)
> 8
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/authentication.PNG)
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/APcognito_verification.PNG)
> 9
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/api_method.PNG)
> 10
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/lambda_requestunicorn.PNG)
> 11
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/method_requestcard.PNG)
> 12 
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/authorized.PNG)
> 13 
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/unicorn%20arrived.PNG)
> 14 
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/cognito_usergroup.PNG)
> 15 
![](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/unicorn_dynamo.PNG)

# Build a Modern Web Application in python

**Goal:**
: *To create a website that enables visitors to a adopt a fantasy creature.*(www.mythicalmysfits.com)

>*host the web application on a front-end web server*

>*connect to backend database*

>*user authentication*

>*collect and analyze user behavior*

>*gathers insight for future analysis*

## Application architecture

>The application architecture diagrams provide a structural representation of the services that make up Mythical Mysfits and how these services interact with each other

> 
![Application Architecture](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/P1.PNG)

## Modules
The project has been divided into following modules:

>Create Static website-*building static website i.e. storing static objects in S3 *

>Build Dynamic Website-*hosting application logic on a web server-using API backend microservice deployed(as a container)--aws fargate*

>Store Mysfit Data-*manage via NoSQl databse i.e. Amazon DynamoDB*

>Add User Registration-*API Gateway/Amazon Cognito*

>Capture User Clicks-*capture user analysi using AWS lambda/kenesis Firehose*

>create the required infrastructure components, which includes a fully managed CI/CD stack utilizing AWS Code Commit, Code Build, and Code Pipeline. Finally, you will complete the development tasks required all within your own browser using the cloud-based IDE, AWS Cloud9.


>Modue1-(static hosting)
![architecture](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/F2.1.PNG)

>>Cloud 9 created
mythical-mysfits-bucket01(S3 bucket created)
aws s3 mb s3://mythical-mysfits-bucket-02

>>basic static site created
---------------
>module 2(host your app on web server)
![]()
*creating microservice hosted with aws fargate to integrate website with backend*
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
after building docker image 
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

>>committing real code change

>>updating website content in S3
----------------

>Module 4: Setup User Registration*To enable registration and authentication of website users, we will create a User Pool in AWS Cognito - a fully managed user identity management service. *
![architecture](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/F4.PNG)
**To make sure that only registered users are authorized to like or adopt mysfits on the website, we will deploy an REST API with Amazon API Gateway to sit in front of our NLB. Amazon API Gateway is also a managed service, and provides commonly required REST API capabilities out of the box like SSL termination, request authorization, throttling, API stages and versioning, and much more.**

>>added user pool for website Users

>>added a new rest api with amazon API gateway

>>Updated the Mythical Mysfits Website
-------------------

>Module 5: Capture User Behavior *in order to make use of the site it is a ggod practice to analyze user response*
![architecture](https://raw.githubusercontent.com/agsrc/dist-sys-practice/master/images/F5.PNG)
**following instructions are required to implement it**

1. create streaming service code
2. update the lambda function package and code
3. create the streaming Service Stack
4. sending mysfit profile clicks to the created micrsoervice

**Conclusion**: Using AWS CLI, A serverless system with multiple modules was managed.

