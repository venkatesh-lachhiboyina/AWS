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

Important Real-Time Concept
Snapshot Captures Blocks

It does NOT care about:

mount points
directories
filenames

It captures:

raw disk blocks
Database Snapshot Best Practice

For:

MariaDB
MySQL
PostgreSQL

Always stop DB or flush writes.

Otherwise:

corrupted logs possible
incomplete transactions possible
Crash Consistent vs Application Consistent
Type	Meaning
Crash-consistent	Like sudden power failure
Application-consistent	Clean DB shutdown before backup

EBS snapshot by default:

crash-consistent

Stopping DB gives:

application-consistent snapshot
Snapshot Restore Process
Create Volume from Snapshot

Snapshot → Actions → Create Volume

Choose:

size
AZ
type
Attach Volume

Example:

/dev/xvdf
Mount Volume
mount /dev/xvdf /data
Verify Data
ls -lah /data
Snapshot vs AMI
Snapshot	AMI
Backup of EBS volume	Full EC2 template
Storage only	OS + storage + config
Used for volumes	Used to launch EC2
Snapshot Use Cases
1. Backup

Daily automated backups.

2. Disaster Recovery

Recover deleted/corrupted server data.

3. Migration

Move data across AZs or regions.

4. Testing

Clone production database to test environment.

5. Rollback

Restore old stable state after failed deployment.

Important Commands
Check mounted disks
lsblk
Check filesystem usage
df -h
Flush filesystem buffers
sync
Stop MariaDB
systemctl stop mariadb
Mount restored volume
mount /dev/xvdf /restore
Common Mistakes
1. Snapshot while DB running

Can cause inconsistent recovery.

2. Deleting files before snapshot completes

Snapshot may capture deleted state.

3. Mounting wrong device

Example:

mounting /dev/xvdf
instead of
/dev/xvdf1
4. Forgetting same AZ

Volume and EC2 must be in same AZ.

5. Wrong permissions after restore

Fix:

chown -R mysql:mysql /var/lib/mysql
Snapshot Lifecycle Example
Create EBS Volume
        ↓
Store application data
        ↓
Stop application
        ↓
Create Snapshot
        ↓
Delete original volume
        ↓
Create new volume from snapshot
        ↓
Attach & mount
        ↓
Data restored
Interview Questions
What is EBS snapshot?

Backup of EBS volume stored internally in S3.

Are snapshots incremental?

Yes.

Can snapshot restore deleted data?

Yes, if snapshot was taken before deletion.

Can snapshot move across AZ?

Yes.

Why stop DB before snapshot?

To avoid inconsistent database state.

Real-Time DevOps Usage

Production companies use:

automated snapshot schedules
retention policies
lifecycle management
cross-region snapshot copies

for:

backups
DR
compliance
Easy Memory Trick
Snapshot = Backup of EBS volume
Used to restore lost data
