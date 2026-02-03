Amazon S3 is an object storage service in AWS used to store and retrieve any amount of data from anywhere over the internet.

Think of it as cloud-based hard storage, but:
Highly durable
Scalable (no size limits practically)
Pay only for what you use


Key Concepts in S3
1. Bucket
 -A bucket is like a folder/container
 -Every object must be stored inside a bucket
 -Bucket name must be globally unique

Example: my-company-backups


2. Object

 -The actual data/file
 -Can be anything: image, video, PDF, logs, backups, etc.
 -Each object has:
 -Key (file name / path)
 -Value (file content)
 -Metadata
Example key:
 -logs/2025/app.log


3. Object Size Limits

-Min: 0 bytes
-Max: 5 TB per object
-For files > 5 GB → Multipart upload


Why do we use S3?

✔ Backup & restore
✔ Static website hosting
✔ Application logs
✔ Data lake & analytics
✔ Media storage (images/videos)
✔ Disaster recovery


S3 Storage Classes (Very Important)
Storage Class  =	Use Case
Standard	= Frequently accessed data
Intelligent-Tiering =	Unknown access pattern
Standard-IA	 = Infrequent access
One Zone-IA	 = Infrequent + single AZ
Glacier Instant Retrieval =	Rare access, fast retrieval
Glacier Flexible Retrieval =	Archive, minutes–hours
Glacier Deep Archive =	Long-term archive (cheapest)


Durability & Availability
Durability: 99.999999999% (11 9’s)

Data automatically stored across multiple Availability Zones

Security in S3
1. Access Control
 -IAM policies
 -Bucket policies
 -ACLs (legacy, rarely used)

2. Encryption
 At rest
 -SSE-S3
 -SSE-KMS
 -SSE-C
In transit
 -HTTPS



S3 Versioning
Keeps multiple versions of the same object

Protects from:
Accidental delete
Overwrite
Must be enabled at bucket level



S3 Lifecycle Rules

Automates data movement:
Move data to cheaper storage
Delete old objects automatically

Example:
After 30 days → Standard-IA
After 90 days → Glacier
After 365 days → Delete



S3 Static Website Hosting

Host HTML/CSS/JS files
Cheap and fast
Supports:
Index document
Error document



Common Interview Points ⭐

S3 is object storage, not block/file storage
S3 is region-specific
Buckets are globally unique
Not suitable for OS boot volumes
Strong read-after-write consistency
