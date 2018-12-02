# Amazon SageMaker
>>https://docs.aws.amazon.com/sagemaker/latest/dg/gs.html
## Setting Up
- Create an S3 Bucket
![avatar](/Image/lab81.png)

## Create an Amazon SageMaker Notebook Instance
- Open the Amazon SageMaker console at https://console.aws.amazon.com/sagemaker/.
![avatar](/Image/lab82.png)
- Choose Notebook instances, then choose Create notebook instance.
> - For Notebook instance name, type ExampleNotebookInstance.
> - For Instance type, choose ml.t2.medium.
> - For IAM role, create an IAM role.
> ![avatar](/Image/lab83.png)
- When the status of the notebook instance is InService, choose Open next to its name to open the Jupyter dashboard.
> ![avatar](/Image/lab84.png)
> ![avatar](/Image/lab85.png)

## Train a Model with a Built-in Algorithm and Deploy It
- Create the notebook.
> - To create a notebook, in the Files tab, choose New, and conda_python3. 
This pre-installed environment includes the default Anaconda installation and Python 3.
> - Name the notebook.
> ![avatar](/Image/lab86.png)
- Copy the following Python code and paste it into your notebook. Add the name of the S3 bucket that you created in 
Step 1: Setting Up, and run the code. The get_execution_role function retrieves the IAM 
role you created at the time of creating your notebook instance.
```Python
from sagemaker import get_execution_role

role = get_execution_role()
bucket = 'bucket-name' # Use the name of your s3 bucket here
```
![avatar](/Image/lab87.png)
-To download the MNIST dataset, copy and paste the following code into the notebook 
and run it:
```Python
%%time
import pickle, gzip, numpy, urllib.request, json

# Load the dataset
urllib.request.urlretrieve("http://deeplearning.net/data/mnist/mnist.pkl.gz", "mnist.pkl.gz")
with gzip.open('mnist.pkl.gz', 'rb') as f:
    train_set, valid_set, test_set = pickle.load(f, encoding='latin1')
```
![avatar](/Image/lab88.png)
- Explore the Training Dataset
```Python
%matplotlib inline
import matplotlib.pyplot as plt
plt.rcParams["figure.figsize"] = (2,10)


def show_digit(img, caption='', subplot=None):
    if subplot == None:
        _, (subplot) = plt.subplots(1,1)
    imgr = img.reshape((28,28))
    subplot.axis('off')
    subplot.imshow(imgr, cmap='gray')
    plt.title(caption)

show_digit(train_set[0][30], 'This is a {}'.format(train_set[1][30]))
```
![avatar](/Image/lab89.png)
- Transform the Train Dataset and Upload It to S3
```Python
%%time
from sagemaker.amazon.common import write_numpy_to_dense_tensor
import io
import boto3

bucket = 'bucket-name' # Use the name of your s3 bucket here
data_key = 'kmeans_lowlevel_example/data'
data_location = 's3://{}/{}'.format(bucket, data_key)
print('training data will be uploaded to: {}'.format(data_location))

# Convert the training data into the format required by the SageMaker KMeans algorithm
buf = io.BytesIO()
write_numpy_to_dense_tensor(buf, train_set[0], train_set[1])
buf.seek(0)

boto3.resource('s3').Bucket(bucket).Object(data_key).upload_fileobj(buf)
```
![avatar](/Image/lab810.png)
- Create an instance of the sagemaker.amazon.kmeans.KMeans class.
```Python
from sagemaker import KMeans

data_location = 's3://{}/kmeans_highlevel_example/data'.format(bucket)
output_location = 's3://{}/kmeans_highlevel_example/output'.format(bucket)

print('training data will be uploaded to: {}'.format(data_location))
print('training artifacts will be uploaded to: {}'.format(output_location))

kmeans = KMeans(role=role,
                train_instance_count=2,
                train_instance_type='ml.c4.8xlarge',
                output_path=output_location,
                k=10,
                data_location=data_location)
```
![avatar](/Image/lab811.png)
- To start model training, call the KMeans estimator's fit method.
```Python
%%time

kmeans.fit(kmeans.record_set(train_set[0]))
```
![avatar](/Image/lab812.png)
- Use the SDK for Python.
```Python
%%time
import boto3
from time import gmtime, strftime

job_name = 'kmeans-lowlevel-' + strftime("%Y-%m-%d-%H-%M-%S", gmtime())
print("Training job", job_name)

images = {'us-west-2': '174872318107.dkr.ecr.us-west-2.amazonaws.com/kmeans:latest',
          'us-east-1': '382416733822.dkr.ecr.us-east-1.amazonaws.com/kmeans:latest',
          'us-east-2': '404615174143.dkr.ecr.us-east-2.amazonaws.com/kmeans:latest',
          'ap-northeast-1': '351501993468.dkr.ecr.ap-northeast-1.amazonaws.com/kmeans:latest',
          'ap-northeast-2': '835164637446.dkr.ecr.ap-northeast-2.amazonaws.com/kmeans:latest',
          'ap-southeast-2': '712309505854.dkr.ecr.ap-southeast-2.amazonaws.com/kmeans:latest',
          'eu-central-1': '438346466558.dkr.ecr.eu-central-1.amazonaws.com/kmeans:latest',
          'eu-west-1': '664544806723.dkr.ecr.eu-west-1.amazonaws.com/kmeans:latest'}
image = images[boto3.Session().region_name]

output_location = 's3://{}/kmeans_lowlevel_example/output'.format(bucket)
print('training artifacts will be uploaded to: {}'.format(output_location))

create_training_params = \
{
    "AlgorithmSpecification": {
        "TrainingImage": image,
        "TrainingInputMode": "File"
    },
    "RoleArn": role,
    "OutputDataConfig": {
        "S3OutputPath": output_location
    },
    "ResourceConfig": {
        "InstanceCount": 2,
        "InstanceType": "ml.c4.8xlarge",
        "VolumeSizeInGB": 50
    },
    "TrainingJobName": job_name,
    "HyperParameters": {
        "k": "10",
        "feature_dim": "784",
        "mini_batch_size": "500"
    },
    "StoppingCondition": {
        "MaxRuntimeInSeconds": 60 * 60
    },
    "InputDataConfig": [
        {
            "ChannelName": "train",
            "DataSource": {
                "S3DataSource": {
                    "S3DataType": "S3Prefix",
                    "S3Uri": data_location,
                    "S3DataDistributionType": "FullyReplicated"
                }
            },
            "CompressionType": "None",
            "RecordWrapperType": "None"
        }
    ]
}


sagemaker = boto3.client('sagemaker')

sagemaker.create_training_job(**create_training_params)

status = sagemaker.describe_training_job(TrainingJobName=job_name)['TrainingJobStatus']
print(status)

try:
    sagemaker.get_waiter('training_job_completed_or_stopped').wait(TrainingJobName=job_name)
finally:
    status = sagemaker.describe_training_job(TrainingJobName=job_name)['TrainingJobStatus']
    print("Training job ended with status: " + status)
    if status == 'Failed':
        message = sagemaker.describe_training_job(TrainingJobName=job_name)['FailureReason']
        print('Training failed with the following error: {}'.format(message))
        raise Exception('Training job failed')

```
- Use the high-level Python library provided by Amazon SageMaker.
```Python
%%time

kmeans_predictor = kmeans.deploy(initial_instance_count=1,
                                 instance_type='ml.m4.xlarge')
```
![avatar](/Image/lab813.png)
- Create an Amazon SageMaker model by identifying the location of model artifacts and the Docker image that contains inference code.
``` Python
%%time
import boto3
from time import gmtime, strftime


model_name = job_name
print(model_name)

info = sagemaker.describe_training_job(TrainingJobName=job_name)
model_data = info['ModelArtifacts']['S3ModelArtifacts']

primary_container = {
    'Image': image,
    'ModelDataUrl': model_data
}

create_model_response = sagemaker.create_model(
    ModelName = model_name,
    ExecutionRoleArn = role,
    PrimaryContainer = primary_container)

print(create_model_response['ModelArn'])
```
- Create an Amazon SageMaker endpoint configuration by specifying the ML compute instances that you want to deploy your model to.
``` Python
from time import gmtime, strftime

endpoint_config_name = 'KMeansEndpointConfig-' + strftime("%Y-%m-%d-%H-%M-%S", gmtime())
print(endpoint_config_name)
create_endpoint_config_response = sagemaker.create_endpoint_config(
    EndpointConfigName = endpoint_config_name,
    ProductionVariants=[{
        'InstanceType':'ml.m4.xlarge',
        'InitialInstanceCount':1,
        'ModelName':model_name,
        'VariantName':'AllTraffic'}])

print("Endpoint Config Arn: " + create_endpoint_config_response['EndpointConfigArn'])
```
- Create an Amazon SageMaker endpoint. This code uses a Waiter to wait until the deployment is complete before returning.
``` Python
%%time
import time

endpoint_name = 'KMeansEndpoint-' + strftime("%Y-%m-%d-%H-%M-%S", gmtime())
print(endpoint_name)
create_endpoint_response = sagemaker.create_endpoint(
    EndpointName=endpoint_name,
    EndpointConfigName=endpoint_config_name)
print(create_endpoint_response['EndpointArn'])

resp = sagemaker.describe_endpoint(EndpointName=endpoint_name)
status = resp['EndpointStatus']
print("Status: " + status)

try:
    sagemaker.get_waiter('endpoint_in_service').wait(EndpointName=endpoint_name)
finally:
    resp = sagemaker.describe_endpoint(EndpointName=endpoint_name)
    status = resp['EndpointStatus']
    print("Arn: " + resp['EndpointArn'])
    print("Create endpoint ended with status: " + status)

    if status != 'InService':
        message = sagemaker.describe_endpoint(EndpointName=endpoint_name)['FailureReason']
        print('Create endpoint failed with the following error: {}'.format(message))
        raise Exception('Endpoint creation did not succeed')

```
![avatar](/Image/lab814.png)

- Get an inference for the 30th image of a handwritten number in the valid_set dataset.
```Python
result = kmeans_predictor.predict(valid_set[0][30:31])
print(result)
```
![avatar](/Image/lab815.png)
- Get inferences for the first 100 images.
```Python
%%time 

result = kmeans_predictor.predict(valid_set[0][0:100])
clusters = [r.label['closest_cluster'].float32_tensor.values[0] for r in result]
```
- Visualize the results
```Python
for cluster in range(10):
    print('\n\n\nCluster {}:'.format(int(cluster)))
    digits = [ img for l, img in zip(clusters, valid_set[0]) if int(l) == cluster ]
    height = ((len(digits)-1)//5) + 1
    width = 5
    plt.rcParams["figure.figsize"] = (width,height)
    _, subplots = plt.subplots(height, width)
    subplots = numpy.ndarray.flatten(subplots)
    for subplot, image in zip(subplots, digits):
        show_digit(image, subplot=subplot)
    for subplot in subplots[len(digits):]:
        subplot.axis('off')

    plt.show()
```
![avatar](/Image/lab816.png)
- Send a request that sends the 30th image in the train_set as input. Each image is a
28x28 (total of 784) pixel image. The request sends all 784 pixels in the image as 
comma-separated values.
```Python
import json

# Simple function to create a csv from our numpy array
def np2csv(arr):
    csv = io.BytesIO()
    numpy.savetxt(csv, arr, delimiter=',', fmt='%g')
    return csv.getvalue().decode().rstrip()

runtime = boto3.Session().client('sagemaker-runtime')

payload = np2csv(train_set[0][30:31])

response = runtime.invoke_endpoint(EndpointName=endpoint_name, 
                                   ContentType='text/csv', 
                                   Body=payload)
result = json.loads(response['Body'].read().decode())
print(result)
```
- Run another test. The following code takes the first 100 images
from the valid_set validation set and generates inferences for them.
This test identifies the cluster that the input images belong to and
provides a visual representation of the result.
```Python
%%time 

payload = np2csv(valid_set[0][0:100])
response = runtime.invoke_endpoint(EndpointName=endpoint_name, 
                                   ContentType='text/csv', 
                                   Body=payload)
result = json.loads(response['Body'].read().decode())
clusters = [p['closest_cluster'] for p in result['predictions']]

for cluster in range(10):
    print('\n\n\nCluster {}:'.format(int(cluster)))
    digits = [ img for l, img in zip(clusters, valid_set[0]) if int(l) == cluster ]
    height = ((len(digits)-1)//5) + 1
    width = 5
    plt.rcParams["figure.figsize"] = (width,height)
    _, subplots = plt.subplots(height, width)
    subplots = numpy.ndarray.flatten(subplots)
    for subplot, image in zip(subplots, digits):
        show_digit(image, subplot=subplot)
    for subplot in subplots[len(digits):]:
        subplot.axis('off')

    plt.show()
```
