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
1. I connected to Sharuz-EC2-1 via SSH.
2. I stopped the Apache web server: `sudo systemctl stop httpd`
3. After several health check cycles, the instance was marked unhealthy in the target group.
4. The load balancer automatically routed traffic only to Sharuz-EC2-2.
5. When the service was restarted: `sudo systemctl start httpd` the instance passed the health checks and was added back to the load balancing pool.

## Result
This test demonstrated how the architecture maintains high availability by automatically removing unhealthy instances and routing traffic only to healthy servers running on Amazon EC2.
