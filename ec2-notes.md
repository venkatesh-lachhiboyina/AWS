What is EC2?

EC2 (Elastic Compute Cloud) is a service provided by Amazon Web Services that allows you to create and manage virtual servers (VMs) in the cloud.

Think of EC2 as:

Your Laptop
    ↓
Virtual Machine in AWS
    ↓
EC2 Instance
Why EC2?

Before cloud:

Buy Server
Install OS
Configure Network
Maintain Hardware

Problems:

Expensive (CAPEX)
Takes weeks/months
Scaling is difficult

With EC2:

Launch VM
Pay as you use
Scale anytime

Benefits:

Fast provisioning
Pay-as-you-go
Auto Scaling
Global availability
EC2 Components
1. AMI (Amazon Machine Image)

An AMI is a template used to launch an EC2 instance.

Examples:

Ubuntu
Amazon Linux
Red Hat Linux
Windows Server

Analogy:

AMI = Blueprint
EC2 = House built from blueprint
2. Instance Type

Defines CPU, RAM, and performance.

Examples:

t2.micro
t3.micro
t3.large
m5.large

Example:

t2.micro
1 vCPU
1 GB RAM
3. Key Pair

Used for SSH access.

When launching EC2:

Create Key Pair
Download .pem file

Connect:

ssh -i mykey.pem ec2-user@PUBLIC_IP

Without the key pair, you usually cannot SSH into the instance.

4. Security Group

Acts like a firewall.

Controls:

Inbound Traffic
Outbound Traffic

Example:

SSH    TCP 22    My IP
HTTP   TCP 80    Anywhere
HTTPS  TCP 443   Anywhere

Important:

Security Groups are stateful.

5. Public IP

Assigned to an instance for internet access.

Example:

54.123.45.67

SSH:

ssh -i key.pem ec2-user@54.123.45.67
EC2 Lifecycle
Launch
  ↓
Running
  ↓
Stopped
  ↓
Started
  ↓
Terminated
Running

Server is active.

Charges:

Compute + Storage
Stopped

VM powered off.

Charges:

Only EBS Storage

No compute charges.

Terminated

Server permanently deleted.

Cannot start again.

Common EC2 Commands

Check connectivity:

ping <ip>

SSH:

ssh -i key.pem ec2-user@ip

Check OS:

cat /etc/os-release

Check uptime:

uptime
