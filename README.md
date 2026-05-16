# 🛡️ Enterprise SOC & AWS Cloud Security Monitoring Lab

![Splunk](https://img.shields.io/badge/SIEM-Splunk-FF6B35?style=flat-square&logo=splunk)
![MITRE ATT&CK](https://img.shields.io/badge/Framework-MITRE%20ATT%26CK-red?style=flat-square)
![Windows](https://img.shields.io/badge/Platform-Windows-0078D6?style=flat-square&logo=windows)
![Active Directory](https://img.shields.io/badge/Active%20Directory-soc.local-purple?style=flat-square)
![AWS](https://img.shields.io/badge/Cloud-AWS-FF9900?style=flat-square&logo=amazonaws)
![Splunk Enterprise](https://img.shields.io/badge/Splunk-Enterprise-black?style=flat-square&logo=splunk)
![Cloud Security](https://img.shields.io/badge/Cloud-Security%20Monitoring-orange?style=flat-square)

> A fully cloud-based Enterprise SOC lab deployed on AWS integrating Windows Active Directory, endpoint monitoring, vulnerable web application attacks, and AWS cloud security monitoring with Splunk SIEM. This project demonstrates real-world attack simulation, log collection, detection engineering, cloud monitoring, alerting pipelines, and SOC investigation workflows across both on-premise-style infrastructure and AWS native services.

---

# 🏗️ Unified SOC + AWS Cloud Monitoring Architecture

<div align="center">
  <img src="./assets/main architecture.png" width="1200">
</div>

---

# 📌 Project Overview

This project combines:

- Enterprise SOC infrastructure
- Windows endpoint monitoring
- Active Directory attack detection
- Web application attack simulation
- AWS cloud security monitoring
- Splunk SIEM integration
- Detection engineering workflows
- Real-time alerting pipeline

The lab environment was deployed in AWS using EC2 instances, CloudTrail, CloudWatch, SNS, SQS, S3, and Splunk.

---

# 🔥 Security Domains Covered

| Domain | Description |
|---|---|
| Endpoint Security | Windows attack simulations & detections |
| Active Directory Security | Domain attack monitoring |
| Web Application Security | DVWA attack simulations |
| AWS Cloud Security | CloudTrail + CloudWatch detections |
| SIEM Monitoring | Splunk centralized log analysis |

---

# ☁️ AWS Cloud Security Monitoring Implementation

The project includes a complete AWS cloud-native monitoring pipeline.

## AWS Monitoring Flow

```text
AWS Services → CloudTrail → CloudWatch Logs → Metric Filters
→ CloudWatch Alarms → SNS → SQS → Splunk
```

---

# ☁️ AWS Services Integrated

| Service | Purpose |
|---|---|
| CloudTrail | Capture AWS API activity |
| CloudWatch Logs | Log monitoring |
| Metric Filters | Event detection |
| CloudWatch Alarms | Real-time alerting |
| SNS | Email notifications |
| SQS | Queue integration with Splunk |
| S3 | Log archival |
| Splunk | SIEM monitoring |

---

# 🚨 AWS Cloud Detection Labs

## ☁️ Security Group Monitoring

| Detection | Event Name | Severity |
|---|---|---|
| Security Group Creation | CreateSecurityGroup | 🟡 Medium |
| Inbound Rule Addition | AuthorizeSecurityGroupIngress | 🔴 High |
| Rule Removal | RevokeSecurityGroupIngress | 🔴 High |
| Security Group Deletion | DeleteSecurityGroup | 🔴 Critical |

---

## ☁️ S3 Bucket Monitoring(inprogress)

| Detection | Event Name | Severity |
|---|---|---|
| Bucket Policy Change | PutBucketPolicy | 🔴 Critical |
| Bucket Policy Deletion | DeleteBucketPolicy | 🔴 Critical |
| Bucket ACL Modification | PutBucketAcl | 🔴 High |
| Public Access Block Change | PutBucketPublicAccessBlock | 🔴 High |
| Bucket Deletion | DeleteBucket | 🔴 Critical |

---

# 🖥️ Endpoint Attacks — `index=end_point`

| Lab | Attack | Event ID | MITRE | Severity |
|---|---|---|---|---|
| E1 | Malware Execution Simulation | 4688 | T1204, T1059 | 🔴 High |
| E2 | Suspicious PowerShell Encoded Command | 4688 | T1059.001, T1027 | 🔴 High |
| E3 | Persistence via Registry Run Key | 4657 | T1547.001 | 🔴 High |
| E4 | Privilege Escalation via Administrators Group | 4720, 4732 | T1098 | 🔴 Critical |
| E5 | Malicious Service Creation | 7045 | T1543.003 | 🔴 Critical |

---

# 🏢 Active Directory Attacks — `index=windows`

| Lab | Attack | Event ID | MITRE | Severity |
|---|---|---|---|---|
| AD-01 | RDP Brute Force | 4625, 4624 | T1110 | 🔴 High |
| AD-02 | Account Lockout Detection | 4740 | T1110 | 🟡 Medium |
| AD-03 | Backdoor User & Group Creation | 4720, 4727, 4728 | T1136, T1098 | 🔴 Critical |

---

# 🌐 Web Application Attacks — `index=web_logs`

| Lab | Attack | Payload | MITRE | Severity |
|---|---|---|---|---|
| W1 | SQL Injection | `' OR '1'='1` | T1190 | 🔴 High |
| W2 | Brute Force Login | Credential Stuffing | T1110 | 🔴 High |
| W3 | Command Injection | `127.0.0.1;whoami` | T1059 | 🔴 High |
| W4 | File Upload Web Shell | `shell.php?cmd=whoami` | T1505.003 | 🔴 Critical |
| W5 | Local File Inclusion | `../../../../etc/passwd` | T1006 | 🔴 High |

---

# 📊 Splunk SIEM Integration

Splunk was configured as the centralized SIEM platform for:

- Windows Security Logs
- Sysmon Logs
- Active Directory Logs
- Apache Access Logs
- AWS CloudTrail Events
- CloudWatch Alerts
- SNS/SQS Cloud Notifications

---

# 🔍 Example AWS Splunk Detections

## Security Group Modification Detection

```spl
index=aws_cloudtrail eventName=AuthorizeSecurityGroupIngress
| stats count by userIdentity.arn sourceIPAddress awsRegion
```

---

## Security Group Deletion Detection

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

# 🗺️ MITRE ATT&CK Coverage

| Tactic | Technique | ID |
|---|---|---|
| Execution | Command & Scripting Interpreter | T1059 |
| Persistence | Registry Run Keys | T1547.001 |
| Privilege Escalation | Account Manipulation | T1098 |
| Credential Access | Brute Force | T1110 |
| Initial Access | Exploit Public-Facing Application | T1190 |
| Persistence | Web Shell | T1505.003 |
| Discovery | File and Directory Discovery | T1083 |
| Defense Evasion | Obfuscated Files | T1027 |

---

# 🎯 Key Skills Demonstrated

- SOC Operations
- SIEM Engineering
- Detection Engineering
- Cloud Security Monitoring
- Splunk Administration
- Active Directory Security
- Web Application Security
- AWS Security Monitoring
- Threat Detection
- Log Analysis
- Incident Investigation

---

# 🚀 Future Enhancements

- [ ] Add GuardDuty integration
- [ ] Add AWS Config detections
- [ ] Add Lambda automated response
- [ ] Build Splunk dashboards
- [ ] Add Kerberoasting attacks
- [ ] Add Pass-the-Hash detection
- [ ] Add XSS & CSRF web attacks
- [ ] Add Terraform deployment

---

# 👤 Author

**Nadil** — Cybersecurity Student & SOC Enthusiast

- GitHub: https://github.com/Nadhil-an
- LinkedIn: https://www.linkedin.com/in/nadhilan/
