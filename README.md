# AWS-Day-45-Cloudtrail-logging

# AWS CloudTrail - Account-Wide Activity Logging

Set up CloudTrail to log every single thing that happens in my AWS account. Now I have a complete audit trail of who did what, when and from where.

What was Built

Created a multi-region CloudTrail trail that records all management events across every AWS region. The logs get stored in an S3 bucket with automatic cleanup after 90 days to keep costs down.

The Setup
Trail Configuration:
* Name: account-activity-trail
* Coverage: All AWS regions (not just one)
* Events: Management events (Read + Write)
* Storage: S3 bucket with lifecycle policy
* Validation: Log file integrity checks enabled

Why Multi-Region Matters:
If someone creates resources in Tokyo or any other region I don't normally use, CloudTrail still catches it. This is important because attackers often operate in regions you're not monitoring.

What Gets Logged
Every API call made in my account:
* Creating or deleting EC2 instances
* Modifying IAM users and permissions
* Changes to security groups
* S3 bucket operations
* Literally everything

Each log entry shows:
* Who made the call (IAM user or role)
* What action they performed
* When it happened (exact timestamp)
* Where they were (IP address)
* Which region it happened in
* Whether it succeeded or failed

S3 Storage
All logs are stored in S3 with:
* Organized folder structure by date and region
* Compressed JSON files (.json.gz format)
* Automatic deletion after 90 days (lifecycle policy)
* Bucket policy restricting write access to CloudTrail only

So if someone deletes something at 3 AM, I know exactly who did it, from which IP address, and what they deleted.


Real-World Use Cases

Security Incident Response:
If my AWS bill suddenly spikes or resources get deleted, I can check CloudTrail to see exactly what happened and who did it.

Compliance Audits:
Many compliance standards (SOC 2, HIPAA, PCI-DSS) require audit logs. CloudTrail provides the complete activity history auditors need.

Troubleshooting:
When something breaks, CloudTrail shows what changed. "Who modified that security group?" - check the logs.

Unauthorized Access:
If someone compromises an IAM user, CloudTrail logs show every action they took, which helps with damage assessment and recovery.

What I Learned

CloudTrail is essentially a security camera for your AWS account. It records everything and that's incredibly valuable for both security and troubleshooting.

The multi-region capability is critical, you need to monitor all regions not just the ones you actively use.

Log file validation is important for proving logs haven't been tampered with especially for compliance requirements.

The S3 lifecycle policy is necessary because logs pile up fast and can get expensive if you're not managing retention.
