# AWS Scalable Web Architecture with Auto Scaling & Application Load Balancer  

## Project Overview  

I designed and deployed a highly available and scalable web architecture on AWS using an Application Load Balancer (ALB) and Auto Scaling Group (ASG). This project demonstrates the ability to provision, automate, and troubleshoot distributed infrastructure while following AWS best practices for high availability and fault tolerance.  

The system dynamically scales EC2 instances across multiple subnets and distributes traffic through a load balancer, ensuring reliability and consistent performance.  

## Architecture Summary  

- **Compute:** Amazon EC2 (Amazon Linux 2023)  
- **Scaling:** Auto Scaling Group (ASG)  
- **Load Balancing:** Application Load Balancer (ALB)  
- **Configuration Management:** Launch Template  
- **Networking:** Default VPC with multiple public subnets  
- **Security:** Security Groups with controlled access between ALB and EC2  

## Key Implementation Details  

### Launch Template Configuration  

Created a launch template (**sharuz-web-LT**) to standardize EC2 deployments:  

- Instance type: t3.micro  
- AMI: Amazon Linux 2023  
- Key pair: ph3  
- Security group: EC2-sg
- VPC: Default
- Subnet: Left blank (Auto Scaling Group selects subnets)
- Security Group
       - Name: EC2-sg
       - Inbound rules:
              - SSH (Port 22) → Source: My IP
              - HTTP (Port 80) → initially open, later restricted to ALB-sg

**User Data Automation:**  
Configured instance bootstrapping to automatically install and start a web server:  

```bash
#!/bin/bash
yum update -y
yum install -y httpd
systemctl start httpd
systemctl enable httpd
echo "<h1> Hey this is Auto Scaling EC2 </h1>" > /var/www/html/index.html
```
### Networking Setup  

- Used default VPC  
- Configured two public subnets:  
  - public-sn1  
  - public-sn2 (newly created)  
- I ensured both subnets were associated with the default route  

### Target Group Configuration  

- Name: `ALB-tg`  
- Target type: EC2 instances  
- Protocol: HTTP (Port 80)  

**Health Check Settings:**  
- Protocol: - `HTTP`
- Path: `/` 
- Interval: `30` seconds  
- Healthy threshold: `5`  
- Unhealthy threshold: `2`  

Targets were registered automatically through the ASG.  

### Security Configuration 

**ALB Security Group (ALB-sg):**  
- Inbound: HTTP (80) from 0.0.0.0/0  
- Outbound: Allow all  

### Load Balancer Configuration  

Deployed an internet-facing Application Load Balancer (**sharuz-web-ALB**) to distribute incoming traffic:  

- Listener: HTTP (80) → Forward to target group  
- Subnets: public-sn1 and public-sn2  
- Security group: ALB-sg (HTTP access from internet)  

### Security Configuration (EC2 Update)  

**EC2 Security Group (EC2-sg):**  
- SSH (22) → My IP  
- HTTP (80) → Allowed from ALB-sg  

This ensures that only the load balancer can send web traffic to EC2 instances.  

### Auto Scaling Group Configuration  

Created **sharuz-web-ASG** to manage dynamic scaling:  

- Desired capacity: 2  
- Minimum capacity: 1  
- Maximum capacity: 4  
- Subnets: public-sn1 and public-sn2  
- Health checks: EC2 + ELB  
- Grace period: 300 seconds  
- Launch template: sharuz-web-LT (latest version)  

## Challenges & Troubleshooting  

### 1. ASG Launch Failure (Instance Type Mismatch)  

**Issue:**  
Auto Scaling Group failed to launch instances with error indicating unsupported instance type.  

**Root Cause:**  
Instance type requirements were set to “Specify instance attributes,” allowing AWS to override the launch template and select incompatible instance types.  

**Resolution:**  
Reset configuration to strictly use the launch template, ensuring consistent instance type selection.  

### 2. Capacity Constraints in ASG  

**Issue:**  
ASG initially failed to create due to resource constraints.  

**Resolution:**  
Removed maximum vCPU and memory limits to allow instance provisioning.  

### 3. Unhealthy Instances in Target Group  

**Issue:**  
Instances launched but were marked unhealthy (0 healthy, 2 unhealthy).  

**Error Message:**  
“Instance taken out of service in response to an ELB system check failure.”  

### 4. No Public IP Address on Instances  

**Root Cause:**  
Public subnets were not configured to auto-assign public IPv4 addresses.  

**Resolution:**  
Enabled auto-assignment of public IPv4 on both subnets.  

## Final Outcome  

- Successfully deployed 2 EC2 instances via ASG  
- Instances passed ALB health checks  
- Load balancer distributed traffic correctly  
- Application accessible via ALB DNS  
- Verified connectivity by SSH into both instances  

## Key Skills Demonstrated  

- Auto Scaling Group design and configuration  
- Launch Template management  
- Application Load Balancer setup and routing  
- EC2 provisioning and automation (User Data)  
- AWS networking (subnets, routing, IP addressing)  
- Security group design and least-privilege access  
- Infrastructure troubleshooting and root cause analysis  
