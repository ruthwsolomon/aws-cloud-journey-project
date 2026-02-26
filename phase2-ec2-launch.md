# AWS Cloud Web Server Deployment
### **The Project**
A hands-on implementation of a live, publicly accessible web server hosted on Amazon Web Services (AWS). This project demonstrates the ability to provision cloud infrastructure, manage networking security, and deploy content via the Linux command line.
### **The Solution**
* **Cloud Provider:** AWS (Amazon Web Services)
* **Service:** EC2 (Elastic Compute Cloud)
* **Instance Type:** `t3.micro` (AWS Free Tier)
* **Operating System:** Amazon Linux 2023
* **Web Software:** Apache HTTP Server (httpd)
### **Technical Execution**
#### **1. Infrastructure & Security**
* Provisioned a virtual server (EC2) and configured a **Security Group** as a virtual firewall.
* Configured **Inbound Rules** to allow traffic on **Port 80 (HTTP)** for public web access and **Port 22 (SSH)** for secure administrative management.
#### **2. Server Configuration**
* Connected to the instance via **EC2 Instance Connect**.
* Performed system updates and managed the application lifecycle using `yum` and `systemctl`.
* Installed and initialized the Apache web engine to handle incoming web requests.
#### **3. Deployment**
* Programmatically deployed a styled UI card to the server's root directory (`/var/www/html/`).
* Verified the live deployment by accessing the Public IPv4 address in a standard web browser.
#### **4. Resource Cleanup:**
Executed a full termination of the EC2 instance upon project verification.
### **Key Takeaways for Business**
* **Cost Optimization:** Successfully stayed within Free Tier limits by selecting appropriate resource types.
* **Security-First Approach:** Implemented the "Principle of Least Privilege" by only opening specific required network ports.
* **Deployment Speed:** Demonstrated the ability to move from a blank cloud instance to a live-production state in minutes.
### **Project Evidence**
### 1. **Cloud Architecture:** <img width="1919" height="828" alt="Screenshot 2026-02-26 193820" src="https://github.com/user-attachments/assets/db55083b-d193-4935-b06a-88616b0ecb38" />
### 2. **CLI Deployment:** <img width="1910" height="874" alt="Screenshot 2026-02-26 193835" src="https://github.com/user-attachments/assets/e275eadb-142f-4408-9f41-58d5fd7d6719" />
### 3. **Live Result:** <img width="1911" height="944" alt="Screenshot 2026-02-26 193848" src="https://github.com/user-attachments/assets/fb9bd8f3-7284-46d4-9a94-ac699296c9e1" />
### 4. **Termination:** <img width="1919" height="868" alt="Screenshot 2026-02-26 195445" src="https://github.com/user-attachments/assets/3f3ef3db-130f-4e5e-b33d-c81634e70fb4" />
<img width="1911" height="874" alt="Screenshot 2026-02-26 195620" src="https://github.com/user-attachments/assets/c3b2ef85-42e2-45b8-ab90-6091984ef2d8" />
