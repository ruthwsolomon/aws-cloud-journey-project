# Application Load Balancing (AWS High Availability Architecture)
I designed and deployed a highly available web architecture in AWS using an **Application Load Balancer (ALB)** to distribute traffic across multiple EC2 instances running in different Availability Zones. 
The goal of this project was to demonstrate how **load balancing improves application availability and reliability** by ensuring that user requests are automatically distributed across multiple servers.
To strengthen security, the architecture uses **security group referencing (security group chaining)** so that EC2 instances accept web traffic only from the load balancer and not directly from the internet.

## Architecture Components

- **Amazon VPC** - Provides an isolated network environment for AWS resources.
- **Public Subnets** - Host the EC2 instances and load balancer across different Availability Zones.
- **Target Group** - Registers EC2 instances and performs health checks.
-  **Application Load Balancer (ALB)** - Distributes incoming web traffic across multiple EC2 instances.
- **Security Groups** - Control traffic between the load balancer and EC2 instances.
- **Amazon EC2**- Compute instances hosting the web application.
- **User Data Script** - Automates the installation and configuration of the web server during instance launch.

## Networking Foundation
### VPC

The project used the Default VPC, which already provides built-in routing and internet connectivity.
This VPC acts as the network boundary where all project resources communicate securely.

## Subnet Segmentation

Two public subnets were used to deploy the application servers across different Availability Zones.

**`public-sn1`** - Hosts the first EC2 instance.

**`public-sn2`** - Hosts the second EC2 instance.

Placing instances in separate Availability Zones improves fault tolerance and high availability. If one zone becomes unavailable, the application can still run in the other zone.

## Security Group Configuration
### Load Balancer Security Group

#### Security Group: `ALB-sg`

**Inbound Rule:**

   - **Type:** HTTP (Port 80)
   - **Source:** 0.0.0.0/0

This allows public web traffic from the internet to reach the load balancer.

### EC2 Instance Security Group

#### Security Group: `EC2-sg`

**Inbound Rules**:

 - **Type:** HTTP (Port 80)
 - **Source:** `ALB-sg`

This configuration uses security group referencing, meaning the EC2 instances only accept traffic coming from the load balancer.

 - **Type:** SSH (Port 22)
 - **Source:** My IP

This rule allows secure administrative access to the instances using an RSA key pair.

#### Configuration:

 - **VPC:** Default VPC
 - **Auto-assign Public IP:** Enabled
 - **Security Group:** EC2-SG

Public IP addresses allow the instances to access the internet to download packages during setup.

## Compute Layer
### EC2 Instances
Two Amazon Linux EC2 instances were launched.

**`Sharuz-EC2-1`** - Deployed in public-sn1.

**`Sharuz-EC2-2`** - Deployed in public-sn2.

#### Automation with User Data

A user data script was used to automatically configure the web server during instance launch.

**This is the script I used:** 

`#!/bin/bash`

`yum update -y`

`yum install -y httpd`

`systemctl start httpd`

`systemctl enable httpd`

`echo "<h1>Hello from Sharuz-EC2-1</h1>" > /var/www/html/index.html`

It installs Apache, starts the web server service, and creates a simple webpage.

**I configured each instance with a different message in the index.html file so the load balancing behavior could be seen easily.**

## Load Balancer Layer

### Target Group : `ALBPractice-tg`

**Configuration:**

**Protocol:** HTTP
 - **Port:** 80
 - **Target Type:** I chose the two instances I created.

The target group acts as a logical container that registers EC2 instances and performs health checks. If an instance fails the health check, the load balancer automatically stops sending traffic to it.

### Application Load Balancer `Practice-alb`

The Application Load Balancer acts as the public entry point for the application.

**Configuration:**

 - **Scheme:** Internet facing
 - **VPC:** Default VPC 
 - **Subnets:** `public-sn1` and `public-sn2`
 - **Security Group:** `ALB-sg`
 - **Listener:** HTTP (Port 80)

The listener forwards incoming requests to **`ALBPractice-tg`** target group, which distributes traffic across the two EC2 instances created.

## Testing the Load Balancer

To verify the architecture, I opened the Application Load Balancer DNS name in a web browser.

After refreshing the page multiple times, the message alternated between: **Hello from Sharuz-EC2-1** and **Hello from Sharuz-EC2-2**

## Result

The test confirmed that the ALB successfully distributed traffic across both EC2 instances located in different subnets.

This demonstrates how load balancing improves application availability by ensuring requests are handled by multiple servers instead of relying on a single instance.

## Key Concepts Demonstrated

- High availability using multiple Availability Zones
- Load balancing with Application Load Balancer
- Security group referencing to restrict instance access
- Health checks for server monitoring
- Automated server configuration using EC2 user data

## Skills Demonstrated

- Amazon VPC networking
- Application Load Balancer configuration
- Target group management
- EC2 deployment
- Security group design
- High availability architecture
