# Distributed Systems Practice
Notes from learning about distributed systems in [GW CS 6421](https://gwdistsys18.github.io/) with [Prof. Wood](https://faculty.cs.gwu.edu/timwood/)

Before we go ahead and know what AWS is and what services it offers, it’s very important to understand the basic core terms used in AWS. The oversimplified version of definition would be much easy for the very beginners who would like to know about this platform. 

VPC (Virtual private cloud): It’s a dedicated section of cloud provided by AWS to all its users which isolates other users on same platform to access it <br>

Aws Ec2 (Elastic Cloud Compute):  It’s a virtual equivalent of the computer sitting in front of you, primarily used for processing power 
Instance:  It’s a dedicated piece of virtual computer provided to a customer <br>

S3 (Simple Storage service): It is a cloud supported storage service provided by AWS <br>

DynamoDB: It’s a NoSQL database provided by AWS as a service <br>


## Area 1
> 

### Launching a VM: (24 min)
- After creation of account we are redirected to the home page where can select different services offered by AWS
-	To launch VM we need to select EC2 service and press launch instance button
-	This will direct us towards the wizard where we can select machine image i.e operating system and its instance type i.e configuration of machine  
-	After reviewing we can directly launch our instance or further configure before launching 
-	We will be prompted to choose an existing key pair or create a new key pair where we need to create new key and save it in our user directory in a sub-directory called .ssh
-	to connect we need to open git bash and use command ssh -i {full path of your .pem file} ec2-user@{instance IP address} where IP address can be access once our instance is in running state
-	To terminate instance we need to go to the EC2 Console where in action button, navigate to Instance State, and click Terminate
-	Terminating instance after use is very important as we will be charged for the usage

### Intro to S3: (30 min)
-	We need to click S3 from AWS management console to create a bucket, after clicking create bucket button, name your bucket and keep region as it is
-	We further need to configure bucket by selecting keep all versioning on and set permission as per the requirements (in mange public permission do not grant access to public) of the project then simply click create bucket  
-	To add files simply click your bucket name and then click upload where we can browse the files to be uploaded 
-	The file after uploading file, it will create an access link by clicking the link we won’t be able to access the file as the permission is set to private
-	 To change the permission follow the path  S3>{bucketName}>{filename}>Permission>Public Access> Everyone, this will allow us to access the file by clicking the link
-	We can also create bucket policy to assign set of permission to our bucket manually or by using policy generator 
-	To understand versioning system, add another file with name to the bucket and access it through the link where we will able to see new file which we recently uploaded
-	To access older version click on file name and click latest version to access all old versions


### Virtualization (10 min)

Virtualization is known as an act of emulating a physically realized object where it provides the functionality of the object from which it was virtualized.  IBM in early 1960’s was not able to run few OS because of which they started to lose business. This encouraged them to take a step towards virtualization. Few smart people from Stanford university were able to perform software emulation who later established a company VMware. In todays world cloud technologies can sell a piece of computer by provided required number of core and memory. It is still known that we haven’t made the application which can utilize high numbers of core at a time.


## Area 2
> Include notes here about each of the links
