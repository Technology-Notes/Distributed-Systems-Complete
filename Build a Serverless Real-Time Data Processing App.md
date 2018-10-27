# Build a Serverless Real-Time Data Processing App
>> https://aws.amazon.com/getting-started/projects/build-serverless-real-time-data-processing-app-lambda-kinesis-s3-dynamodb-cognito-athena/?trk=gs_card

## Intro

### Create an AWS Account
- Use AWS account email address and password to sign in as the AWS account root user to the IAM console
at https://console.aws.amazon.com/iam/.
![avatar](/Image/lab01.png)
- In the navigation pane of the console, choose <strong>User</strong>, and then choos <strong>Add user</strong>.
![avatar](/Image/lab02.png)
- For <strong>User name</strong>, type the <strong>Administrator</strong>
- Select the check box next to AWS Management Console access, select Custom password, and then type the new user's password in the text box. You can optionally 
select Require password reset to force the user to create a new password the next time the user signs in.
- Choose <strong>Next:Permissions</strong>
![avatar](/Image/lab03.png)

### Set up AWS Cloud9 IDE
- Go to the AWS Management Console, select <strong>Service</strong> then select <strong>Cloud9</strong> under Developer Tools.
![avatar](/Image/lab91.png)
- Select <strong>Create environment</strong>
- Enter Development into Name and optionally provide a <strong>Description</strong>
![avatar](/Image/lab92.png)
- Select <strong>Next Step</strong>
- ou may leave Environment settings at their defaults of launching a new t2.micro EC2 instance which will be paused after 30 minutes of inactivity.
![avatar](/Image/lab93.png)
- Select <strong>Next steps</strong>
![avatar](/Image/lab94.png)
- Type in Admin:~/environment $ aws sts get-caller-identity
![avatar](/Image/lab911.png)

### Installation
- Switch to the tab where I have Cloud9 environment opened
- Download and upack the command line clients by running the following command in the Cloud9 terminal: curl -s https://dataprocessing.wildrydes.com/client/client.tar | tar -xv
![avatar](/Image/lab96.png)

## Real-time Streaming Data

### Create an Amazon Kinesis stream
- Go to the AW Management Console, select Service then select Kinesis under Analytics
![avatar](/Image/lab97.png)
- Select <strong>Get started</strong> if prompted with an introductory screen
![avatar](/Image/lab98.png)
- Select <strong>Create data stream</strong>
- Enter  wildrydes  into Kinesis stream name and 1 into Number of shards, then select Create Kinesis stream.
- Within 60 seconds, Kinesis stream will be ACTIVE and ready to store real-time streaming data. 
![avatar](/Image/lab99.png)
![avatar](/Image/lab910.png)

### Produce messages into the stream
- Switch to the tab where have Cloud9 environment opened.
- In the terminal, run the producer to start emiting sensor data to the stream: ./producer
![avatar](/Image/lab912.png)

### Read messages from the stream
- Click <strong>New Terminal </strong>to open a new terminal tab.
- Run the consumer to start reading sensor data from the stream: ./consumer
![avatar](/Image/lab913.png)

### Create an identity pool for teh unicorn dashboard
- Go to the AWS Management Console, services Services then select Cognito under Security, Identity & Compliance.
![avatar](/Image/lab914.png)
- Select Manage Identity Pools.
- Enter wildrydes  into Identity pool name.
- Tick the Enable access to unauthenticated identities checkbox.
![avatar](/Image/lab915.png)
- Click Create Pool.
![avatar](/Image/lab916.png)
- Click Allow which will create authenticated and unauthenticated roles for your identity pool.
![avatar](/Image/lab917.png)
- Select Go to Dashboard.
![avatar](/Image/lab918.png)
- Select Edit identity pool in the upper right hand corner.
![avatar](/Image/lab919.png)
- Note the Identity pool ID for use in a later step.

### Grant the unauthenticated role access to the stream
- Go to the AWS Management Console, services Services then select IAM under Security, Identity & Compliance.
![avatar](/Image/lab920.png)
- Select Roles in the left-hand navigation.
![avatar](/Image/lab921.png)
- Select the Cognito_wildrydesUnauth_Role.
![avatar](/Image/lab922.png)
- Select Add inline policy.
- Select Choose a service and select Kinesis.
- Tick the Read and List permissions checkboxes in the Actions section.
- Select Resources to limit the role to the wildrydes  stream.
![avatar](/Image/lab923.png)
- Select Add ARN next to stream
![avatar](/Image/lab924.png)
- Enter the region you're using in Region (e.g. us-east-1), your Account ID in Account, and wildrydes  in Stream name.
To find your twelve digit AWS Accout ID number in the AWS Management Console, select Support in the navigation bar in the upper-right, and then select Support Center. Your currently signed ID appears in the upper-right corner below the Support menu.
![avatar](/Image/lab925.png)
- Select Add
- Select Review policy
![avatar](/Image/lab926.png)
- Enter wildrydesDashboardPolicy in Name.
- Select Create policy

### View unicorn status on the dashboard
- Open the Unicorn Dashboard.
- Enter the Cognito Identity Pool ID and select Start.
![avatar](/Image/lab927.png)
- Validate that you can see the unicorn on the map.
![avatar](/Image/lab928.png)
- Click on the unicorn to see more details from the stream.
![avatar](/Image/lab929.png)

### Experiment with the producer
- Stop the producer by pressing Control + C and notice the messages stop and the unicorn disappear after 30 seconds.
- Start the producer again and notice the messages resume and the unicorn reappear.
- Hit the (+) button and click New Terminal to open a new terminal tab.
- Start another instance of the producer in the new tab. Provide a specific unicorn name and notice data points for both unicorns in consumer’s output:: ./producer -name Bucephalus
![avatar](/Image/lab930.png)
- Check the dashboard and verify you see multiple unicorns.
![avatar](/Image/lab931.png)

## Aggregate data

### Create an Amazon Kinesis stream
- Go to the AWS Management Console, click Services then select Kinesis under Analytics.
- Select Get started if prompted with an introductory screen.
- Select Create data stream.
- Enter wildrydes-summary into Kinesis stream name and 1 into Number of shards, then select Create Kinesis stream.
- Whithin 60 seconds, your Kinesis stream will be ACTIVE and ready to store the real-time streaming data.
![avatar](/Image/lab932.png)
 
### Create an Amazon Kinesis Data Analytics application
- Switch to the tab where you have your Cloud9 environment open.
- Run the producer to start emiting sensor data to the stream.
- Go to the AWS Management Console, click Services then select Kinesis under Analytics.
- Select Create analytics application.
- Enter wildrydes into the Application name and then select Create application.
![avatar](/Image/lab933.png)
![avatar](/Image/lab934.png)
- Select Connect streaming data.
- Select wildrydes from Kinesis stream.
![avatar](/Image/lab935.png)
- Scroll down and click Discover schema, wait a moment, and ensure that schema was properly auto-discovered.
![avatar](/Image/lab936.png)
- Select Save and continue.
- Select Go to SQL editor. This will open up an interactive query session where we can build a query on top of our real-time Amazon Kinesis stream.
- Select Yes, start application. It will take 30-90 seconds for your application to start.
- Copy and pase the following SQL query into the SQL editor:
```SQL
CREATE OR REPLACE STREAM "DESTINATION_SQL_STREAM" (
  "Name"                VARCHAR(16),
  "StatusTime"          TIMESTAMP,
  "Distance"            SMALLINT,
  "MinMagicPoints"      SMALLINT,
  "MaxMagicPoints"      SMALLINT,
  "MinHealthPoints"     SMALLINT,
  "MaxHealthPoints"     SMALLINT
);

CREATE OR REPLACE PUMP "STREAM_PUMP" AS
  INSERT INTO "DESTINATION_SQL_STREAM"
    SELECT STREAM "Name", "ROWTIME", SUM("Distance"), MIN("MagicPoints"),
                  MAX("MagicPoints"), MIN("HealthPoints"), MAX("HealthPoints")
    FROM "SOURCE_SQL_STREAM_001"
    GROUP BY FLOOR("SOURCE_SQL_STREAM_001"."ROWTIME" TO MINUTE), "Name";
```
- Select Save and run SQL. Each minute, you will see rows arrive containing the aggregated data. Wait for the rows to arrive.
![avatar](/Image/lab938.png)
- Click the Console link.
- Select Connect to a destination.
![avatar](/Image/lab940.png)
 - Select wildrydes-summary from Kinesis stream.
 - Select DESTINATION_SQL_STREAM from In-application stream name.
 ![avatar](/Image/lab940.png)
 - Select Save and continue.
 
 ### Read messages from the stream
 -  Switch to the tab where you have your CLoud9 environment opened.
- Run the consumer to start reading sensor data from the stream: ./consumer -stream wildrydes-summary
 ![avatar](/Image/lab941.png)
 
 ### Experiment with the producer
- Switch to the tab where you have your Cloud9 environment opened.
- Stop the producer by pressing Control + C and notice the messages stop.
- Start the producer again and notice the messages resume.
- Hit the (+) button and click New Terminal to open a new terminal tab.
- Start another instance of the producer in the new tab. Provide a specific unicorn name and notice data points fo rboth unicorns in 
 ![avatar](/Image/lab942.png)
 
 ## Process streaming data
 
 ### Create an Amazon DynamoDB tables
 -  Go to the AWS Management Console, choose Services then select DynamoDB under Database.
  ![avatar](/Image/lab943.png)
 - Click Create table.
 - Enter UnicornSensorData for the Table name.
 - Enter Name  for the Partition key and select String for the key type.
 - Tick the Add sort key checkbox. Enter StatusTime for the Sort key and select String for the key type.
 ![avatar](/Image/lab944.png)
 - Leave the Use default settings box checked and choose Create.
 ![avatar](/Image/lab945.png)
 - Scroll to the Table details section of your new table's properties and note the Amazon Resource Name (ARN). You will use this in the next step.
 
 ### Create an IAM role for your Lambda function
 -  From the AWS Console, click on Services and then select IAM in the Securit, Identiy & Compliance section.
 - Select Policies from the left navigation and then click Create policy.
 - Using the Visual editor, we're going to create an IAM policy to allow our Lambda function access to the DynamoDB table created in the last section. To begin, select Service, begin typing DynamoDB in Find a service, and click DynamoDB.
 - Select Action, begin typing BatchWriteItem in Filter actions, and tick the BatchWriteItem checkbox.
 - In Region, enter the AWS Region in which you created the DynamoDB table in the previous section, e.g.: us-east-1.
 - In Account, enter your AWS Account ID which is a twelve digit number, e.g.: 123456789012. To find your AWS account ID number in the AWS Management Console, click on Support in the navigation bar in the upper-right, and then click Support Center. Your currently signed ID appears in the upper-right corner below the Support menu.
 - In Table Name, enter UnicornSensorData.
 - Select Add.
 ![avatar](/Image/lab946.png)
 - Select Review policy.
 - Enter WildRydesDynamoDBWritePolicy in the Name field.
 ![avatar](/Image/lab947.png)
 - Select Create policy.
 - Select Roles from the left navigation and then select Create role.
 ![avatar](/Image/lab949.png)
 - Select Next: Permissions.
 - Begin typing AWSLambdaKinesisExecutionRole in the Filter text box and check the box next to that role.
 - Begin typing WildRydesDynamoDBWritePolicy in the Filter text box and check the box next to that role.
 - Clikc Next: Review.
 - Enter WildRydesStreamProcessorRole for the Role name.
  ![avatar](/Image/lab950.png)
  - Click Create role.
  
  ### Create a Lambda function to process the stream
  - Go to the AWS Management Console, choose Service then select Lambda under Compute.
  ![avatar](/Image/lab951.png)
  - Select Create a function.
  - Enter WildRydesStreamProcessor in the Name field.
  - Select Node.js 6.10 from Runtime.
  - Select WildRydesStreamProcessorRole from the Existing role dropdown.
  - Select Create function.
  ![avatar](/Image/lab952.png)
  - Scroll down to the Function code section.
  - Copy and paste the JavaScript code below into the code editor.
  ```SQL
  'use strict';

const AWS = require('aws-sdk');
const dynamoDB = new AWS.DynamoDB.DocumentClient();
const tableName = process.env.TABLE_NAME;

exports.handler = function(event, context, callback) {
  const requestItems = buildRequestItems(event.Records);
  const requests = buildRequests(requestItems);

  Promise.all(requests)
    .then(() => callback(null, `Delivered ${event.Records.length} records`))
    .catch(callback);
};

function buildRequestItems(records) {
  return records.map((record) => {
    const json = Buffer.from(record.kinesis.data, 'base64').toString('ascii');
    const item = JSON.parse(json);

    return {
      PutRequest: {
        Item: item,
      },
    };
  });
}

function buildRequests(requestItems) {
  const requests = [];

  while (requestItems.length > 0) {
    const request = batchWrite(requestItems.splice(0, 25));

    requests.push(request);
  }

  return requests;
}

function batchWrite(requestItems, attempt = 0) {
  const params = {
    RequestItems: {
      [tableName]: requestItems,
    },
  };

  let delay = 0;

  if (attempt > 0) {
    delay = 50 * Math.pow(2, attempt);
  }

  return new Promise(function(resolve, reject) {
    setTimeout(function() {
      dynamoDB.batchWrite(params).promise()
        .then(function(data) {
          if (data.UnprocessedItems.hasOwnProperty(tableName)) {
            return batchWrite(data.UnprocessedItems[tableName], attempt + 1);
          }
        })
        .then(resolve)
        .catch(reject);
    }, delay);
  });
}
  ```
 ![avatar](/Image/lab953.png)
 -  In the Environment variable section, enter an environment variable with Key TABLE_NAME and Value UnicornSensorData.
 ![avatar](/Image/lab955.png)
 - In the Basic settinggs section. Set the Timeout to 1 minute.
 ![avatar](/Image/lab954.png)
 - Scroll up and select Kinesis from the Designer section
 - In the Configure triggers section, select wildrydes-summary from Kinesis Stream.
 - Leave Batch size set to 100 and Starting position set to Latest.
 - Select Enable trigger
  ![avatar](/Image/lab957.png)
 - Select Add.
  ![avatar](/Image/lab956.png)
  - Select Save.
  
  ### Monitor the Lambda function
  - Run the producer to start emiting sensor data to the stream with a unicorn name : ./producer -name Rocinante
  - Select the Monitor tab and eplore the metrics available to monitor the function. Select Jump to Logs to explore the function's log output.
   ![avatar](/Image/lab959.png)
   
  ### Query the DynamoDB table
  - Select Services then select DynamoDB in the Database section.
  - Select Tables from the left-hand navigation.
  - Select UnicornSensorData.
  - Select the Items tab. Here you should see each per-minute data point for each Univorn for which you're running a producer.
  ![avatar](/Image/lab960.png)
  
  ## Store & query data
  
  ### Create an Amazon S3 bucket
  - From the AWS Management Console select Services then select S3 under Storage.
  - Select + Create bucket.
  - Provide a globally unique name for your bucket such as wildeydes-data-yourname.
  ![avatar](/Image/lab961.png)
  - Select the region you've been using for your bucket.
  - Select Next twice, and then select Create bucket.
  
  
  ### Create an Amazon Kinesis Data Firehose delivery stream
  - From the AWS Management Console select Services then select Kinesis under Analytics.
  - Select Create delivery stream.
  - Enter wildrydes into Delivery stream name.
  - Select Kinesis stream as Source and select wildrydes as the source stream.
  ![avatar](/Image/lab962.png)
  -  Select Next.
  - Leave Record transformation and Record format conversation disabled and select Next.
  - Select Amazon S3 from Desitation.
  - Choose the bucket you crerated in the previous section (i.e. wildrydes-data-johndoe) from S3 bucket.
  ![avatar](/Image/lab963.png)
  - Select Next.
  - Enter 60 into Buffer interval under S3 Buffer to set the frequency of S3 deliveries once per minute.
  - Scroll down to the bottom of the page and select Create new or Choose from IAM role. In the new tab, click Allow.
  ![avatar](/Image/lab964.png)
  - Select Next. Review the delivery stream details and select Create delivery stream.
  ![avatar](/Image/lab965.png)
  
  
  ### Create an Amazon Athena table
  
  - Select Services then select Athena in the Analytics section.
  ![avatar](/Image/lab966.png)
  - If prompted, select Get started and exit the first-run tutorial by hitting the x in the upper right hand corner of the modal dialog
  - Copy and paste the following SQL statement to create the table. Replace the YOUR_BUCKET_NAME_HERE placeholder with your bucket name (e.g. wildrydes-data-johndoe) in the LOCATION clause:
  ```SQL
  CREATE EXTERNAL TABLE IF NOT EXISTS wildrydes (
       Name string,
       StatusTime timestamp,
       Latitude float,
       Longitude float,
       Distance float,
       HealthPoints int,
       MagicPoints int
     )
     ROW FORMAT SERDE 'org.apache.hive.hcatalog.data.JsonSerDe'
     LOCATION 's3://YOUR_BUCKET_NAME_HERE/';
  ```
  ![avatar](/Image/lab967.png)
  - Select Run Query.
  - Verify the table wildrydes was crerated by ensuring it has been added to the list of tables in the left navigation.
  ![avatar](/Image/lab968.png)
  
  
  ### Explore the batched data files
  - Select Services then select S3 in the Storage section.
  - Enter the bucket name you created in the first section in the Search for buckets text input.
  - Select one of the files and select Download. Open the file with a text editor and explore its content.
  ![avatar](/Image/lab969.png)
  
  ### Query the data files
  - Select Services then select Athena in the Analytics section.
  - Copy and paste the following SQL query:
  ```SQL
  SELECT * FROM wildrydes
  ```
  - Select Run Query.
  ![avatar](/Image/lab970.png)
  
  ## Clean Up
  - Clean Amazon Athena
  ![avatar](/Image/lab971.png)
  - Clean Kinesis Data firehose
  ![avatar](/Image/lab972.png)
  - Clean S3
  ![avatar](/Image/lab973.png)
  - Clean Lambda
  ![avatar](/Image/lab974.png)
  - Clean DynamoDB
  ![avatar](/Image/lab975.png)
  - Clean IAM
  ![avatar](/Image/lab976.png)
  
