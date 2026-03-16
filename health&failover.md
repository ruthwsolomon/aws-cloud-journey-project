# Health Checks and Failover Testing

The target group was configured with HTTP health checks to monitor the availability of the registered EC2 instances. These checks ensure that only healthy instances receive traffic from the Application Load Balancer.

## Health Check Configuration

- Protocol: `HTTP`
- Path: `/`
- Interval: `30 seconds`
- Healthy threshold: `5`
- Unhealthy threshold: `2`

To verify the high availability behavior of the architecture, I simulated an instance failure.

## Failover Test
1. I connected to `Sharuz-EC2-1` via SSH.
2. I stopped the Apache web server: `sudo systemctl stop httpd`
3. After several health check cycles, the instance was marked unhealthy in the target group.
4. The load balancer automatically routed traffic only to Sharuz-EC2-2.
5. When the service was restarted: `sudo systemctl start httpd` the instance passed the health checks and was added back to the load balancing pool.

## Result
This test demonstrated how the architecture maintains high availability by automatically removing unhealthy instances and routing traffic only to healthy servers running on Amazon EC2.

## Screenshots (Click each arrow to expand)

<details>
<summary><b> 1. Configuring Target Group Health Checks</b> </summary>
<img width="1897" height="753" alt="image" src="https://github.com/user-attachments/assets/dc242de1-4689-4116-a3dd-91b7c794350e" />
</details>

<details>
<summary><b>2. Confirming Active Traffic Flow to Primary Target <code>Sharuz-EC2-1</code> Instance</b> </summary>
<img width="1914" height="183" alt="Screenshot 2026-03-16 194946" src="https://github.com/user-attachments/assets/9ee5961d-0385-4319-b7a5-71a9b0a5c604" />
</details>

<details>
<summary><b>3. Simulating Failure: Stopping <code>Sharuz-EC2-1</code> Instance</b></summary>
<img width="1919" height="1006" alt="image" src="https://github.com/user-attachments/assets/061c9c3f-695b-44ff-9d48-37342cd95c06" />
</details>

<details>
<summary><b>4. ALB Traffic Failover to <code>Sharuz-EC2-2</code> Instance</b></summary>
<img width="1914" height="252" alt="Screenshot 2026-03-16 195031" src="https://github.com/user-attachments/assets/6d74bdbc-1a0f-44c1-841e-a51ce31b7ced" />
</details>

<details>
<summary><b>5.  Monitoring Target Group: 'Unhealthy' Status Detected</b> </summary>
<img width="1919" height="748" alt="image" src="https://github.com/user-attachments/assets/50e92e4c-4df4-47be-be86-15e486cf6f68" />
</details>

<details>
<summary><b>6. Identifying the Specific Unhealthy Resource</b></summary>
<img width="1498" height="461" alt="image" src="https://github.com/user-attachments/assets/eded71da-f605-42ff-9a07-5b2285a6f1b7" />
</details>

<details>
<summary><b>7. Recovery: Restarting <code>Sharuz-EC2-1</code> Instance</b> </summary>
<img width="1919" height="1002" alt="image" src="https://github.com/user-attachments/assets/183d8f19-d605-48e9-ab81-54ae6549b21c" />
</details>

<details>
<summary><b>8. All Targets Return to 'Healthy' Status</b> </summary>
<img width="1893" height="749" alt="image" src="https://github.com/user-attachments/assets/3b5e80fc-fdfa-4a0b-8259-ea1485450530" />
</details>

<details>
<summary><b>9. Traffic Reversion: ALB Routes Traffic Back to  `Sharuz-EC2-1` Instance</b> </summary>
<img width="1918" height="231" alt="Screenshot 2026-03-16 195919" src="https://github.com/user-attachments/assets/bb11b21f-b348-4060-ac0e-6e04793b052a" /> 
</details>
