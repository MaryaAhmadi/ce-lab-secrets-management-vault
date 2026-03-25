# CIS Control Mapping — 2-Tier Application

| CIS Control | Description | AWS Service | Status | Evidence / Remediation |
|---|---|---|---|---|
| CIS 1.4 | Ensure no root user access keys exist | IAM | ❌ Not compliant | Remove root access keys from IAM console immediately |
| CIS 1.5 | Ensure MFA is enabled for the root user | IAM | ❌ Not compliant | Enable MFA on root account via IAM console |
| CIS 1.10 | Ensure MFA is enabled for all IAM users | IAM | ❌ Not compliant | Enable MFA for all IAM users |
| CIS 3.1 | Ensure CloudTrail is enabled in all regions | CloudTrail | ❌ Not compliant | Enable multi-region CloudTrail logging |
| CIS 3.2 | Ensure CloudTrail log file validation is enabled | CloudTrail | ✅ Compliant | Already enabled (assumed from scan results) |
| CIS 2.1.1 | Ensure S3 Block Public Access is enabled | S3 | ✅ Compliant | Confirm via S3 settings: Block Public Access ON |
| CIS 5.1 | Ensure no security groups allow SSH from 0.0.0.0/0 | EC2 / VPC | ❌ Not compliant | Restrict SSH access to specific IP range |
| CIS 5.3 | Ensure default security group restricts all traffic | VPC | ✅ Compliant | Default SG has no inbound/outbound rules |
