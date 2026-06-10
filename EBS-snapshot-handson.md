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

7. Unmount Volume
umount /var/lib/mysql
8. Detach Original Volume

Detach from EC2 in AWS console.

9. Create New Volume from Snapshot

Snapshot → Create volume

Same AZ as EC2.

10. Attach New Volume

Attach as:

/dev/xvdf
11. Mount Restored Volume
mount /dev/xvdf /var/lib/mysql
12. Check Files
ls -lah /var/lib/mysql

You SHOULD get all old files back.

13. Fix Permissions

Sometimes needed:

chown -R mysql:mysql /var/lib/mysql
14. Start MariaDB
systemctl start mariadb

Should work normally.

Important Concept

Snapshot captures:

filesystem blocks
exact state of disk at snapshot time

So even if you later:

delete files
format disk
detach volume

snapshot remains unchanged.

One Important Warning

If you do:

rm -rf /var/lib/mysql/*

WHILE EBS is NOT mounted there,
then you are deleting root-volume files instead.

Always verify mount first:

df -h

Check that:

/var/lib/mysql

is actually mounted from /dev/xvdf.

Best Practice for Testing

Instead of deleting immediately:

Mount restored snapshot somewhere else first:

mkdir /restore-test
mount /dev/xvdf /restore-test
ls -lah /restore-test

Safer and easier for debugging.
