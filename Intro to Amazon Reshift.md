# Intro to Amazon Reshift

## Launch an Amazon Redshift Cluster
- In the <strong>AWS Management Console</strong>, on the <strong>Services</strong> menu, click <strong>Amazon Redshift</strong>
- Click <strong>Launch cluster</strong> to open the Redshift Cluster Creation Wizard
![avatar](/Image/lab31.png)
- On the <strong>CLUSTER DETAILS</strong> page, configure:
> - Cluster identifer:lab
> - Database name: labdb
> - Master user name: master
> - Master user password: Redshift123
> - Confirm password: Redshift123
> ![avatar](/Image/lab33.png)
- Click <strong>Continue</strong>
![avatar](/Image/lab34.png)
- Click <strong>Continue</strong>
- At the <strong>ADDITIONAL CONFIGURATION</strong> page, configure:
> - Choose a VPC: Select the other VPC
> - VPC security groups: Redshift Security Group
> - Avalable roles: Redshift-Role
> ![avatar](/Image/lab35.png)
- Leave all other settings at their default value and click <strong>Continue</strong>
- Click <strong>Launch cluster</strong>
![avatar](/Image/lab36.png)
- Click <strong>Close</strong>
![avatar](/Image/lab37.png)

## Launch Pgweb to Communicate with your Redshift Cluster

- Open a new tab in web browser, paste the IP Address and hit Enter.
![avatar](/Image/lab38.png)
- Enter the following information:
> - Host:lab.c3uxk4gpn3xo.us-east-2.redshift.amazonaws.com
> - Username: kevin
> - Password: Redshift123
> - Database: labdb
> - Port: 5439
- Click <strong>Connect</strong>

## Create a Table

- Using the SQL command:
```SQL
CREATE TABLE users (
  userid INTEGER NOT NULL,
  username CHAR(8),
  firstname VARCHAR(30),
  lastname VARCHAR(30),
  city VARCHAR(30),
  state CHAR(2),
  email VARCHAR(100),
  phone CHAR(14),
  likesports BOOLEAN,
  liketheatre BOOLEAN,
  likeconcerts BOOLEAN,
  likejazz BOOLEAN,
  likeclassical BOOLEAN,
  likeopera BOOLEAN,
  likerock BOOLEAN,
  likevegas BOOLEAN,
  likebroadway BOOLEAN,
  likemusicals BOOLEAN
);
```
- Click the <strong>Run Query</strong> button to execute the SQL script
- Click the users table, then click the <strong>Structure</strong> tab

## Load Sample Data from Amazon S3

- In Pgweb, click the <strong>SQL Query</strong> tab at the top of the window.
- Delete the exiting query, then past this SQL command into Pgweb:
```SQL
COPY users FROM 's3://awssampledbuswest2/tickit/allusers_pipe.txt'
CREDENTIALS 'aws_iam_role=YOUR-ROLE'
DELIMITER '|';
```
- To the left of the instructions currently reading, copy the value for Role.
- Paste the Role into Pgweb query, <strong>replacing the text*Role*.
- Click the <strong>Run Query</strong> button to execute the SQL comman.
- Click the users table and then click the Rows tab.

## Query Data
- Return to the <strong>SQL Query</strong>
- Run the query script:
```SQL
SELECT COUNT(*) FROM users;
```
- Run the query:
```SQL
SELECT userid, firstname, lastname, city, state
FROM users
WHERE likesports AND NOT likeopera AND state = 'OH'
ORDER BY firstname;
```
- Run the query:
```SQL
SELECT
  city,
  COUNT(*) AS count
FROM users
WHERE likejazz
GROUP BY city
ORDER BY count DESC
LIMIT 10;
```
