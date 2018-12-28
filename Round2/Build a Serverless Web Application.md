## Host a Static Website
### Create S3 Bucket
![avatar](image/5-1.png)
- Set the S3 policy
![avatar](image/5-2.png)

## Manage users
- Create an Amazon Cognite User Pool
- Add an App to User Pool
![avatar](image/5-4.png)
![avatar](image/5-5.png)
![avatar](image/5-6.png)

## Serverless Service Backend
- Create an Amazon DynamoDB Table
![avatar](image/5-7.png)
- Create an IAM Role for Your Lambda function
- Set the policy
![avatar](image/5-8.png)

## Create a Lamdba Function for Handling Requests
- Deploy a RESTful API
![avatar](image/5-9.png)
![avatar](image/5-10.png)
- Create a Cognito User Pools Authorizer
![avatar](image/5-11.png)
- Create a new resource and method
![avatar](image/5-12.png)
- Deploy API
![avatar](image/5-13.png)
- Update the Website Config
> Update the invokeUrl setting under the api key in the config.js file. Set the value to the Invoke URL for the deployment stage your created in the previous section.
```
window._config = {


    cognito: {


        userPoolId: 'us-west-2_uXboG5pAb', // e.g. us-east-2_uXboG5pAb         


        userPoolClientId: '25ddkmj4v6hfsfvruhpfi7n4hv', // e.g. 25ddkmj4v6hfsfvruhpfi7n4hv


        region: 'us-west-2' // e.g. us-east-2 


    }, 


    api: { 


        invokeUrl: 'https://rc7nyt4tql.execute-api.us-west-2.amazonaws.com/prod' // e.g. https://rc7nyt4tql.execute-api.us-west-2.amazonaws.com/prod, 


    } 


};
```
