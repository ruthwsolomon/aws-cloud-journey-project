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

### Networking Setup  

- Used default VPC  
- Configured two public subnets:  
  - `public-sn1`  
  - `public-sn2` (newly created)  
- I ensured both subnets were associated with the default route
  
### Launch Template Configuration  

Created a launch template `sharuz-web-LT` to standardize EC2 deployments:  

- Instance type: t3.micro  
- AMI: Amazon Linux 2023  
- Key pair: ph3  
- VPC: Default
- Subnet: Left blank (Auto Scaling Group selects subnets)
- Security group: EC2-sg
  - Inbound rules:
  1. SSH (Port 22) → Source: My IP
  2. HTTP (Port 80) → initially open, later restricted to ALB Security Group `ALB-sg`. This ensures that only the load balancer can send web traffic to EC2 instances.  

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
### Target Group Configuration  

- Name: `ALB-tg`  
- Target type: Instances  
- Protocol: HTTP (Port 80)
- VPC: Default VPC 

**Health Check Settings:**  
- Protocol: - `HTTP`
- Path: `/` 
- Interval: `30` seconds  
- Healthy threshold: `5`  
- Unhealthy threshold: `2`  

Note: Did not manually register targets because the ASG handles registration. 

### Security Configuration 

**ALB Security Group (ALB-sg):**  
- Inbound: HTTP (80) from 0.0.0.0/0  
- Outbound: Allow all  

### Load Balancer Configuration  

Deployed an Application Load Balancer `Sharuz-web-ALB` to distribute incoming traffic:  

- Scheme: Internet-facing
- IP type: IPv4
- Network: Default VPC
- Subnets: `public-sn1` and `public-sn2`
- Security group: `ALB-sg`
- Listener: HTTP (80) → Forward to `ALB-tg`

### Auto Scaling Group Configuration  

Created `Sharuz-web-ASG` to manage dynamic scaling:  

- Desired capacity: 2  
- Minimum capacity: 1  
- Maximum capacity: 4  
- Subnets: `public-sn1` and `public-sn2`
- Target group attached: ALB-tg
- Health checks: EC2 + ELB  
- Grace period: 300 seconds  
- Launch template: `Sharuz-web-LT` (latest version)  

## Challenges & Troubleshooting  

### 1. Capacity Constraints in ASG  

**Issue:**  
ASG initially failed to create due to resource constraints.  

**Resolution:**  
Removed maximum vCPU and memory limits to allow instance provisioning.  

### 2. ASG Launch Failure (Instance Type Mismatch)  

**Issue:**  
Auto Scaling Group failed to launch instances with error indicating unsupported instance type.  

**Root Cause:**  
Instance type requirements were set to “Specify instance attributes,” allowing AWS to override the launch template and select incompatible instance types.  

**Resolution:**  
I reset configuration to strictly use the launch template, ensuring consistent instance type selection.  

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

## Architecture Evidence (Each topic drops down to a screenshot)

<details>
<summary><b>1. Application Load Balancer Output (Live Application)</b></summary>
<img width="1915" height="278" alt="Screenshot 2026-03-17 164306" src="https://github.com/user-attachments/assets/3b56f439-b093-4997-8da7-5bfad6cc20f3" />
</details>
<details>
<summary><b>2. Target Group Health Status</b></summary>
<img width="1901" height="750" alt="Screenshot 2026-03-17 161824" src="https://github.com/user-attachments/assets/1f2ed7d4-0ee7-40c7-b8dd-9a0446ebf04e" />
</details>
<details>
<summary><b>3. Auto Scaling Group Instances</b></summary>
<img width="1892" height="743" alt="image" src="https://github.com/user-attachments/assets/0e89b8a9-af17-477e-ac6a-fa8222314e55" />
</details>
<details>
<summary><b>4. Subnet Configuration (Public IP Enabled)</b></summary>
<img width="1556" height="352" alt="image" src="https://github.com/user-attachments/assets/a111d473-bbc4-477d-8752-a7d959a0540b" />
</details>
<details>
<summary><b>5. Launch Template Configuration</b></summary>
<img width="1891" height="749" alt="image" src="https://github.com/user-attachments/assets/45d554c8-8ca9-4c7a-b243-6109c24073a2" />
</details>
<details>
<summary><b>6. Auto Scaling Activity History (Failure & Recovery)</b></summary>
<img width="1893" height="731" alt="image" src="https://github.com/user-attachments/assets/2b8b3f98-148f-4c28-bf63-d1f21bbe6796" />
<img width="1892" height="705" alt="image" src="https://github.com/user-attachments/assets/2c2b842e-a254-4f06-9640-348d805e4f4f" />
</details>
<details>
<summary><b>7. Security Group Configuration (ALB ↔ EC2)</b></summary>
<img width="1879" height="737" alt="image" src="https://github.com/user-attachments/assets/8af3d88a-e2c9-46f5-99cb-c80ac3a2ac8c" />
<img width="1889" height="739" alt="image" src="https://github.com/user-attachments/assets/8a8bf305-7950-4e65-9d05-a44de7929de0" />
</details>

