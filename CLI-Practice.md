[`← Previous: EC2 Launch` ](phase2-ec2-launch.md) **.** [`Phase2 Home`](phase2-main.md) **.** [`Home`](./README.md) **.** [`Next: Service Management →`](service-management.md)
# Phase 2 - Linux CLI Practice
This section documents my hands-on practice using the EC2 instance through the Command Line Interface (CLI).
## Command Reference  
- **pwd** – Displays the current directory I’m working in.  
- **ls** – Lists files and folders in the current directory.  
- **cd** – Navigates between directories.  
- **mkdir** – Creates a new directory.  
- **nano** – Opens a terminal-based text editor to create or modify files.  
- **cat** – Displays the contents of a file in the terminal.  
- **rm** – Removes a file from the system.
 
## Practice Summary  
1. I began by running `pwd` to confirm my current location in the Linux filesystem, which showed the path `/home/ec2-user`.
2. I attempted to create a directory named SHARUZ using `mkdir` `SHARUZ`. The system responded that the directory already existed, confirming that it had previously been created.
3. used `ls` to list the contents of the current directory. The output showed two directories: `SHARUZ` and `SOLOMON`.
4. I navigated into the `SHARUZ` directory using `cd SHARUZ`.
5. Inside this directory, I created and edited a new text file using `nano ruth-diary.txt`. Within the file, I wrote the message: "Am playing around with CLI commands".
6. After saving the file, I ran ls again to confirm that `ruth-diary.txt` had been successfully created in the directory.
7. To verify the file’s contents directly from the terminal, I used `cat ruth-diary.txt`, which displayed the message written inside the file.
8. Once verified, I removed the file using `rm ruth-diary.txt`.
9. I then returned to the main home directory by running `cd (space)`
10.  To remove a directory that doesn't contains files or subdirectories, I used the command `rmdir SOLOMON`, which deleted the directory and all of its contents.
11. To remove a directory that contains files or subdirectories, I used the recursive command `rm -r SHARUZ`, which deleted the directory and all of its contents.
12. I ran `ls` one last time to confirm that the workspace was empty and all created files and directories had been removed.
13. After completing the practice session, I exited the server by typing exit, which closed the SSH connection to the EC2 instance.

Using these commands, I created a file, wrote a custom message, verified its existence, and then safely deleted it.
This exercise strengthened my confidence in managing a Linux environment directly from the terminal.

### Screenshots:
<img width="1919" height="874" alt="Screenshot 2026-02-27 225418" src="https://github.com/user-attachments/assets/e837295d-ed0b-44df-a884-f88e4b263726" />
<img width="1898" height="871" alt="Screenshot 2026-02-27 230216" src="https://github.com/user-attachments/assets/8a9bebb2-fc22-4dc1-9a0f-acd0686045ea" />
<img width="1897" height="881" alt="Screenshot 2026-02-27 230736" src="https://github.com/user-attachments/assets/de7d85ac-eed1-4ab4-9a39-a518e3440fe5" />

[`← Previous: EC2 Launch` ](phase2-ec2-launch.md) **.** [`Phase2 Home`](phase2-main.md) **.** [`Home`](./README.md) **.** [`Next: Service Management →`](service-management.md)
