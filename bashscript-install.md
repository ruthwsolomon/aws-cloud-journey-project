## Automation: Web Server Deployment via Bash Scripting
I was able to automate the installation and configuration of the Apache Web Server (httpd) on Amazon Linux 2023 to ensure a repeatable and error-free deployment.

### Execution Steps
1. **Deployed an EC2 Instance:** I connected to the EC2 instance via Amazon EC2 connect
2. **Script Creation:** Created a shell script file named `install_apache.sh` using the `nano` editor.
3. **Script Content:**
   - **Shebang**  `#!/bin/bash`
   -  **Update system and install Apache**  `sudo yum update -y`   `sudo yum install httpd -y`
   -   **Start and enable the service**  `sudo systemctl start httpd`  `sudo systemctl enable httpd`
5. **Permissions:** Modified the file permissions to make the script executable: `chmod +x install_apache.sh`
6. **Execution:** Ran the script to trigger the automated installation `./install_apache.sh`
   
**Key Takeaway**: 
Automating the setup via a Bash script reduces manual effort and minimizes the risk of human error during the configuration phase of the deployment.
 
