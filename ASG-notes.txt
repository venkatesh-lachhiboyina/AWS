ASG notes

key point : always use shared storage (EFS)

ASG (Auto Scaling Group) in AWS 🚀

-An Auto Scaling Group (ASG) is an AWS service that automatically manages EC2 instances for you so your application always has the right number of servers running.


Why ASG is used

✅ High availability – replaces unhealthy instances automatically
📈 Scalability – adds/removes EC2 instances based on load
💰 Cost optimization – you pay only for what you use
🤖 Automation – no manual instance management





Core components of ASG

1.Launch Template / Launch Configuration

 -AMI, instance type
 -Security group, key pair
 -User data (startup scripts)

2.Auto Scaling Group

 -Minimum instances
 -Maximum instances
 -Desired capacity
 -VPC & subnets

3.Scaling Policies

 -When to scale out or in
 
 

How ASG works (simple flow)

1.You define min, max, desired EC2 instances
2.ASG launches EC2 instances using the launch template
3.ASG monitors instance health
4.If an instance fails → new one is created automatically
5.If traffic increases → scale out
6.If traffic decreases → scale in




Types of scaling

1.Dynamic Scaling

 -Based on CloudWatch metrics (CPU, memory, requests)
 -Example: CPU > 70% → add instance

2.Step Scaling

 -Scale more aggressively for bigger metric changes

3.Target Tracking

 -Maintain a target (e.g., CPU at 50%)

4.Scheduled Scaling

 -Scale at specific times (office hours, sales events)
 
 
 
 
 

.Health checks
 
 -EC2 health check
 -ELB health check (recommended)
 -Unhealthy instances are terminated & replaced





.ASG with Load Balancer

Most common setup:

User → ALB → Auto Scaling Group → EC2 instances

 -Load is evenly distributed
 -Zero downtime scaling





Real-world example

👉 E-commerce website

 -Normal traffic → 2 EC2 instances
 -Sale starts → ASG scales to 10 instances
 -Sale ends → scales back to 2



Key interview points 💡

 -ASG works only with EC2
 -ASG ensures desired capacity
 -ASG + ALB + CloudWatch is a standard architecture
 -You cannot manually attach random EC2; ASG controls lifecycle
