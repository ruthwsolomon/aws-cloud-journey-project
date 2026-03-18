[`← Previous:  NAT Gateway vs Internet Gateway`](BastionHost.md) **.** [`Home`](./README.md) **.** [`Next: Application Load Balancing → `](ALB1.md)

# PHASE 4

## Production Architecture

In this phase, I transformed the environment into a production-ready architecture by implementing load balancing, automatic scaling, and monitoring. The goal was to make the system elastic, resilient, and able to handle real-world traffic.

## Accomplishments

- [Application Load Balancer](ALB1.md) - Deployed an ALB to distribute traffic across multiple EC2 instances for high availability.
- [Scalable Web Architecture](aws-auto-scaling-practice.md) - Configured an Auto Scaling Group with a launch template connected to the ALB, enabling automatic scale-out and scale-in based on demand.
- [Stress Test (Dynamic Scaling Demo.)](ASG-Stress-Test.md) - Successfully CPU stress tests to trigger scaling events, validating that the architecture dynamically adjusts capacity to handle load efficiently. 
- [CloudWatch Metrics](BastionHost.md) – Monitored CPU utilization, desired capacity, and in-service instances in CloudWatch to verify that the scaling policy worked as expected and resources were used efficiently.
