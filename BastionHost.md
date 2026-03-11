# AWS Networking: NAT Gateway vs Internet Gateway (Private Internet Routing)

In this project I built a networking architecture from scratch in AWS to demonstrate **how private resources can securely access the internet without being publicly exposed.** The goal was to understand the difference between **an Internet Gateway (IGW) and a NAT Gateway** and how they are used to control internet connectivity inside a Virtual Private Cloud.

The architecture separates resources into public and private subnets. Instances in the public subnet access the internet directly through an Internet Gateway, while instances in the private subnet route outbound internet traffic through **a NAT Gateway**. This design ensures that private instances can access the internet for updates or package downloads without allowing inbound internet connections.

## Architecture Components

**Amazon EC2** – compute instances used to test network connectivity
**Amazon VPC** – isolated virtual network environment
**Public Subnet** – hosts resources that require direct internet access
**Private Subnet** – hosts internal resources that should not be accessible from the internet
**Internet Gateway (IGW)** – allows public subnet resources to communicate with the internet
**NAT Gateway** – enables outbound internet access for private subnet resources
**Elastic IP Address** – provides a static public IP required for the NAT Gateway
**Route Tables** – control network traffic flow inside the VPC

## Networking Foundation
### VPC Creation
A Virtual Private Cloud was created to isolate the network environment for this architecture.
VPC Name: NATPractice-vpc
CIDR Block: 10.0.0.0/16
This CIDR range provides sufficient address space for multiple subnets and future scaling.

## Subnet Architecture
Two subnets were created to separate internet-facing resources from internal resources.
- Public Subnet : public-sn – 10.0.1.0/24
This subnet hosts the NAT Gateway and public EC2 instances that require direct internet connectivity.
- Private Subnet : private-sn – 10.0.2.0/24
This subnet hosts internal the EC2 instance that should not be accessible directly from the internet.
Instances deployed here do not receive public IP addresses.

## Internet Gateway Configuration
An Internet Gateway named `NATPractice-igw` was created and attached to `NATPractice-vpc`.
This gateway enables internet access for resources located in the public subnet.

NAT Gateway Configuration
A NAT Gateway was created to allow private subnet resources to access the internet without exposing them to inbound traffic.
Steps performed:
- -Allocated an Elastic IP address
- -Created a NAT Gateway
- -Placed the NAT Gateway inside public-sn
- -Attached the Elastic IP to the NAT Gateway

The NAT Gateway acts as a controlled outbound internet access point for private instances.











You successfully logged into the Bastion (10.0.1.250) and then reached out to the Private Instance (10.0.2.232).

The Permission denied (publickey) error happened because the Private Instance is asking, "Where is your key?" and the Bastion doesn't have it.

o fix this, we need to use SSH Agent Forwarding. This allows the Bastion to "borrow" the key from your local Windows machine for a split second to unlock the Private Instance.
