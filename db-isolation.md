[`← Previous: Connect EC2 to RDS(MySQL)` ](ec2-rds.md) **.** [`Phase3 Home`](phase3-main.md) **.** [`Home`](./README.md) **.** [`Next: SG chaining (EC2 ↔ RDS) →`](controlled-access.md)

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

* **HTTP (Port 80)** → Source: My IP
* **SSH (Port 22)** → Source: Anywhere IPv4

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

### Screenshots

<details>
<summary><b>1. Custom VPC Infrastructure Deployment</b> </summary>
<img width="1905" height="749" alt="Screenshot 2026-03-06 131439" src="https://github.com/user-attachments/assets/b851dba2-8441-4e4d-a928-061fa4ae1d94" />
</details>

<details>
<summary><b>2. Network Segmentation: 1 Public & 2 Private Subnet Provisioning</b> </summary>
<img width="1913" height="749" alt="Screenshot 2026-03-06 132123" src="https://github.com/user-attachments/assets/ac5ca8df-9735-4894-bdd3-41169abcf7ad" />
</details>

<details>
<summary><b>3. Internet Gateway (IGW) Attachment for Public Access</b> </summary>
<img width="1915" height="752" alt="Screenshot 2026-03-06 132713" src="https://github.com/user-attachments/assets/e03e092a-f026-4d3f-a7e8-992d5ea4a913" />
</details>

<details>
<summary><b>4. Routing Logic: Configuring Public & Private Route Tables</b> </summary>
<img width="1919" height="741" alt="image" src="https://github.com/user-attachments/assets/bbfc9595-c647-415b-a3ba-9ba37ae96a5c" />
<img width="1901" height="746" alt="Screenshot 2026-03-06 134245" src="https://github.com/user-attachments/assets/12b7c3b8-b719-4e8d-8f3f-b81133c21140" />
</details>

<details>
<summary><b>5. Frontend Security: <code>Web-Server-SG</code> Configuration</b> </summary>
<img width="1891" height="748" alt="Screenshot 2026-03-06 135005" src="https://github.com/user-attachments/assets/63da1a34-b514-49dc-8a66-ff1c1bd1e044" />
</details>

<details>
<summary><b>6. Backend Security: <code>RDS-Database-SG</code> Configuration</b> </summary>
<img width="1893" height="758" alt="Screenshot 2026-03-06 145604" src="https://github.com/user-attachments/assets/7fb46a21-42e7-4dbf-a347-541b5aa04940" />
</details>

<details>
<summary><b>7. EC2 Instance Launch</b> </summary>
<img width="1889" height="747" alt="Screenshot 2026-03-06 150448" src="https://github.com/user-attachments/assets/3566bd02-e474-4089-b1fb-eb94f660d38c" />
</details>

<details>
<summary><b>8. Instance Metadata & Verification</b> </summary>
<img width="1883" height="739" alt="Screenshot 2026-03-06 155650" src="https://github.com/user-attachments/assets/1d261592-5ff0-498d-b387-fabe72e3f77a" />
<img width="1908" height="748" alt="image" src="https://github.com/user-attachments/assets/f1683a53-2a79-4101-93b7-fd6e5662df1a" />
</details>

<details>
<summary><b>9. Successful EC2 to RDS (MySQL) Handshake</b> </summary>
<img width="1912" height="1005" alt="Screenshot 2026-03-06 161104" src="https://github.com/user-attachments/assets/47cb2a50-5b8e-4b32-aecd-7cf6c223bce3" />
<img width="1915" height="1004" alt="Screenshot 2026-03-06 181704" src="https://github.com/user-attachments/assets/fc0ee720-7e9e-47ff-97ba-368d018d07fd" />
</details>




[`← Previous: Connect EC2 to RDS(MySQL)` ](ec2-rds.md) **.** [`Phase3 Home`](phase3-main.md) **.** [`Home`](./README.md) **.** [`Next: SG chaining (EC2 ↔ RDS) →`](controlled-access.md)



