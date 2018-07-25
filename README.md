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
```
Step 6:
==============================================================
#!/bin/bash
# Please replace "devopsinuse.com"
# at each occurance with your own
# domain name.

kops create cluster \
# this is the name of our cluster \
--name=kops.devopsinuse.com \
# this is S3 bucket on AWS (object storage)
--state=s3://kops.devopsinuse.com \
# Role Based Authorization
--authorization RBAC \
# Actual datacenter in Frankfurt
--zones=ap-south-1 \
# How many NODES we want
--node-count=2 \
# How powerfull EC2 instance we want
--node-size=t2.micro \
--master-size=t2.micro \
# How many MASTERS in k8s cluster we want
--master-count=1 \
# Hosted Zone - we need to create it in advance in AWS Route53
# you have to define your own name
--dns-zone=kops.devopsinuse.com \
# this is the name of output folder where
# kops will generate => terraform code
--out=devopsinuse_terraform \
# target is "terraform" code
--target=terraform \
You can create this key pair files
`ssh-keygen -f ~/.ssh/udemy_devopsinuse`
--ssh-public-key=~/.ssh/udemy_devopsinuse.pub
==============================================================
```

https://github.com/kubernetes/kops/blob/master/docs/aws.md 
 
  
