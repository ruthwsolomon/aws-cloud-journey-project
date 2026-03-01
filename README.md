
# AWS Cloud Journey Project
This repository documents my hands-on journey learning Amazon Web Services by building a real cloud architecture step by step.
## Project Roadmap
### Phase 1 – Static Website Hosting (S3) ([See details](phase1-static-website.md))
**Objective:** Deploy a globally accessible static website using Amazon S3 buckets.

### Phase 2 – Web Server on EC2 ([See details](phase2-ec2-launch.md))
**Objective:** Deployed a Linux web server on AWS EC2 and managed it securely via Windows PowerShell and Instance Connect, ensuring 24/7 availability with optimized security configurations.

**Accomplishments:**
* **Network Security:**
  - Configured Security Group firewalls to manage traffic on **Port 80 (HTTP)** and **Port 22 (SSH)**.
  - Generated custom RSA key pairs using Windows PowerShell and updated the server’s ~/.ssh/authorized_keys file to enable secure, passwordless SSH access ([see SSH Security Lab](ssh-security.md))
* **System Administration:** Managed the **Apache** service lifecycle using Linux CLI.
* **Deployment:** Successfully deployed custom-styled web assets to the server's production directory.
* **Status:** Complete & De-provisioned (Cost Optimized)
* **Identity & Access Management:** Generated custom RSA key pairs using Windows PowerShell and manually updated the ~/.ssh/authorized_keys file to enable secure, passwordless SSH authentication. 

**Project details:** [View Phase 2](phase2-ec2-launch.md)
### Phase 3 – Database Integration
**Goal:** Connect a running application to a managed Relational Database Service (RDS).
### Phase 4 – Production Architecture
**Goal:** Implement high availability using Load Balancing, Auto Scaling, and CloudWatch monitoring.
## Phase Deliverables
Each phase includes:
- Architecture explanation
- Steps followed
- Screenshots
- Lessons learned
