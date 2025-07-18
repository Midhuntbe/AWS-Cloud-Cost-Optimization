# AWS-Cloud-Cost-Optimization
# AWS Cloud Cost Optimization – Identifying Stale EBS Snapshots

This project uses an AWS Lambda function to find and remove unnecessary EBS snapshots, illustrating a useful method for automated AWS cost optimization. It is a component of a broader effort to create cloud environments that are cost-conscious.

# Project Overview

EBS snapshots can build up over time, particularly in settings where instance or volume provisioning occurs frequently. These outdated snapshots add to needless storage expenses if they are not monitored.
This Lambda-based solution looks through all of the account's snapshots, checks to see if they are connected to any **active EC2 instances**, and removes any that are no longer required.

# How It Works

- **Step 1:** Fetches all EBS snapshots owned by the account (`Owner='self'`)
- **Step 2:** Retrieves all EC2 instances and associated volumes
- **Step 3:** For each snapshot:
  - Checks if the associated volume exists
  - Checks if it’s still attached to any active instance
  - If not, it’s considered **stale** and will be deleted
    
 > This ensures only truly unnecessary snapshots are removed.

# Tools & Services Used
  
- **AWS Lambda**
- **Boto3 (Python SDK)**
- **Amazon EC2**
- **Amazon CloudWatch (for logs)**
- **IAM (with permissions for EC2 and Snapshot deletion)**

# Screenshots

**Terminated instances**

<img width="1908" height="995" alt="Screenshot 2025-07-06 113536" src="https://github.com/user-attachments/assets/92320911-2bc6-410b-a967-c2ba5790d8c6" />

 **Lambda output** - Deleted all the snapshots that are not attached to a volumes

<img width="1915" height="965" alt="Screenshot 2025-07-06 113517" src="https://github.com/user-attachments/assets/eb3babf5-eb24-4c9a-921f-b2071e760f4a" />





