[`← Previous: SG chaining (EC2 ↔ RDS) →`](controlled-access.md) **.** [`Phase3 Home`](phase3-main.md) **.** [`Home`](./README.md) **.** [`Next: Multi-AZ database failover →`](High-Availability.md)

## Manual Database Snapshot

The objective was to create a manual database snapshot to ensure *data durability* and provide a reliable *recovery point*. This allows the database to be restored to a known state in case of accidental data loss, configuration errors, or infrastructure changes.

## Architecture Used

- **Amazon RDS**: MySQL database hosted in a *private subnet* to ensure secure network isolation.
- **Amazon EC2**: Publicly accessible instance used to connect and manage the database.
- **Security Groups**: Configured to allow database access only from the EC2 instance.
- **Manual Snapshot**: Captures the state of the RDS database at a specific point in time, stored within AWS for point-in-time recovery.

### Steps Performed

1. Navigated to the **Amazon RDS Console**.
2. Selected the running database instance.
3. Clicked **Actions → Take snapshot**.
4. Entered a snapshot identifier.
5. Created the snapshot and waited for the status to change to **Available**.

### Result

The manual snapshot was successfully created and stored in Amazon RDS. This backup can be used to restore the database or create a new database instance if recovery is required.

### Screenshots
## Modifying the DB back up settings
<img width="1861" height="785" alt="image" src="https://github.com/user-attachments/assets/5e7e7a08-9b6b-4ffa-b714-75033fc10bb9" />
<img width="1892" height="741" alt="image" src="https://github.com/user-attachments/assets/55db6759-41b9-42d9-b701-6a1ea342ebca" />

<img width="1860" height="750" alt="image" src="https://github.com/user-attachments/assets/d8ab48e5-ad8a-4c2d-893e-390d838163dd" />

## Taking Manual Snapshots
<img width="1892" height="743" alt="image" src="https://github.com/user-attachments/assets/111ad2fd-2084-458b-94c4-d6b1c3064d98" />

## Manual Snapshots created
<img width="1887" height="794" alt="image" src="https://github.com/user-attachments/assets/25666e1d-1e24-4d0b-9330-feac55dc9fe1" />

[`← Previous: SG chaining (EC2 ↔ RDS) →`](controlled-access.md) **.** [`Phase3 Home`](phase3-main.md) **.** [`Home`](./README.md) **.** [`Next: Multi-AZ database failover →`](High-Availability.md)

