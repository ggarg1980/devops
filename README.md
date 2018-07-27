```
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

Step:7
kops validate cluster 

Step 8
--> kubectl get nodes

Step 9:
//Create deployment
kubectl create deployment my-nginx-deployment image=nginx 

// How to expose deployment via service
kubectl expose deployment my-nginx-deployment --port=80 --type=NodePort --name=my-nginx-service

kubectl get pods
kubectl get svc




kubectl get pod,svc
kubectl edit service <<service_name>>

kubectl create configmap <<config_map_name>> --from-file=/<path>/<to>/<some>/<location>/data

//to get config maps
kubectl get cm 

kubectl describer cm <<config_map_name>>

kubectl create -f <filename>.yaml 
kubectl apply -f deployment_file.yaml

kubectl logs nginx-deployment-object -f 

kubectl exec -it nginx-deployment-object --bash

kubectl get deploy,pod,svc,cm

kubectl delete pod <<pode>>

kubectl create -f pod-helloword.ym

kubectl describe pod helloworld.com

//rc - replication controller (old version)
kubectl scale --replicas=4 -f helloworld-controller.yml (file based)
kubectl get rc
kubectl scale --replicas=4 -f rc/helloworld-controller (name based)
kubectl delete rc/helloworld-controller

//Replication Set -> Advance version 

//Deployments -> Great version
kubectl create -f deployment/helloworld.yml
kubectl get deployments
kubectl get rs
kubectl get pods
kubectl get pods --show-labels
kubectl rolout status deployment/helloworld-deployments
kubectl expose deployment helloworld-deployment --type=NodePort (Service Creation)
kubectl set image deployment/helloworld-deployment k8s-demo=ggarg/k8s-demo:2
kubectl rollout status deployment/helloworld-deployment
kubectl get pods

kubectl rollout undo deployment/helloworld-deployment

kubectl rollout undo deployment/helloworld-deployment --to-revision=3

kubectl edit deployment/helloworld-deployment

kubectl rollout undo deployment/helloworld-deployment --to-revision=3

kubectl edit deployment/helloworld-deployment

kubectl label nodes node1 hardware=high-spec
kubectl label nodes node2 hardware=low-spec
kubectl get nodes --show-labels

//build docker file based on Dockerfile
docker build . 
docker build -t your-login/docker-demo . 


//pushing the image to docker hub for example my login-id is -> ggarg so that means -> ggarg/docker-1
docker login
docker tag imageid your-login/docker-demo
docker push your-login/docker-demo

//build
sudo docker build -t ggarg/loyalty:v1 .

//DOCKER FILE
FROM openjdk:8-jdk-alpine
COPY ./target/restful-web-bank-0.0.1-SNAPSHOT.jar restful-web-bank-0.0.1-SNAPSHOT.jar
EXPOSE 9100
ENTRYPOINT ["java","-jar","restful-bank-loyalty-0.0.1-SNAPSHOT.jar"]


Loyalty.yml
--
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: loyalty-deployment
spec:
  replicas: 3
  template:
    metadata:
      labels:
        app: loyalty-app
    spec:
      containers:
      - name: loyalty-app
        image: ggarg/loyalty
        ports:
        - name: nodejs-port
          containerPort: 9100
--
apiVersion: v1
kind: Service
metadata:
  name: loyalty-svc
spec:
  ports:
  - port: 31001
  	nodePort:31001
  	targetPort:nodejs-port
    protocol: TCP
  selector:
    app: loyalty-app
  type: NodePort
  
  
kubectl get pods -o wide
kubectl exec loyalty-deployment-78b4f754ff-jsbgm -- printenv | grep SERVICE
kubectl get services kube-dns --namespace=kube-system
kubectl run curl --image=radial/busyboxplus:curl -i --tty

730  sudo docker build -t ggarg/bank:v1 .
  731  sudo docker push ggarg/bank:v1
  732  sudo docker build -t ggarg/bank:v1 .
  733  mvn clean  package
  734  sudo docker build -t ggarg/bank:v1 .
  735  sudo docker push ggarg/bank:v1
  736  kops create cluster --name=kops2.itseasy.k8s.local --state=s3://kops-state-ggarg --authorization RBAC --zones=ap-south-1a --node-count=2 --node-size=t2.micro --master-size=t2.micro --master-count=1 --dns-zone=kops2.itseasy.k8s.local --ssh-public-key=~/.ssh/id_rsakey.pub --yes
  737  kops validate cluster
  738  kubectl get pods





```

https://github.com/kubernetes/kops/blob/master/docs/aws.md 
 
  
