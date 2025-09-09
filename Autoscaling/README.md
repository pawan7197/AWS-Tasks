🚀 AWS Auto Scaling Group (ASG) Setup Guide

This repository provides a simple, step-by-step guide to configure an Auto Scaling Group (ASG) in the AWS Console, integrating with an Application Load Balancer (ALB) for scalable and highly available applications.

## Prerequisites 

AWS Account

Existing VPC and Subnets

Application Load Balancer (ALB) with Target Group created

EC2 Key Pair (optional, recommended for SSH)

⚡ Step-by-Step Guide to Configure Auto Scaling Group (ASG)
## Step 1: Open Auto Scaling Console

Go to AWS Console → EC2 → Auto Scaling Groups

Click Create Auto Scaling Group

## Step 2: Create or Select Launch Template

Option A: Select an existing Launch Template

Option B: Create a new Launch Template:

Name: my-launch-template

AMI ID: ami-00ca32bbc84273381

Instance Type: t3.micro

Key Pair: For SSH access (optionnal)

Security Group: Should allow HTTP traffic from the Load Balancer

Save Launch Template

## Step 3: Configure Auto Scaling Group

Name your ASG (AWS-Auto sacling)

Select the Launch Template

Set Version: Latest

## Step 4: Choose Network and Subnets

Select appropriate VPC

Choose multiple Availability Zones (≥2) for high availability

## Step 5: Attach Load Balancer

Attach to Application Load Balancer (ALB)

Select Target Group (created earlier)

This enables automatic registration of instances to ALB

## Step 6: Configure Health Checks

Health check type: Select ELB

Optionally use EC2+ELB for stricter checks

## Step 7: Set Group Size

Minimum Instances: 3

Desired Instances: 3

Maximum Instances: 4

## Step 8: Configure Scaling Policies

Recommended: Target Tracking Policy (e.g., CPU utilization at 50%)

Alternatively, use Step or Simple Scaling Policies (e.g., Add 1 instance if CPU > 70%)

## Step 9: Notifications (Optional)

Add SNS Notifications to alert on scaling events

## Step 10: Add Tags (Optional)

Example Tag:

Key: Name

Value: WebServer-ASG

## Step 11: Review and Create ASG

Validate configuration

Click Create Auto Scaling Group

## Step 12: Test Setup

Generate load (e.g., open multiple browser tabs, run a load testing tool)

Monitor scaling activity and instance count in ASG Dashboard

Verify ALB distributes traffic to new instances

## Images 
1.Instances

<img width="1592" height="707" alt="Image" src="https://github.com/user-attachments/assets/e89aa1d0-2061-48cf-94ff-309db3a2596e" />

2.App1 Instance

<img width="1592" height="733" alt="Image" src="https://github.com/user-attachments/assets/5a0872b6-b842-4f2c-a728-a3d6c09be7bf" />

3. App2 Instance

   <img width="1599" height="707" alt="Image" src="https://github.com/user-attachments/assets/520a50b7-1b61-4491-9e23-88e5d5cda174" />
   
4. Target Group

<img width="1597" height="700" alt="Image" src="https://github.com/user-attachments/assets/ab536b14-9b2a-4774-965b-4b56880c75d4" />
6. Load Balancer

<img width="1596" height="692" alt="Image" src="https://github.com/user-attachments/assets/78aa57af-c1c3-4df5-bf5c-05f88deea7c6" />

7. Launch template

<img width="1599" height="721" alt="Image" src="https://github.com/user-attachments/assets/a60c2f50-46c2-4a91-8536-d9d6e1d4ccd1" />

8. Auto Scaling

<img width="1591" height="720" alt="Image" src="https://github.com/user-attachments/assets/d379c6c9-6e5f-4f60-b8bf-d96078fdcd23" />

9. DNS Name copied

<img width="1289" height="574" alt="Image" src="https://github.com/user-attachments/assets/e6ab69fa-a7b0-4d4a-b752-94a46a735442" />

10. Output1

<img width="1583" height="470" alt="Image" src="https://github.com/user-attachments/assets/9befe193-4ee8-4fcc-9cb9-8487226bcf2a" />

11. Output2

<img width="1599" height="520" alt="Image" src="https://github.com/user-attachments/assets/d6987e74-4f7b-4abc-a91c-ca552fcca83e" />

12. Output3

<img width="1431" height="350" alt="Image" src="https://github.com/user-attachments/assets/faecd3a7-ae84-43af-804e-8f34915c7aa1" />

13. Instance terminated 

<img width="1593" height="578" alt="Image" src="https://github.com/user-attachments/assets/a84cce3b-95ba-4b98-97c1-b0743e987c4f" />

14. Instances added

<img width="1586" height="723" alt="Image" src="https://github.com/user-attachments/assets/c07661fd-e886-4648-a13f-edafd44ae332" />



## Author:
Pawan Kumar Kothapalli

AWS Cloud Practioner

Mail-Id: pawankumarkothapalli22644@gmail.com

Linkedin-URL: https://www.linkedin.com/in/pawan-kumar-kothapalli-17865b302/
