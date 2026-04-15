[`← Previous: EC2 Launch` ](ec2-launch.md) **.** [`Phase2 Home`](phase2-main.md) **.** [`Home`](./README.md) **.** [`Next: Service Management →`](service-management.md)
# Phase 2 - Linux CLI Practice
This section documents my hands-on practice using the EC2 instance through the Command Line Interface (CLI).
## Command Reference  
- **ssh -i** – Connects to an EC2 instance using a private key file.
- **pwd** – Displays the current working directory.
- **mkdir** – Creates a new directory.
- **ls** – Lists files and folders in the current directory.
- **cd** – Navigates between directories.
- **nano** – Opens a terminal-based text editor used to create or modify files.
- **cat** – Displays the contents of a file in the terminal.
- **rm** – Removes a file from the system.
- **rm -r** – Recursively deletes a directory and its contents.
- **exit** – Closes the SSH session.

<details>
<summary><b>Detailed Execution Workflow</b> (Click to expand)</summary>

1. I first connected to the EC2 instance using: `ssh -i ph3.pem ec2-user@public-ip-address`
2. After connecting, I ran `pwd` and this confirmed my current location in the Linux filesystem as `/home/ec2-user`.
3. I attempted to create a directory named SHARUZ using `mkdir` `SHARUZ`. The system responded that the directory already existed, confirming that it had previously been created.
4. used `ls` to list the contents of the current directory. The output showed two directories: `SHARUZ` and `SOLOMON`.
5. I navigated into the `SHARUZ` directory using `cd SHARUZ`.
6. Inside this directory, I created and edited a new text file using `nano ruth-diary.txt`. Within the file, I wrote the message: "Am playing around with CLI commands".
7. After saving the file, I ran ls again to confirm that `ruth-diary.txt` had been successfully created in the directory.
8. To verify the file’s contents directly from the terminal, I used `cat ruth-diary.txt`, which displayed the message written inside the file.
9. Once verified, I removed the file using `rm ruth-diary.txt`.
10. I then returned to the main home directory by running `cd (space)`
11.  To remove a directory that doesn't contains files or subdirectories, I used the command `rmdir SOLOMON`, which deleted the directory and all of its contents.
12. To remove a directory that contains files or subdirectories, I used the recursive command `rm -r SHARUZ`, which deleted the directory and all of its contents.
13. I ran `ls` one last time to confirm that the workspace was empty and all created files and directories had been removed.
14. After completing the practice session, I exited the server by typing exit, which closed the SSH connection to the EC2 instance.

</details>

### Key Learning Outcome

This exercise strengthened my understanding of interacting with Linux systems through the command line. Since Amazon EC2 instances are Linux-based in many production environments, being comfortable with CLI operations is an important foundational skill.

Through this practice, I learned how to:

- Connect securely to a remote EC2 instance using SSH.
- Navigate the Linux filesystem.
- Create and manage directories and files.
- Verify file contents directly from the terminal.
- Safely delete files and directories.

These skills are essential when managing cloud infrastructure, troubleshooting servers, and performing administrative tasks on EC2 instances within an AWS environment.

### Screenshots:
<img width="1909" height="1003" alt="Screenshot 2026-03-15 213018" src="https://github.com/user-attachments/assets/9bc65b91-55e4-4e5e-b2c1-542e9869b68b" />
<img width="1915" height="1005" alt="Screenshot 2026-03-15 212014" src="https://github.com/user-attachments/assets/3d742f27-9d53-4b6e-b3a6-4fdf812e80e4" />
<img width="1904" height="1002" alt="Screenshot 2026-03-15 213031" src="https://github.com/user-attachments/assets/0b58a3a1-3e3f-454b-be9f-251715d5fa2f" />

[`← Previous: EC2 Launch` ](phase2-ec2-launch.md) **.** [`Phase2 Home`](phase2-main.md) **.** [`Home`](./README.md) **.** [`Next: Service Management →`](service-management.md)
