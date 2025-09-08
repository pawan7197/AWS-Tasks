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

📌 Key Concepts Summary
Feature	Purpose
Launch Template	Defines how EC2 instances are launched
Auto Scaling Group	Manages instance scaling automatically
Target Group	Tracks instance health for Load Balancer
Cooldown Period	Prevents rapid scaling in/out
Health Checks	Determines if instance should be terminated