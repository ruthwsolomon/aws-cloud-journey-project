[← Phase2 Home](phase1-ec2-launch.md) | [Home](./README.md) | [Next: CLI Practice →](CLI-Practice.md) 

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
- **Infrastructure & IaaS:** Gained hands-on experience managing cloud servers without physical hardware.
- **Networking & Security:** Balanced port access, configured Security Groups, and resolved connection issues.
- **Linux & Web Server Administration:** Installed Apache, managed services, deployed web content, and ensured automatic startup.
- **Troubleshooting & Cost Management:** Developed problem-solving skills and reinforced best practices like terminating instances to avoid unexpected cloud costs.
### **SCREENSHOTS**

### 1. **Cloud Architecture:** 
<img width="1889" height="778" alt="Screenshot 2026-02-26 193812" src="https://github.com/user-attachments/assets/9ea03b77-5107-4c39-90cb-8b673bc78e04" />

### 2. **CLI Deployment:** 
<img width="1910" height="874" alt="Screenshot 2026-02-26 193835" src="https://github.com/user-attachments/assets/cd45d8d4-ab5c-4879-a8cf-8b6d2d051f10" />

### 3. **Live Result:** 
<img width="1911" height="944" alt="Screenshot 2026-02-26 193848" src="https://github.com/user-attachments/assets/7262aaf2-b3e5-42a4-9567-74da29aa4d20" />

### 4. **Termination:** 
<img width="1919" height="868" alt="Screenshot 2026-02-26 195445" src="https://github.com/user-attachments/assets/eea2624d-ce1e-439d-a994-5d870e0aaaef" />
<img width="1911" height="874" alt="Screenshot 2026-02-26 195620" src="https://github.com/user-attachments/assets/24c9543e-59d9-4700-9b5b-95b78a85562f" />

[← Phase2 Home](phase1-ec2-launch.md) | [Home](./README.md) | [Next: CLI Practice →](CLI-Practice.md) 
