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

[AWS Tutorial: Build a Serverless Web Application](https://aws.amazon.com/getting-started/projects/build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito/?trk=gs_card) (time: 90min)

In this tutorial, I experienced the power of AWS by building a serverless web application which enables users to request unicorn rides from the Wild Rydes fleet. This application presents users with HTML based user interface for indicating the location where they would like to be picked up and will interface on the backend with a RESTful web service to submit the request and dispatch a nearby unicorn. The application also provides facilities for users to register with the service and log in before requesting rides.

In this tutorial, I tried to use **AWS Lambda** to simulate the backend and response to the user requests, use **Amazon API Gateway** to interface user and backend, use **Amazon S3** to store the static website files,  use **Amazon DynamoDB** to store the histories of user request, and use **Amazon Cognito** to create and authenticate the user accounts. 

![Serverless_Web_App_LP](images/Serverless_Web_App_LP.png)

The above picture shows the architecture and steps of this application. Here is the summary of the four steps:

1. Amazon S3 hosts static web resources including HTML, CSS, Javascript, and image files which are loaded in the user's browser.

2. Amazon Cognito provider user management and authentication functions to secure the backend API.

3. Amazon DynamoDB provides a persistence layer where data can be stored by the API's Lambda function.

4. Javascript executed in the browser sends and receives data from a public backend API built using Lambda and API Gateway.

In the first step, I learned that the Amazon S3 can be used not only to store the data but to be a website hosting.

In the second step, I tried to create an Amazon Cognito user pool to manage the users' account of this application. When users visit the website they will first register a new user account. After users submit their registration, Amazon Cognito will send a confirmation email with a verification code to the address they provided. To confirm their account, users will return to the site and enter their email address and the verification code they received. After users have a confirmed account, they will be able to sign in. When users sign in, they enter their username (or email) and password. A JavaScript function then communicates with Amazon Cognito, authenticates using the Secure Remote Password protocol (SRP), and receives back a set of JSON Web Tokens (JWT). The JWTs contain claims about the identity of the user and will be used to authenticate against the RESTful API which is built with Amazon API Gateway.

The following is the function code for register and signin. We call `aws-cognito-sdk.min.js` and `amazon-cognito-identity.min.js` to achieve the Amazon Cognito.

```javascript
function register(email, password, onSuccess, onFailure) {
        var dataEmail = {
            Name: 'email',
            Value: email
        };
        var attributeEmail = new AmazonCognitoIdentity.CognitoUserAttribute(dataEmail);

        userPool.signUp(email, password, [attributeEmail], null,
            function signUpCallback(err, result) {
                if (!err) {
                    onSuccess(result);
                } else {
                    onFailure(err);
                }
            }
        );
    }

function signin(email, password, onSuccess, onFailure) {
  var authenticationDetails = new AmazonCognitoIdentity.AuthenticationDetails({
    Username: email,
    Password: password
  });

  var cognitoUser = createCognitoUser(email);
  cognitoUser.authenticateUser(authenticationDetails, {
    onSuccess: onSuccess,
    onFailure: onFailure
  });
}
```

In the third and fourth step, I tried to use AWS Lambda and Amazon DynamoDB to build a backend process for handling requests for the web application, and use Amazon API Gateway to expose the Lambda function as a RESTful API. 

The following code is the important part of the Lambda function. In this function, we not only return the information of a unicorn to the client but record the request history to Amazon DynamoDB.

```
exports.handler = (event, context, callback) => {
    if (!event.requestContext.authorizer) {
      errorResponse('Authorization not configured', context.awsRequestId, callback);
      return;
    }

        // omit some code...

    recordRide(rideId, username, unicorn).then(() => {
        callback(null, {
            statusCode: 201,
            body: JSON.stringify({
                RideId: rideId,
                Unicorn: unicorn,
                UnicornName: unicorn.Name,
                Eta: '30 seconds',
                Rider: username,
            }),
            headers: {
                'Access-Control-Allow-Origin': '*',
            },
        });
    }).catch((err) => {
        console.error(err);
        errorResponse(err.message, context.awsRequestId, callback)
    });
};


function findUnicorn(pickupLocation) {
    console.log('Finding unicorn for ', pickupLocation.Latitude, ', ', pickupLocation.Longitude);
    return fleet[Math.floor(Math.random() * fleet.length)];
}

function recordRide(rideId, username, unicorn) {
    return ddb.put({
        TableName: 'Rides',
        Item: {
            RideId: rideId,
            User: username,
            Unicorn: unicorn,
            UnicornName: unicorn.Name,
            RequestTime: new Date().toISOString(),
        },
    }).promise();
}
```

Another interesting point in the fourth step is that we create a cognito user pools authorizer. Amazon API Gateway can use the JWT tokens returned by Cognito User pools to authenicate API calls. After that, we deploy the API Gateway to trigger the Lambda function.

> Bring it together

[AWS Tutorial: Build a Modern Web Application](https://aws.amazon.com/getting-started/projects/build-modern-app-fargate-lambda-dynamodb-python/?trk=gs_card) (time: 240min)

In this Tutorial, I tried to build a sample website called Mythical Mysfits that enables visitors to adopt a fantasy creature as pet. This project can be implemented in 5 modules and I will analyze the technologies in each modules step by step.

1. Create Static Website. Build a static website, using **Amazon Simple Storage Service** (S3) that serves static content (images, static text, etc.) for the website.

2. Build Dynamic Website. Host the application logic on a web server, using an API backend microservice deployed as a container through **AWS Fargate**.

3. Store Mysfit Data. Externalize all of the mysfit data and persist it with a managed NoSQL database provided by **Amazon DynamoDB**.

4. Add User Registration. Enable users to registration, authentication, and authorization so that Mythical Mysfits visitors can like and adopt myfits, enabled through **AWS API Gateway** and its integration with **Amazon Cognito**.

5. Capture User Clicks. Capture user behavior with a clickstream analysis microservice that will record and analyze clicks on the website using **AWS Lambda** and **Amazon Kinesis Firehose**. 

![Mythical_module1_architecture](images/Mythical_module1_architecture.png)

The topic of Module 1 is to upload the static web content. I host the static content of the website on **Amazon S3**. The detail steps is similar with the tutorial before which includes uploading static website files, changing the access permission of the contents, and publishing the website content to S3. Besides, I use **AWS Cloud9** as a command-line tool to deal with these tasks.

![Mythical_module2_architecture](images/Mythical_module2_architecture.png)

The Module 2 contains something new technologies. In this module, I create a new miroservice hosted using **AWS Fargate** so that my website can integrate with an application backend. AWS Fargate is a deployment option in **Amazon Elastic Container Service (ECS)** that allows user to deploy containers without having to manage any clusters or server. The reason to choose Fargate is that it's a great choice for building long-running processes such as microservices backends for web and mobile and PaaS platforms. With Fargate, we get the control of containers and the flexibility to choose when they run without worring about provisioning or scaling servers.

Before we can create our service, the first step is to create the core infrastructure environment that the service will use, including the networking infrastructure in **Amazon VPC**, and the **AWS Identity and Access Management Roles** that will define the permission that ECS and the containers will have on top of AWS. To achieve this task, we use **AWS CloudFormation**. AWS CloudFormation is a service that can programmatically provision AWS resources that we declare within JSON or YAML files called CloudFormation Templates, enabling the common best practice of infrastructure as code.  

The second step is to create a Docker container image that contains all of the code and configuration required to run the Mythical Mysfits backend as a microservice API created with Flask. In this step, I use **Cloud9** to build the Docker container image and then push it to the **Amazon Elastic Container Registry (ECR)**, where it will be available to pull when I create the service using Fargate. One thing need to noted here is that I should provision a **Network Load Balancer (NLB)** to sit in front of my service tier, rather than directly expose my backend service to the internet. This would enable my frontend website code to communicate with a single DNS name while my backend service would be free to elastically scale in-and-out based on demand or if failures occur and new containers need to be provisioned. After this step, the user can see my Mythical website which is retrieving JSON data from my Flask API running within a Docker container deployed to AWS Fargate.

The last step is for optimizing. I create a working CI/CD pipeline to deliver changes to that service automatically whenever I update my code repository, I can quickly move new application features from conception to available for my Mythical Mysfits users.

![Mythical_module3_architecture](images/Mythical_module3_architecture.png)

In Module 3, I create a table in **Amazon DynamoDB** which is mentioned in previous tutorial. Rather than have all of the Mysfits be stored in a static JSON file, I store them in a database to make the websites future more extensible scalable. The key step is to update the code of operating the DynamoDB to the CI/CD pipeline. The request is formed using the AWS Python SDK called boto3. This SDK is a powerful yet simple way to interact with AWS services via Python code. It enables the developers to use service client definitions and functions that have great symmetry with the AWS APIs and CLI commands they have already been executing as part of this workshop. When finishing this module, the user can see the new polulation of Mysfits loading from my DynamoDB table and how the Filter functionality is working.

![Mythical_module4_architecture](images/Mythical_module4_architecture.png)

The Module 4 contains some familiar technologies I learned in the previous tutorials. The topic in this module is setup user registration. In order to add some more critical aspects to the Mythical Mysfits website, like allowing users to vote for their favorite mysfit and adopt a mysfit, I need to first have users register on the website. To enable registration and authentication of website users, I need to create a User Pool in **AWS Cognito** - a fully managed user identity management service. Then, to make sure that only registered users are authorized to like or adopt mysfits on the website, I need to deploy an REST API with **Amazon API Gateway** to sit in front of the NLB. The detailed steps is similar to the previous tutorial of AWS Cognito and Amazon API Gateway, the only key need attention is to configure an API Gateway VPC Link that enables API Gateways APIs to directly integrate with backend web services that are privately hosted inside a VPC. After this module, the users can register, login, view mysfits profiles, like, and adopt mysfits.

![Mythical_module5_architecture](images/Mythical_module5_architecture.png)

The final module is about the interacting between the users and my website and the user action data collection. It would be easy for me to analyze user actions taken on the website that lead to data changes in my backend - when mysfits are adopted or liked. But understanding the actions my users are taking on the website before a decision to like or adopt a mysfit could help me design a better user experience in the future that leads to mysfits getting adopted even faster. To help gather these insights, I implement the ability for the website frontend to submit a tiny request, each time a mysfit profile is clicked by a user, to a new microservice API I create. Those records are processed in real-time by a serverless code function, aggregated, and stored for any future analysis that I may want to perform. In this module, I use several technologies. Some of them are new: **AWS Kinesis Firehose delivery stream**, Kinesis Firehose is a highly available and managed real-time streaming service that accepts data records and automatically ingests them into several possible storage destinations within AWS, such as Amazon S3 bucket, or Amazon Redshift data warehouse cluster. Kinesis Firehose also enables all of the records received by the stream to be automatically delivered to a serverless function created with AWS Lambda This means that code I've written can perform any additional processing or transformations of the records before they are aggregated and stored in the configured destination. Others are familiar: **Amazon S3 bucket**, a new bucket is created in S3 where all of the processed click event records are aggregated into files and stored as objects; **AWS Lambda function**, AWS Lambda enables developers to write code functions that only contain what their logic requires and have their code be deployed, invoked, made highly reliable, and scaled without having to manage infrastructure whatsoever. Here, a Serverless code function is defined using **AWS SAM**. It will be deployed to AWS Lambda, written in Python, and then process and enrich the click records that are received by the delivery stream; **IAM Roles**, Kinesis Firehose requires a service role that allows it to deliver received records as events to the created Lambda function as well as the processed records to the destination S3 bucket. The Amazon API Gateway API also requires a new role that permits the API to invoke the PutRecord API within Kinesis Firehose for each received API request.

In conclusion, via the experiences from module 1 to module 5, I have built a modern application on top of AWS. I have mastered the usage of some AWS technologies mentioned above. I have learnt to use AWS resrouces not only by the AWS CLI but the AWS consoles. In addition, I am only very familiar with Python, but in this tutorial I feel the greatness of this language: the powerful extensive support libraries make me do all the thing I want!



## Area 2

> Beginner Level



> Intermediate Level



## Area 3 Docker and Containers

> Beginner Level

[Video: Why Docker?](https://www.youtube.com/watch?v=RYDHUTHLf8U&t=0s&list=PLBmVKD7o3L8tQzt8QPCINK9wXmKecTHlM&index=23) (time: 20 min)

This video introduces the benefits of Docker. When talking about docker, we need to know container first. As I learned in the Aera 1, a container is a set of software that packages up code and all its dependencies so the application can run quickly and reliably from one computing environment to another. A Docker container image is a typical container. The Docker can reduce the infrastructure and maintenance costs of supporting the application portfolio. I also learn the differences between containers and virtual machines, they have similar resource isolation and allocation benefits, but function differently. Containers virtualize the operation system instead of hardware, containers are more portable and efficient. The following is the detailed comparison between container and vm:

![docker-containerized-appliction](images/docker-containerized-appliction.png)

Containers are an abstraction at the app layer that packages code and dependencies together. Multiple containers can run on the same machine and share the OS kernel with other containers, each running as isolated processes in user space. Containers take up less space than VMs (container images are typically tens of MBs in size), can handle more applications and require fewer VMs and Operating systems.

![vm](images/vm.png)

Virtual machines (VMs) are an abstraction of physical hardware turning one server into many servers. The hypervisor allows multiple VMs to run on a single machine. Each VM includes a full copy of an operating system, the application, necessary binaries and libraries - taking up tens of GBs. VMs can also be slow to boot.



[Lab: DevOps Docker Beginners Guide](https://training.play-with-docker.com/ops-s1-hello/) (time: 50min)

In this guide, I learnt the basic of how container work, how the Docker engine executes and isolates containers from eachother via some command line scripts.

![Docker_1](images/Docker_1.svg)

First, I execute the script `docker run hello-world` which means run the container named *hello-world*. Enssentially, the Docker engine running in my terminal tried to find an image named hello-world, if there are no images stored locally, the Docker engine goes to its default Docker register, which is **Docker Store**, to look for an image named *hello-world*. It finds the image there, pulls it down, and then runs it in a container.

![Docker_2](images/Docker_2.svg)

Second, I execute the command `docker container run alpine ls -l`, which means that I execute the command `ls -l` inside the container which name is *alpine*. Another similar script is `socker container run alpine echo "hello from alpine"`.

![Docker_3](images/Docker_3.svg)

The third is about Docker container isolation. In the steps above I ran several commands via container instances with the help of `docker container run`. The `docker container ls -a` command showed us that there were several containers listed. Why are there so many containers listed if they are all from the alpine image? This is a critical security concept in the world of Docker containers. Even though each docker container run command used the same alpine image, each execution was a separate, isolated container. Each container has a separate filesystem and runs in a different namespace; by default a container has no way of interacting with other containers, even those from the same image. 
