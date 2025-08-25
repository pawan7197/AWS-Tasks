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


## Clean Up:

To avoid unnecessary charges:

Terminate EC2 instances

Delete VPC peering connection

Delete VPCs and associated resources (IGWs, subnets)

## Conclusion:

This project demonstrates how to set up private communication between two VPCs via VPC Peering.
A foundational skill for multi-VPC architectures, microservices, and hybrid cloud networking.