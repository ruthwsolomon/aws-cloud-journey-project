# AWS EC2 to RDS MySQL Connection

This project demonstrates how to connect an EC2 instance to a MySQL database hosted on Amazon RDS using proper AWS networking and security group configuration.

## The infrastructure used in this project:
- EC2 Instance – used as the compute server to access the database
- Amazon RDS (MySQL) – managed relational database service
- VPC – both EC2 and RDS are deployed in the same Virtual Private Cloud
- Security Groups – used to control network access between EC2 and RDS
- MySQL/MariaDB Client – installed on EC2 to test the database connection – installed on EC2 to test the database connection

### What I did:
1. Created an EC2 Instance - Launched an EC2 instance inside a VPC to act as the server connecting to the database.
2. Created an RDS MySQL Database - Provisioned a MySQL database using Amazon RDS within the same VPC.
3. Verified VPC Configuration - Confirmed that both the EC2 instance and RDS database were running in the same VPC to allow internal communication.
4. Configured the RDS Security Group - Added an inbound rule allowing MySQL traffic on port 3306 from the EC2 security group.
5. Verified EC2 Security Group - Ensured outbound traffic from EC2 was allowed so it could communicate with the RDS instance.
6. Connected to EC2 via SSH - `ssh -i mykey.pem ec2-user@EC2-PUBLIC-IP`
7. Installed MySQL / MariaDB Client - `sudo dnf install mariadb105 -y`
8. Tested the Database Connection - `mysql -h RDS-ENDPOINT -P 3306 -u USERNAME -p`
9. Ran a test query - `SELECT NOW();`
10. Exited MySQL using: `exit`

**Result:** The EC2 instance successfully connected to the Amazon RDS MySQL database using the configured security group rules.
