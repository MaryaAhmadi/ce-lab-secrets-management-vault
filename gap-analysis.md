# Compliance Gap Analysis

## Summary
- Total controls checked: 12
- Passed: 5 (42%)
- Failed: 7 (58%)
- Current score: 52 / 100

---

## Critical Gaps (fix immediately)

### 1. [CIS 1.4] Root user has access keys
- **Risk:** If root access keys are compromised, an attacker gains full administrative control over the AWS account, including deleting resources, accessing sensitive data, and locking out legitimate users.
- **Remediation:** 
  - Go to IAM → Users → Root account
  - Delete all root access keys
  - Use IAM roles/users instead of root for daily operations
- **Estimated effort:** 15 minutes

---

### 2. [CIS 5.1] Security group allows SSH from 0.0.0.0/0
- **Risk:** Exposes EC2 instances to the entire internet, making them vulnerable to brute-force attacks and unauthorized access.
- **Remediation:**
  - Go to EC2 → Security Groups
  - Edit inbound rules
  - Restrict SSH (port 22) to a specific IP (e.g., your office IP) or remove entirely
- **Estimated effort:** 15 minutes

---

### 3. [CIS 3.1] CloudTrail is not enabled in all regions
- **Risk:** Without full logging, malicious activities in unused regions may go undetected, reducing visibility and audit capability.
- **Remediation:**
  - Go to CloudTrail
  - Create a new trail
  - Enable “Apply trail to all regions”
  - Store logs in an S3 bucket
- **Estimated effort:** 30 minutes

---

## High Priority Gaps

### 4. [CIS 1.5] MFA not enabled for root user
- **Risk:** If root credentials are compromised, lack of MFA makes account takeover trivial.
- **Remediation:**
  - Enable MFA (virtual or hardware) for root account
- **Estimated effort:** 15 minutes

---

### 5. [CIS 1.10] MFA not enabled for IAM users
- **Risk:** Increases risk of credential compromise and unauthorized access.
- **Remediation:**
  - Enforce MFA for all IAM users
  - Optionally enforce via IAM policy
- **Estimated effort:** 30–60 minutes

---

### 6. [CIS 4.3] No alarm for root account usage
- **Risk:** Root account usage is highly sensitive; without alerts, suspicious activity may go unnoticed.
- **Remediation:**
  - Create CloudWatch alarm for root usage
  - Use CloudTrail logs as source
- **Estimated effort:** 30 minutes

---

### 7. [CIS 4.1] No alarm for unauthorized API calls
- **Risk:** Unauthorized API calls may indicate intrusion attempts or compromised credentials.
- **Remediation:**
  - Create CloudWatch metric filters for unauthorized API calls
  - Trigger SNS alerts
- **Estimated effort:** 30–60 minutes

---

## Remediation Roadmap

| Week | Actions |
|---|---|
| Week 1 | Remove root access keys, enable MFA (root + IAM), restrict SSH access |
| Week 2 | Enable CloudTrail in all regions, configure CloudWatch alarms (root usage + unauthorized API calls) |

---

## What would the score be after fixing all Critical items?

- Current passed controls: 5  
- Critical failures: 3  

If all Critical issues are fixed:
- New passed = 5 + 3 = 8  
- Total controls = 12  

**New score = (8 / 12) × 100 = 67 / 100**

Fixing only the critical issues increases the score significantly, but additional improvements (high-priority items) are needed to reach a strong security posture.
