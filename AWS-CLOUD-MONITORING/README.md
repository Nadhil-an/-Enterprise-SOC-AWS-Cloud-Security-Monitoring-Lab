# ☁️ AWS Security Monitoring Architecture

A real-time AWS cloud security monitoring and alerting pipeline built using AWS native services integrated with Splunk SIEM for centralized security monitoring, alerting, and detection engineering.

---

# 📌 Overview

This project demonstrates a cloud-native security monitoring architecture implemented in Amazon Web Services (AWS). The environment captures AWS API activities using CloudTrail, processes logs through CloudWatch, detects suspicious activity using Metric Filters and Alarms, and forwards alerts to Splunk SIEM using SNS and SQS integration.

The architecture enables:

- Real-time AWS security event monitoring
- Cloud-native detection engineering
- Automated alerting workflows
- Centralized SIEM log analysis
- SOC-style monitoring and investigation

AWS services such as EC2, S3, IAM, and Secrets Manager generate API events that are continuously monitored and analyzed for suspicious or security-relevant activity.

---

# 🏗️ Architecture Overview

<div align="center">
  <img src="/assets/architecture.png" width="1000">
</div>

---

# 🔄 Detection Workflow

```text
AWS Service Activity
        ↓
CloudTrail
       ↙ ↘
S3 Bucket  CloudWatch Logs
                 ↓
            Metric Filter
                 ↓
         CloudWatch Alarm
                 ↓
              SNS Topic
             ↙        ↘
         Email      SQS Queue
                         ↓
                      Splunk
```

---

# ☁️ AWS Services Used

| Service | Purpose |
|---|---|
| AWS CloudTrail | Captures AWS API activities |
| AWS CloudWatch Logs | Stores and monitors CloudTrail logs |
| CloudWatch Metric Filters | Detects specific security events |
| CloudWatch Alarms | Triggers alerts on suspicious activity |
| AWS SNS | Sends real-time notifications |
| AWS SQS | Queues events for Splunk ingestion |
| AWS S3 | Stores CloudTrail logs |
| Splunk SIEM | Centralized log analysis and monitoring |

---

# 🚨 Security Monitoring Implemented

## Security Group Monitoring

| Detection | Event Name |
|---|---|
| Security Group Creation | `CreateSecurityGroup` |
| Inbound Rule Addition | `AuthorizeSecurityGroupIngress` |
| Rule Removal | `RevokeSecurityGroupIngress` |
| Security Group Deletion | `DeleteSecurityGroup` |

---

## S3 Bucket Monitoring

| Detection | Event Name |
|---|---|
| Bucket Policy Change | `PutBucketPolicy` |
| Bucket Policy Deletion | `DeleteBucketPolicy` |
| Bucket ACL Modification | `PutBucketAcl` |
| Public Access Block Change | `PutBucketPublicAccessBlock` |
| Bucket Deletion | `DeleteBucket` |

---

# 📊 Splunk Integration

Splunk SIEM is integrated using AWS SNS and SQS.

## Splunk Log Flow

```text
CloudWatch Alarm
        ↓
     SNS Topic
        ↓
     SQS Queue
        ↓
Splunk Add-on for AWS
        ↓
      Splunk
```

Splunk consumes AWS alert notifications from SQS using the Splunk Add-on for AWS, enabling centralized security monitoring and detection analysis.

---

# 🔍 Example Splunk Detection Queries

## Security Group Modification

```spl
index=aws_cloudtrail eventName=AuthorizeSecurityGroupIngress
| stats count by userIdentity.arn sourceIPAddress awsRegion
```

---

## Security Group Deletion

```spl
index=aws_cloudtrail eventName=DeleteSecurityGroup
| table _time userIdentity.arn sourceIPAddress awsRegion
```

---

## S3 Bucket Policy Modification

```spl
index=aws_cloudtrail eventName=PutBucketPolicy
| table _time requestParameters.bucketName userIdentity.arn
```

---

# 🎯 Key Skills Demonstrated

- AWS Cloud Security Monitoring
- Detection Engineering
- CloudTrail Monitoring
- CloudWatch Alarms & Metric Filters
- SNS & SQS Integration
- Splunk SIEM Integration
- Security Event Detection
- SOC Monitoring Workflows
- Log Analysis & Alerting

---

# 🚀 Future Enhancements

- Add GuardDuty integration
- Add AWS Config monitoring
- Add Lambda automated response
- Build Splunk dashboards
- Add IAM privilege escalation detections
- Add Secrets Manager monitoring
- Add EC2 instance monitoring

---

# 👤 Author

**Nadil** — Cybersecurity Student & SOC Enthusiast

- GitHub: https://github.com/Nadhil-an
- LinkedIn: https://www.linkedin.com/in/nadhilan/
