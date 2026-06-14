# Vault Secrets Management using HashiCorp Vault & Terraform

## 📌 Project Overview

This project demonstrates secure secrets management using HashiCorp Vault. AWS credentials are securely stored and retrieved using the Vault KV (Key-Value) Secrets Engine and integrated with Terraform for secure infrastructure deployment practices.

The project helps eliminate hardcoded credentials and improves security in DevOps workflows.

---

# 🚀 Technologies Used

* HashiCorp Vault
* Terraform
* AWS
* Linux
* PowerShell / Bash
* Git & GitHub

---

# 🎯 Objectives

* Configure HashiCorp Vault Dev Server
* Store AWS credentials securely
* Retrieve secrets using Vault CLI
* Integrate Vault with Terraform
* Implement secure DevOps practices

---

# 🛠️ Prerequisites

Before starting, ensure you have:

* HashiCorp Vault Installed
* Terraform Installed
* AWS Account
* AWS Access Key & Secret Key
* Git Installed

---

# 📂 Project Structure

```bash id="zjqgk3"
vault-terraform-project/
│
├── main.tf
├── variables.tf
├── terraform.tfvars
├── outputs.tf
└── README.md
```

---

# 🔐 Step 1 — Start Vault Dev Server

Run the following command:

```bash id="n52hfc"
vault server -dev
```

Expected Output:

```bash id="fyqg34"
Root Token: hvs.xxxxxx
Vault server started!
```

Vault runs locally on:

```bash id="gtqk6e"
http://127.0.0.1:8200
```

---

# 🔑 Step 2 — Configure Vault Environment Variables

## Windows PowerShell

```powershell id="0rl9jf"
$env:VAULT_ADDR="http://127.0.0.1:8200"
$env:VAULT_TOKEN="hvs.xxxxxx"
```

## Linux / macOS

```bash id="tjlwm6"
export VAULT_ADDR="http://127.0.0.1:8200"
export VAULT_TOKEN="hvs.xxxxxx"
```

---

# ☁️ Step 3 — Store AWS Credentials in Vault

Run:

```bash id="n65lqf"
vault kv put secret/aws \
access_key=AKIAxxxxxxxx \
secret_key=xxxxxxxxxxxxxxxx
```

---

# ✅ Step 4 — Verify Stored Secrets

```bash id="g1vudm"
vault kv get secret/aws
```

Expected Output:

```bash id="fw1p27"
====== Secret Path ======
secret/data/aws

======= Data =======
access_key    AKIAxxxxxxxx
secret_key    ************
```

---

# 📝 Step 5 — Terraform Configuration

Example `main.tf`

```hcl id="g0iy59"
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }

    vault = {
      source  = "hashicorp/vault"
      version = "~> 4.0"
    }
  }
}

provider "vault" {
  address = "http://127.0.0.1:8200"
}

data "vault_kv_secret_v2" "aws" {
  mount = "secret"
  name  = "aws"
}

provider "aws" {
  region     = "ap-south-1"
  access_key = data.vault_kv_secret_v2.aws.data["access_key"]
  secret_key = data.vault_kv_secret_v2.aws.data["secret_key"]
}
```

---

# ▶️ Step 6 — Initialize Terraform

```bash id="ftv8zb"
terraform init
```

---

# ▶️ Step 7 — Validate Terraform Code

```bash id="g3q8hc"
terraform validate
```

---

# ▶️ Step 8 — Deploy Infrastructure

```bash id="jps23m"
terraform apply
```

Type:

```bash id="0fk4d4"
yes
```

---

# 🔥 Key Features

* Secure secrets management
* AWS credentials stored safely
* Terraform integration with Vault
* Elimination of hardcoded secrets
* Infrastructure automation support

---

# 📚 Learning Outcomes

After completing this project, you will understand:

* HashiCorp Vault basics
* Secrets management concepts
* Vault KV engine
* Terraform + Vault integration
* Secure DevOps workflows
* Infrastructure security practices

---

# ⚠️ Security Best Practices

* Never expose AWS secret keys publicly
* Avoid hardcoding credentials in Terraform files
* Rotate credentials regularly
* Use IAM roles in production environments
* Do not use Vault Dev Server in production

---

# ✅ Conclusion

This project successfully demonstrated secure secrets management using HashiCorp Vault integrated with Terraform. AWS credentials were securely stored and retrieved using the Vault KV engine, improving security and automation practices in cloud infrastructure deployment workflows.

---

# 👨‍💻 Author

Sheikh Sarim

GitHub: https://github.com/sar1211im


