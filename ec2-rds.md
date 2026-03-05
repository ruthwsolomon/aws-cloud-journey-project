# AWS EC2 to RDS MySQL Connection

This project demonstrates how to connect an EC2 instance to a MySQL database hosted on Amazon RDS using proper AWS networking and security group configuration.

## Architecture
- **Compute:** Amazon EC2 (t3.micro – Free Tier)
- **Database:** Amazon RDS (db.t3.micro – MySQL 8.4.7)
- **Operating System:** Amazon Linux 2023
- **Networking:** Virtual Private Cloud (VPC) with unified routing
- **Security:** Custom Security Groups (EC2-SG & RDS-SG) acting as virtual firewalls
- **Database Client:** MariaDB 10.5 (MySQL-compatible client)

### What I did:
1. **Created an EC2 Instance** - Launched an EC2 instance inside a VPC to act as the server connecting to the database.
2. **Created an RDS MySQL Database** - Provisioned a MySQL database using Amazon RDS within the same VPC.
3. **Verified VPC Configuration** - Confirmed that both the EC2 instance and RDS database were running in the same VPC to allow internal communication.
4. **Configured the RDS Security Group** - Added an inbound rule allowing MySQL traffic on port 3306 from the EC2 security group.
5. **Verified EC2 Security Group** - Ensured outbound traffic from EC2 was allowed so it could communicate with the RDS instance.
6. **Connected to EC2 via SSH** - `ssh -i mykey.pem ec2-user@EC2-PUBLIC-IP`
7. **Installed MySQL / MariaDB Client** - `sudo dnf install mariadb105 -y`
8. **Tested the Database Connection** - `mysql -h RDS-ENDPOINT -P 3306 -u USERNAME -p`
9. **Ran a test query** - `SELECT NOW();`
10. **Exited MySQL using:** `exit`

**Result:** The EC2 instance successfully connected to the Amazon RDS MySQL database using the configured security group rules.
