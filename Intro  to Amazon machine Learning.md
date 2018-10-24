# Introduction to Amazon Machine Learnig

## Upload Training Data
- Right-click this link and download the file restaurants.data.
- In the <strong>AWS Management Console</strong>, click <strong>Service</strong> and then click <strong>S3</strong>.
![avatar](/Image/lab61.png)
- Click <strong>Create bucket</strong>, then configure:
> - <strong>Bucket name</strong>:data1995
> - Replace <strong>NUMBER</srong> with a random number
> - Copy the anme of bucket to text editor
> - Click <strong>Create</strong>
> ![avatar](/Image/lab62.png)
- Upload the restaurants.data file into new bucket by doing the following:
![avatar](/Image/lab64.png)

## Create a Datasource
- In the <strong>Service</strong> menu, click </strong>Machine Learning</strong>.
- Click <strong>Get start</strong>
![avatar](/Image/lab65.png)
- Click <strong>View Dashboard</strong>
![avatar](/Image/lab66.png)
- Click <strong>Create new...?Datasource and ML model</strong>
![avatar](/Image/lab67.png)
- Click <strong>Continue</strong>
- For <strong>Does the first line in your CSV contain the column names?</strong>
- Select rating
![avatar](/Image/lab68.png)

## Create an ML Model form the Datasource
- Review the <strong>ML model settings</strong> page.
- Click <strong>Review</strong>
![avatar](/Image/lab69.png)
- Click <strong>Create ML model</strong>
- In the top-left of the window, click <strong>Amazon Machine Learning</strong> and then click <strong>Dashboard</strong>
![avatar](/Image/lab611.png)

## Evaluate an ML Model
- Click Refresh every 60 seconds util the staus of the Evaluation row is <strong>Completed</strong>.
![avatar](/Image/lab613.png)
- Click <strong>Evaluation: ML model: Restaurants.dat</strong>
- Click <strong>Explore model performance</strong>
![avatar](/Image/lab614.png)

## Generate Predictions Form Your ML Model
- In the top-left of the window, click <strong>Amazon Machine Learning</strong> and then click <strong>ML models</strong>
- Click the displayed ML model.
![avatar](/Image/lab616.png)
- Under <strong>Predictions</strong> click <strong>Try real-time predictions</strong>
![avatar](/Image/lab617.png)
- Enter the following data into the form:
> - age: under_19
> - gender: male 
> - budget: under_20
> - price: over_50
> - cuisine_type: Continental
![avatar](/Image/lab618.png)
- Click <strong>Create prediction</strong>
![avatar](/Image/lab620.png)


