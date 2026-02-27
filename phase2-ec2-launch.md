# Phase 2 – Web Server Deployment (Amazon EC2)
## Goal
Deploy a live Linux web server using Amazon EC2 and make it accessible from the public internet.
## Architecture
- **Compute:** Amazon EC2 (t3.micro – Free Tier)
- **Operating System:** Amazon Linux 2023
- **Security:** Custom Security Group acting as a virtual firewall
- **Web Server:** Apache HTTP Server (httpd)
## What I Did
1. Provisioned a t3.micro EC2 instance using the Amazon Linux 2023 AMI.
2. Configured a Security Group allowing SSH (Port 22) and HTTP (Port 80).
3. Accessed the server CLI using EC2 Instance Connect.
4. Updated the system and installed Apache using the `yum` package manager.
5. Persisted the web server to run automatically on boot using `systemctl`.
6. Deployed custom HTML/CSS to `/var/www/html/` via the Linux terminal.
7. Verified the deployment using the Public IPv4 address.
8. Terminated the instance to maintain zero-cost cloud management.
## Challenge Faced – “Connection Timeout”
**Problem:** The instance was running, but the website wouldn’t load in the browser.

**Fix:** I discovered the Security Group was too restrictive. I updated the HTTP rule to allow traffic from **Anywhere-IPv4 (0.0.0.0/0)**, which opened public access to the server.
## Lessons Learned
- **Infrastructure as a Service (IaaS):** Gained hands-on experience managing cloud infrastructure without physical access.
- **Port Management:** Understood the balance between opening ports for access (80) and keeping them restricted for security (22).
- **Network Troubleshooting:** Learned that most “Connection Timeout” errors are networking-related, specifically in the Security Group layer.
- **CLI Confidence:** Became comfortable managing a server fully through the command line.
- **Cost Awareness:** Reinforced the importance of terminating resources to prevent unexpected cloud costs.
### **SCREENSHOTS**
### 1. **Cloud Architecture:** <img width="1889" height="778" alt="Screenshot 2026-02-26 193812" src="https://github.com/user-attachments/assets/d03f303f-274b-48ab-a99f-c5c52a20f592" />
### 2. **CLI Deployment:** <img width="1910" height="874" alt="Screenshot 2026-02-26 193835" src="https://github.com/user-attachments/assets/e275eadb-142f-4408-9f41-58d5fd7d6719" />
### 3. **Live Result:** <img width="1911" height="944" alt="Screenshot 2026-02-26 193848" src="https://github.com/user-attachments/assets/fb9bd8f3-7284-46d4-9a94-ac699296c9e1" />
### 4. **Termination:** <img width="1919" height="868" alt="Screenshot 2026-02-26 195445" src="https://github.com/user-attachments/assets/3f3ef3db-130f-4e5e-b33d-c81634e70fb4" />
<img width="1911" height="874" alt="Screenshot 2026-02-26 195620" src="https://github.com/user-attachments/assets/c3b2ef85-42e2-45b8-ab90-6091984ef2d8" />
