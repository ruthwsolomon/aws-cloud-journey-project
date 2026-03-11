# AWS Networking: NAT Gateway vs Internet Gateway (Private Internet Routing)

In this project I built a networking architecture from scratch in AWS to demonstrate **how private resources can securely access the internet without being publicly exposed.** The goal was to understand the difference between **an Internet Gateway (IGW) and a NAT Gateway** and how they are used to control internet connectivity inside a Virtual Private Cloud.

The architecture separates resources into public and private subnets. Instances in the public subnet access the internet directly through an Internet Gateway, while instances in the private subnet route outbound internet traffic through **a NAT Gateway**. This design ensures that private instances can access the internet for updates or package downloads without allowing inbound internet connections.

## Architecture Components

- **Amazon EC2** – compute instances used to test network connectivity
- **Amazon VPC** – isolated virtual network environment
- **Public Subnet** – hosts resources that require direct internet access
- **Private Subnet** – hosts internal resources that should not be accessible from the internet
- **Internet Gateway (IGW)** – allows public subnet resources to communicate with the internet
- **NAT Gateway** – enables outbound internet access for private subnet resources
- **Elastic IP Address** – provides a static public IP required for the NAT Gateway
- **Route Tables** – control network traffic flow inside the VPC

## Networking Foundation
### VPC Creation
A Virtual Private Cloud was created to isolate the network environment for this architecture.
- VPC Name: `NATPractice-vpc`
- CIDR Block: 10.0.0.0/16

This CIDR range provides sufficient address space for multiple subnets and future scaling.

## Subnet Architecture
Two subnets were created to separate internet-facing resources from internal resources.

- Public Subnet : `pub-sn` – `10.0.1.0/24`
  
This subnet hosts the NAT Gateway and the public EC2 instance that require direct internet connectivity.

- Private Subnet : `priv-sn` – `10.0.2.0/24`

This subnet hosts internal the EC2 instance that should not be accessible directly from the internet. Instances deployed here do not receive public IP addresses.

## Internet Gateway Configuration
An Internet Gateway named `NATPractice-gtw` was created and attached to `NATPractice-vpc`.

This gateway enables internet access for resources located in the public subnet.

## NAT Gateway Configuration
A NAT Gateway `NATPractice-getway` was created to allow private subnet resources to access the internet without exposing them to inbound traffic.
  (notes after going through my photos: names look similar, next time i can write the igw for internet gateway)
Steps performed:
   - Changed availability mode to Zonal
   - Placed the NAT Gateway inside `pub-sn`
   - Allocated and attached an Elastic IP address to the NAT Gateway
   - Created a NAT Gateway `NATPractice-gtw`

This NAT Gateway acts as a controlled outbound internet access point for private instances.

## Route Table Configuration
Two route tables were created to manage network traffic.

 - **Public Route Table**
   - Route Table: `NATPractice-PublicRoute`
   - Routes configured: Destination →  `0.0.0.0/0` Target → `NATPractice-igw`
   - Associated Subnet: `pub-sn`

This allows resources in the public subnet to communicate directly with the internet.

- **Private Route Table**
    - Route Table: `NATPractice-PublicRoute`
    - Routes configured: Destination →  `0.0.0.0/0` Target → `NATpractice-getway`
    - Associated Subnet: `priv-sn`

This configuration ensures that instances in the private subnet send outbound traffic through the NAT Gateway instead of directly accessing the internet.

## Security Group Configuration

### 1. Bastion Host Security Group (`BastionHost-sg`)

**Inbound rules:**
* Type: `SSH (Port 22)`
* Source: `My IP`

This configuration allows administrative access to the bastion host from a trusted IP address while preventing unauthorized external connections.

**Outbound rules:** All traffic → Allowed

This allows the bastion host to initiate connections to resources inside the VPC, including private EC2 instances.

### 2. Private EC2 Security Group (`NATPractice-Private-SG`)

**Inbound rules:**
* Type: `SSH (Port 22)`
* Source: `BastionHost-sg`
  
This ensures that only the bastion host can initiate SSH connections to the private EC2 instance. Direct SSH access from the internet is not permitted.

**Outbound rules:** All traffic → Allowed

This allows the instance to send outbound internet traffic through the NAT Gateway for software updates or package installations.

## Launching Resources

### Bastion Host EC2 Instance 
An Amazon Linux 2023 EC2 instance (`BastionHost`) was launched to function as the bastion host.

**Network configuration:**
* **VPC:** NATPractice-vpc
* **Subnet:** pub-sn
* **Security Group:** BastionHost-sg
* **Auto-assign Public IP:** Enabled

The bastion host acts as the secure entry point for accessing private resources inside the VPC.

### Private EC2 Instance
A second EC2 instance (`PrivateEC2`) was deployed inside the private subnet to simulate an internal server.

**Network configuration:**
* **VPC:** `NATPractice-vpc`
* **Subnet:** `priv-sn`
* **Security Group:** `NATPractice-Private-SG`
* **Auto-assign Public IP:** `Disabled`

Because this instance is located in the private subnet and does not have a public IP address, it cannot be accessed directly from the internet.
Access is only possible through the bastion host.

## Challenges Faced: SSH Authentication Error
During the bastion host connectivity test, I encountered an authentication error when attempting to SSH into the private EC2 instance. I received this error `Permission denied (publickey,gssapi-keyex,gssapi-with-mic)`

**The issue:**
The bastion host did not have access to the SSH key required to authenticate with the private EC2 instance.

**The resolution:** **(SSH Agent Forwarding)**
- I first uploaded the key to bastion: `scp -i ph3.pem ph3.pem ec2-user@52.87.249.137:/home/ec2-user/`
- I then SSH into bastion: `ssh -i ph3.pem ec2-user@52.87.249.137`
- Then I fixed permissions on bastion : `chmod 400 ph3.pem`
- I finally SSH into private EC2: `ssh -i ph3.pem ec2-user@10.0.2.232`
- And I was in.

## Testing the NAT Gateway
I ran `curl -I https://www.google.com` and saw my NAT Gateway is correctly routing traffic from my private resources to the web.

## SCREENSHOTS
### VPC CREATION
<img width="1915" height="756" alt="Screenshot 2026-03-10 205954" src="https://github.com/user-attachments/assets/e8fb84fd-ed65-4989-93f0-dcd2f4ecc98e" />

### Subnet Created
<img width="1918" height="796" alt="Screenshot 2026-03-10 210447" src="https://github.com/user-attachments/assets/e4118347-9ae6-47fd-bc84-46a7d65d3ee0" />

### Internet Gateway
<img width="1910" height="791" alt="Screenshot 2026-03-10 211259" src="https://github.com/user-attachments/assets/c1c8ed72-7d97-43ce-b411-f57a0001d053" />

### NAT Getway created
<img width="1899" height="798" alt="Screenshot 2026-03-10 213104" src="https://github.com/user-attachments/assets/3491ef60-26f9-4c6a-8a8e-b2e6de232e32" />

### Public and Private Route
<img width="1896" height="795" alt="Screenshot 2026-03-10 213713" src="https://github.com/user-attachments/assets/b6e78a43-952c-45f2-a826-1759c3f68f9e" />
<img width="1908" height="797" alt="Screenshot 2026-03-10 214543" src="https://github.com/user-attachments/assets/ee6b3737-325d-484f-b7ba-dec5db23d0b9" />

### The security groups

<img width="1906" height="795" alt="Screenshot 2026-03-10 215454" src="https://github.com/user-attachments/assets/0abdc99b-6a06-42b6-9674-4ec9eb298fa6" />
<img width="1898" height="799" alt="Screenshot 2026-03-10 215839" src="https://github.com/user-attachments/assets/b79aa076-af67-40b5-9785-bfee0a7c2aa6" />

### The Bastion Host and private EC2
<img width="1906" height="791" alt="Screenshot 2026-03-10 221219" src="https://github.com/user-attachments/assets/7c99cadd-c4ac-429b-9ab9-c16a28fca83b" />
<img width="1900" height="794" alt="Screenshot 2026-03-10 221709" src="https://github.com/user-attachments/assets/7b8d14cf-c3eb-4ce1-9b85-ece218c72184" />

### First attempt error
<img width="1917" height="1005" alt="Screenshot 2026-03-10 222323" src="https://github.com/user-attachments/assets/fce7b678-eddb-4390-8bbc-911a38cdab35" />

### Succesfully in and tested the private ec2
<img width="1919" height="1003" alt="Screenshot 2026-03-10 223523" src="https://github.com/user-attachments/assets/990fd6bf-8b3b-4463-bdae-8fe9aa843456" />
<img width="1919" height="1006" alt="Screenshot 2026-03-10 223710" src="https://github.com/user-attachments/assets/3b701d48-824f-4dab-8d9c-7f15db5f2423" />














