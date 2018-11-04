# Distributed Systems Practice

Notes from learning about distributed systems in [GW CS 6421](https://gwdistsys18.github.io/) with [Prof. Wood](https://faculty.cs.gwu.edu/timwood/)

## Area 1: Cloud Web Apps

> Beginner Level

[AWS Tutorial: Launch a VM](https://aws.amazon.com/getting-started/tutorials/launch-a-virtual-machine/) (time: 30 min)

Notes: In this lecture, I have learned how to lauch, configure, connect, and terminate an instance in the cloud. Besides, I have learned 2 linux commands:  `chmod` and `ssh` :

- chmod xxx filename . Change the access permissions, **ch**ange **mod**e. 3 digits stand for: user, group, and world. 4 means read, 2 means write, 1 means execute.

```
chmod 400 file.txt    // allow read by owner
chmod 740 file.txt     // allow read, write, execute by owner, allow read by group
chmod 777 file.txt    // allow everyone to read, write, and execute file
```

- ssh (SSH client) is a program for logging into a remote machine and for executing commands on a remote machine.

```
ssh -i file [user@]hostname    // here, -i means selecting a file from which the identity for RSA is read.
```

[QwikLab: Intro to S3](https://awseducate.qwiklabs.com/focuses/30?parent=catalog) (time: 25 min)

Notes: In this lab, I learned the basic usage of **S3** by finishing the tasks one by one. Amazon Simple Storage Service (Amazon S3) is storage for the Internet. Users can use Amazon S3 to store and retrieve any amount of data at any time, from anywhere on the web. Following the instructions, I have created a bucket in S3, added 2 pictures to my bucket, managed access permisson on pictures, created a Bucket Policy for permisson control, and tried to use bucked versioning.

> Intermediate Level

[Video: Virtualization](https://www.youtube.com/watch?v=GIdVRB5yNsk) (time: 20 min)

[AWS Tutorial: Install a LAMP Web Server on Amazon Linux 2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-lamp-amazon-linux-2.html) (time: 45min)

In this practice, I learned how to install a **Lamp Web Server** on amazon Linux 2 by installing an Apache web server with PHP and MariaDB (a community-developed fork of MySQL) . We can use this server to host a static website or deploy a dynamic PHP application that reads and writes information to a database.

The first step is to prepare and lauch LAMP Server. When finishing connecting to the EC2 instance via SSH, we need to install the latest version of the LAMP MariaDB and PHP packages for Amazon Linux 2, then use **yum install** commond to install multiple software packages and related dependencies (such as httpd, mariadb-server). After that, we start the Apache webserver via `sudo systemctl start httpd` command. By the way, to test the web server in the web browser, we need to first add a security rule to allow inbound HTTP (port 80) to the instance, then type the public DNS address of the instance on browser, we can see the Apache test page. Besides, setting file permission inside `/var/www/html` to ensure we can add, delete, and edit files in the Apache document root.

The second step is to test the LAMP Server via creating a PHP file in the Apache document root. We use `echo` command to write something into a file. By entering the public DNS address plus the file address, we can see the webpage on the web browser.

The second step is to secure the database server because the default installation of the MariaDB server should be disabled or removed for production servers.

[QwikLab: Intro to DynamoDB](https://awseducate.qwiklabs.com/focuses/23?parent=catalog) (time: 20min)

In this lecture, I learned about **Amazon DynamoDB**. It is a fast and flexible NoSQL database service. It's also a fully managed database and supports both document and key-value data models.

In this lecture, I tried to create a table in Amazon DynamoDB, and added and edited some data to it, then tried to query and search data from it, finally I deleted the table I created. All of the operations can be done on the console by mouse clicking.

[AWS Tutorial: Deploy a Scalable Node.js Web App](https://aws.amazon.com/getting-started/projects/deploy-nodejs-web-app/?trk=gs_card) (time: 60min)

In this lecture, I tried to deploy a Node.js application with DynamoDB to Elastic Beanstalk. Elastic Beanstalk can us quickly deploy and manage applications in the AWS Cloud without worrying about the infrastructure that runs those applications. Here is the deployment architecture for this lecture.

![Elastic_Beanstalk](images/Elastic_Beanstalk.png)

The first step is to **lauch an Elastic Beanstalk environment** via the Elastic Beanstalk console. Elastic Beanstalk will create the environment with the following resources:

- EC2 instance -- the configured virtual machine to run web apps

- Instance security group -- configured to allow ingress on port 80

- Load balancer -- configured to distribute request to the instance running the application and eliminate the need to expose the intance directly to the internet

- Load balancer security group -- configured to allow ingress on port 80

- Auto Scaling group -- configured to replace an instance if it is terminated or becomes unavailable

- Amazon S3 bucket -- store the source code, logs, and other artifacts that are created when using Elastic Beanstalk

- Amazon CloudWatch alarms -- monitor the load on the instances and are triggered if the load is too high or too low

- AWS CloudFormation stack -- lauch the resource in the environment and propagate configuration changes

- Domain name -- routes to the web app

The second step is to **add permissions** to the environment instance. For this lecture, the sample application uses instance permissions to write data to a DynamoDB table, and to send notifications to an Amazon SNS topic with the SDK for JavaScript in Node.js.

The third step is to **deploy the sample application** via uploading the application source bundle to Elastic Beanstalk. This web app will collect the name and email entered by user and store it to default DynamoDB.

To create our own DynamoDB, the fourth step is to **create a new DynamoDB table** and **reupload the application's configuration files**. To make the configurations, we need to change the signup email and the STARTUP_SIGNUP_TABLE to our own name. When redeploying the application,  the new DynamoDB table will store the information entered by users.

The finally step is to **configure the environment for high availability** via configuring the auto scaling group with a higher minimum instance count.

In a word, this lecture helps me to know the basic framework of Elastic Beanstalk and the basic steps to deploy the web apps and database on the Internet.

[QwikLab: Intro to AWS Lambda](https://awseducate.qwiklabs.com/focuses/36?parent=catalog) (time: 70min)

This lecture introduces AWS Lambda. AWS Lambda is a compute service that runs  developer's code in response to events and automatically manages the compute resources for developer, making it easy to build application that respond quickly to new information. AWS Lambda starts running the code within milliseconds of an event such as an image upload, in-app activity, website click, or output from a connected device. AWS Lambda can also be used  to create new back-end services where compute resources are automatically triggered based on custom requests. 

In this lecture, I tried to create an AWS Lambda function, configure an S3 bucket as a Lambda Event Source, then trigger a Lambda function by uploading an object to Amazon S3. Here is the application flow for AWS Lambda in this lecture:

![Lambda](images/Lambda.png)

1. A user uploads an object to the source bucket in Amazon S3.

2. Amazon S3 detects the object-created event.

3. Amazon S3 publishes the object-created event to AWS Lambda by invoking the Lambda function and passing event data as a function parameter.

4. AWS Lambda executes the Lambda function.

5. From the event data it receives, the Lambda function knows the source bucket name and object key name. The lambda function reads the object and creates a thumbnail using graphics libraries, then saves the thumbnail to the target bucket.

The highlight of this lecture is creating an AWS Lambda function that reads an image from Amazon S3, resizes the image and then stores the new image in Amazon S3. Here we use a pre-written function: 

```python
import boto3
import os
import sys
import urllib
from PIL import Image
import PIL.Image

s3_client = boto3.client('s3')

def resize_image(image_path, resized_path):
    with Image.open(image_path) as image:
        image.thumbnail((128,128))
        image.save(resized_path)

def handler(event, context):
    for record in event['Records']:
        bucket = record['s3']['bucket']['name']
        key = record['s3']['object']['key']
        raw_key = urllib.parse.unquote_plus(key)
        download_path = '/tmp/{}'.format(key)
        upload_path = '/tmp/resized-{}'.format(key)

        s3_client.download_file(bucket, raw_key, download_path)
        resize_image(download_path, upload_path)
        s3_client.upload_file(upload_path,
             '{}-resized'.format(bucket),
             'thumbnail-{}'.format(raw_key),
             ExtraArgs={'ContentType': 'image/jpeg'})
```

As the above code shows, when being called, the python function `handler` will download the image, resize the image using function `resize_image`, and upload the resized image to the *-resized* bucket in Amazon S3.

The AWS Lambda function can be **triggered** automatically by activities. Here we need to configure a S3 trigger to active the AWS Lambda function.

Another interesting place is the **monitoring and logging** in AWS Lambda function. We can monitor AWS Lambda functions to identify problems and view log files to assist in debugging.



[QwikLab: Intro to Amazon API Gateway](https://awseducate.qwiklabs.com/focuses/21?parent=catalog) (time: 30min)

In this lecture, I created a simple FAQ micro-service. The micro-service will return a JSON object containing a random question and answer pair using an **Amazon API Gateway** endpoint that invokes an **AWS Lambda function**. Here is the architecture pattern for this micro-service:![api_gateway_micro_service](images/api_gateway_micro_service.png)

Amazon API Gateway is a managed service that creating, deploying and maintaining APIs easy. The steps in this lecture is similar with previous lecture: Creating a Lambda function first, then trigger the function via API Gateway. The lambda function (implemented with Node.js) defines a list of FAQs and returns a random FAQ. The API Gateway will produce a endpoint `https://8tx6efu970.execute-api.us-west-2.amazonaws.com/myDeployment/FAQ`. When we  copy endpoint to the browser, we can see a random FAQ entry, that means when users request server with this endpoint, the Lambda function developer created will be triggered.

Besides, I want to talk more about API. An **application programming interface** is a set of instructions that defines how developers interface with an application. The idea behind an API is to create a standardized approach to interfacing the various services provided by an application. An API is designed to be used with a **Software Development Kid (SDKs)**, which is a collection of tools that allows developers to easily create downstream applications based on the API.

Then, I learn about **API-First strategy**, which is adopted by many software organizations. It means that each service within their stack is first and always released as an API. When designing a service, it is hard to know all of the various applications that may want to utilize the service. For instance, the FAQ service in this lecture would be ideal to seed FAQ pages on an external website. However, it is feasible to think that a cloud education company would also want to ingest the FAQ within their training materials for flash cards or training documents. If it was simply a static website, the ingestion process for the education company would be very difficult. By providing an API that can be *consumed in a standardized format*, the microservice is enabling the development of an ecosystem around the service, and use-cases that were not initially considered. 

The last useful tip is about RESTful API, which refers to architectures that follow 6 constraints:

- **Separation of concerns** via a client-server model.

- **State** is stored entirely on the client and the communication between the client and server is **stateless**.

- The client will **cache** data to improve network efficiency.

- There is a uniform interface (in the form of an API) between the server and client.

- As complexity is added into the system, layers are introduced. There may be multiple layers of RESTful components.

- Follows a **code-on-demand** pattern, where code can be downloaded on the fly (in this lecture implemented in Lambda) and changed without having to update clients.

In this lecture, the steps follow the RESTful model. Clients send requests to backend Lambda function (server). The logic of service is encapsulated within the Lambda function and it is providing a uniform interface for clients to use.



[AWS Tutorial: Build a Serverless Web Application](https://aws.amazon.com/getting-started/projects/build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito/?trk=gs_card) (time: )

> Bring it together

[AWS Tutorial: Build a Modern Web Application](https://aws.amazon.com/getting-started/projects/build-modern-app-fargate-lambda-dynamodb-python/?trk=gs_card) (time: )

## Area 2

> Include notes here about each of the links
