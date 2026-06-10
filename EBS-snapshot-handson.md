here i have created a volume and attached my instance and partiotioned and formatted and mounted it in a /var/lib/mysql path then i creted a snapshot and
umounted and deleted the volume and recoverd every file in that path here is the setp by step flow


Step-by-Step Proper Flow
1. Mount EBS volume

Example:

mount /dev/xvdf /var/lib/mysql
2. Start MariaDB
systemctl start mariadb

MariaDB creates/uses files in that mounted EBS volume.

3. Verify files exist
ls -lah /var/lib/mysql

You should see:

mysql/
performance_schema/
ibdata1
aria_log*
4. Stop MariaDB BEFORE Snapshot

Very important:

systemctl stop mariadb
sync
5. Create Snapshot

In AWS:

EBS → Volumes
Select volume
Create snapshot

WAIT until snapshot status becomes:

completed

Do NOT continue before completion.

6. Delete Files (for testing)

Example:

rm -rf /var/lib/mysql/*

Now directory becomes empty.
