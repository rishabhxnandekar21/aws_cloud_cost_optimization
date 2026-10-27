# AWS Cloud Cost Optimization – Identifying Stale EBS Snapshots

## Overview

This project uses AWS Lambda and Python (Boto3) to identify and delete potentially unused Amazon EBS snapshots, helping optimize AWS storage costs.

## How It Works

1. **Retrieve EBS Snapshots:** Fetches all EBS snapshots owned by the current AWS account using `describe_snapshots(OwnerIds=['self'])`.
2. **Identify Running EC2 Instances:** Retrieves EC2 instances in the `running` state and stores their instance IDs.
3. **Check Snapshot Volumes:** Examines the volume associated with each snapshot.
4. **Identify Potentially Stale Snapshots:** Identifies snapshots whose associated volume has no attachments or whose associated volume no longer exists.
5. **Delete Snapshots:** Uses the `delete_snapshot()` API to delete snapshots matching these conditions.
6. **Log Cleanup Operations:** Prints messages identifying the snapshots deleted and the reasons for deletion.

## Technologies Used

- **AWS Lambda** – Executes the automated cleanup function.
- **Amazon EC2** – Retrieves instance and volume information and manages snapshots.
- **Amazon EBS** – Provides snapshot storage.
- **Python & Boto3** – Implements AWS API interactions.
- **AWS IAM** – Provides the permissions required to access and delete snapshots.

## Key Features

- Automated EBS snapshot discovery.
- Identification of snapshots associated with unattached or deleted volumes.
- Automated snapshot deletion.
- Logging of deletion operations for basic monitoring.

## Cost Optimization

Removing potentially unnecessary EBS snapshots helps reduce storage costs and limits the accumulation of unused cloud resources.

**Note:** The current code checks whether a volume has any attachments, not whether it is attached to one of the running instances collected earlier. Snapshots can also be important backups, so validate deletion candidates before using this function in production.
