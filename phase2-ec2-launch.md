# Phase 2 – Web Server Deployment (Amazon EC2)

## Goal
Provision a live Linux-based web server using Amazon EC2 and configure networking to allow global internet access.

## Architecture
- **Compute:** Amazon EC2 Instance (t3.micro)
- **OS:** Amazon Linux 2023 (AL2023)
- **Security:** Custom Security Group acting as a virtual firewall
- **Web Service:** Apache HTTP Server (httpd)
  
## Steps Followed
1. Launched a virtual server using the Amazon Linux 2023 AMI on the Free Tier.
2. Created a Security Group with specific Inbound Rules for SSH (Port 22) and HTTP (Port 80).
3. Accessed the server's command line interface (CLI) using EC2 Instance Connect.
4. Performed system-wide security updates and installed the Apache Web Server using the `yum` package manager.
5. Initialized the web service and configured it to automatically restart on boot using `systemctl`.
6. Used the Linux terminal to inject custom-styled HTML and CSS into the production directory (`/var/www/html/`).
7. Validated the deployment by accessing the Public IPv4 address via a web browser.
8. Terminated the instance post-verification to ensure cost-efficiency and security.
## Lessons Learned
- How to manage Hardware as a Service without physical access to the machine.
- The importance of opening specific ports (80 vs 22) to balance accessibility and security.
- Managing a server entirely through a terminal rather than a graphical interface.
- The necessity of de-provisioning resources to prevent Cloud Waste and unnecessary billing.
### **SCREENSHOTS**
### 1. **Cloud Architecture:** <img width="1919" height="828" alt="Screenshot 2026-02-26 193820" src="https://github.com/user-attachments/assets/db55083b-d193-4935-b06a-88616b0ecb38" />
### 2. **CLI Deployment:** <img width="1910" height="874" alt="Screenshot 2026-02-26 193835" src="https://github.com/user-attachments/assets/e275eadb-142f-4408-9f41-58d5fd7d6719" />
### 3. **Live Result:** <img width="1911" height="944" alt="Screenshot 2026-02-26 193848" src="https://github.com/user-attachments/assets/fb9bd8f3-7284-46d4-9a94-ac699296c9e1" />
### 4. **Termination:** <img width="1919" height="868" alt="Screenshot 2026-02-26 195445" src="https://github.com/user-attachments/assets/3f3ef3db-130f-4e5e-b33d-c81634e70fb4" />
<img width="1911" height="874" alt="Screenshot 2026-02-26 195620" src="https://github.com/user-attachments/assets/c3b2ef85-42e2-45b8-ab90-6091984ef2d8" />
