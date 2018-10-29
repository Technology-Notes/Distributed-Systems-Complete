# Distributed Systems Practice
Notes from learning about distributed systems in [GW CS 6421](https://gwdistsys18.github.io/) with [Prof. Wood](https://faculty.cs.gwu.edu/timwood/)

Before we go ahead and try to understand what AWS is and what services it offers, it’s very important to understand the basic core terms used in AWS. The oversimplified version of definition would be much easy for the very beginners who would like to know about this platform. 


**VPC (Virtual private cloud)**: It’s a dedicated section of cloud provided by AWS to all its users which isolates other users on same platform to access it <br>

**Aws EC2 (Elastic Cloud Compute)**:  It’s a virtual equivalent of the computer sitting in front of you, primarily used for processing power 

**Instance**:  It’s a dedicated piece of virtual computer provided to a customer <br>

**S3 (Simple Storage service)**: It is a cloud supported storage service provided by AWS <br>

**DynamoDB**: It’s a NoSQL database provided by AWS as a service <br>


## Cloud Web Apps
> **_Beginner Level_**

### [Launching a VM:](https://aws.amazon.com/getting-started/tutorials/launch-a-virtual-machine/) (24 min)
- After creation of account we are redirected to the home page where we can select different services offered by AWS
-	To launch VM we need to select EC2 service and press launch instance button
-	This will direct us towards the wizard where we can select machine image i.e operating system and its instance type i.e configuration of machine  
-	After reviewing we can directly launch our instance or configure it futhermore before launching it 
-	We will be prompted to choose an existing key pair or create a new key pair where we need to create new key and save .pem file in our user directory by creating a sub-directory called .ssh
-	to connect we need to open git bash and use command `ssh -i {full path of your .pem file} ec2-user@{instance IP address}` where IP address can be access once our instance is in running state
-	To terminate instance we need to go to the EC2 Console where in action button, navigate to Instance State, and click Terminate
-	Terminating instance after use is very important as we will be charged for the usage

### [Intro to S3:](https://awseducate.qwiklabs.com/focuses/30?parent=catalog) (30 min)
-	We need to click S3 from AWS management console to create a bucket, after clicking create bucket button, name your bucket and keep region as it is
-	We further need to configure bucket by selecting keep all versioning on and set permission as per the requirements (in manage public permission do not grant access to public) of the project then simply click create bucket  
-	To add files simply click your bucket name and then click upload where we can browse the files to be uploaded 
-	The file after uploading file, it will create an access link by clicking the link we won’t be able to access the file as the permission is set to private
-	 To change the permission follow the path  `S3>{bucketName}>{filename}>Permission>Public Access>Everyone`, this will allow us to access the file by clicking the link
-	We can also create bucket policy to assign set of permission to our bucket manually or by using policy generator 
-	To understand versioning system, add another file with name to the bucket and access it through the link where we will able to see new file which we recently uploaded
-	To access older version click on file name and click latest version to access all old versions

>**_Intermediate Level_**

### [Virtualization:](https://www.youtube.com/watch?v=GIdVRB5yNsk) (10 min)

Virtualization is known as an act of emulating a physically realized object where it provides the functionality of the object from which it was virtualized.  IBM in early 1960’s was not able to run few OS because of which they started to lose business. This encouraged them to take a step towards virtualization. Few smart people from Stanford university were able to perform software emulation who later established a company VMware. In todays world cloud technologies can sell a piece of computer by provided required number of core and memory. It is still known that we haven’t made the application which can utilize high numbers of core at a time.


### [Installing a LAMP Web Server on Amazon Linux 2:](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-lamp-amazon-linux-2.html) (40 min)
-	We need to launch and connect to Amazon Linux 2 instance as shown in above tutorial 
-	Now we need to download extra repo by running command`sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2` and then `sudo yum install -y httpd mariadb-server` command will install mariaDB on the instance which we have launched
-	`sudo systemctl enable httpd` command will start each system boot and to check if its enable run `sudo systemctl is-enabled httpd`
-	We need to add security rule to a ‘launch-wizard-N’ security group with following values:  type: HTTP, Protocol: TCP, Port Range:80, Source: Custom 
-	Type your public dns of your instance to web browser to test the server
-	We can create a file under /var/www/html/ directory and try to access it through public dns generated

### S3 versus an EC2 VM (20 min)

Amazon Elastic Cloud Compute (EC2) provides a scalable and elastic computer facility as a cloud web service. It is highly scalable service where as per the requirement we can easily scale up the capacity, at same time, it also elastic i.e. we can reduce the computing power as per the change of requirement. This service provides high configurational facility with various option of preexisting setups. However, EC2 is designed for providing processing power and ideally it recommended to be used as computing service. 

> Serving the content on EC2 :
-	We will be needed an additional service called EBS which provides storage capacity to EC2 instance
-	We will have to pay for whole block of EBS even if it is not in use fully
-	Multiple EBS volume can be attached to one instance
-	 It also provides instance storage which is recommended for temporary storage which changes quickly such as buffer, caches an scratch data etc 

Simple Storage Service (S3) is storage service provided by Amazon which in highly scalable in nature. It provided infrastructure and hardware to maintain and store data. It provides unlimited storage capacity where the limit of storage is very high which is hard to achieve. S3 supports various format which makes it easier for anyone to store multiple types of files. 

> Serving the content on S3:
-	It is highly scalable service
-	We need to pay according to size of the data we have stored i.e. pay as you go
-	It provided high reliability as data is duplicated to various servers
-	 Uptime of the servers is also very high 
-	It provides object level security apart from user level security 


### [Introduction to Amazon DynamoDB:](https://awseducate.qwiklabs.com/focuses/23?parent=catalog) (20 min)
-	DynamoDB is NoSQL database service provided by AWS
-	In AWS Management console we need to select DynamoDB under services where we can create a table by specifying table name and primary key
-	We can add data to table by clicking Create item under 'Items tab'
-	 To create additional attributes just click “+” sign in create item window
-	There are two ways to query table i.e. “Scan” and “Query” where we can provide query information and click start search which will give required output


### [Deploy a Node.js web app:](https://aws.amazon.com/getting-started/projects/deploy-nodejs-web-app/?trk=gs_card) (30 min)

-	To deploy the app, we can use 'Elastic Beanstalk' Environment where we can select the platform which matches language used in our application 
-	Select ‘Sample Application’ and launch the application by clicking ‘Create App’
-	Add permission to your environment instance by selecting “AmazonSNSFullAccess” in Roles page in IAM console which will give permission to the http requests to use AWS services
-	Deploy your application by uploading it in management page of Elastic Beanstalk console and your application will be up and running 
-	Information uploaded by the user in the app will be stored in DynamoDB table which is already created when we launch an app 
-	We can delete our app by selecting ‘Terminate’ in actions menu of Elastic Beanstalk console and we need to delete the table created in DynamoDB manually

### [Intro to AWS Lambda:](https://awseducate.qwiklabs.com/focuses/36?parent=catalog) (25 min)

-	AWS Lambda is a compute service which responds to the events by running associated code after event occurs
-	To use the service, we need to create functions by selecting Lambda from AWS services and add triggers once function is created
-	We can test the function by specifying events name and templet where we also have to modify our template according to the services we are using, e.g. by specifying bucket name created in S3
-	We can monitor different status of lambda function by selecting monitor tab by clicking name of the function we have created 

### [Intro to Amazon API Gateway:](https://awseducate.qwiklabs.com/focuses/21?parent=catalog) (15 min)
-	By using API Gateways in AWS we can create an application which uses microservices architecture 
-	To use API Gateway service, we can create a lambda function and integrate API Gateway
-	To create Lambda function we need to select AWS Lambda service and create function
-	We can configure the function according to our requirement and write function code
-	In designer section of Lambda we need to add trigger and configure it to add it in application
-	Our API is created, now we need to test our API which can be accomplish by clicking right arrow under API gateway section to view the details
-	Copy and paste API endpoint to new browser which will show us the entry we have added in function code
-	This proves that the part of the data requested was successfully shown on the browser which serves as the Client-Server model and it could be considered as a form of microservice architecture where we are using RESTful API and format of the API is JSON


### [Building a serverless web application:](https://aws.amazon.com/getting-started/projects/build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito/?trk=gs_card) (1.50 hours) 

-	We are basically using various services offered by AWS to host a complete serverless web app on cloud
-	The services used in the application are DynamoDB, AWS Lambda, API Gateway, S3, Cognito
-	We will use S3 to host a static website where we need to enable website hosting in addition to the above tutorials mentioned on “Intro to S3” and index.html will always be the index document 
-	Amazon Cognito have two way of authenticating the user where user can use sign-up and sign-in functionality or use social identity provider such as Facebook, Twitter or Amazon
-	Note the pool id by creating a ‘User Pool’ and add your application through app client in general settings 
-	Update your config.js file where you need to add values for ‘userPoolId’, ‘userPoolClientId’ and ‘region’
-	We will have to create a DynamoDB table and IAM Role to provide various permission to the application
-	Later we must create Lambda function to handle requests where request details will be recorded in DynamoDB table and respond to the frontend application 
-	To use the function created in Lambda as a RESTFul API we will need to add API Gateway 
-	To authenticate we will need to add authorizers newly created API
-	Create a new resource method with ‘POST’ method and configure it to use Lambda function
-	Now we need to deploy the API and add ‘Invoke URL’ to config.js
-	Now simply test working of your application with website url created 
-	To destroy the application we need to delete S3 bucket, Cognito user pool, Lambda function, IAM Role, DynamoDB table, API and CloudWatch logs separately

## Docker and Containers
> **_Beginner Level_**

### [Why docker?:](https://www.youtube.com/watch?v=RYDHUTHLf8U&t=0s&list=PLBmVKD7o3L8tQzt8QPCINK9wXmKecTHlM&index=23) (10 min)

There has been shifts thought the era of computers and in future we are more likely to shift to another technology as it happens. Docker is all about speed. Everyone in the industry would like to do things quickly which will give them enough time to spend on more important task or enhancement of the project. Docker makes it quicker to develop, build, test, deploy, update and recover the software. It includes almost all the software development cycle which it is why expected to bring the next computer shift in the world. A docker allows us to package the software and distribute it irrespective of the OS or the system we are using. It brings lots of flexibility in the whole process of software development.


### [DevOps Docker Beginners Guide:](https://training.play-with-docker.com/ops-s1-hello/)(35 min)

-	This DevOps beginners guide gives us brief insight into docker engine, containers, images and isolation 
-	A container is an application abstraction, where containers run on application layer and the focus is not so too much interaction with hardware
- This makes it boot faster and run the command and exit the container just like running command on normal terminal
-	 Isolation allows users to quickly create separate, isolated test copies of an application or service and have them run side-by-side without interfering with one another
-	We can run container with the command `docker container run hello-world` where it will check if docker has an image with name ‘hello-world’. If not present it will download from ‘Docker Registry’ and run it. Also `pull` command can be used to download image.
-	`docker container run alpine ls -l` command run alpine container and runs command `ls -l` in that container
-	We can also instantiate another container with same image with command like `docker container run alpine /bin/sh` where `docker container run -it alpine /bin/sh` will give you interactive shell where we can type command for that perticular instance
-	The command `docker container ls -a` will give us list of containers we instantiated before where we can select particular ‘Container ID’ and use it to access files or application stored or running on that container

