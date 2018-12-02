# Intro to S3
## Create a Bucket
- In the <strong>AWS Management Console</strong>, on the <strong>Services</strong> menu, click <strong>S3</strong>.
- Click <strong>+Create bucket</strong> then configure:
![avatar](/Image/lab21.png)
> - <strong>Bucket name</strong>: mybucket19950314
> - Replace <strong>NUMBER</strong> with a random number
> - Leave <strong>Region</stron> at its default value
> ![avatar](/Image/lab23.png)
- Click Next
- Read the short description for the categories listed.
- For <strong>Versioning</strong>, Select <strong>Keep all versions of an object in the same bucket</strong>.
![avatar](/Image/lab24.png)
- Click Next
- Examine the <strong>Manage users</strong> section.
- Examine the <strong>Manage public permissions</strong> section.
![avatar](/Image/lab25.png)
- Click Next
- Review the setting and then click <strong>Create bucket</strong>

## Upload an Object to the Bucket

- Right-click this link and download the picture to computer
- In the <strong>S3 Management Console</strong>, click bucket that starts with the name: mybucket.
- Click Upload
![avatar](/Image/lab27.png)
- At the <strong>Select files</strong>, click <strong>Add files</strong> then configure:
![avatar](/Image/lab28.png)

## Make Your Object Public 

- Click the <strong>Sheep.jpg</strong> file.
- Copy the S3 <strong>Link</strong> displayed at the bottom of the window.
![avatar](/Image/lab29.png)
- Open a new web browser tab, paste the link into the address filed, and hit enter.
![avatar](/Image/lab211.png)
- In the <strong>S3 management Console</strong>, click the Permissions tab, then configure.
![avatar](/Image/lab212.png)
- Return to the browser tab that displyed <strong>Access Denied</strong> and refresh the page.
![avatar](/Image/lab214.png)

## Create a Bucket Policy

- Right -click this link and download the picture to your computer: Eiffel.jpg
- In the S3 Management Console tab, click the name of bucket at the top of the window
- Click Upload and use the same upload process to upload the Eiffel.jpg file.
- Click on the Eiffel.jpg name.
- Copy the S3 Link displyed at the bottom of the window.
- Click the <strong>Permissions</strong> tab.
- In the Permissions tab, click Bucket Policy
![avatar](/Image/lab213.png)
- Copy the <strong>ARN</strong> of your bucket to the clipboard. Itis displayed at the top of the policy editor.
- Click the <strong>Policy generator</strong> link at the bottom of the page.
- In the <strong>AWS Policy Generator</storng> window, configure the following:
> - Select Type of Policy: S3 Bucket Policy
> - Principal: *
> - Actions:GetObject
> - <strong>Amazon Resource Name(ARN): Past the ARN that previously copied.
> - At the end of the ARN, append /*
> ![avatar](/Image/lab217.png)
- Click <strong>Add Statement</strong>
- Click <strong>Generate Policy</strong>
![avatar](/Image/lab218.png)
- Copy the policy to clipboard.
- Close the web browser tab and return to the web browser tab with the <strong>Bucket policy edit</strong>.
- Paste the bucket policy into the <strong>Bucket policy editor</strong>.
![avatar](/Image/lab220.png)
- Click <strong>Save</strong>
- Return to the browser tab that displyed <strong>Access Denied</strong> and refresh the page.
![avatar](/Image/lab219.png)

## Explore Versioning 
- Right-click this lilnk and save the picture to your computer using the same name:
- In the S3 Management Console, click <strong>Overview</strong>
- Click Upload.
- Go to the browser tab that has the picture of the Eiffel tower.
- Take note of the contentsof the picture, then refresh the page.
- Click <strong>Latest version</strong>
- Click <strong>Open</strong>
