Environment

• AWS region: eu-north-1 (Stockholm)  
• EC2 instance type: t3.micro
• OS: Ubuntu
• Splunk: local Splunk Enterprise trial/free setup

What I Implemented

1. EC2 Instance Deployment

• Launched a Linux EC2 instance in AWS
• Restricted SSH access to a specific public IP in the security group
• Used key-based SSH authentication

2. IAM Role + Systems Manager

• Created and attached an EC2 IAM role with AmazonSSMManagedInstanceCore
• Verified the instance as a managed node in AWS Systems Manager
• Troubleshot SSM registration by validating IMDSv2-based role credential access and restarting the SSM agent

3. CloudTrail Logging

• Created a CloudTrail trail and enabled logging for AWS management events
• Verified logged activity in CloudTrail Event History
• Reviewed audit details including event name, event source, user identity, AWS region, and source IP address

4. VPC Flow Logs

• Enabled VPC Flow Logs and sent output to CloudWatch Logs
• Created a dedicated IAM role for Flow Logs publishing
• Verified flow log delivery to CloudWatch

5. Splunk Ingestion and Analysis

• Downloaded CloudTrail logs from the S3 bucket used by CloudTrail
• Resolved file handling issues caused by .json.gz compression by extracting valid JSON before ingestion
• Uploaded CloudTrail log data into Splunk
• Used SPL to parse nested JSON records and summarize cloud activity

Lessens Learned:
• IAM roles are safer than storing static credentials on hosts
• Systems Manager depends on correct IAM role access and metadata service behavior
• Splunk ingestion can require manual parsing when JSON records are nested inside arrays
• Security analysis often involves troubleshooting the logging pipeline before the actual investigation work begins

Future Improvements:
• Add GuardDuty when account plan/billing allows it
• Ingest VPC Flow Logs into Splunk
• Build simple dashboards for user activity, source IPs, and event types
• Add a small incident simulation workflow and written findings
