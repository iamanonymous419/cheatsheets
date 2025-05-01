# 🛠️ Terraform CLI Cheatsheet

A complete and expanded reference for Terraform CLI, covering all core commands and best practices. Use this as a guide for initializing, planning, applying, managing state, using workspaces, variables, modules, backends, and more.

---

## 📦 1. Terraform Installation

### Download and Install
Visit the [Terraform downloads page](https://developer.hashicorp.com/terraform/downloads) and follow instructions for your OS.

```bash
# Verify installation
terraform -version
```

### Upgrade Terraform
```bash
terraform -install-autocomplete
terraform -upgrade
```

---

## 🔀 2. Terraform Workflow Overview

```bash
terraform init      # Initialize configuration
terraform plan      # Preview changes
terraform apply     # Apply infrastructure changes
terraform destroy   # Destroy managed infrastructure
```

---

## 📁 3. Initialization

```bash
terraform init
```

- Initializes backend and installs required providers and modules.
- Add `-upgrade` to update modules and providers.

---

## 🧠 4. Planning

```bash
terraform plan
```

- Previews changes without applying them.
- Save plan to a file:

```bash
terraform plan -out=tfplan
```

- Use variables:
```bash
terraform plan -var="region=us-west-1"
terraform plan -var-file="dev.tfvars"
```

---

## 🚀 5. Apply Changes

```bash
terraform apply
```

- Apply saved plan:
```bash
terraform apply tfplan
```

- Use `-auto-approve` to skip interactive approval:
```bash
terraform apply -auto-approve
```

---

## 💥 6. Destroy Infrastructure

```bash
terraform destroy
terraform destroy -auto-approve
```

---

## 📄 7. Terraform Show

```bash
terraform show
terraform show -json > tfstate.json
```

- Shows details from the state or plan file.

---

## 📅 8. Format Code

```bash
terraform fmt
terraform fmt -recursive  # Format nested directories
```

---

## ✅ 9. Validate Configuration

```bash
terraform validate
```

- Ensures syntax and internal consistency are correct.

---

## 🔄 10. Refresh State

```bash
terraform apply --refresh-only
```

- Refresh resource states without making changes.

---

## 📊 11. State Management

```bash
terraform state list                 # List tracked resources
terraform state show <resource>     # Show details
terraform state mv <src> <dst>      # Move resource within state
terraform state rm <resource>       # Remove from state
terraform state pull                 # Download state
terraform state push <file>         # Upload state
```

---

## 🛠️ 12. Providers

Defined in configuration:
```hcl
provider "aws" {
  region = "us-east-1"
}
```

List all providers:
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

Backends supported:
- local (default)
- s3
- azurerm
- gcs
- consul
- remote (Terraform Cloud)

---

## 🔎 14. Logging and Debugging

```bash
TF_LOG=DEBUG terraform apply
```

Log levels:
- TRACE
- DEBUG
- INFO
- WARN
- ERROR

---

## 📊 15. Outputs

Define outputs:
```hcl
output "instance_ip" {
  value = aws_instance.web.public_ip
}
```

Get outputs:
```bash
terraform output
terraform output instance_ip
```

---

## ⚖️ 16. Variables

Declare variable:
```hcl
variable "region" {
  default = "us-east-1"
  type    = string
  description = "AWS region"
}
```

Pass via CLI:
```bash
terraform apply -var="region=us-west-2"
```

From file:
```bash
terraform apply -var-file="prod.tfvars"
```

Environment variables:
```bash
export TF_VAR_region=us-east-1
```

---

## 🔄 17. Workspaces

Manage multiple states:
```bash
terraform workspace list
terraform workspace new dev
terraform workspace select dev
terraform workspace show
```

---

## 📃 18. Modules

Use a module:
```hcl
module "vpc" {
  source     = "./modules/vpc"
  cidr_block = "10.0.0.0/16"
}
```

Remote modules:
```hcl
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = ">= 3.0.0"
}
```

---

## 📈 19. Dependency Graph

Generate a DOT graph:
```bash
terraform graph | dot -Tsvg > graph.svg
```

---

## 🔢 20. Version Constraints

```hcl
terraform {
  required_version = ">= 1.5.0"
}
```

With providers:
```hcl
provider "aws" {
  version = "~> 4.0"
}
```

---

## ⚙️ 21. Terraform Cloud CLI

Login to Terraform Cloud:
```bash
terraform login
```

---

## 📙 Additional Resources

- Official Docs: https://developer.hashicorp.com/terraform/docs
- Terraform Registry: https://registry.terraform.io/
- Tutorials: https://developer.hashicorp.com/terraform/tutorials
- GitHub Repo: https://github.com/hashicorp/terraform

---

**Maintained by:** _Your Name_
**Last Updated:** _April 2025_

