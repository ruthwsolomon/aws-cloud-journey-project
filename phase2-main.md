[`← Previous: Phase1` ](phase1-static-website.md) **.** [`Home`](./README.md) **.** [`Next: Launching EC2 →`](phase2-ec2-launch.md)

# Phase 2 – Web Server on EC2 Accomplishments

This section documents my hands-on process for managing a live AWS EC2 server entirely via the command line and this is what I accomplished:

- [Launched the Server (AWS EC2)](phase2-ec2-launch.md) - I created a live Linux instance on Amazon EC2, configuring the virtual hardware and networking to make the server accessible over the internet.
-  [CLI-Practice](CLI-Practice.md) - I gained hands-on experience with the EC2 instance by practicing to navigate directories, managing file ownership, and using core Linux CLI tools, building comfort with working entirely in the terminal.
-   [Service Management](service-management.md) - I managed the Apache web server, monitoring its status, starting and stopping the service, and configuring it to automatically restart on server reboot.
- [Connecting Windows to Linux and AWS SSH & Security](ssh-security.md)- I established a secure remote management pipeline by configuring Windows PowerShell to connect to an AWS EC2 Linux instance, where I manually generated RSA key pairs, hardened file permissions via `icacls`, and updated the server's `authorized_keys` to enforce strictly controlled, key-based access.

**Note:** Each link points to a detailed `.md` file with full commands, screenshots, and documentation. 

[`← Previous: Phase1` ](phase1-static-website.md) **.** [`Home`](./README.md) **.** [`Next: Launching EC2 →`](phase2-ec2-launch.md)
