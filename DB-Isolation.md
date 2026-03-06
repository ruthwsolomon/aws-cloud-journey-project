# AWS Multi-Tier Architecture: Database Isolation
I designed and deployed a production-ready, two-tier architecture in AWS to demonstrate **Network Isolation**. This project demonstrates how to connect an Amazon EC2 instance to a MySQL database hosted on Amazon RDS using secure AWS networking. The EC2 instance is deployed in a public subnet while the RDS database is placed in private subnets to improve security. The connection is controlled through security group rules that allow database access only from the EC2 instance.
## Infrastructure
- **Amazon EC2** – compute instance used to access and interact with the database
- **Amazon RDS (MySQL)** – managed relational database service hosting the application database
- **Amazon VPC** – isolated network environment for AWS resources
- **Public Subnet** – hosts the EC2 instance and allows internet access
- **Private Subnets** – host the RDS database and prevent direct internet access
- **Internet Gateway** – enables internet connectivity for resources in the public subnet
- **Route Table** – routes traffic from the public subnet to the internet gateway
- **Security Groups** – control network access between EC2 and the RDS database
- **MySQL/MariaDB Client** – installed on EC2 to test the database connection
## Steps I Took
### Networking Foundation (VPC & Subnets)
1. Created a Custom VPC: Established a dedicated virtual network to isolate the project resources. `CIDR Block: 10.0.0.0/16`
2. Segmented the Network : Created three subnets across different Availability Zones to support a multi-tier architecture.
- Public Subnet – `10.0.1.0/24` (Application Layer)
- Private Subnet 1 – `10.0.2.0/24` (Database Layer – AZ A)
- Private Subnet 2 – `10.0.3.0/24` (Database Layer – AZ B)
3. Enabled Internet Access : Created and attached an Internet Gateway (IGW) to the VPC. I configured a Route Table to route internet traffic `(0.0.0.0/0)` through the IGW associated the route table with the public subnet.  
### Compute & Hardened Access
1. **Launched an EC2 Instance** - Deployed an Amazon Linux 2023 instance in the public subnet to act as the application server that connects to the database.
2. **Configured Security Group** `webEC2-sg`
- SSH (Port 22) – allowed access only from my local machine’s public IP
- HTTP (Port 80) – allowed inbound traffic from the internet
  It ensures secure administrative access while allowing web traffic.
3. **Authentication & Access:** Used an RSA key pair `ph3.pem` for secure passwordless authentication and connected to the EC2 instance via SSH using `ssh -i ph3.pem ec2-user@EC2-PUBLIC-IP`
## Database Layer (Amazon RDS)
1. **Created an Amazon RDS MySQL Database** : I deployed a MySQL database instance inside the private subnets using an RDS subnet group. This ensures the database is not publicly accessible from the internet.
2. **Configured Database Security Group**(rds-sg)
Added an inbound rule:
- Type: `MySQL/Aurora`
- Port: 3306
- Source: EC2 Security Group (webEC2-sg)
This allows only the EC2 instance to connect to the database.

## Testing the Connection
1. **Installed the MariaDB Client** - Installed the database client on the EC2 instance usning `sudo dnf install mariadb105 -y`
2. **Connected to the RDS Database** - Used the RDS endpoint to connect from the EC2 instance using `mysql -h RDS-ENDPOINT -P 3306 -u USERNAME -p`
3. **Ran a Test Query** : by using `SELECT NOW();` This confirmed the EC2 instance could successfully communicate with the RDS database.
4. Exited the Database: typed `exit`
   
**Result** : The EC2 instance successfully connected to the Amazon RDS MySQL database using secure AWS networking. The database remained isolated in private subnets while allowing controlled access from the EC2 application layer.

## Screenshots

