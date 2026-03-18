# AWS Auto Scaling Stress Test – Dynamic Scaling Demonstration

To test the Auto Scaling Group I set up in my [AWS Scalable Web Architecture project](aws-auto-scaling-practice.md), I ran a CPU stress test to simulate real-world load and see how the infrastructure reacts. The goal was to observe automatic **scale-out and scale-in behavior** and validate that the scaling policy worked as expected.

## Configuration Details:

- **Automatic Scaling policy type:** Dynamic scaling
- **Scaling Policy:** Target Tracking policy
- **Metric type:** Average CPU utilization
- **Target value:** 50% (later lowered to 30% for more sensitivity)
- **Instance warm-up:** 60s (shortened for testing)

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

## Architecture Evidence (Each topic drops down to a screenshot)

<details>
<summary><b>1. ASG – Target Tracking Policy</b></summary>
<img width="1895" height="743" alt="image" src="https://github.com/user-attachments/assets/9caa1da5-e03e-42d5-8d0c-539310b99107" />
</details>

<details>
<summary><b>2. ASG Activity History</b></summary>
<img width="1879" height="749" alt="image" src="https://github.com/user-attachments/assets/9c83a316-1ff5-4e39-8dfa-3fecd83380de" />
</details>

<details>
<summary><b>3. EC2 Instances – Initial State</b></summary>
<img width="1494" height="236" alt="Screenshot 2026-03-18 130752" src="https://github.com/user-attachments/assets/2f91fd5b-45ee-4978-a06f-173f11d3a72b" />
</details>

<details>
<summary><b>4. ALB Target Group – Initial State</b></summary>
<img width="1893" height="731" alt="Screenshot 2026-03-18 131524" src="https://github.com/user-attachments/assets/3a2185e6-eae1-4b1a-8304-37708b958fee" />
<img width="1507" height="488" alt="Screenshot 2026-03-18 131537" src="https://github.com/user-attachments/assets/27b0f281-4c36-49c6-a093-04d2afbd9734" />
</details>

<details>
<summary><b>5. Scale-In Trigger Command</b></summary>
<img width="1918" height="1000" alt="Screenshot 2026-03-18 125627" src="https://github.com/user-attachments/assets/a950e126-953e-46c7-9712-34db18d422a6" />
</details>

<details>
<summary><b>6. EC2 Instances – After Scale-In</b></summary>
<img width="1887" height="438" alt="Screenshot 2026-03-18 140747" src="https://github.com/user-attachments/assets/6c4aa805-a281-4e82-b3c7-b26f41536408" />
</details>

  <details>
<summary><b>7. Installing Stress Tool & Running CPU Stress Test (scale out)</b></summary>
<img width="1919" height="1002" alt="Screenshot 2026-03-18 143445" src="https://github.com/user-attachments/assets/f2f5c80b-65b4-4381-92d7-70e15ac58820" />
</details>

  <details>
<summary><b>8. EC2 Instances – After Scale-Out</b></summary>
<img width="1517" height="425" alt="Screenshot 2026-03-18 143658" src="https://github.com/user-attachments/assets/91f5e26b-bef3-41b4-aedd-6375468e717c" />
</details>

  <details>
<summary><b>9. ALB Target Group – After Scale-Out</b></summary>
  <img width="1512" height="666" alt="Screenshot 2026-03-18 144040" src="https://github.com/user-attachments/assets/058ed4a5-88b5-45cd-874f-69477e92f1f9" />
<img width="1523" height="666" alt="Screenshot 2026-03-18 144029" src="https://github.com/user-attachments/assets/3e1b1045-dbd6-4cfa-8375-9478897fa07e" />
</details>
 
