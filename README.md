# links to mindmaps
*	These maps will be up durrning class
*	https://20250111-ceh-upclass-plus7-636623.s3.us-east-1.amazonaws.com/MaplinkonAWS.pdf
*	You can get them in PDF format while in class or in the recording
*	Do not not ask for them outside of class
*	This link above is open one day before class and 5 days after
# Ways to build lab for 20250730
*	 https://github.com/deanbushmiller/CEH-bootcamp/wiki/Z-Non-oreilly-way-to-build-lab
*	The new way (below) requires the O'Reilly images to be uploaded ( NOT READY ) 
*	We can build the lab at the beginning of class

# DO NOT DO for 20250730 - 31 class
# AWS Lab Environment Deployment Guide
	You will not need to install any software locally to run this lab.
	You will need an AWS account and a creditcard on file with Amazon.
	This will cost less than two dollars per hour while it is running
	VERSION: 20250109.01
## 9 minute video walk-thru of lab setup & tear down https://vimeo.com/941430484

### AWS account
	To build your AWS account consider using a non-work / disposable email adddress.
	You cannot use a one-time use email address.
	https://portal.aws.amazon.com/billing/signup#/start/email
### Choose a region
*	In order track costs easily deploy in an empty region (where no other machines are deployed).
#### Run this test to determine your closest region:
*	https://cloudpingtest.com/aws
*	Less than 200 ms is optimal.
### Create SSH keypair in EC2
1. Login to the AWS Console
2. In left sevices search type key pairs
3. On right click "create key pair"
 - This is used to create an SSH key pair for connecting to the attacker machine in emergencies.
4. Name your key 'lab' and append today's date, Example 'lab20250109'
 - Windows = .ppk / Everyone else .pem
5. Click create key pairs.
 - The key will automatically download
## Resource Deployment
1. Search for CloudFormation in service
2. On right Click Create Stack > With New Resources (standard)
4. Template source, https://20241231-always-up-rid3031.s3.us-east-1.amazonaws.com/CAP-flag-20250109v5.yml
5. Click Next
6. Fill in the parameters
 - Name stack:
   - Same as key pairs from above
 - PublicIpAddress:
   - Your public IPv4 address. ( https://whatismyipaddress.com/ )
 - SSHKeyPair:
   - key pair you created before will be listed in the drop down
6. Click Next
7. Scroll to bottom: you must CHECK I acknowledge that AWS CloudFormation might create IAM resources.
8. Click (Create stack)
### Wait 5 min
It will take up to 5 minutes for the resources to be created
### Connecting to Guacamole
1. Search for EC2 console at top of AWS interface / click Instances and sub menu Instances / right side will show your running machines
2. Identify the guacamole public IP address
- Name of instance will say "This-Pub-IP-ADDRESS-GUAC"
3. Copy & Paste IP into your browser
4. Login kali with password kali
### Smile your lab is ready

## Cleaning Up
When you are done using the solution, you will want to tear down the resources you built in order to prevent unwanted costs in your AWS account.

### You will CONTINUALLY incur charges from AWS if you DO NOT clean up
Stopping instance will REDUCE charges and allow you to do the lab on your own.

### CloudFormation clean up
1. Go to AWS CloudFormation console, https://console.aws.amazon.com/cloudformation/home
2. Select the stack you built previously and click Delete. 
- This will delete all resources for the solution
- At this point, your account is clear of all resources created by this solution.

# FILES
## They are not perfect, if you have constructive ideas on improvement email me.
## You do not need these files to attend class.
## I do make changes and trim down these files at class time due to the compressed schedule 

