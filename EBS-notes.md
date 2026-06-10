AWS EBS (Elastic Block Store) Notes
What is EBS?

Amazon Elastic Block Store is a block storage service used with Amazon EC2 instances.

Think of it like:

EC2 = Computer/Server
EBS = Hard Disk attached to that server

It stores:

OS files
Application files
Databases
Logs
Persistent data

Even if EC2 stops/restarts, data in EBS remains.

Real-Time Example

Suppose you launch:

EC2 instance for a Java application
EBS volume attached as storage

Your:

Linux OS
Application code
MySQL/PostgreSQL data
Logs

all are stored in EBS.

If EC2 crashes:

You can attach same EBS to another EC2
Data remains safe
Main Features of EBS
1. Persistent Storage

Data remains even after:

reboot
stop/start

But if you terminate EC2:

EBS may delete or may retain depending on setting.
2. Attached to EC2

EBS cannot work alone.
It must attach to EC2.

One EBS volume:

Usually attached to one EC2 at a time.
3. Availability Zone (AZ) Specific

EBS volume and EC2 should be in same AZ.

Example:

EC2 → ap-south-1a
EBS → ap-south-1a

Otherwise attachment fails.

EBS Volume Types
1. gp3 (General Purpose SSD)

Most commonly used.

Best for:

web apps
dev/test
small-medium databases

Features:

SSD based
Good balance of performance and cost

Default choice in most projects.

2. io1 / io2 (Provisioned IOPS SSD)

High performance disks.

Used for:

high traffic databases
banking apps
production DB workloads

Provides:

very high IOPS
low latency

Costly.

3. st1 (Throughput Optimized HDD)

Good for:

big logs
analytics
streaming workloads

Not for boot volume.

4. sc1 (Cold HDD)

Cheapest.

Used for:

backups
rarely accessed data

Very slow.

Important Terms
Volume

The actual virtual disk.

Example:

20GB EBS volume
Snapshot

Backup of EBS volume stored in Amazon Simple Storage Service.

You can:

restore volume
create new volumes
recover data

Real-time use:

before production deployment take snapshot
IOPS

Input Output Operations Per Second.

Measures disk speed.

Higher IOPS = faster disk performance.

Encryption

EBS supports encryption using AWS Key Management Service.

Used for:

security compliance
protecting sensitive data
EBS Lifecycle Example
Step 1

Launch EC2.

Step 2

Attach EBS volume.

Step 3

Mount volume in Linux.

Example:

lsblk
sudo mkfs -t xfs /dev/xvdf
sudo mkdir /data
sudo mount /dev/xvdf /data
Resize EBS Volume

Suppose disk becomes full.

You can increase:

20GB → 50GB

Without server downtime (mostly).

Steps:

Modify volume in AWS
Extend filesystem in Linux

Example:

sudo growpart /dev/xvda 1
sudo xfs_growfs -d /
EBS vs Instance Store
Feature	EBS	Instance Store
Persistent	Yes	No
Data after stop	Remains	Lost
Best for	Long-term storage	Temporary cache
Backup	Snapshot supported	No snapshot
Multi-Attach

Some io1/io2 volumes support attaching to multiple EC2s simultaneously.

Used in:

clustered applications
high availability systems
