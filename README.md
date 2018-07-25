# devops
Step 1.
# RedHat like systems
sudo yum install python2-pip
sudo yum install python2-pip
sudo pip install awscli
sudo pip3 install awscli

windows -> https://docs.aws.amazon.com/cli/latest/userguide/awscli-install-windows.html

Step 2.
aws-user-details
go to path -> \home\<user>\.aws
1. config 
   [default]
   region = ap-south-1
   output = JSON
2. credentials
   [default]
    aws_access_key_id = XXXXXXXXXXXXXXX
    aws_secret_access_key = XXXXXXXXXXXXXXXXXX
    
Step 3: Installing kubectl binanry -> refer net for the same
Step 4: Installing kops binary -> refer net
Step 5: Installing tereform

Step 6:
==============================================================
#!/bin/bash
# Please replace "devopsinuse.com"
# at each occurance with your own
# domain name.
kops create cluster \
8 # this is the name of our cluster \
9 --name=kops.devopsinuse.com \
10 # this is S3 bucket on AWS (object storage)
11 --state=s3://kops.devopsinuse.com \
12 # Role Based Authorization
13 --authorization RBAC \
14 # Actual datacenter in Frankfurt
15 --zones=eu-central-1a \
16 # How many NODES we want
17 --node-count=2 \
18 # How powerfull EC2 instance we want
19 --node-size=t2.micro \
20 --master-size=t2.micro \
21 # How many MASTERS in k8s cluster we want
22 --master-count=1 \
23 # Hosted Zone - we need to create it in advance in AWS Route53
24 # you have to define your own name
25 --dns-zone=kops.devopsinuse.com \
26 # this is the name of output folder where
27 # kops will generate => terraform code
28 --out=devopsinuse_terraform \
29 # target is "terraform" code
30 --target=terraform \
31 # You can create this key pair files
32 # `ssh-keygen -f ~/.ssh/udemy_devopsinuse`
33 --ssh-public-key=~/.ssh/udemy_devopsinuse.pub
==============================================================


 
 
  
