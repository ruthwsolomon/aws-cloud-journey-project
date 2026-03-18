[`← Previous: Multi-AZ database failover →`](High-Availabity.md) **.** [`Phase3 Home`](phase3-main.md) **.** [`Home`](./README.md) **.** [`Next: NAT Gateway vs Internet Gateway  →`](BastionHost.md)

# Failure Testing

The objective was to test the architecture for resilience by manually rebooting the RDS database instance from the AWS console. This test simulates a temporary database interruption to observe how the system behaves during downtime and recovery.

## Steps taken:
- To simulate a real-world failure scenario, I manually the RDS database instance  rebooted from the AWS console.
- During the reboot process, connection attempts from the EC2 instance failed as expected because the database was temporarily unavailable.
- After the reboot completed and the database returned to the _Available_ state, the EC2 instance successfully reconnected to the database using the MySQL client.

## Lessons learnt
Failure testing showed that even correctly configured infrastructure can experience temporary service interruptions. Observing the behaviour during database reboot helped build a better understanding of how cloud systems recover from operational events.

## Screenshots(words drop down to screnshots)
<details>
<summary><b>1. Simulated Database Failure via RDS Reboot</b></summary>
<img width="1919" height="800" alt="Simulated Database Failure via RDS Reboot" src="https://github.com/user-attachments/assets/f2f29390-a5e9-47f5-a8b8-185d9468ab39" />
</details>

<details>
<summary><b>2. Database Connection Failure During Downtime</b></summary>
<img width="1919" height="1006" alt="Database Connection Failure During Downtime" src="https://github.com/user-attachments/assets/b85b678d-5445-4492-a0e8-9ddf1bc13db1" />
</details>

<details>
<summary><b>3. Available State Restored</b></summary>
<img width="1919" height="795" alt="Available State Restored" src="https://github.com/user-attachments/assets/434600b7-86d7-4545-91cb-118bfbc7c613" />
</details>

<details>
<summary><b>4. Successful Database Reconnection After Recovery</b></summary>
<img width="1919" height="1005" alt="Successful Database Reconnection After Recovery" src="https://github.com/user-attachments/assets/113a2a40-ecb5-43b3-b22a-1a3061b58d30" />
</details>

[`← Previous: Multi-AZ database failover →`](High-Availabity.md) **.** [`Phase3 Home`](phase3-main.md) **.** [`Home`](./README.md) **.** [`Next: NAT Gateway vs Internet Gateway  →`](BastionHost.md)
  
