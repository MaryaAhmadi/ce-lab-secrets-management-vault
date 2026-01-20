# Lab M8.06 - Secrets Management with Vault (Alternative)

**Repository:** [https://github.com/cloud-engineering-bootcamp/ce-lab-secrets-management-vault](https://github.com/cloud-engineering-bootcamp/ce-lab-secrets-management-vault)

**Activity Type:** Individual  
**Estimated Time:** 60 minutes

## Learning Objectives

- [ ] Install and configure HashiCorp Vault
- [ ] Store and retrieve secrets from Vault
- [ ] Use dynamic database credentials
- [ ] Compare Vault vs AWS Secrets Manager

## Prerequisites

- [ ] Docker installed locally
- [ ] PostgreSQL database (local or RDS)
- [ ] Completed Module 8 Lesson 5

## Task

Deploy Vault in Docker, configure database secret engine, generate dynamic credentials, and compare with AWS Secrets Manager.

## Step-by-Step Instructions

### Step 1: Run Vault in Docker

```bash
docker run --cap-add=IPC_LOCK -d --name=vault \
  -p 8200:8200 \
  -e 'VAULT_DEV_ROOT_TOKEN_ID=myroot' \
  vault:latest

# Access Vault
export VAULT_ADDR='http://127.0.0.1:8200'
export VAULT_TOKEN='myroot'
```

### Step 2: Store Static Secret

```bash
# Enable KV engine
vault secrets enable -path=secret kv-v2

# Store database credentials
vault kv put secret/prod/db \
  username=dbadmin \
  password=SecretPassword123!

# Retrieve secret
vault kv get secret/prod/db
```

### Step 3: Configure Dynamic Database Credentials

```bash
# Enable database engine
vault secrets enable database

# Configure PostgreSQL connection
vault write database/config/postgresql \
  plugin_name=postgresql-database-plugin \
  connection_url="postgresql://{{username}}:{{password}}@postgres:5432/mydb" \
  allowed_roles="readonly" \
  username="vault" \
  password="vault-password"

# Create role
vault write database/roles/readonly \
  db_name=postgresql \
  creation_statements="CREATE ROLE \"{{name}}\" WITH LOGIN PASSWORD '{{password}}' VALID UNTIL '{{expiration}}'; GRANT SELECT ON ALL TABLES IN SCHEMA public TO \"{{name}}\";" \
  default_ttl="1h" \
  max_ttl="24h"

# Generate credentials
vault read database/creds/readonly
```

**Output:**
```
Key                Value
---                -----
username           v-root-readonly-abc123
password           A1b2C3d4E5f6
lease_duration     1h
```

### Step 4: Comparison Table

Create `comparison.md`:

```markdown
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
- **AWS Secrets Manager:** For AWS-only workloads, RDS rotation
- **Vault:** For multi-cloud, dynamic secrets, advanced use cases
```

## Submission

- Screenshots of Vault UI showing secrets
- Dynamic credentials generated from Vault
- `comparison.md` with analysis

## Verification Checklist

- [ ] Vault deployed and accessible
- [ ] Static secret stored and retrieved
- [ ] Dynamic database credentials generated
- [ ] Comparison table completed

**Good luck! 🔒**
