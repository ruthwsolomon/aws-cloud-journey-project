# AWS Auto Scaling Stress Test – Dynamic Scaling Demonstration

To test the Auto Scaling Group I set up in my AWS Scalable Web Architecture project, I ran a CPU stress test to simulate real-world load and see how the infrastructure reacts. The goal was to observe automatic **scale-out and scale-in behavior** and validate that the scaling policy worked as expected.

## Configuration Details:

- Automatic Scaling policy type: Dynamic scaling
- Scaling Policy: Target Tracking policy
- Metric tpe: Average CPU utilization
- Target value: 50% (later lowered to 30% for more sensitivity)
- Instance warm-up: 60s (shortened for testing)

## Stress Test Steps:

**1. SSH into one of the EC2 instances:** `ssh -i ph3.pem ec2-user@<Public-IP>`

**2. Installed the stress tool:** `sudo yum install -y stress`

**3. Ran initial CPU stress:** `stress --cpu 4 --timeout 120`

_**Result:** One instance terminated due to low traffic. This confirmed the **scale-in mechanism** was working to reduce costs during periods of low overall traffic._

**4. Adjusted test:** `stress --cpu 4 --timeout 600` and lowered CPU target to `30%`

_**Result:** ASG detected high CPU load and 4 new instances launched automatically to handle increased traffic._

## What I Learned
- Target Tracking scaling responds to CPU spikes dynamically
- Scale-in works to save costs when traffic is low
- Even a single stressed instance can trigger scale-out when thresholds are adjusted
- Stress testing validates elasticity and resiliency of AWS architecture

## Skills Demonstrated

- Configuring Auto Scaling Groups and Target Tracking policies
- Running real-world stress tests on EC2 instances
- Monitoring and interpreting scaling behavior
- Understanding cost-saving scale-in mechanisms
- Verifying instance health and ALB registration
