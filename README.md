welcome to my aws project 
here i will describe the step to complete my task
first Create a private repository in Amazon ECR using appropriate documentation 
will maintain the necessary access permissions and authentication configurations for the ECR repository.

Configure Jenkins Agent with EC2:
1. install aws-ec2-fleet plugin 
all the necessary dependencies and tools
2. create ami thet hase:  
a. java
b.docker
c.snyk
d.aws
e.kubectl
f.helm
g.create Launch Templates
h. create sg
i. create asg that containing all the ami ans tLaunch Templates at the right version
j.create role with the right permission and add to asg 
k.create a new ec2 cloud on jenkins GUI
l.create credential for access key and ssh 
m.sea node capacity
n. label
3. check your pipeline with the ec2 agent 
"  agent { label 'osher-ec2-fleet' }"

uploading my html file to s3 bucket and making it available via link:
http://osher-s3-bucket.s3-website.us-east-2.amazonaws.com
1. Set up an Amazon S3 Bucket :osher-s3-bucket
2. upload my html file to s3 bucket using GUI upload
Test and Verify


Migrate Jenkins to EKS
FIRST i create a place for me to doploy a jenkins helm by using: kubectl create namespace osher-jenkins         
then i deploy jenkins helm using:
helm upgrade --install release-jenkins jenkins/jenkins --namespace osher=jenkins 
-f valueov.yaml --set namespaceOverride=osher-jenkins
using the values.yaml:
---
controller:
  serviceType: LoadBalancer  # Expose Jenkins via LoadBalancer service
  admin:
    username: oj          # Updated field for admin username
    password: oj   # Admin password
  JCasC:
    defaultConfig: false

  serviceAnnotations:
    service.beta.kubernetes.io/aws-load-balancer-type: external
    service.beta.kubernetes.io/aws-load-balancer-nlb-target-type: ip
    service.beta.kubernetes.io/aws-load-balancer-scheme: internet-facing

persistence:
  storageClass: gp2          # EBS storage class for persistent volume
  size: 50Gi                 # Persistent volume size
---
Update Jenkinsfile
https://github.com/eldiabloj/ImageProcessingService/blob/main/app/build.jenkinsfile

https://github.com/eldiabloj/polyboy-kubernetes--tampelts/blob/main/jenkins/kubernetes-deploy-nginx.jenkinsfile

https://github.com/eldiabloj/polyboy-kubernetes--tampelts/blob/main/jenkins/kubernetes-deploy.jenkinsfile
 in-side the pip line you can see i use the environment variable
to allow aws access to the eks ,ecr 
and Configure Jenkins to use your AWS credentials


Add a post-build step to your Jenkins job to send an SNS notification
useing aws GUI we go to sns and creating our-on topic for the pipeline my topic alart my to a success or failure,
of the pipelne via email 

deleting old resource and vms 

