# VPC, Gateways and Private/Public Subnets

## Overview
This project demonstrates how I am able to create a VPC with public and private subnets in different availability zones to ensure fault tolerance. I will also be attaching Internet gateways, NAT gateways to my VPC to ensure internet access.

---

## Objective
- Create a Virtual Private Cloud that hosts multiple public subnets and private subnets that can hold resources such as load balancers and instances)
- Attach an internet gateway
- Attach a NAT gateway
- Create and connect a virtual machine

--

## Implementation Steps

### 1. Creating a VPC
- I went on the AWS console to access the VPC resource. I then created a VPC with the Ipv4 CIDR block 10.0.0.0/16

![Creating VPC](./screenshots/01-create-a-vpc.png)
![VPC Created](./screenshots/01.2-create-a-vpc.png)

### 2. Creating Subnets
- Here I will be making 4 subnets, with both private and public have 2 subnets each. 2 public subnets will be places in 2 different availability zones to ensure fault tolerance and the same will be done for the private subnets. 

![Creating First Subnet](./screenshots/02-creating-public-sub.png)

- My second public subnet intentionally has a different CIDR block and availability zone to my first public subnet.

![Creating Second Subnet](./screenshots/02.1-creating-second-pubsub.png)

- All 4 subnets have been created

![Four Subnets](./screenshots/02.2-four-subnets-created.png)

### 3. Creating Internet Gateway
- I created an internet gateway for internet access and attached it to my VPC

![Creating Internet Gateway](./screenshots/03-attaching-ig-to-vpc.png)
![Attaching Internet Gateway](./screenshots/03.1-confirming-ig-attachment.png)

### 4. Creating NAT Gateway
- I created a NAT gateway attached to my VPC, and placed it in my public subnet

![Creating NAT Gateway](./screenshots/04-connectivity-type.png)

- I set the connectivity type to public because I want my virtual machines to have internet access before allocating an Elastic IP ID

![NAT Gateway Created](./screenshots/04.1-nat-gateway-available.png)

### 5. Route Tables
- I created a new route table and attached it to my VPC

![Route Table Created](./screenshots/05-route-table-created.png)

- I then added routes for internet connectivity via the internet gateway

![Internet Gateway Route](./screenshots/05.1-internet-gateway-route.png)

- I then gave both my public subnets explicit subnet associations on my internet gateway route table

![Public Subnet Associations](./screenshots/05.2-pubsub-associations.png)

- I then created a new route table for my NAT gateway and edited the routes like I did for my internet gateway

- I then placed both my private subnets in my NAT gateway route table

![Private Subnet Associations](./screenshots/05.3-privsub-associationss.png)

### 6. Launching Instances
- I created 2 Instances (Amazon Linux AMI's) within my VPC network and placed them in my private subnets before creating a security group. Inbound rules were set to my IP so not every IP can access my instance

![Creating Instance](./screenshots/06-launching-instance.png)


### 7. Creating Load Balancer
- I created an application load balancer to control traffic of my instances. I then put both my public subnets in 2 different availability zones.

![Creating Load Balancer](./screenshots/07-creating-loadbalancer.png)

- I then created a new security group for my instance and added target groups

![Target Groups](./screenshots/07.1-target-groups.png)

- I edited the inbound rules on my instance security group to communicate my load balancer

![Instance SG Inbound Rules](./screenshots/07.2-instance-inbound-rules.png)

