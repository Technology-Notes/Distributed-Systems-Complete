# Introduction to AWS DynamoDB

## Create a New Table
- Click Create table
- For Table name, Type: Music
- For Primary key, type Artist and leave String selected
- Select Add sort key
- Clik Create
![avatar](image/2-1.png)

## Add Data 
- Click the Items tab, then click Create item
- For Artist String, type: Pink Floyd
- For Song String, type: Money
![avatar](image/2-2.png)
- Click Append to create additional attribute
![avatar](image/2-3.png)

## Modify an Existing Item
- Click Psy
- Change the Year from 2011 to 2012
- Click Save
![avatar](image/2-4.png)

## Query the Table 
- Choose Query
- Partition key:Psy
- Sort key: Gangname Style
- Click Start search 
![avatar](image/2-6.png)

## Scan the Data
- Add filter
- Type in the data
![avatar](image/2-7.png)

## Summary
>> From this lab we can learn how to create Dynamodb in aws, and how to append new key. When there are too many data, we can use 
Scan function and Query function to search the data instead of using SQL.

