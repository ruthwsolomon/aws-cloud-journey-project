[`← Previous: Writing a Bashscript`](bashscript-install.md) **.** [`Home`](./README.md) **.** [`Next: Connect EC2 to RDS(MySQL)` ](ec2-rds.md)

 # PHASE 3 MAIN
 
## AWS Database Integration & High Availability

This phase focuses on integrating a managed database service into the cloud infrastructure and implementing security, backup, and resilience best practices using Amazon RDS and EC2.
The objective was to move from a single compute server to a multi-tier architecture, where the application layer and database layer are separated and secured through AWS networking controls.

## Accomplishments

- [AWS EC2 to RDS MySQL Connection](ec2-rds.md) – I successfully configured an Amazon EC2 instance to connect to a MySQL database hosted on Amazon RDS using the MySQL client. This demonstrated how compute services interact with managed database services inside a VPC.
- [AWS Multi-Tier Architecture: Database Isolation](db-isolation.md) - I designed a network architecture where the EC2 instance resides in a public subnet, while the RDS database is placed in private subnets to prevent direct internet access and improve security.
- [Security Group Chaining: EC2 → RDS](controlled-access.md) I implemented security group referencing so the database accepts connections only from the EC2 instance, ensuring controlled service-to-service communication instead of exposing database ports publicly.
- [Manual Database Snapshot](data-durability.md)- I created a manual RDS snapshot, demonstrating how managed databases can be backed up and restored to protect against data loss.
- [Multi-AZ Database Failover (High Availability)](High-Availabity.md) – I enabled Multi-AZ deployment for the RDS instance and observed how AWS performs automatic failover to a standby database in another availability zone to maintain availability.
- [`Failure testing: Reboot DB & test connectivity](failure-testing.md) – I simulated a real operational event by rebooting the RDS database instance and testing connectivity from EC2 before and after the reboot to observe system recovery behavior.

**Note:** Each link points is a detailed **.md** file containing the architecture diagrams, configuration steps, commands used, and supporting screenshots.

[`← Previous: Writing a Bashscript`](bashscript-install.md) **.** [`Home`](./README.md) **.** [`Next: Connect EC2 to RDS(MySQL)` ](ec2-rds.md)
