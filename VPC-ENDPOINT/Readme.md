# 🧪 AWS VPC Endpoint Lab

## 🎯 Objective
The goal of this lab is to **enable private access to AWS services (Amazon S3 and AWS Secrets Manager)** from EC2 instances located in a **private subnet** without requiring a NAT Gateway or Internet Gateway.

---

## 🛠️ Architecture Overview

               ┌────────────┐
                │   VPC      │
                │ 10.0.0.0/16│
                └─────┬──────┘
                      │
  ┌────────────────┐  │   ┌────────────────────┐
  │  Public Subnet │──┘   │   Private Subnet    │
  │  10.0.1.0/24   │      │    10.0.2.0/24      │
  └────────────────┘      └─────────┬──────────┘
         |                             |
    [ EC2-A: Bastion ]           [ EC2-B: No public IP ]
                                      |
                           ┌──────────▼─────────┐
                           │ Gateway Endpoint   │
                           │     (S3)           │
                           └────────────────────┘
                           ┌──────────▼─────────┐
                           │ Interface Endpoint │
                           │ (Secrets Manager)  │
                           └────────────────────┘
markdown
---

## **Lab Setup & Implementation**

### **Part 1: VPC & Subnets Setup**

1. **Create a VPC**
   - **Name:** `VPC-Endpoint-Lab`
   - **CIDR Block:** `10.0.0.0/16`

2. **Create Subnets**
   - **Public Subnet:** `10.0.1.0/24`
   - **Private Subnet:** `10.0.2.0/24`

3. **Create & Attach Internet Gateway**
   - **Name:** `IGW-Lab`
   - Attach IGW to your VPC.

4. **Configure Route Tables**
   - **Public Route Table:**
     - Add route: `0.0.0.0/0 → Internet Gateway`
     - Associate with **Public Subnet**.
   - **Private Route Table:**
     - No internet route yet.
     - Associate with **Private Subnet**.

---

### **Part 2: Launch EC2 Instances & Test**

1. **Launch EC2-A (Bastion Host in Public Subnet)**
   - **AMI:** Amazon Linux 2
   - **Public IP:** Enabled
   - **Security Group:** Allow SSH (port 22)

2. **Launch EC2-B (Private Subnet)**
   - **AMI:** Amazon Linux 2
   - **Public IP:** Disabled
   - **Security Group:** 
     - Allow SSH from EC2-A
     - Allow HTTPS (port 443)

3. **Access Configuration**
   - SSH into **EC2-A**.
   - From **EC2-A**, SSH into **EC2-B** using its private IP.

---

### **Part 3: Gateway Endpoint for Amazon S3**

1. **Create an S3 Bucket**
   ```
   aws s3 mb s3://vpc-endpoint-lab-<your-name>
   ```
**Verify Access from EC2-B (Expected Failure)**

```
aws s3 ls
```
Expected: Fails due to no internet/NAT.

Create Gateway Endpoint for S3

Navigate: VPC → Endpoints → Create Endpoint

Name: S3GatewayEndpoint

Service: com.amazonaws.<region>.s3

Type: Gateway

Attach to Private Route Table
(Automatically adds prefix-list route for S3)

## Verify Access Again:

```
echo "test" > test.txt
aws s3 cp test.txt s3://vpc-endpoint-lab-<your-name>/
```
Expected: Success via private connection.

## Part 4: Interface Endpoint for AWS Secrets Manager
**Create a Secret in Secrets Manager**

Name: MyTestSecret

Key/Value:

username: admin

**Create Interface Endpoint**

Navigate: VPC → Endpoints → Create Endpoint

Name: SecretsManagerEndpoint

Service: com.amazonaws.<region>.secretsmanager

Type: Interface

Subnet: Private Subnet

Enable Private DNS

Attach security group allowing HTTPS (443) from EC2-B

**Verify Secrets Manager Access from EC2-B**


aws secretsmanager get-secret-value --secret-id MyTestSecret
Expected: Success via VPC Interface Endpoint.

## Images:


## Cleanup (Optional)
To avoid unnecessary costs:

Terminate EC2 instances.

Delete VPC Endpoints (S3 & Secrets Manager).

Delete S3 bucket contents and bucket.

Delete Secrets Manager secret.

Delete VPC and related resources.

## Key Takeaways
Gateway Endpoints: Used for S3/DynamoDB, adds route in the route table.

Interface Endpoints: Used for other AWS services, creates ENIs in subnets.

Provides private connectivity without NAT or Internet Gateway.

Use Cases
Highly secure environments with no internet access.

Compliance-driven architectures.

Reducing NAT Gateway cost for private resources.
## Author:

**Pawan Kumar Kothapalli**

**AWS Cloud Practioner**



**Mail-Id:** pawankumarkothapalli22644@gmail.com

**Linkedin-URL:** https://www.linkedin.com/in/pawan-kumar-kothapalli-17865b302/

