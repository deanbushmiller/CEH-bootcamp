# Completely new way to build lab 20220828
## old way is at bottom
# Penetration Testing AWS Lab Environment Deployment Guide
	You will not need to install any software locally to run this lab.
	Open a plaintext editor like notepad or ultra edit
	You will need an AWS account and a creditcard on file with Amazon.
	These resources are updated and changed regularly.
	VERSION: 20220715.1


## 12 minute video walk-thru of lab setup https://vimeo.com/731196164

### AWS account
	To build your AWS account consider using a non-work / disposable email adddress and disposable credit card.
	You cannot use a one-time use email address.
	https://portal.aws.amazon.com/billing/signup#/start/email

### Choose a region

	When deploying this solution, you should perform all of the steps in the same AWS region. 
	In order track costs easily this lab should not be a region where you perform actual business.
	Run this test first:
	https://cloudpingtest.com/aws
		This will determine your closest region.
		>200 ms is going to slow your lab down.

* Choose a region close to your geographic location to deploy the solution. 
* In the AWS Console, the region you have selected is shown in the top right.

### Create SSH keypair in EC2

Follow the steps [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/create-key-pairs.html#having-ec2-create-your-key-pair) 
https://console.aws.amazon.com/ec2/v2/#KeyPairs
This is used to create an SSH key pair for connecting to the attacker machine in advanced lab setups.
Name your key 'pentestlab' and append today's date, Example 'pentestlab19991231'
Copy the name to text editor
Windows users = .ppk
The key will automatically download - save it for later use.

### Copy 1 attacker and 2 victim machine AMIs (total of 3)

The attacker instance is a Kali Linux VM, which is based on Debian Linux. The victims are virtual machines derived from the [Metasploitable3](https://github.com/rapid7/metasploitable3) project. 

Dean Bushmiller is hosting public AMIs in the us-east-1 region in AWS, which you will need to copy into your own AWS account in order to use with this solution.

1. Login to the AWS Console with your AWS account credentials
2. In the top navigation, to the right of the search bar, click the "shell" icon that looks like a terminal prompt to launch CloudShell (it will take a few moments to initialize the environment)
3. Run the following three commands to copy the public AMI's into your account

`aws ec2 copy-image --name kali-linux --source-image-id ami-0e0c5931cfadd2102 --source-region us-east-1`

`aws ec2 copy-image --name metasploitable3-linux --source-image-id ami-0b186198cc048aa9d --source-region us-east-1`

`aws ec2 copy-image --name metasploitable3-windows --source-image-id ami-02a92b6ee54981f06 --source-region us-east-1`

Copy the names to text editor

ADVANCED TRICK: you can run all three at once by adding a space && space between them. If you use an editor without line wrap this will BREAK.

> `aws ec2 copy-image --name kali-linux --source-image-id ami-0e0c5931cfadd2102 --source-region us-east-1 && aws ec2 copy-image --name metasploitable3-linux --source-image-id ami-0b186198cc048aa9d --source-region us-east-1 && aws ec2 copy-image --name metasploitable3-windows --source-image-id ami-02a92b6ee54981f06 --source-region us-east-1`


**Important: Each command will output an _ImageId_.  YOUR ImageId is NOT typically the orginal ImageId. You need to copy these 3 to a local text file and keep them for the deployment steps below.**

## Deployment Guide:

This solution is provided as a CloudFormation template in YAML format. The template can be used to deploy the solution the CloudFormation console within AWS.

1. Login to the AWS Console
2. Go to the CloudFormation service
3. Click Create Stack > With New Resources (standard)
4. Give the stack a name and append today's date, Example 'pentestlab19991231' 
5. For template source, https://ceh-v11-20220609.s3.amazonaws.com/20220715-LAB-Pentest/pentestlab.yml
  _This may be turned off until class time_
6. For step 2 fill in the parameters (see reference below)
7. For step 3 it is not nessessary to Configure stack options (Next)
8. For step 4 scroll to bottom: you must CHECK I acknowledge that AWS CloudFormation might create IAM resources.
9. Create stack

### Parameter Reference

- AttackerAMIId: The AMI ID of the attacker image created above
- LinuxVictimAMIId: The AMI ID of the Linux victim image created above
- WindowsVictimAMIId: The AMI ID of the Windows victim image created above
- PublicIpAddress: Your public IP address.
  This can be acquired by searching https://whatismyipaddress.com/ . Note: this must be an IPv4 address
- SSHKeyPair: An SSH keypair created in the EC2 console for use with this solution.

### Next Steps

It will take several minutes for the resources to be created, but once it has completed you will have the following resources created in your account:

- 1 VPC with a public subnet (10.0.0.0/24)
- 1 Kali Linux attacker instance (Public IP: generated on launch, Private IP: 10.0.0.4)
- 1 Linux victim instance (10.0.0.10)
- 1 Windows victim instance (10.0.0.21)


### Connecting to attacker using Session Manager

Once the stack is built, you can connect directly in your browser using AWS Session Manager. 
Follow the steps [here](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager-working-with-sessions-start.html#start-ec2-console) in the EC2 Console to connect.

_Tip: The default session is not a full login shell, so running 'bash' once the session is started will provide a better experience._

## Cleaning Up
When you are done using the solution, you will want to tear down the resources you built in order to prevent unwanted costs in your AWS account.

### You will CONTINUALLY incur charges from AWS if you DO NOT clean up
Stopping instance will REDUCE charges and allow you to do the lab on your own.

2 phases:
- CloudFormation phase
1. Go to AWS CloudFormation console, https://console.aws.amazon.com/cloudformation/home
2. Select the stack you built previously and click Delete. 
3. This will delete all resources for the solution (except the three copied AMIs; see below)

- AMI phase
To delete the copied AMIs:
1. Go to the EC2 Console > AMIs
2. Find the three AMIs that were created earlier with the copy commands and deregister them
3. After deregistering the AMIs, go to Snapshots in the EC2 Console
4. There will be three snapshots associated with the deleted AMIs that you can delete

At this point, your account is clear of all resources created by this solution.

## Advanced versions
Advanced versions of this lab allow for SSH & RDP connections. 
Software installation is required to use an SSH client like Putty or RDP client like Royal TSX
You must support your own setup in this case.

# classroom feedback tool FREE use the browser version only
## Most O' students have security controls in place that limit access to sites from a computer & all students have a personal mobile device
## Test on you mobile device you use for class: www.menti.com
### Use the browser on your phone or open a second desktop  browser and point it at the URL sent in the chat by the producer

# FILES
## They are not perfect, if you have constructive ideas on improvement email me.
## You do not need these files to attend class.
## I do make changes and trim down these files at class time due to the compressed schedule 


# OLD WAY 4 days student links to files stored on AWS update
## You must have virtualbox or vmware installed and running
## You must support your own networking
## Download the kali image https://www.kali.org/get-kali/#kali-virtual-machines
### Configure networking for 2 NICs: 1 internal, 1 internet
## Download - 10GB of data (watch your download speed) 2 victims
### https://ceh-v11-20220609.s3.amazonaws.com/CEHv11-metasploitable3-win2k8.ova
### https://ceh-v11-20220609.s3.amazonaws.com/Metasploitable3-ub1404.ova
### images will be accessible 6/10 to 6/17 but not durring class. After 6/17 you must build them yourself.
## Or build metasploitable3 yourself https://github.com/rapid7/metasploitable3
### Configure networking for 1 NIC: 1 internal (sames as kali) ensure Virtual sniffing

# This github is for 2 different classes: 2-Day Bootcamp = what you must know to pass. 4-Day Bootcamp What you must do to pass.
## 2-day Knowing = Glossary/notecards, Readings. You can read on your once you understand the depth and focus of the exam.
## 4-day Doing = Understanding and apply concept in a lab. You can do the activities of Ethical hacking once you know the process and the tools.


## 2021-06-08 - PLEASE NOTE you can get much more if you email ask for an account on my vmlt.com site
### In the spirit of hacking: You must do some recon and find my email address to get an account.
### Your message must have
### a subject line: o'iwantmyCEH
### a body containing: first,last name, country
### I resever the right to reject any request for any reason and not tell you the reason.

# CEH-bootcamp 
## 2 versions of setup
## These only work if you have administrative control over your computer
## They will not work on a Tablet or Chromebook
## 1 Profesional video setup process overview: https://vimeo.com/471972833
## 2 Minimal to follow along (get Kali)
	A. If you can support docker: docker pull kalilinux/kali
	B. If you can support Virtualization: https://www.kali.org/docs/virtualization/
	C. If none of this is possible you must purchase a lab / or just watch (you will not pass if you do not do labs)
		#1. 6 months:  ECC $200 complete -best for CEHv11 exam takers
		#2. 3hrs per day FREE OR $19 Per month:  Offensive Security’s Proving Grounds: https://www.offensive-security.com/labs/individual/
# CEH classroom feedback tool FREE use the browser version only
## Most O' students have security controls in place that limit access to sites from a computer & all students have a personal mobile device
## Test on you mobile device you use for class: www.menti.com
## Way to play along
### EASY: open your phone's camera and point at the QRCODE when your instructor shows it on the screen
### Use the browser on your phone or opena second desktop  browser and point it at the URL sent in the chat by the producer

# On a per topic basis this course has: 
##  A. What information you need to know for the CEH v11 exam (knowledge) = readings
##  B. What you need to be able to do (tasks with tools) = labs
##  C. What and how a professional does penetration testing (skills) = practices and context

# FILES
## They are not perfect, if you have constructive ideas on improvement email me.
## You do not need these files to attend class.
## I do make changes and trim down these files at class time due to the compressed schedule of covering a 40-hour class in 16 hours / (8hrs for 2-day BC)
## These files are meant as a START to your CEH exam preparation
## There are many links in the mindmaps to O' books so that can focus on GREAT readings
## You must learn and study the details yourself
## You must do the labs on your own

## Practice harder than you compete and you will win/pass
## I am your coach for the high jump of the CEH 11 exam
## I can show you how to train and help you adjust when you are off course
## I cannot jump for you
