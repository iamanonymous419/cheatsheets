Sure! Below is a comprehensive **Terraform CLI Cheatsheet** in the form of a `README.md` file. It covers all core CLI commands and options, including initialization, planning, applying, destroying, state management, formatting, validation, and more.

---

### 📄 `README.md` — **Terraform CLI Cheatsheet**

```markdown
# 🛠️ Terraform CLI Cheatsheet

A quick reference to commonly used Terraform CLI commands. Suitable for beginners and professionals managing infrastructure as code with Terraform.

---

## 📦 1. Terraform Installation

Install Terraform: https://developer.hashicorp.com/terraform/downloads

Verify installation:
```bash
terraform -version
```

---

## 🔰 2. Terraform Workflow Basics

```bash
terraform init      # Initialize Terraform configuration directory
terraform plan      # Show execution plan (what will be created, modified, destroyed)
terraform apply     # Apply the changes required to reach the desired state
terraform destroy   # Destroy the Terraform-managed infrastructure
```

---

## 📁 3. Project Initialization

```bash
terraform init
```
- Downloads providers
- Initializes the backend
- Sets up the working directory

---

## 🧠 4. Execution Plan

```bash
terraform plan
```
- Shows what Terraform *will* do before it does it
- Use `-out=plan.out` to save the plan

```bash
terraform plan -out=plan.out
```

---

## 🚀 5. Apply Changes

```bash
terraform apply
```
- Applies changes to match your configuration

```bash
terraform apply plan.out
```

---

## 💥 6. Destroy Infrastructure

```bash
terraform destroy
```
- Tears down all resources defined in the Terraform configuration

---

## 📄 7. Show Current State

```bash
terraform show
```
- Displays the current state or saved plan

---

## 🧾 8. Format Configuration Files

```bash
terraform fmt
```
- Formats `.tf` files to a canonical style

```bash
terraform fmt -recursive  # Format in all subdirectories
```

---

## ✅ 9. Validate Configuration

```bash
terraform validate
```
- Validates the syntax and internal consistency

---

## 🔄 10. Refresh State

```bash
terraform refresh
```
- Syncs the state file with real infrastructure (deprecated in Terraform 1.1+, use `terraform apply --refresh-only`)

---

## 📊 11. State Management

```bash
terraform state list                 # List all resources in state
terraform state show <resource>     # Show details of a resource
terraform state mv <src> <dest>     # Move a resource in state
terraform state rm <resource>       # Remove from state (does not delete the resource)
terraform state pull                 # Download local state
terraform state push <file>         # Upload state file
```

---

## 🧱 12. Providers

```hcl
provider "aws" {
  region = "us-east-1"
}
```
List providers:
```bash
terraform providers
```

---

## 🔐 13. Backend Configuration

Defined in `main.tf`:
```hcl
terraform {
  backend "s3" {
    bucket = "my-tf-state"
    key    = "dev/terraform.tfstate"
    region = "us-east-1"
  }
}
```

---

## 🧪 14. Debugging & Logging

```bash
TF_LOG=DEBUG terraform apply
```
- Logging levels: `TRACE`, `DEBUG`, `INFO`, `WARN`, `ERROR`

---

## 🗃️ 15. Output Values

```hcl
output "instance_ip" {
  value = aws_instance.web.public_ip
}
```

Show outputs:
```bash
terraform output
terraform output instance_ip
```

---

## ⚙️ 16. Input Variables

```hcl
variable "region" {
  default = "us-east-1"
}
```

Pass values:
```bash
terraform apply -var="region=us-west-2"
```

From file:
```bash
terraform apply -var-file="dev.tfvars"
```

---

## 🧪 17. Test/Preview Resources

Dry run:
```bash
terraform plan -out=tfplan
terraform show -json tfplan | jq .
```

---

## 📦 18. Modules

```hcl
module "vpc" {
  source = "./modules/vpc"
  cidr_block = "10.0.0.0/16"
}
```

---

## 🌐 19. Workspaces

```bash
terraform workspace list
terraform workspace new dev
terraform workspace select dev
terraform workspace show
```

---

## 📜 20. Version Constraints

```hcl
terraform {
  required_version = ">= 1.5.0"
}
```

---

## 🧰 21. Helpful Flags & Options

```bash
terraform plan -var="env=prod" -out=plan.out
terraform apply -auto-approve
terraform destroy -auto-approve
terraform init -upgrade
```

---

## 📚 Resources

- Docs: https://developer.hashicorp.com/terraform/docs
- Registry: https://registry.terraform.io/
- Tutorial: https://developer.hashicorp.com/terraform/tutorials

---

**Created by:** _Your Name_  
**Last Updated:** _April 2025_
```

---

Would you like this saved as a downloadable `README.md` file?