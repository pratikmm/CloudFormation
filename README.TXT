#AWS Cloud Formation Assignment

##Objective: To create a CloudFormation template to provision the following resources:
1) EC2 instance
2) S3 bucket
3) CFT
4) IAM

##Prerequeisite
To create the CF stack using CFT you will need to have IAM user (Console access or Access key and id).

##Overview
Using this CFT we are creating following AWS resources.
1.VPC
2.Internet Gateway
3.Public Subnet and route table.
4.IAM Role with s3* permissions
5.S3 bucket with bucket policy to allow access to only IAM role.
6.EC2 instance to which the Role is connected.
7.Configuring packages on Ubuntu 14.04 ec2 instance using User-Data.
8.Accessing S3 bucket files from EC2 instance.

##Assumptions/Hardcoded values
1.VCP and Subnet CIDR. Currently its 10.35.0.0/16. If you already have VPC in your AWS account with this CIDR please update the JSON for both CIDRs(VPC and Subnet).
2.This CFT will create stack only in us-east-1a zone, since its hardcoaded in configuration file.
3.This CFT is using Ubuntu 14.04 HVM AMI (AMI id: ami-841f46ff).
4.Instance type of eC2 instance(t2.micro)

##User-Data operations.
1.Perform apt-get update
2.Install apache webserver change its default port 80 to 8090.
3.Install AWS CLI to perform S3 bucket operations
4.Create a file and upload to S3 bucket.
5.Fetch same file from S3 bucket place it at /var/www/ location. (index.html)
6.Restart apache server.


##Deployment
There are two ways by which this CFT can be deployed to create stack.

###AWS management Console
1.Copy CFT JSON, click on Create stack in AWS CF and upload it CloudFormation dash board .
2.After the JSON andformat of CFT is verified click next, check the box to create IAM related resources.
3.After the execution is completed, under output tab you will get the URL to access apache server's index page.

###Command line.
1.Configure  the AWS access key and ID.
2.Copy CFT JSON or upload it to S3 bucket.
3.User follwiong Command to create stack(File path can be given as per CFT location)
PROMPT> aws cloudformation create-stack --stack-name myteststack --template-body file:///filemame.json





