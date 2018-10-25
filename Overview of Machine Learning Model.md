# An overview of Amazon SageMaker
## Amazon SageMaker 
- Notebook instance 
> Explore AWS data in note books, and use algorithms to create models via training job
- Jobs
> Defining training jobs
- Models
> Create models for hosting from job ouputs or import externally trained models into Amazon SageMaker
- Endpoint
> Deploy endpoints for developers to use in production. A/B Text model variants.

## Notebook instance
- Create notebook instance
> - Notebook instance name
> - Notebook instance type
> - LAM role
> - VPC -optional
> -Encryption key - optional
- Click Action -> Open
- Defining the parameters for the model

## Trian and Host
- Using implementation of XJ boost
- Setting S3 bucket
- Loading Data
- Converting the data format that AI Gore acquire to VM format
- Defining training Job
- Going to console dashboard to check state
- Building endpoint configuration
- Hosting model on a C for Excel
- Testing

## Just Host
- Using MX net with our own training script
- Bringing  a model outside the sagemaker
- Converting data
- Going to pakage model and copy to s3
- Setting docker
- Creating model by API
- Setting up the endpoint
- Taking pretrained model to container


## Build your own algorithm container
> You can bring your own docker container to perform training and prediciton
- Writing a docker file and build a container
- Pushing container to ECR
- Training with the estimator 
- Deploying it with that predictor object
