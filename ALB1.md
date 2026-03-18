[`← Previous: Phase4 Home`](phase4-home.md) **.** [`Home`](./README.md) **.** [`Next: Scalable Web Architecture (ALB & ASG)`](aws-auto-scaling-practice.md)

# Application Load Balancing
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

## Compute Layer
### EC2 Instances
Two Amazon Linux EC2 instances were launched.

**`Sharuz-EC2-1`** - Deployed in public-sn1.

**`Sharuz-EC2-2`** - Deployed in public-sn2.

#### Configuration:

 - **VPC:** Default VPC
 - **Auto-assign Public IP:** Enabled
 - **Security Group:** EC2-SG

Public IP addresses allow the instances to access the internet to download packages during setup.

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
 - **Target Type:** Instances
      - **Registered Targets:** `Sharuz-EC2-1` , `Sharuz-EC2-2`

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

## Architecture eveidence (each drops down to a screenshot)

<details> <summary><b>1. Subnets on VPC</b></summary> <img width="1914" height="802" alt="Screenshot 2026-03-12 215721" src="https://github.com/user-attachments/assets/b9d91878-3aa3-4027-b4a1-56be72110d12" /> </details> 

<details> <summary><b>2. Target Group Configuration</b></summary> 
<img width="1448" height="307" alt="image" src="https://github.com/user-attachments/assets/2c6c7aba-2c99-4dce-8376-ac589ed21553" /> 
<img width="1905" height="795" alt="Screenshot 2026-03-12 202351" src="https://github.com/user-attachments/assets/eee3b9e0-651f-4647-8763-55e65b5bb02c" /> 
<img width="1904" height="792" alt="Screenshot 2026-03-12 195302" src="https://github.com/user-attachments/assets/efdb0e4c-5c99-4102-a5ff-f9276acaec48" /> </details>

<details> <summary><b>3. EC2 Security Group</b></summary> <img width="1883" height="748" alt="Screenshot 2026-03-12 215814" src="https://github.com/user-attachments/assets/ea2b9812-fcb4-4310-8cc4-61ac1abd180e" /> 

</details> <details> <summary><b>4. ALB Security Group</b></summary> <img width="1918" height="799" alt="Screenshot 2026-03-12 215845" src="https://github.com/user-attachments/assets/f5fc54f3-e1fb-4558-8c45-1d2c4dd45455" /> </details> 

<details> <summary><b>5. EC2 Instances and the User Data used </b></summary> <img width="1915" height="761" alt="Screenshot 2026-03-12 161257" src="https://github.com/user-attachments/assets/0b9f8801-496a-44c5-896e-c10c1460675b" /> <img width="1905" height="792" alt="Screenshot 2026-03-12 213628" src="https://github.com/user-attachments/assets/ad2fe4cd-22de-4d49-81ea-dfb52a13e2aa" /> <img width="1905" height="801" alt="Screenshot 2026-03-12 215623" src="https://github.com/user-attachments/assets/dbbd2afa-8348-465b-a5c2-c8a7e12934bb" /> </details> 

<details> <summary><b>6. Application Load Balancer Setup</b></summary> <img width="1919" height="749" alt="Screenshot 2026-03-12 212250" src="https://github.com/user-attachments/assets/aea46b79-fc0e-4780-9e83-35cc040793a0" /> <img width="1919" height="745" alt="Screenshot 2026-03-12 215917" src="https://github.com/user-attachments/assets/cd238244-b319-488d-b799-4f76a4dc65b8" /> </details> 

<details> <summary><b>7. Initial Web Access</b></summary> <img width="1907" height="206" alt="Screenshot 2026-03-12 204020" src="https://github.com/user-attachments/assets/385228e0-95c6-4b4f-9397-352a7611cb66" /> </details>

<details> <summary><b>8. Load Balancing in Action</b></summary> <img width="1911" height="197" alt="Screenshot 2026-03-12 211938" src="https://github.com/user-attachments/assets/6c561807-89aa-4267-9d22-96bc1e3a9691" /> </details>

[`← Previous: Phase4 Home`](phase4-home.md) **.** [`Home`](./README.md) **.** [`Next: Scalable Web Architecture (ALB & ASG)`](aws-auto-scaling-practice.md)
