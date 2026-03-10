[`← Previous: Configure automated DB snapshots →`](data-durability.md) **.** [`Phase3 Home`](phase3-main.md) **.** [`Home`](./README.md) **.** [`Next: Configure automated DB snapshots →`](data-durability.md)

# Multi-AZ Database Failover (High Availability)

The objective was to ensure high availability for the database by deploying it across multiple Availability Zones (AZs) so it can survive hardware or AZ failure.

### Architecture
- **Primary DB**: in AZ1, private subnet.  
- **Standby DB**: in AZ2, private subnet.  
- **EC2 Instance**: public subnet, connects securely to the DB.  
- **Failover Mechanism**: automatic; EC2 connects via the same endpoint, no code changes required.

### Steps Taken
1. Enabled Multi-AZ on the RDS instance.  
2. Rebooted the DB with failover for testing.  
3. Verified EC2 connectivity after failover.

### Result
- Database remained available during failover.  
- Endpoint did not change and EC2 connection remained functional.  
- High availability confirmed.

### Evidence
Screenshot of RDS showing Multi-AZ configuration and successful failover:

