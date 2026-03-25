# Lab M8.06 - Secrets Management with Vault (Alternative)

**Repository:** https://github.com/MaryaAhmadi/ce-lab-secrets-management-vault.git

**Activity Type:** Individual  
**Estimated Time:** 60 minutes

###  📌 Overview
In this lab, we explore modern secrets management using HashiCorp Vault. You will deploy Vault in a Docker container, store and retrieve secrets, generate dynamic database credentials, and compare Vault with AWS Secrets Manager.
This lab focuses on understanding why dynamic secrets are more secure than static credentials and how Vault enables advanced security use cases.

###  🎯 Learning Objectives
* Install and configure HashiCorp Vault locally
* Store and retrieve secrets using KV engine
* Generate dynamic PostgreSQL credentials
* Understand the difference between static vs dynamic secrets
* Compare Vault with AWS Secrets Manager

###  ⚙️ Prerequisites
Before starting, ensure you have:
* Docker installed and running
* PostgreSQL database (local container or AWS RDS)
* Basic familiarity with AWS and CLI tools
* Completed Module 8 Lesson 5

###  🚀 Lab Steps

🔹 Step 1: Run Vault in Docker
Start a development Vault server:
docker run --cap-add=IPC_LOCK -d --name=vault \
  -p 8200:8200 \
  -e 'VAULT_DEV_ROOT_TOKEN_ID=myroot' \
  vault:latest
Set environment variables:
export VAULT_ADDR='http://127.0.0.1:8200'
export VAULT_TOKEN='myroot'
✅ Expected Result: Vault is running and accessible at http://localhost:8200



🔹 Step 2: Store and Retrieve Static Secrets
Enable the KV (Key-Value) secrets engine:
vault secrets enable -path=secret kv-v2
Store a secret:
vault kv put secret/prod/db \
  username=dbadmin \
  password=SecretPassword123!
Retrieve the secret:
vault kv get secret/prod/db

### ✅ Expected Result: You can successfully store and retrieve database credentials.
📌 Key Concept: This is a static secret — it does not expire automatically.

🔹 Step 3: Configure Dynamic Database Credentials

Enable database secrets engine:
vault secrets enable database

Configure PostgreSQL connection:

vault write database/config/postgresql \
  plugin_name=postgresql-database-plugin \
  connection_url="postgresql://{{username}}:{{password}}@postgres:5432/mydb" \
  allowed_roles="readonly" \
  username="vault" \
  password="vault-password"
Create a role for dynamic users:
vault write database/roles/readonly \
  db_name=postgresql \
  creation_statements="CREATE ROLE \"{{name}}\" WITH LOGIN PASSWORD '{{password}}' VALID UNTIL '{{expiration}}'; GRANT SELECT ON ALL TABLES IN SCHEMA public TO \"{{name}}\";" \
  default_ttl="1h" \
  max_ttl="24h"

Generate dynamic credentials:
vault read database/creds/readonly

### ✅ Expected Output:
username: v-root-readonly-abc123
password: A1b2C3d4E5f6
lease_duration: 1h

### 📌 Key Concept:
* Credentials are auto-generated
* They expire automatically
* Reduced risk compared to static secrets

🔹 Step 4: Comparison — Vault vs AWS Secrets Manager
Create a file comparison.md:
# Secrets Manager vs Vault Comparison

| Feature | AWS Secrets Manager | HashiCorp Vault |
|---------|---------------------|-----------------|
| **Cost** | $0.40/secret/month | Free (self-hosted) |
| **Automatic Rotation** | ✅ RDS, Redshift | ✅ Dynamic secrets |
| **Dynamic Secrets** | ❌ | ✅ |
| **Multi-Cloud** | AWS only | ✅ AWS, Azure, GCP |
| **Encryption** | AWS KMS | Built-in |
| **Audit Logging** | CloudTrail | Built-in audit log |
| **Management** | Fully managed | Self-managed |

## Recommendation

- AWS Secrets Manager:** Best for AWS-only environments with minimal operational overhead
- HashiCorp Vault:** Ideal for multi-cloud, dynamic secrets, and advanced security requirements

### 📸 Submission Requirements
Include the following in your repository:
* Screenshot of Vault UI showing stored secrets
* Screenshot of generated dynamic credentials
* comparison.md file
* This README file

### ✅ Verification Checklist
*  Vault is running and accessible
*  Static secrets stored and retrieved successfully
*  Dynamic database credentials generated
*  Comparison file completed
*  Screenshots included

### 🧠 Key Takeaways
* Static secrets are simple but risky
* Dynamic secrets improve security by reducing exposure time
* Vault provides fine-grained control and flexibility
* AWS Secrets Manager is easier but less powerful for advanced use cases


###🏁 Conclusion
This lab demonstrates how modern systems move away from hardcoded credentials toward dynamic, short-lived secrets, significantly improving security posture in cloud environments.



## Verification Checklist

- [ ✅ ] Vault deployed and accessible
- [ ✅ ] Static secret stored and retrieved
- [ ✅ ] Dynamic database credentials generated
- [ ✅ ] Comparison table completed


