[`← Previous:  NAT Gateway vs Internet Gateway`](BastionHost.md) **.** [`Home`](./README.md) **.** [`Next: Application Load Balancing → `](ALB1.md)

# PHASE 4

## Production Architecture

In this phase, I transformed the environment into a production-ready architecture by implementing load balancing, automatic scaling, and monitoring. The goal was to make the system elastic, resilient, and able to handle real-world traffic.

## Accomplishments

- [Application Load Balancing (AWS High Availability Architecture)](ALB1.md) - Deployed an ALB to distribute traffic across multiple EC2 instances for high availability.
- [AWS Scalable Web Architecture with Auto Scaling & Application Load Balancer)](aws-ato-scaling-practice.md) - Configured an Auto Scaling Group with a launch template connected to the ALB, enabling automatic scale-out and scale-in based on demand.
- [AWS Auto Scaling Stress Test (Dynamic Scaling Demonstration)](ASG-Stress-Test.md) - Ran CPU stress tests to trigger scaling events, validating that the architecture dynamically adjusts capacity to handle load efficiently.
- [Analyze Scaling in CloudWatch (Metrics Reading)](BastionHost.md) – Monitored CPU utilization, desired capacity, and in-service instances in CloudWatch to verify that the scaling policy worked as expected and resources were used efficiently.
