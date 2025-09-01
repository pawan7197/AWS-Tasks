## Lab: Deploy EC2 Instances with Application Load Balancer

##  Introduction

In this lab, we will deploy two EC2 instances across two Availability Zones, install and configure Apache HTTPD web server with a sample application, and then create an Application Load Balancer (ALB) to distribute incoming traffic across the servers. This ensures high availability and scalability for web applications.

## Lab Objectives

Launch EC2 instances across two AZs.

Configure HTTPD and deploy a sample application.

Create an Application Load Balancer (ALB).

Configure a Target Group and register EC2 instances.

Validate traffic distribution via ALB DNS.

##  Prerequisites

AWS account with access to EC2 and Load Balancer services.

Basic knowledge of Linux commands.

Git installed on EC2 instances to pull application code.

## Step-by-Step Guide

## Step 1: Launch EC2 Instances
Log in to AWS Management Console.

Navigate to EC2 → Launch Instance.

Configure the following:

Name: AppServer1, AppServer2

AMI: Amazon Linux 2

Instance Type: t2.micro (Free tier eligible)

Key Pair: Select existing or create new

Security Group: Allow SSH (22) and HTTP (80)

Storage: Default (8GB or more)

Launch instances in different Availability Zones for redundancy.

## Step 2: Configure Web Servers (Apache + Application)
Install Apache HTTPD:
```
sudo yum update -y
sudo yum install -y httpd
```
Start and enable Apache:
```
sudo systemctl start httpd
sudo systemctl enable httpd
```
Install Git and clone application code:
```
sudo yum install -y git
sudo git clone https://github.com/Ai-TechNov/mario.git /var/www/html/
```
Verify application is running: 

Navigate to
```
http://<EC2_PublicIP> 
```
in a browser




Step 3: Create Application Load Balancer

Navigate to EC2 → Load Balancers → Create Load Balancer.

Select Application Load Balancer.

Configure the following:

Name: AppLoadBalancer

Scheme: Internet-facing

IP type: IPv4

VPC: Default VPC (or custom)

Availability Zones: Select subnets where EC2s are deployed

Security Group: Allow HTTP (80) and SSH (22)

Listener: HTTP on port 80

Step 4: Create Target Group

Navigate to Target Groups → Create Target Group.

Configure:

Name: AppTargetGroup

Target Type: Instances

Protocol: HTTP

Port: 80

IP type: IPv4

VPC: Default VPC

Protocol version: HTTP1

Health Checks: Path /, Protocol HTTP, Port 80

Register targets: Select both EC2 instances and include them.

Step 5: Attach Target Group to Load Balancer

Navigate to your Application Load Balancer.

Under Listeners → Rules, select the created Target Group.

Save configuration.


Step 6: Test Load Balancer

Once ALB is deployed and active, note the DNS name generated.

Open a browser and navigate to:
```
http://<ALB_DNS_Name>
```

Refresh multiple times to confirm round-robin traffic distribution between EC2 instances.
## Images

1.App1 Server
<img width="1589" height="718" alt="Image" src="https://github.com/user-attachments/assets/ab193052-c780-47c4-b8bf-f653d5874bb8" />

2. App1 output Image
<img width="1586" height="706" alt="Image" src="https://github.com/user-attachments/assets/d976ee8c-ed99-4627-9f07-cb5930bc1fe7" />

3. App2 server
<img width="1585" height="704" alt="Image" src="https://github.com/user-attachments/assets/5447a2f2-e4c8-4da5-a5ec-c398664f6b47" />

4. App2 output
<img width="1588" height="708" alt="Image" src="https://github.com/user-attachments/assets/ea2c6f03-b62e-405d-8a1b-23a3dd343356" />

5. AWS Target Group
<img width="1599" height="702" alt="Image" src="https://github.com/user-attachments/assets/ace85ffa-83e9-4cc8-a77e-de3b88c6f0b0" />

6. Application Loadbalancing
<img width="1594" height="703" alt="Image" src="https://github.com/user-attachments/assets/8554ad9a-2550-464a-9d6e-64adbd313a0e" />

7.Loadbalancer output
<img width="1599" height="726" alt="Image" src="https://github.com/user-attachments/assets/6aa7c1cf-323d-41ff-bec9-18e56c66ee44" />


Cleanup


Terminate EC2 instances.

Delete Load Balancer.

Delete Target Group.

Remove unused Security Groups and Key Pairs.

✅ Lab Completed: Successfully deployed EC2 instances, configured Apache with a sample app, and set up an Application Load Balancer to distribute traffic.

## Author: 

**Pawan Kumar Kothapalli**

**AWS Cloud Practioner**

**Mail-Id:** pawankumarkothapalli22644@gmail.com

**Linkedin-URL:** https://www.linkedin.com/in/pawan-kumar-kothapalli-17865b302/
