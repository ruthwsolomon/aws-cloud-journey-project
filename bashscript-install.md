[`← Previous: SSH & Security` ](service-management.md) **.** [`Phase2 Home`](phase2-main.md) **.** [`Home`](./README.md) **.** [`Next: Phase3 Home →`](phase3-main.md) 
# Phase 2 : Automation Using IaaS and Bash Scripting
The objective was to automate the installation and configuration of the Apache Web Server on an Amazon Linux 2023 EC2 instance using a Bash script.
## Infrastructure & Automation Tools
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

 ## Screenshots
<details> <summary><b>1. Created a shell script file named install_apache.sh using the nano.</b></summary> 
  <img width="1895" height="486" alt="Screenshot 2026-03-03 165312" src="https://github.com/user-attachments/assets/23e01a62-c0d2-44fc-9579-74d060d4f3ce" />
</details>

<details> <summary><b>1. DNS on Web After Reloading the Site 10 min Later</b></summary> 
<img width="1894" height="582" alt="Screenshot 2026-03-03 165203" src="https://github.com/user-attachments/assets/7374545d-ed63-4432-ab8a-da5cf9fed0b7" />
</details>

<details> <summary><b>1. DNS on Web After Reloading the Site 10 min Later</b></summary> 
<img width="1897" height="536" alt="Screenshot 2026-03-03 165458" src="https://github.com/user-attachments/assets/a5d4aceb-d99d-4fd2-896f-5ee89e0d202f" />
</details>

<details> <summary><b>1. DNS on Web After Reloading the Site 10 min Later</b></summary> 
<img width="1897" height="878" alt="Screenshot 2026-03-03 165516" src="https://github.com/user-attachments/assets/baf1b850-e360-40c5-b92e-87cd8557d2a3" />
</details>

<details> <summary><b>1. DNS on Web After Reloading the Site 10 min Later</b></summary> 
<img width="1919" height="219" alt="Screenshot 2026-03-03 165656" src="https://github.com/user-attachments/assets/892997b1-2646-4ef2-8b2f-23d4d4794d1f" />
</details>


[`← Previous: SSH & Security` ](service-management.md) **.** [`Phase2 Home`](phase2-main.md) **.** [`Home`](./README.md) **.** [`Next: Phase3 Home →`](phase3-main.md) 


