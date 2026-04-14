# AWS Cloud Security Monitoring Lab with Splunk

## Overview
Built a small AWS cloud security lab to practice cloud auditing, network visibility, and SIEM-based log analysis. The project focused on securing and monitoring an EC2 instance, enabling AWS-native logging, and importing CloudTrail data into Splunk for analysis using SPL.

## Goals
- Deploy and manage a Linux EC2 instance in AWS
- Use IAM role-based access instead of long-lived credentials on the host
- Configure AWS Systems Manager for secure instance management
- Enable CloudTrail for AWS audit logging
- Enable VPC Flow Logs for network traffic metadata
- Import CloudTrail logs into Splunk and practice log parsing and analysis

## Architecture
```text
+-------------------+       +-----------------------+
| AWS EC2 Instance  |       | AWS Control Plane     |
| Ubuntu t3.micro   |       | IAM / CloudTrail      |
| IAM Role attached |       | VPC Flow Logs         |
+---------+---------+       +-----------+-----------+
          |                                 |
          | SSM Managed Node                | Logs
          v                                 v
+-------------------+              +-------------------+
| AWS Systems       |              | S3 / CloudWatch   |
| Manager (SSM)     |              | Log Storage       |
+-------------------+              +---------+---------+
                                             |
                                             | Download / ingest
                                             v
                                    +-------------------+
                                    | Local Splunk      |
                                    | Search & Reporting|
                                    +-------------------+
