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

## Screenshots :
<img width="1895" height="743" alt="Screenshot 2026-03-05 222706" src="https://github.com/user-attachments/assets/706d899b-7254-4de3-998c-0ac883e53d4d" />
<img width="1908" height="749" alt="Screenshot 2026-03-05 223722" src="https://github.com/user-attachments/assets/2ff24fa5-7da3-4b07-abb9-bbaeb2cc56fd" />
<img width="1918" height="756" alt="Screenshot 2026-03-05 223119" src="https://github.com/user-attachments/assets/254a6e47-96cd-4307-bc7e-0971c402c32f" />
<img width="1629" height="860" alt="Screenshot 2026-03-05 222545" src="https://github.com/user-attachments/assets/98e41010-d825-477e-908e-7028c98cd48a" />
<img width="1919" height="1010" alt="Screenshot 2026-03-05 211726" src="https://github.com/user-attachments/assets/f45c9b38-abd3-450d-8ee8-938c10850d7b" />




