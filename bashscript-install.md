## Automation: Web Server Deployment via Bash Scripting
The objective was to automate the installation and configuration of the Apache Web Server on an Amazon Linux 2023 EC2 instance using a Bash script.
## Tech Stack
- AWS EC2
- Amazon Linux 2023
- Apache (httpd)
- Bash
## Execution Steps
1. Launched EC2 Instant and connected via EC2 Connect
2. Created a shell script file named `install_apache.sh` using the `nano`.

   **Script Content:**
   - **Shebang**  `#!/bin/bash`
   -  **Update system and install Apache**  `sudo yum update -y`   `sudo yum install httpd -y`
   -   **Start and enable the service**  `sudo systemctl start httpd`  `sudo systemctl enable httpd`
5. Modified the file permissions to make the script executable: `chmod +x install_apache.sh`
6. Ran the script to trigger the automated installation `./install_apache.sh`
7. Verified deployment in browser.
   
**Key Takeaway**: 
Automating the setup via a Bash script reduces manual effort and minimizes the risk of human error during the configuration phase of the deployment.
 
