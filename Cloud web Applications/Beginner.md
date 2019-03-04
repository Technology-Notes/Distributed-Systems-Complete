## ********************** CLOUD BEGINNER **********************
----------------
### AWS Tutorial: Launch a VM 

> **Following are the main processes done after entering the amazon EC2 console**

> launched instance:
![launched instance](https://github.com/agsrc/dist-sys-practice/blob/master/Cloud%20web%20Applications/Screenshots-Beginner/launched%20instance.PNG)

> pair key:
![pair key ](https://github.com/agsrc/dist-sys-practice/blob/master/Cloud%20web%20Applications/Screenshots-Beginner/pair%20key.PNG)

connection through putty:
![connection through putty](https://github.com/agsrc/dist-sys-practice/blob/master/Cloud%20web%20Applications/Screenshots-Beginner/putty.PNG)

---------------------------------
### Introduction to Amazon Simple Storage Service S3
new to S3? watch this [intro to S3](https://www.youtube.com/watch?v=77lMCiiMilo).
---------------------------------
>**Use cases** of S3
1. Frequently accessed data
2. S3 Standard-*Infrequent Access*
3. S3 One Zone-*Infrequent Access* for long-lived, but less frequently accessed data.
4. Amazon Glacier for *long-term archive*.

>**reliable**- use SSL and management policies

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
