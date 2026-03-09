[`← Previous: SG chaining (EC2 ↔ RDS) →`](controlled-access.md) **.** [`Phase3 Home`](phase3-main.md) **.** [`Home`](./README.md) **.** [`Next: Configure automated DB snapshots`](phase3-main.md)

# Security Group Chaining: EC2 → RDS

## Objective
Securely connect an EC2 instance to a MySQL RDS database hosted in private subnets using Security Group chaining. The focus is on **controlled access** and reinforcing **database isolation**.

---

## Architecture

### **Compute**
- **EC2 Instance**  
  - Deployed in **public subnet**  
  - Security Group: `webEC2-sg`  
    - SSH access: My IP only  
    - HTTP access: Anywhere  
  - Purpose: Acts as the only allowed client to access the RDS database  

### **Database**
- **RDS MySQL**  
  - Deployed in **private subnets** (multi-AZ)  
  - Security Group: `dbEC2-sg`  
    - Only allows MySQL (port 3306) traffic from `webEC2-sg`  
  - Public access: Disabled  
  - Purpose: Store application data securely while remaining isolated from the internet  

### **Network**
- **VPC:** `project-vpc` (10.0.0.0/16)  
- **Public Subnet:** `public-subnet` (10.0.1.0/24) – hosts EC2 instance  
- **Private Subnets:** `private-subnet-1` (10.0.2.0/24), `private-subnet-2` (10.0.3.0/24) – host RDS database  
- **Internet Gateway:** Attached to VPC to allow EC2 outbound internet access  
- **Route Tables:** Public subnet routes traffic to the Internet Gateway  

### **Security**
- **Security Group Chaining:**  
  - `webEC2-sg` allows inbound SSH and HTTP  
  - `dbEC2-sg` allows MySQL inbound only from `webEC2-sg`  
  - Ensures **RDS is inaccessible from the internet** and only EC2 can access it  

---

## Testing & Verification
1. SSH into the EC2 instance  
2. Install MySQL client: `sudo yum install mysql -y`  
3. Connect to RDS using the endpoint:  
   ```bash
   mysql -h <RDS-ENDPOINT> -u admin -p


# Sreenshots
## SharuzDB inbound rules
<img width="1916" height="746" alt="Screenshot 2026-03-09 211126" src="https://github.com/user-attachments/assets/e71b50eb-69b5-4851-a31f-b8a153831114" />
<img width="1891" height="735" alt="image" src="https://github.com/user-attachments/assets/96f4dfac-4a8c-47c2-aab0-55cf832ee896" />

## RDS security group attached to the database
<img width="1888" height="687" alt="Screenshot 2026-03-09 212631" src="https://github.com/user-attachments/assets/6215cb2b-bfaf-458b-a1aa-26c60bf4a2b3" />

## SharuzEC2-sg inbound rules
<img width="1876" height="732" alt="image" src="https://github.com/user-attachments/assets/27723f4c-82a3-42d5-94f4-83b8f549c528" />

## EC2 security group attached to the EC2 Instance
<img width="1890" height="743" alt="image" src="https://github.com/user-attachments/assets/e57af705-acf2-499f-ae2e-53414537cb66" />

## Successful MySQL connection from EC2
<img width="1918" height="1004" alt="image" src="https://github.com/user-attachments/assets/03d6451e-2fc2-4880-8981-49957007b756" />
<img width="1919" height="1008" alt="image" src="https://github.com/user-attachments/assets/116f38b5-de18-4fc4-8ae1-f5c3c1a6e21d" />

