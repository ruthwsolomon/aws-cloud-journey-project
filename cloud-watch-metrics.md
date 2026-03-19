# Analyzing Scaling in CloudWatch (Metrics Reading)

To go beyond basic setup, I performed **functional validation testing** on the Auto Scaling Group (ASG) to confirm that the system behaves reliably under repeated stress and not just once.

## Testing Strategy (Why I Ran It Twice)

In real-world environments, a single successful scaling event isn’t enough to prove stability. I deliberately triggered the scaling policy twice to validate:

- **Reliability:** Confirm that CloudWatch Alarms consistently trigger scaling actions
- **Consistency:** Verify that the ASG cooldown period works correctly, allowing the system to stabilize before scaling again

This “double-stress** approach ensures the system isn’t a one-time success, but a repeatable and dependable setup.

## Load Simulation

I used the stress utility to generate high CPU load `--cpu 4` across two separate 120-second intervals:

- Run 1: Triggered the initial scale-out event
- Run 2: Confirmed the system could sustain or adjust capacity under continued demand

## Observations & Metrics (CloudWatch Graph)

The CloudWatch graph captures the full scaling lifecycle:

### Scaling Gap Visibility:**

At 07:45 UTC, there is a clear gap where:
- `GroupDesiredCapacity` = 3
- `GroupInServiceInstances` = 2.8
This reflects the transition phase as a new instance moves from `Pending` to `InService`

### Full Recovery (Scale-In):
After the stress test ended, CPU usage dropped and the Low CPU alarm triggered.
The ASG successfully scaled back down to a cost-efficient baseline of 1 instance

## Technical Insight

By documenting two distinct load spikes, this test confirms that the scaling policy is not a one-time event. It operates as a robust automated feedback loop, where `GroupInServiceInstances` dynamically follows demand and responds correctly to real-time traffic changes.
