# AWS SSH & Security
Platform: Windows 11 (PowerShell) → AWS EC2 (Amazon Linux)

This lab focused on securing remote access between a Windows machine and a Linux EC2 instance. The goal was not just to connect, but to do it properly with controlled permissions, key-only authentication and restricted network access.

## Skills Demonstrated
- **Windows File Permission Control** : Used **_icacls_** to remove inherited permissions and restrict the **_.pem_** file to a single user account, effectively replicating the behavior of **_chmod 400_** on Linux.

- **Secure Remote Access via SSH**: Connected to an EC2 instance over Port 22 using the OpenSSH client in PowerShell.

- **SSH Key Management**: Inspected the **_~/.ssh/authorized_keys_** file on the Linux server, generated a new RSA key pair using **_ssh-keygen_**, and manually added a public key to the remote server to enable authentication.

- **Server Hardening** : Modified the SSH configuration (**_sshd_config_**) to disable password authentication, enforcing key-based access only. Restarted the SSH service to apply changes.

- **Network-Level Security**: Applied the principle of least privilege by restricting the AWS Security Group to allow SSH access from “My IP” only.

## Key Commands Used
| Action | Command |
|--------|---------|
| Secure Key (Windows) | `icacls another1key.pem /inheritance:r; icacls another1key.pem/grant:r "$($env:USERNAME):(R)` |
| Connect to Server | `ssh -i another1key.pem ec2-user@13.48.194.121` |
| Generate RSA Key | `ssh-keygen -t rsa -b 2048` |
| Restart SSH Service | `sudo systemctl restart sshd` |

## Screenshots
<img width="1914" height="1011" alt="Screenshot 2026-02-28 145122" src="https://github.com/user-attachments/assets/36b351ba-41de-4ac1-869c-a7e153493f0c" />
<img width="1919" height="1003" alt="Screenshot 2026-02-28 145251" src="https://github.com/user-attachments/assets/a8736569-8297-421b-a6c8-c8c4bfcd81e2" />
<img width="1919" height="1010" alt="Screenshot 2026-02-28 150258" src="https://github.com/user-attachments/assets/ec019449-4028-41f2-b484-e6b34f1718d5" />
<img width="1919" height="1003" alt="Screenshot 2026-02-28 150427" src="https://github.com/user-attachments/assets/330481f4-6548-4c03-84bd-72a98aae55b0" />
<img width="1919" height="999" alt="Screenshot 2026-02-28 150504" src="https://github.com/user-attachments/assets/a3f5d2a9-c4c9-4f46-851f-40ebfc7e34b0" />
<img width="1917" height="1011" alt="Screenshot 2026-02-28 150738" src="https://github.com/user-attachments/assets/ce59b30f-b684-4039-996b-72a226f97a3f" />
<img width="1916" height="1004" alt="Screenshot 2026-02-28 150831" src="https://github.com/user-attachments/assets/5b02636e-15fa-412d-a58b-622d0b1eecf5" />
<img width="1911" height="821" alt="Screenshot 2026-02-28 131732" src="https://github.com/user-attachments/assets/7030404a-54c2-4c4b-9ecc-4fe2b651f7ea" />





