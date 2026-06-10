AWS Snapshot Notes
What is Snapshot in AWS?

A snapshot is a backup of an EBS volume.

AWS stores snapshots internally in Amazon Simple Storage Service.

Used for:

backup
disaster recovery
restoring deleted data
cloning servers
migration
Real-Time Example

Suppose:

EC2 server running MariaDB
EBS volume mounted at:
/var/lib/mysql

You create snapshot before:

patching
deployment
risky changes

If server/data gets corrupted:

create new EBS volume from snapshot
attach to EC2
restore data
Snapshot Architecture
EC2
 ↓
EBS Volume
 ↓
Snapshot (stored in S3 internally)
 ↓
Create New Volume
 ↓
Attach to EC2
Important Characteristics
1. Incremental Backup

First snapshot:

copies all blocks

Next snapshots:

only changed blocks copied

Benefits:

storage efficient
faster
2. Point-in-Time Backup

Snapshot captures disk state at that moment.

3. AZ Independent

Snapshot is region-level.

Example:

volume in ap-south-1a
snapshot usable in:
ap-south-1a
ap-south-1b
ap-south-1c
Snapshot Workflow
Step 1 — Create Volume

Attach EBS to EC2.

Step 2 — Store Data

Example:

DB files
logs
application data
Step 3 — Stop Application (Best Practice)

For databases:

systemctl stop mariadb
sync

Ensures consistent backup.

Step 4 — Create Snapshot

AWS Console:

EBS
Volumes
Actions
Create Snapshot
Step 5 — Wait for Completion

Snapshot status must become:

completed

NOT:

pending
Step 6 — Restore

Snapshot → Create Volume

Attach to EC2.

Mount filesystem.
