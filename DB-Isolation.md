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
1. **VPC Creation:** Created a Virtual Private Cloud named `project-vpc` to establish a dedicated and isolated network for the project resources with CIDR Block `10.0.0.0/16`
2. **Segmented the Network :**- Within project-vpc, I created three distinct subnets, to support a multi-tier architecture across different Availability Zones.
- Public Subnet – 10.0.1.0/24 (Application Layer)
- Private Subnet 1 – 10.0.2.0/24 (Database Layer – AZ A)
- Private Subnet 2 – 10.0.3.0/24 (Database Layer – AZ B)
4. **Enabled Internet Access :** Created an Internet Gateway named `project-igw` and attached it to `project-vpc` to allow internet connectivity for resources in the public subnet.
5. **Route Tables:** I configured two distinct route tables `public-rt` and `private-rt` to manage the flow of network traffic by directing the public subnet to the internet gateway and keeping the database subnets isolated.
On `public-rt` I added a default route `0.0.0.0/0` targeting `igw-0aaf7688738cd3058` (`project-igw` ID) to grant the EC2 instance internet connectivity.
For the Private Route Table, I established `private-rt` without an internet gateway target to ensure the RDS database subnets remain strictly internal and secure.
  
### Compute & Hardened Access 
1. **Configured Security Group** - Created a security group named `webEC2-sg` and attached it to `project-vpc` to control inbound traffic to the EC2 instance. This security group acts as a virtual firewall protecting the application server.
Configured inbound rules:
- SSH (Port 22) – allowed access only from my local machine’s public IP
- HTTP (Port 80) – allowed inbound web traffic from the internet
This configuration allows secure administrative access while enabling web connectivity.

2. **Launched EC2 Instance:** Launched an Amazon Linux 2023 EC2 instance and configured the network settings to use `project-vpc` and the public subnet. The instance was associated with the webEC2-sg security group to control access to the server.
  
2. **Created Security Group dbEC2-sg:** Created another security group `dbEC2-sg` and attached it to project-vpc to protect the database layer. An inbound rule was added to allow MySQL/Aurora traffic on port `3306` from the `webEC2-sg` security group `sg-0607799b74472f868`. This ensures that only the EC2 instance can access the database.
3. **Launched an EC2 Instance** - Deployed an Amazon Linux 2023 instance in the public subnet to act as the application server that connects to the database.
Configured inbound rules:
- SSH (Port 22) – allowed access only from my local machine’s public IP
- HTTP (Port 80) – allowed inbound web traffic from the internet
This configuration allows secure administrative access while enabling web connectivity.
3. **Configured Security Group** `webEC2-sg`
- SSH (Port 22) – allowed access only from my local machine’s public IP
- HTTP (Port 80) – allowed inbound traffic from the internet
  It ensures secure administrative access while allowing web traffic.
3. **Authentication & Access:** Used an RSA key pair `ph3.pem` for secure passwordless authentication and connected to the EC2 instance via SSH using `ssh -i ph3.pem ec2-user@EC2-PUBLIC-IP`
## Database Layer (Amazon RDS)
1. **Created an Amazon RDS MySQL Database** : I deployed a MySQL database instance inside the private subnets using an RDS subnet group. This ensures the database is not publicly accessible from the internet.
2. **Configured Database Security Group** `rds-sg` : I removed the default inbound rule and configured a custom rule to restrict access.
Added an inbound rule:
- Type: `MySQL/Aurora`
- Port: 3306
- Source: EC2 Security Group `webEC2-sg`
This allows only the EC2 instance to connect to the database.

## Testing the Connection
1. **Installed the MariaDB Client** - Installed the database client on the EC2 instance usning `sudo dnf install mariadb105 -y`
2. **Connected to the RDS Database** - Used the RDS endpoint to connect from the EC2 instance using `mysql -h RDS-ENDPOINT -P 3306 -u USERNAME -p`
3. **Ran a Test Query** : by using `SELECT NOW();` This confirmed the EC2 instance could successfully communicate with the RDS database.
4. Exited the Database: typed `exit`
   
**Result** : The EC2 instance successfully connected to the Amazon RDS MySQL database using secure AWS networking. The database remained isolated in private subnets while allowing controlled access from the EC2 application layer.

## Screenshots
<img width="1887" height="755" alt="Screenshot 2026-03-06 131251" src="https://github.com/user-attachments/assets/b94cc712-fa75-40fb-891a-d6f371144eef" />
<img width="1913" height="749" alt="Screenshot 2026-03-06 132123" src="https://github.com/user-attachments/assets/92d8ed30-36b4-45c8-b07a-8da04ce868b8" />
<img width="1909" height="683" alt="Screenshot 2026-03-06 132605" src="https://github.com/user-attachments/assets/0c4a246b-7e2f-4d53-a50e-368dc8819ebd" />
<img width="1915" height="752" alt="Screenshot 2026-03-06 132713" src="https://github.com/user-attachments/assets/d523faee-b5bd-404e-8320-8fab5e59b8e1" />
<img width="1911" height="754" alt="Screenshot 2026-03-06 132932" src="https://github.com/user-attachments/assets/ec921fae-efe8-4f55-a6d9-e21d7feb7f3b" />
<img width="1918" height="737" alt="Screenshot 2026-03-06 133151" src="https://github.com/user-attachments/assets/cb1884db-4cd5-4a86-9f7b-9e89f98eb92d" />
<img width="1901" height="746" alt="Screenshot 2026-03-06 134245" src="https://github.com/user-attachments/assets/abee8e49-70ff-4c68-8d4b-0482b46fa4a7" />
<img width="1891" height="748" alt="Screenshot 2026-03-06 135005" src="https://github.com/user-attachments/assets/fa734b8e-fae1-49fc-b062-694501d52bb3" />
<img width="1896" height="748" alt="Screenshot 2026-03-06 135708" src="https://github.com/user-attachments/assets/5e76fcbf-c6bb-43de-9839-465fea4323d2" />
<img width="1889" height="756" alt="Screenshot 2026-03-06 135718" src="https://github.com/user-attachments/assets/96019168-4067-4d08-88dc-8b827978432d" />
<img width="1916" height="751" alt="Screenshot 2026-03-06 135742" src="https://github.com/user-attachments/assets/afafde76-59c0-4714-b38f-8b2e459c0e22" />
<img width="1886" height="746" alt="Screenshot 2026-03-06 150254" src="https://github.com/user-attachments/assets/387e388d-b7cd-4dfd-8a72-ed634abd2984" />
<img width="1889" height="747" alt="Screenshot 2026-03-06 150448" src="https://github.com/user-attachments/assets/0f7443cd-0a4e-4e71-824f-a72aaff9c5ee" />
<img width="1885" height="750" alt="Screenshot 2026-03-06 150626" src="https://github.com/user-attachments/assets/9a5a7b4d-0ff0-4eba-9a3a-3fbf20c3fb64" />
<img width="1913" height="758" alt="Screenshot 2026-03-06 154922" src="https://github.com/user-attachments/assets/d8e6da3a-f166-4d51-b4ee-a78332f3b017" />
<img width="1883" height="739" alt="Screenshot 2026-03-06 155650" src="https://github.com/user-attachments/assets/49e96c24-a362-4721-bfca-c7157fdb8f16" />
<img width="1916" height="740" alt="image" src="https://github.com/user-attachments/assets/a1aed2dc-a8ee-4634-a84a-1f174d380638" />
<img width="1912" height="1005" alt="Screenshot 2026-03-06 161104" src="https://github.com/user-attachments/assets/59d061a0-aa7e-41f5-bd32-475ff7e368e8" />
<img width="1919" height="1003" alt="Screenshot 2026-03-06 161750" src="https://github.com/user-attachments/assets/2575dc77-0ea3-4290-8b40-aeb76b7616e5" />













