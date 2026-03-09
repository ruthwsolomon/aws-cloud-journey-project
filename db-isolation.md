# AWS Multi-Tier Architecture: Database Isolation
## Project Overview
I designed and deployed a production-ready, two-tier architecture in AWS to demonstrate **network isolation**. The goal of this project was to securely connect an Amazon EC2 instance to a MySQL database hosted on Amazon RDS using AWS networking best practices.
The EC2 instance is deployed in a **public subnet**, while the RDS database is placed in **private subnets** to improve security. Access to the database is restricted through **security group rules** that allow MySQL traffic only from the EC2 instance.

## Architecture Components
* **Amazon EC2** – compute instance used to access and interact with the database
* **Amazon RDS (MySQL)** – managed relational database service hosting the application database
* **Amazon VPC** – isolated network environment for AWS resources
* **Public Subnet** – hosts the EC2 instance and allows internet access
* **Private Subnets** – host the RDS database and prevent direct internet access
* **Internet Gateway** – enables internet connectivity for resources in the public subnet
* **Route Tables** – manage traffic routing within the VPC
* **Security Groups** – control network access between EC2 and the RDS database
* **MySQL/MariaDB Client** – installed on EC2 to test the database connection

## Networking Foundation
### VPC Creation
Created a Virtual Private Cloud named **project-vpc** with CIDR block **10.0.0.0/16** to establish a dedicated and isolated network for project resources.

### Subnet Segmentation
Three subnets were created across different availability zones to support a multi-tier architecture.
* **Public Subnet** `public-sn` – 10.0.1.0/24 (Application Layer)
* **Private Subnet 1** `private-sn-1` – 10.0.2.0/24 (Database Layer – AZ A)
* **Private Subnet 2** `private-sn-2` – 10.0.3.0/24 (Database Layer – AZ B)
  
### Internet Gateway
Created an Internet Gateway named **project-igw** and attached it to **project-vpc** to allow internet connectivity for resources in the public subnet.
### Route Tables

Two route tables were configured:

**public-rt**
* Default route `0.0.0.0/0` → `project-igw`
* Associated with `public-sn`
* Allows EC2 internet connectivity
  
**private-rt**
* No internet gateway route
* Associated with `private-sn-1` and `private-sn-2`
* Keeps database subnets isolated

## Security Group Configuration
### EC2 Security Group
Security group: **webEC2-sg**

Inbound rules:

* **SSH (Port 22)** → Source: Anywhere IPv4
* **HTTP (Port 80)** → Source: My IP

This configuration allows administrative SSH access and inbound web traffic.

### Database Security Group
Security group: **dbEC2-sg**

Inbound rules:

* **MySQL/Aurora (Port 3306)**
* Source: **webEC2-sg**

This configuration ensures that **only the EC2 instance** can communicate with the database.

Even if someone had the database credentials, they could not connect unless they were inside the allowed security group.

## Launching Resources
### EC2 Instance
Launched an **Amazon Linux 2023 EC2 instance** named `web-server`.

Network configuration:
* VPC: `project-vpc`
* Subnet: `public-sn`
* Security Group: `webEC2-sg`

### RDS MySQL Database
Created an **Amazon RDS MySQL database instance** named `project-dbEC2`.

Network configuration:
* VPC: `project-vpc`
* Subnets: `private-sn-1`, `private-sn-2`
* Security Group: `dbEC2-sg`
* Public access: **Disabled**

This ensures the database has **no public IP address** and remains accessible only within the VPC.
## Testing the Connection
### Connected to EC2
From Windows PowerShell: using `ssh -i ph3.pem ec2-user@public-ip-address`
### Installed MariaDB Client
I used : `sudo dnf install mariadb105 -y`
### Connected to RDS Database
Using : `mysql -h project-dbec2.ckp220cga86d.us-east-1.rds.amazonaws.com -u DBEC2 -p`

Then i entered the database password when prompted.
### Result
The connection was successfully established, confirming that the EC2 instance could securely communicate with the RDS database within the AWS VPC network.

Exited the session using: `exit`

## Key Security Concepts Demonstrated
* Network isolation using **public and private subnets**
* **Security group referencing** for controlled database access
* Preventing database exposure by disabling **public access**
* Controlled routing through **internet gateways and route tables**

## Skills Demonstrated
* Amazon VPC networking
* Subnet architecture
* Route table configuration
* Security group design
* EC2 deployment
* Amazon RDS configuration
* Secure database connectivity
