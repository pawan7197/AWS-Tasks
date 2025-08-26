## VPC Peering Lab: AjaVPC ↔ IbmVPC
## Project Overview:

This lab demonstrates how to create and configure VPC Peering between two VPCs (AjaVPC and IbmVPC) in the same AWS account and same region, allowing EC2 instances in both VPCs to communicate with each other using private IP addresses.



Create two VPCs (AjaVPC and IbmVPC)

Launch EC2 instances in each VPC

Configure VPC Peering

Allow ICMP (ping) communication over private IP addresses

## Lab Steps:
## 1. Create AjaVPC:

Navigate to VPC → Your VPCs → Create VPC

Name: AjaVPC

IPv4 CIDR: 10.0.0.0/16

Create Public Subnet: 10.0.1.0/24

Create and attach Internet Gateway to AjaVPC

Update Route Table:

Destination: 0.0.0.0/0

Target: Internet Gateway (IGW)

## 2. Create IbmVPC:

Navigate to VPC → Your VPCs → Create VPC

Name: IbmVPC

IPv4 CIDR: 192.168.0.0/16

Create Public Subnet: 192.168.1.0/24

Create and attach Internet Gateway to IbmVPC

Update Route Table:

Destination: 0.0.0.0/0

Target: Internet Gateway (IGW)

## 3. Launch EC2 Instances:

Launch EC2 instances in each VPC using Amazon Linux 2 AMI:

VPC	Instance Name	Subnet	Security Group Rules
AjaVPC	EC2-A	10.0.1.0/24	Allow SSH (22), ICMP (Ping)
IbmVPC	EC2-B	192.168.1.0/24	Allow SSH (22), ICMP (Ping)

Make sure Security Groups allow inbound ICMP and SSH.

## 4. Create VPC Peering Connection:

Navigate to VPC → Peering Connections → Create Peering

Name: Aja-to-Ibm

Requester VPC: AjaVPC (10.0.0.0/16)

Accepter VPC: IbmVPC (192.168.0.0/16)

Click Create Peering Connection

## 5. Accept Peering Request:

Go to VPC → Peering Connections

Select the newly created peering connection

Click Actions → Accept Request

## 6. Update Route Tables:

AjaVPC Route Table:

Destination: 192.168.0.0/16

Target: Peering Connection (pcx-xxxx)

IbmVPC Route Table:

Destination: 10.0.0.0/16

Target: Peering Connection (pcx-xxxx)

## 7. Update Security Groups:

EC2-A Security Group (AjaVPC):

Inbound Rule: Type ICMP (Echo Request), Source: 192.168.0.0/16

EC2-B Security Group (IbmVPC):

Inbound Rule: Type ICMP (Echo Request), Source: 10.0.0.0/16

## 8. Test Connectivity:

SSH into EC2-A

Run:
```

ping <Private-IP-of-EC2-B>

```

You should receive successful ping replies 🎉

Optional: Cross-Region Peering

Same steps apply, except:

VPCs must be in different regions

Ensure cross-region peering is selected

Update route tables and security groups accordingly

## Verification Checklist:

 VPCs created with correct CIDR ranges

 EC2 instances launched and reachable

 Peering connection created and accepted

 Routes updated for both VPCs

 ICMP allowed in Security Groups

 Successful ping between EC2-A and EC2-B

## Key Learnings:

VPC Peering enables private network communication across VPCs

Proper route table updates and security group rules are essential

Peering connections are non-transitive (works only between two VPCs directly peered)

## Technologies Used:

**AWS VPC**

**AWS EC2**

**VPC Peering**

**Security Groups**

**Routing**

## Images:
## 1.IBM-VPC-STACK:

<img width="1600" height="900" alt="Image" src="https://github.com/user-attachments/assets/31ca76e4-7d99-452d-8596-89152d9eadce" />

## 2.VPCs

<img width="1600" height="900" alt="Image" src="https://github.com/user-attachments/assets/4c00471c-1962-408c-90d7-197d85f6d8ed" />

## 3.AJA VPC

<img width="1600" height="900" alt="Image" src="https://github.com/user-attachments/assets/ba5d801d-eaa5-44a1-b2ff-bf5c276d3d66" />

## 4. IBM VPC

<img width="1600" height="900" alt="Image" src="https://github.com/user-attachments/assets/05e7b890-11a1-4e8c-9220-b2634a97efe5" />

## 5. SUBNETS

<img width="1600" height="900" alt="Image" src="https://github.com/user-attachments/assets/2e802ddf-3436-4450-9e56-144d5f5b1beb" />

## 6. ROUTE TABLES

<img width="1600" height="900" alt="Image" src="https://github.com/user-attachments/assets/2234029d-400b-412a-b1b6-e07e1c2d9553" />

## 7. INTERNET GATEWAYS

<img width="1600" height="900" alt="Image" src="https://github.com/user-attachments/assets/61375994-a267-43e3-852c-15c768468535" />

## 8. PEERING CONNECTION

<img width="1600" height="900" alt="Image" src="https://github.com/user-attachments/assets/2f9cdcd5-a23f-42f4-b266-934d8038faa2" />

## 9. ACCEPT VPC REQUEST

<img width="1600" height="900" alt="Image" src="https://github.com/user-attachments/assets/29626a6c-3209-44f6-8bff-3be284d34f78" />

## 10. VPC PEERING-STATUS-ACTIVE

<img width="1600" height="900" alt="Image" src="https://github.com/user-attachments/assets/e11ccced-c91f-4064-857c-ba8c913718c5" />

## 11. IBM-DB-RT

<img width="1600" height="900" alt="Image" src="https://github.com/user-attachments/assets/07989e57-3a12-4733-948e-7b53814fc62d" />

## 12. AJA-DB-RT

<img width="1600" height="900" alt="Image" src="https://github.com/user-attachments/assets/9ee30dea-0693-4322-83cf-cc24f5366769" />

## 13. VPC-FILE-PERMISSIONS

<img width="1600" height="900" alt="Image" src="https://github.com/user-attachments/assets/26595cc9-e35a-4310-8c2a-fed67e7beec2" />

## 14. VPC-PEERING-OUTPUT

<img width="1600" height="900" alt="Image" src="https://github.com/user-attachments/assets/cdff0e8f-c019-493c-8b7b-250ed84ea6bc" />
## Clean Up:

To avoid unnecessary charges:

Terminate EC2 instances

Delete VPC peering connection

Delete VPCs and associated resources (IGWs, subnets)

## Conclusion:

This project demonstrates how to set up private communication between two VPCs via VPC Peering.
A foundational skill for multi-VPC architectures, microservices, and hybrid cloud networking.

## Author:

**Pawan Kumar Kothapalli**

**AWS Cloud Practioner**

**Mail-Id:** pawankumarkothapalli22644@gmail.com

**Linkedin-URL:** https://www.linkedin.com/in/pawan-kumar-kothapalli-17865b302/


