## Lauch an Amazon EC2 Instance
- Click Launch Instance to create and configure your virtual machine
![avatar](/Image/lab51.png)
- Find Amazon Linux AMI and click <strong>Select</strong>
![avatar](/Image/lab52.png)
- The default option of t2.micro should already be checked.  This instance type is covered within the Free Tier and offers enough compute capacity to tackle simple workloads. Click Review and Launch at the bottom of the page.
![avatar](/Image/lab5.png)
- Click <strong>Launch</strong> at the bottom of the page.
![avatar](/Image/lab53.png)
- Select Create a new key pair and give it the name <strong>MyKeyPair</strong>. Next click the Download Key Pair button
![avatar](/Image/lab55.png)
- Click <strong>View Instances</strong> on the next screen to view your instances and see the status of the instance have just started.
![avatar](/Image/lab56.png)
- Right click on desktop (not on an icon or file) and select Git Bash Here to open a Git Bash command promp
- Enter ssh -i 'c:\Users\yourusername\.ssh\MyKeyPair.pem' ec2-user@{IP_Address} (ex. ssh -i 'c:\Users\adamglic\.ssh\MyKeyPair.pem' ec2-user@52.27.212.125)
![avatar](/Image/lab58.png)
- Back on the EC2 Console, select the box next to the instance you created.  Then click the Actions button, navigate to Instance State, and click Terminate.
![avatar](/Image/lab59.png)
