## Prepare Data
- Download the datasets
- Sign in to the AWS Management Console and open the Amazon S3 console
![avatar](/Image/lab71.png)
- In the navigation bar, choose <strong>Upload</strong>
- Choose <strong>Add File</strong>
![avatar](/Image/lab72.png)

## Create a Training Datasource
- Open the Amazon Machine Learning console
- Choose <strong>Get started</strong>
- On the <strong>Get started with Amazon Machine Learning</strong> page, choose <strong>Launch</strong>
![avatar](/Image/lab73.png)
- On the <strong>Input Data</strong> page
- Fill the <strong>S3 Location</strong>
![avatar](/Image/lab74.png)
- Choose <strong>Verify</strong>
- In the <strong>S3 permissions</strong> dialog box, choose <strong>Yes</strong>
![avatar](/Image/lab75.png)
- In the <strong>Target</strong> column, select y
![avatar](/Image/lab76.png)
- Choose <strong>Continue</strong>
- choose <strong>Review</strong>
![avatar](/Image/lab77.png)

## Create an ML Model
- For <strong>Training and evaluation settings</strong>, ensure that <strong>Default</strong> is selected.
![avatar](/Image/lab78.png)
- Choose <strong>Review</strong>

## Review the ML Model's Predictive Performance and Set a Score Threshold
- On the ML model summary page, in the ML model report navigation pane, choose Evaluations, 
choose Evaluation: ML model: Banking model 1, and then choose Summary.
- On the Evaluation summary page, review the evaluation summary, including the model's AUC 
performance metric.
![avatar](/Image/lab79.png)
- On the Evaluation Summary page, choose Adjust Score Threshold.
![avatar](/Image/lab710.png)

## Using Amazon ML to Predict Responses to a Marketing Offer
- In the ML model report navigation pane, choose Try real-time predictions.
- Choose Paste a record.
![avatar](/Image/lab712.png)
### To create a batch prediction
- Choose Amazon Machine Leaning, and then choose Batch Predictions
- Choose Create new batch prediction
- On the Ml model for batch predictions page, choose ML model: Banking Data 1. 
Amazon ML displays the ML model name, ID, creation time, and the associated datasource ID.
- Choose Continue
- For Datasource name, type Banking Data 2.
- For S3 Location, type the full location of the banking-batch.csv file: your-bucket/banking-batch.csv.
![avatar](/Image/lab714.png)
- For Does the first line in your CSV contain the column names?, choose Yes.
- Choose Verify.
- Amazon ML validates the location of your data.
- Choose Continue.
- For S3 destination, type the name of the Amazon S3 location where you uploaded the files in Step 1: Prepare Your Data. Amazon ML uploads the prediction results there.
- For Batch prediction name, accept the default, Batch prediction: ML model: Banking Data 1. Amazon ML chooses the default name based on the model it will use to create predictions. In this tutorial, the model and the predictions are named after the training datasource, Banking Data 1.
- Choose Review.
-In the S3 permissions dialog box, choose Yes.
![avatar](/Image/lab715.png)
### To view the predictions
- Choose Amazon Machine Learning, and then choose Batch Predictions.
- In the list of predictions, choose Batch prediction: ML model: Banking Data 1. The Batch prediction info page appears.
- To view the results of the batch prediction, go to the Amazon S3 console at https://console.aws.amazon.com/s3/ and navigate to the Amazon S3 location referenced in the Output S3 URL field. From there, navigate to the results folder, which will have a name similar to s3://aml-data/batch-prediction/result.
- Download the prediction file to your desktop, uncompress it, and open it.
![avatar](/Image/lab716.png)
