# Analyzing Scaling in CloudWatch (Metrics Reading)

To go beyond basic setup, I performed **functional validation testing** on the Auto Scaling Group (ASG) to confirm that the system behaves reliably under repeated stress and not just once.

## Testing Strategy (Why I Ran It Twice)

In real-world environments, a single successful scaling event isn’t enough to prove stability. I deliberately triggered the scaling policy twice to validate:

- **Reliability:** Confirm that CloudWatch Alarms consistently trigger scaling actions
- **Consistency:** Verify that the ASG cooldown period works correctly, allowing the system to stabilize before scaling again

This **double-stress** approach ensures the system isn’t a one-time success, but a repeatable and dependable setup.

## Load Simulation

I used the stress utility to generate high CPU load `--cpu 4` across two separate 120-second intervals:

- **Run 1:** Triggered the initial scale-out event
- **Run 2:** Confirmed the system could sustain or adjust capacity under continued demand

## Observations & Metrics (CloudWatch Graph)

The CloudWatch graph captures the full scaling lifecycle:

### Scaling Gap Visibility:

At 07:45 UTC, there is a clear gap where:
- `GroupDesiredCapacity` = 3
- `GroupInServiceInstances` = 2.8

This reflects the transition phase as a new instance moves from `Pending` to `InService`

### Full Recovery (Scale-In):
After the stress test ended, CPU usage dropped and the Low CPU alarm triggered.
The ASG successfully scaled back down to a cost-efficient baseline of 1 instance

## Technical Insight

By documenting two distinct load spikes, this test confirms that the scaling policy is not a one-time event. It operates as a robust automated feedback loop, where `GroupInServiceInstances` dynamically follows demand and responds correctly to real-time traffic changes.

## Evidence of Scaling Lifecycle (each line drops to a screenshot)

<details>
<summary>1. Auto Scaling Group Metric Collection Enabled</summary>
<img width="1413" height="469" alt="Screenshot 2026-03-19 094509" src="https://github.com/user-attachments/assets/96f47894-b6ca-47ad-a40f-17feae7a3245" />
</details>

<details>
<summary>2. Stress Tool Setup and CPU Load Simulation (Double Run – 4 CPUs)</summary>
<img width="1915" height="1004" alt="Screenshot 2026-03-19 095704" src="https://github.com/user-attachments/assets/47adcdcb-2acb-4377-96e5-f362cdddd782" />
</details>

<details>
<summary>3. Key Scaling Metrics Selected (Desired vs In-Service Capacity)</summary>
<img width="1892" height="302" alt="image" src="https://github.com/user-attachments/assets/16dfb4dc-8f53-416b-b767-60d67088fa58" />
<img width="1879" height="289" alt="image" src="https://github.com/user-attachments/assets/e160881f-609b-4ba5-ab0e-d1a38e7c6d3c" />
</details>

<details>
<summary>4. Scale-Out Response Under Sustained Load (Double Stress Execution)</summary>
<img width="1900" height="655" alt="Screenshot 2026-03-19 095538" src="https://github.com/user-attachments/assets/3a10aab8-bf13-4b16-93d1-4eec058c3a3a" />
</details>

<details>
<summary>5. Scale-In Behaviour After Cooldown (Return to Baseline Capacity)</summary>
<img width="1910" height="587" alt="Screenshot 2026-03-19 102027" src="https://github.com/user-attachments/assets/b964ac33-0d4a-4e04-aa58-e0ccde3606be" />
</details>

