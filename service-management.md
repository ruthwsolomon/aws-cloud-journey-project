[`← Previous: CLI Practice` ](CLI-Practice.md) **.** [`Phase2 Home`](phase2-main.md) **.** [`Home`](./README.md) **.** [`Next: SSH & Security →`](ssh-security.md) 

##  Server Status & Service Management

In this section, I practiced monitoring and managing the Apache web server on the EC2 instance, learning how to check its status, stop and start services, and ensure automatic recovery on reboot.

* **Audit:** Ran **sudo systemctl status httpd** and confirmed the server was **active (running)**.
* **Manual Stop:** Stopped the web server successfully using **sudo systemctl stop httpd**.
* **Outage Check:** Verified the server was **inactive (dead)** using the status command.
* **Recovery:** Restarted the server and confirmed it **was enabled**, so it will automatically start on reboot.

*This exercise helped me understand how to monitor, control, and automate services on a Linux server.*

<img width="1900" height="825" alt="Screenshot 2026-02-27 233814" src="https://github.com/user-attachments/assets/f0acf7d5-661c-47cb-9fda-722a70819b39" />
<img width="1898" height="825" alt="Screenshot 2026-02-27 234026" src="https://github.com/user-attachments/assets/0196ac86-7c51-4dd5-9faa-55f968bf0320" />
<img width="1913" height="883" alt="Screenshot 2026-02-27 234206" src="https://github.com/user-attachments/assets/5626f78d-7fac-4a5b-bfe3-77dce1be6aa6" />
<img width="1895" height="830" alt="Screenshot 2026-02-27 234327" src="https://github.com/user-attachments/assets/51ff005a-dee7-40ec-ac5f-ab580f986745" />
<img width="1895" height="880" alt="Screenshot 2026-02-27 234457" src="https://github.com/user-attachments/assets/9656d7fc-7be5-496c-989b-83a50df21cd0" />

[`← Previous: CLI Practice` ](CLI-Practice.md) **.** [`Phase2 Home`](phase2-main.md) **.** [`Home`](./README.md) **.** [`Next: SSH & Security →`](ssh-security.md) 
