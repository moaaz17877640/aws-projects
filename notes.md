# Layer 3 — Task 3.3 Answers

## 1. If CPU hits 60% on one instance, what happens next — step by step?

1. CloudWatch collects the average CPU metric across all instances in the ASG.
2. When the average CPU utilization reaches the target value (60%), the Target Tracking policy is triggered.
3. The Auto Scaling Group calculates how many new instances are needed to bring the average CPU back down to 60%.
4. The ASG launches new EC2 instances using the Launch Template.
5. The new instances are registered with the ALB Target Group.
6. Once they pass the health checks, they start receiving traffic.

## 2. When does a new instance start receiving traffic? Why not immediately?

A new instance starts receiving traffic only after it passes the ALB health checks.
It does not receive traffic immediately because the instance needs time to boot up, start the application, and become healthy.
If traffic was sent before the app is ready, users would get errors.
The health check ensures the instance is fully ready before serving real users.

## 3. Why did we choose min=2 instead of min=1?

We chose min=2 for High Availability.
With min=2, the instances are placed in two different Availability Zones (AZ-a and AZ-b).
If one AZ or one instance fails, the other instance keeps the application running.
With min=1, a single failure would cause complete downtime.
