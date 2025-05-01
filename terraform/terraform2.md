# Terraform CLI Cheatsheet

## Table of Contents
- [Installation & Setup](#installation--setup)
- [Basic Commands](#basic-commands)
- [Initialization](#initialization)
- [Planning](#planning)
- [Applying Changes](#applying-changes)
- [State Management](#state-management)
- [Workspace Management](#workspace-management)
- [Module Management](#module-management)
- [Variables & Outputs](#variables--outputs)
- [Import & Export](#import--export)
- [Providers](#providers)
- [Console & Debugging](#console--debugging)
- [Formatting & Validation](#formatting--validation)
- [Environment Variables](#environment-variables)
- [Advanced Options](#advanced-options)
- [Remote Operations](#remote-operations)
- [Testing](#testing)
- [Security](#security)
- [Terraform Cloud & Enterprise](#terraform-cloud--enterprise)
- [Common Workflows](#common-workflows)
- [Troubleshooting](#troubleshooting)
- [Best Practices](#best-practices)

## Installation & Setup

### Installation Methods

#### MacOS
```bash
# Using Homebrew
brew install terraform

# Using tfenv (Terraform version manager)
brew install tfenv
tfenv install latest
tfenv use latest
```

#### Windows
```bash
# Using Chocolatey
choco install terraform

# Using Scoop
scoop install terraform

# Using tfenv for Windows
scoop install tfenv
tfenv install latest
tfenv use latest
```

#### Linux
```bash
# Using apt (Ubuntu/Debian)
curl -fsSL https://apt.releases.hashicorp.com/gpg | sudo apt-key add -
sudo apt-add-repository "deb [arch=amd64] https://apt.releases.hashicorp.com $(lsb_release -cs) main"
sudo apt update
sudo apt install terraform

# Using yum (RHEL/CentOS)
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo
sudo yum -y install terraform

# Manual installation
wget https://releases.hashicorp.com/terraform/1.6.6/terraform_1.6.6_linux_amd64.zip
unzip terraform_1.6.6_linux_amd64.zip
sudo mv terraform /usr/local/bin/
```

### Version Management
```bash
# Check current version
terraform version

# List available versions (with tfenv)
tfenv list-remote

# Install specific version (with tfenv)
tfenv install 1.6.6
tfenv use 1.6.6

# Pin project to specific version (create .terraform-version file)
echo "1.6.6" > .terraform-version
```

### Auto-completion Setup
```bash
# Bash
terraform -install-autocomplete
source ~/.bashrc

# Zsh
terraform -install-autocomplete
source ~/.zshrc

# PowerShell
terraform -install-autocomplete
```

### Development Environment Setup
```bash
# Install helpful tools
# pre-commit hooks for Terraform
pip install pre-commit
pre-commit install

# tflint for linting
curl -s https://raw.githubusercontent.com/terraform-linters/tflint/master/install_linux.sh | bash

# terraform-docs for documentation
go install github.com/terraform-docs/terraform-docs@latest

# infracost for cost estimation
curl -s https://raw.githubusercontent.com/infracost/infracost/master/scripts/install.sh | bash
```

## Basic Commands

### Help System
```bash
terraform -help                  # General help
terraform <command> -help        # Command-specific help
terraform -help commands         # List all commands
terraform -help providers        # List provider commands
```

### Basic Command Structure
```bash
terraform [global options] <subcommand> [args]
```

### Common Global Options
```bash
-chdir=<dir>                     # Change working directory before executing
-version                         # Show version
-help                            # Show help
-json                            # Output in JSON format
-no-color                        # Disable color output
```

### Getting Information
```bash
terraform version                # Show version
terraform -version               # Show version with limited additional info
terraform -v                     # Short version flag
```

## Initialization

### Initialize Working Directory
```bash
terraform init                   # Initialize directory, download plugins
terraform init -upgrade          # Upgrade plugins to latest version
terraform init -reconfigure      # Reconfigure backend without migration
terraform init -migrate-state    # Reconfigure backend and migrate state
terraform init -backend=false    # Initialize without backend configuration
terraform init -get-plugins=false # Skip plugin installation
terraform init -input=false      # Disable interactive prompts
```

### Backend Configuration
```bash
# Load backend settings from file
terraform init -backend-config=backend.hcl

# Set specific backend settings inline
terraform init -backend-config="bucket=my-terraform-state" \
               -backend-config="region=us-west-2" \
               -backend-config="dynamodb_table=terraform-locks"

# Partial backend configuration (mixing .tf files and CLI params)
terraform init -backend-config="key=prod/terraform.tfstate"
```

### Backend Types and Examples

#### S3 Backend
```hcl
# In terraform configuration
terraform {
  backend "s3" {
    bucket         = "terraform-state-bucket"
    key            = "path/to/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-locks"
    encrypt        = true
  }
}
```

#### Azure Backend
```hcl
terraform {
  backend "azurerm" {
    resource_group_name  = "tfstate"
    storage_account_name = "tfstate"
    container_name       = "tfstate"
    key                  = "prod.terraform.tfstate"
  }
}
```

#### GCS Backend
```hcl
terraform {
  backend "gcs" {
    bucket      = "tf-state-bucket"
    prefix      = "terraform/state"
    credentials = "path/to/account.json"
  }
}
```

## Planning

### Create Execution Plan
```bash
terraform plan                   # Show execution plan
terraform plan -out=plan.tfplan  # Save plan to file
terraform plan -destroy          # Plan for resource destruction
terraform plan -refresh=false    # Skip state refresh
terraform plan -refresh-only     # Plan refresh without changes
terraform plan -target=aws_instance.example  # Plan specific resource
terraform plan -target=module.vpc            # Plan specific module
terraform plan -var 'instance_count=5'       # Set variable
terraform plan -var-file=prod.tfvars         # Load variables from file
terraform plan -var-file=common.tfvars -var-file=prod.tfvars  # Multiple var files
```

### Advanced Planning Options
```bash
terraform plan -compact-warnings            # Compact warnings
terraform plan -detailed-exitcode           # Detailed exit codes (0=no changes, 1=error, 2=changes)
terraform plan -lock=false                  # Don't hold state lock
terraform plan -lock-timeout=30s            # State lock timeout
terraform plan -no-color                    # Disable color output
terraform plan -parallelism=10              # Limit concurrent operations
terraform plan -replace=aws_instance.example # Force replacement plan
terraform plan -generate-config-out=generated.tf # Generate configuration for imported resources
```

### Plan File Usage
```bash
# Create and save plan
terraform plan -out=plan.tfplan

# Show saved plan contents
terraform show plan.tfplan

# Show plan in JSON format
terraform show -json plan.tfplan

# Render plan as graph
terraform graph -plan=plan.tfplan | dot -Tsvg > plan.svg
```

## Applying Changes

### Apply Changes
```bash
terraform apply                   # Apply changes (prompts for confirmation)
terraform apply -auto-approve     # Apply without confirmation
terraform apply plan.tfplan       # Apply saved plan
terraform apply -target=aws_instance.example  # Apply specific resource
terraform apply -target=module.vpc  # Apply specific module
terraform apply -var 'instance_count=5'  # Set variable
terraform apply -var-file=prod.tfvars    # Load variables from file
```

### Advanced Apply Options
```bash
terraform apply -compact-warnings         # Compact warnings
terraform apply -lock=false               # Don't hold state lock
terraform apply -lock-timeout=30s         # State lock timeout
terraform apply -parallelism=10           # Limit concurrent operations
terraform apply -refresh=false            # Skip state refresh
terraform apply -refresh-only             # Refresh state without making changes
terraform apply -replace=aws_instance.example  # Force replacement of resource
terraform apply -json                     # JSON output format
```

### Destroy Resources
```bash
terraform destroy                         # Destroy all resources (prompts for confirmation)
terraform destroy -auto-approve           # Destroy without confirmation
terraform destroy -target=aws_instance.example  # Destroy specific resource
terraform destroy -target=module.vpc      # Destroy specific module
terraform destroy -var-file=prod.tfvars   # Destroy with variables
```

### Targeted Operations
```bash
# Target multiple resources
terraform apply -target=aws_instance.web -target=aws_instance.db

# Target resources by pattern
terraform apply -target="aws_instance.web[*]"  # All instances in a list
terraform apply -target="module.vpc.*"         # All resources in a module
```

## State Management

### View State
```bash
terraform state list                    # List resources in state
terraform state list aws_instance.*     # List with filter
terraform state list 'module.vpc.*'     # List module resources
terraform state show aws_instance.web   # Show resource details
terraform state show 'module.vpc.aws_subnet.public[0]'  # Show indexed resource
```

### State Operations
```bash
# Move resource within state
terraform state mv aws_instance.web aws_instance.web_server

# Move resource between modules
terraform state mv module.old.aws_instance.web module.new.aws_instance.web

# Move indexed resources
terraform state mv 'aws_instance.web[0]' 'aws_instance.web["prod"]'

# Remove resource from state (doesn't destroy infrastructure)
terraform state rm aws_instance.web
terraform state rm 'module.vpc.*'  # Remove multiple resources

# Import existing infrastructure
terraform import aws_instance.web i-1234567890abcdef0
terraform import 'aws_instance.web[0]' i-1234567890abcdef0

# Pull remote state to local file
terraform state pull > terraform.tfstate

# Push local state to remote
terraform state push terraform.tfstate

# Refresh state
terraform refresh
terraform refresh -var-file=prod.tfvars
```

### State Backup
```bash
# Backup state before operations
cp .terraform/terraform.tfstate terraform.tfstate.backup

# Recover from backup
cp terraform.tfstate.backup .terraform/terraform.tfstate
```

## Workspace Management

### Workspace Operations
```bash
terraform workspace list          # List workspaces
terraform workspace show          # Show current workspace
terraform workspace new dev       # Create new workspace
terraform workspace new prod      # Create another workspace
terraform workspace select dev    # Switch to workspace
terraform workspace delete test   # Delete workspace
```

### Workspace Examples
```bash
# Create infrastructure in multiple environments
terraform workspace new prod
terraform apply -var-file=prod.tfvars

terraform workspace new dev
terraform apply -var-file=dev.tfvars

# Use current workspace in configuration
variable "instance_count" {
  default = {
    default = 1
    dev     = 2
    prod    = 5
  }
}

resource "aws_instance" "example" {
  count = lookup(var.instance_count, terraform.workspace, var.instance_count["default"])
  # ... other configuration ...
}
```

## Module Management

### Module Operations
```bash
terraform get                    # Download modules
terraform get -update            # Update modules
terraform providers              # Show providers required by modules
```

### Module Configuration Examples
```hcl
# Basic module usage
module "vpc" {
  source = "terraform-aws-modules/vpc/aws"
  version = "3.14.0"
  
  name = "my-vpc"
  cidr = "10.0.0.0/16"
}

# Local module
module "web_app" {
  source = "./modules/web_app"
}

# Git module
module "network" {
  source = "git::https://github.com/example/network.git?ref=v1.2.0"
}

# Module with providers
module "k8s" {
  source = "./modules/kubernetes"
  
  providers = {
    kubernetes = kubernetes.eks
  }
}
```

### Module Documentation
```bash
# Generate module documentation (requires terraform-docs)
terraform-docs markdown table . > README.md
terraform-docs markdown . --output-file README.md
terraform-docs yaml ./modules/vpc/
```

## Variables & Outputs

### Variable Definition Methods
```bash
# Command line
terraform apply -var 'region=us-west-2'
terraform apply -var 'zones=["us-west-2a", "us-west-2b"]'
terraform apply -var 'instance_config={type="t2.micro", count=5}'

# From file
terraform apply -var-file=prod.tfvars
terraform apply -var-file=common.tfvars -var-file=prod.tfvars

# Auto-loaded files
# terraform.tfvars
# terraform.tfvars.json
# *.auto.tfvars
# *.auto.tfvars.json

# Environment variables
export TF_VAR_region=us-west-2
export TF_VAR_zones='["us-west-2a", "us-west-2b"]'
export TF_VAR_instance_config='{"type":"t2.micro", "count":5}'
```

### Variable Types and Syntax
```hcl
# String variable
variable "region" {
  type        = string
  default     = "us-east-1"
  description = "AWS region to deploy resources"
}

# Number variable
variable "instance_count" {
  type        = number
  default     = 2
  description = "Number of instances to deploy"
}

# Boolean variable
variable "enable_monitoring" {
  type        = bool
  default     = true
  description = "Enable detailed monitoring"
}

# List variable
variable "availability_zones" {
  type        = list(string)
  default     = ["us-east-1a", "us-east-1b"]
  description = "List of availability zones"
}

# Map variable
variable "instance_types" {
  type        = map(string)
  default     = {
    dev  = "t2.micro"
    test = "t2.medium"
    prod = "t2.large"
  }
  description = "Instance types by environment"
}

# Object variable
variable "vpc_config" {
  type = object({
    cidr_block = string
    enable_dns = bool
    tags       = map(string)
  })
  default = {
    cidr_block = "10.0.0.0/16"
    enable_dns = true
    tags       = {
      Environment = "dev"
    }
  }
  description = "VPC configuration"
}

# Sensitive variable
variable "database_password" {
  type        = string
  sensitive   = true
  description = "Database password"
}

# Variable with validation
variable "environment" {
  type        = string
  default     = "dev"
  description = "Deployment environment"

  validation {
    condition     = contains(["dev", "test", "prod"], var.environment)
    error_message = "Environment must be one of: dev, test, prod."
  }
}
```

### Outputs Management
```bash
terraform output                 # Show all outputs
terraform output vpc_id          # Show specific output
terraform output -json           # Show outputs in JSON format
terraform output -raw vpc_id     # Show raw value without quotes
```

### Output Configuration
```hcl
# Basic output
output "instance_ip" {
  value = aws_instance.example.public_ip
  description = "Public IP of the instance"
}

# Sensitive output
output "db_password" {
  value       = random_password.db.result
  sensitive   = true
  description = "Generated database password"
}

# Complex output
output "vpc_info" {
  value = {
    id         = aws_vpc.main.id
    cidr_block = aws_vpc.main.cidr_block
    subnets    = aws_subnet.main[*].id
  }
  description = "VPC information"
}

# Output with precondition
output "load_balancer_dns" {
  value       = aws_lb.example.dns_name
  description = "Load balancer DNS name"
  
  precondition {
    condition     = var.environment == "prod"
    error_message = "Load balancer is only created in production environment."
  }
}
```

## Import & Export

### Import Resources
```bash
# Basic import
terraform import aws_instance.web i-1234567890abcdef0

# Import with module
terraform import module.app.aws_instance.web i-1234567890abcdef0

# Import indexed resource
terraform import 'aws_instance.web[0]' i-1234567890abcdef0
terraform import 'aws_instance.web["prod"]' i-1234567890abcdef0

# Import with variables
terraform import -var 'env=prod' aws_instance.web i-1234567890abcdef0
terraform import -var-file=prod.tfvars aws_instance.web i-1234567890abcdef0
```

### Generate Configuration
```bash
# Generate configuration for imported resources (Terraform 1.5+)
terraform plan -generate-config-out=generated.tf

# Use with import
terraform import aws_instance.web i-1234567890abcdef0
terraform plan -generate-config-out=generated.tf
```

### Config-driven Imports (Terraform 1.5+)
```hcl
# In terraform configuration
import {
  to = aws_instance.web
  id = "i-1234567890abcdef0"
}

import {
  to = aws_s3_bucket.logs
  id = "my-logs-bucket"
}
```

### Export Data
```bash
terraform show                   # Display state
terraform show -json             # Display state in JSON
terraform show plan.tfplan       # Display saved plan
terraform show -json plan.tfplan > plan.json  # Export plan as JSON
```

## Providers

### Provider Management
```bash
terraform providers              # List providers
terraform providers schema       # Show provider schema
terraform providers schema -json # Show provider schema in JSON
```

### Provider Installation
```bash
terraform init                   # Install providers needed in configuration
terraform init -upgrade          # Upgrade providers to latest version
terraform init -plugin-dir=PATH  # Use plugins from specific path
```

### Provider Versions
```hcl
# Specify provider version
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"          # Any 4.x version
    }
    
    azurerm = {
      source  = "hashicorp/azurerm"
      version = ">= 3.0.0, < 4.0.0"  # Between 3.0.0 and 4.0.0
    }
    
    google = {
      source  = "hashicorp/google"
      version = "4.51.0"          # Exactly 4.51.0
    }
  }
}
```

### Provider Lock File
```bash
terraform providers lock         # Create provider lock file
terraform providers lock -platform=darwin_amd64  # Lock for specific platform
terraform providers lock -platform=windows_amd64 -platform=linux_amd64  # Multiple platforms
```

### Provider Mirror
```bash
terraform providers mirror <dir> # Mirror providers to directory
```

### Multiple Provider Configurations
```hcl
# Define multiple provider configurations
provider "aws" {
  region = "us-west-2"
  alias  = "west"
}

provider "aws" {
  region = "us-east-1"
  alias  = "east"
}

# Use specific provider configuration
resource "aws_instance" "west_instance" {
  provider = aws.west
  ami      = "ami-0a1b2c3d4e5f6g7h8"
  instance_type = "t2.micro"
}
```

## Console & Debugging

### Interactive Console
```bash
terraform console                # Start interactive console
terraform console -var 'env=prod'  # Console with variables
terraform console -var-file=prod.tfvars  # Console with var file
```

### Console Commands
```
> var.region                     # Show variable value
> aws_instance.web.id            # Show resource attribute
> length(aws_subnet.main)        # Use function
> jsondecode(file("config.json"))  # Parse JSON file
> templatefile("template.tpl", { port = 8080 })  # Render template
> exit                           # Exit console
```

### Debug Logging
```bash
export TF_LOG=TRACE              # Set log level (TRACE, DEBUG, INFO, WARN, ERROR)
export TF_LOG_PATH=./terraform.log  # Set log file
export TF_LOG_CORE=TRACE         # Core log level
export TF_LOG_PROVIDER=TRACE     # Provider log level
```

### Crash Log
```bash
terraform crash-log              # Show crash log (if available)
```

### Debugging Techniques
```bash
# Debug version info
TF_LOG=DEBUG terraform version

# Debug initialization
TF_LOG=DEBUG terraform init

# Debug provider/plugin communication
TF_LOG=TRACE terraform apply
```

## Formatting & Validation

### Format Code
```bash
terraform fmt                    # Format current directory
terraform fmt -recursive         # Format code recursively
terraform fmt -check             # Check formatting (exit code 0 if formatted)
terraform fmt -diff              # Show formatting differences
terraform fmt -write=false       # Don't write changes to files
```

### Validate Configuration
```bash
terraform validate               # Validate configuration
terraform validate -json         # Validate with JSON output
terraform validate -no-color     # Validate without color
```

### Linting with tflint
```bash
# Install tflint
curl -s https://raw.githubusercontent.com/terraform-linters/tflint/master/install_linux.sh | bash

# Run tflint
tflint
tflint --format=json
tflint --var-file=prod.tfvars
```

## Environment Variables

### Core Variables
```bash
TF_CLI_ARGS                      # Additional CLI args for all commands
TF_CLI_ARGS_<command>            # Args for specific command, e.g., TF_CLI_ARGS_plan
TF_DATA_DIR                      # Directory for plugin cache and state (default: .terraform)
TF_IN_AUTOMATION                 # Set to any value for automation mode
TF_INPUT                         # Disable interactive prompts (0/1)
TF_LOG                           # Log level (TRACE, DEBUG, INFO, WARN, ERROR)
TF_LOG_PATH                      # Log file path
TF_WORKSPACE                     # Set workspace
```

### Provider-Specific Variables
```bash
# AWS Provider
AWS_ACCESS_KEY_ID                # AWS access key
AWS_SECRET_ACCESS_KEY            # AWS secret key
AWS_PROFILE                      # AWS profile name
AWS_REGION                       # AWS region

# Azure Provider
ARM_CLIENT_ID                    # Azure client ID
ARM_CLIENT_SECRET                # Azure client secret
ARM_SUBSCRIPTION_ID              # Azure subscription ID
ARM_TENANT_ID                    # Azure tenant ID

# Google Provider
GOOGLE_CREDENTIALS               # Path to or contents of a service account key file
GOOGLE_PROJECT                   # Google Cloud project ID
GOOGLE_REGION                    # Google Cloud region
```

### Performance Variables
```bash
TF_PLUGIN_CACHE_DIR              # Plugin cache directory
TF_SKIP_PROVIDER_VERIFY          # Skip provider checksum verification (1/0)
TF_CLI_ARGS_plan="-parallelism=30"  # Increase parallelism for plan
```

### Variable Definition
```bash
TF_VAR_region=us-west-2          # Set 'region' variable
TF_VAR_availability_zones='["us-west-2a", "us-west-2b"]'  # List variable
TF_VAR_instance_config='{"type":"t2.micro", "count":5}'  # Map/object variable
```

## Advanced Options

### Terraform Lock
```bash
terraform force-unlock <lock-id> # Force unlock state
terraform force-unlock -force <lock-id>  # Force unlock without confirmation
```

### Graph Generation
```bash
terraform graph                  # Generate resource graph
terraform graph -type=plan       # Generate plan graph
terraform graph -type=plan-destroy  # Generate destroy plan graph
terraform graph -type=apply      # Generate apply graph
terraform graph | dot -Tsvg > graph.svg  # Generate SVG graph
terraform graph | dot -Tpng > graph.png  # Generate PNG graph
```

### Resource Targeting
```bash
terraform taint aws_instance.web  # Mark resource for recreation
terraform untaint aws_instance.web  # Remove taint from resource
terraform apply -replace="aws_instance.web"  # Force replacement (Terraform 0.15.2+)
```

### Command Timing
```bash
time terraform apply              # Time command execution
```

### JSON Output Processing
```bash
# Extract output value with jq
terraform output -json | jq '.vpc_id.value'

# Process plan output
terraform show -json plan.tfplan | jq '.resource_changes[] | select(.change.actions[] | contains("create"))'
```

## Remote Operations

### Remote State Operations
```bash
# Configure remote state (example for S3 backend)
terraform init \
  -backend-config="bucket=tf-state-bucket" \
  -backend-config="key=prod/terraform.tfstate" \
  -backend-config="region=us-east-1"

# Force local state
terraform init -backend=false

# Reconfigure backend
terraform init -reconfigure

# Migrate between backends
terraform init -migrate-state

# Disable remote operations
terraform init -backend=false
```

### Remote Execution
```bash
# Configure remote execution
terraform init \
  -backend-config="address=app.terraform.io" \
  -backend-config="organization=my-org" \
  -backend-config="token=$TF_API_TOKEN"

# Run in remote environment
terraform plan -remote
terraform apply -remote
```

## Testing

### Basic Testing
```bash
# Run all tests in directory
terraform test

# Test specific module
cd modules/vpc && terraform test

# Test with variables
TF_VAR_region=us-west-2 terraform test
```

### Test Configuration
```hcl
# In a test file (*.tftest.hcl)
variables {
  region = "us-west-2"
  instance_type = "t2.micro"
}

run "create_instance" {
  command = plan

  assert {
    condition     = aws_instance.example.instance_type == "t2.micro"
    error_message = "Incorrect instance type"
  }
}
```

### Terratest (Go Testing Framework)
```go
// test/vpc_test.go
package test

import (
	"testing"
	"github.com/gruntwork-io/terratest/modules/terraform"
	"github.com/stretchr/testify/assert"
)

func TestVPC(t *testing.T) {
	terraformOptions := &terraform.Options{
		TerraformDir: "../modules/vpc",
		Vars: map[string]interface{}{
			"region": "us-west-2",
			"cidr": "10.0.0.0/16",
		},
	}

	defer terraform.Destroy(t, terraformOptions)
	terraform.InitAndApply(t, terraformOptions)

	vpcId := terraform.Output(t, terraformOptions, "vpc_id")
	assert.NotEmpty(t, vpcId)
}
```

## Security

### Static Analysis
```bash
# Install checkov
pip install checkov

# Run checkov on directory
checkov -d .

# Run tfsec
docker run --rm -v "$(pwd):/src" aquasec/tfsec /src

# Run terrascan
docker run --rm -v "$(pwd):/src" accurics/terrascan scan -d /src
```

### Sensitive Data Handling
```hcl
# Mark variable as sensitive
variable "db_password" {
  type      = string
  sensitive = true
}

# Mark output as sensitive
output "admin_password" {
  value     = random_password.admin.result
  sensitive = true
}

# Protect sensitive data in state
terraform {
  backend "s3" {
    bucket         = "terraform-state-bucket"
    key            = "terraform.tfstate"
    region         = "us-east-1"
    encrypt        = true                 # Encrypt state
    kms_key_id     = "arn:aws:kms:us-east-1:123456789012:key/abcd1234"
    dynamodb_table = "terraform-locks"    # Locking table
  }
}
```

### Access Control
```hcl
# Require approval for specific actions
terraform {
  cloud {
    organization = "my-org"
    workspaces {
      name = "prod"
    }
  }
}

# Use IAM roles for provider authentication
provider "aws" {
  region = "us-west-2"
  assume_role {
    role_arn     = "arn:aws:iam::123456789012:role/TerraformExecutionRole"
    session_name = "Terraform"
  }
}
```

## Terraform Cloud & Enterprise

### Login/Authentication
```bash
terraform login                  # Login to Terraform Cloud/Enterprise
terraform logout                 # Log out from Terraform Cloud/Enterprise
```

### Workspace Management
```bash
# Configure workspace
terraform {
  cloud {
    organization = "my-org"
    workspaces {
      name = "prod-infrastructure"
    }
  }
}

# Or with tags
terraform {
  cloud {
    organization = "my-org"
    workspaces {
      tags = ["networking", "prod"]
    }
  }
}
```

### Cloud Operations
```bash
# View state in Terraform Cloud
terraform state list

# Run operations in Terraform Cloud
terraform plan
terraform apply

# Migrate local state to Terraform Cloud
terraform init
```

### CLI Configuration
```bash
# Configure CLI credentials
# ~/.terraform.d/credentials.tfrc.json
{
  "credentials": {
    "app.terraform.io": {
      "token": "TERRAFORM_CLOUD_TOKEN"
    },
    "terraform.example.com": {
      "token": "TERRAFORM_ENTERPRISE_TOKEN"
    }
  }
}
```

## Common Workflows

### Typical Development Workflow
```bash
# Initialize and check formatting
terraform init
terraform fmt -recursive -check

# Validate syntax and plan
terraform validate
terraform plan

# Apply changes and verify outputs
terraform apply
terraform output

# Clean up
terraform destroy
```

### CI/CD Pipeline Workflow
```bash
# CI/CD Setup
export TF_IN_AUTOMATION=true
terraform init -input=false
terraform validate
terraform plan -out=tfplan -input=false
terraform show -json tfplan > tfplan.json

# Review plan

# Apply in CI/CD
terraform apply -input=false -auto-approve tfplan
```

### Module Development Workflow
```bash
# Set up module structure
mkdir -p modules/vpc
touch modules/vpc/{main.tf,variables.tf,outputs.tf,README.md}

# Initialize and format
cd modules/vpc
terraform init
terraform fmt

# Generate documentation
terraform-docs markdown table . > README.md

# Test module
cd ../../
terraform init
terraform validate
terraform plan -target=module.vpc
terraform apply -target=module.vpc
```

### Production Deployment Workflow
```bash
# Setup environments
terraform workspace new prod
terraform workspace select prod

# Create plan
terraform plan -out=prod.plan -var-file=prod.tfvars

# Review plan
terraform show prod.plan

# Apply plan
terraform apply prod.plan

# Verify
terraform output
```

### State Migration Workflow
```bash
# Backup current state
terraform state pull > terraform.tfstate.backup

# Configure new backend
terraform init -backend-config="bucket=new-tf-state-bucket" \
               -backend-config="key=terraform.tfstate" \
               -backend-config="region=us-east-1"

# Migrate state
terraform init -migrate-state
```

### Infrastructure Refactoring Workflow
```bash
# Step 1: Create a backup
terraform state pull > terraform.tfstate.backup

# Step 2: Move resources (when renaming)
terraform state mv aws_instance.app aws_instance.application

# Step 3: Move resources between modules
terraform state mv module.old.aws_vpc.main module.new.aws_vpc.main

# Step 4: Plan to verify changes
terraform plan

# Step 5: Apply new configuration
terraform apply
```

## Troubleshooting

### Common Issues and Solutions

#### State Lock Issues
```bash
# Error: Error acquiring the state lock
terraform force-unlock <LOCK_ID>

# Check for the lock ID in error message:
# "Error: Error acquiring the state lock
#  Lock Info: ID:<LOCK_ID>"
```

#### Provider Plugin Issues
```bash
# Clear plugin cache
rm -rf .terraform/providers

# Re-initialize with debug info
TF_LOG=DEBUG terraform init

# Force reinstall plugin
terraform init -upgrade
```

#### State Corruption
```bash
# Restore from backup
cp terraform.tfstate.backup terraform.tfstate

# Push fixed state
terraform state push terraform.tfstate
```

#### Backend Configuration Issues
```bash
# Reset to local state
terraform init -backend=false

# Verify backend config
cat backend.tf
terraform init -reconfigure
```

#### Authentication Issues
```bash
# Check provider credentials
env | grep AWS
env | grep ARM
env | grep GOOGLE

# Set credentials explicitly
export AWS_ACCESS_KEY_ID="your-access-key"
export AWS_SECRET_ACCESS_KEY="your-secret-key"
terraform plan
```

#### Performance Issues
```bash
# Enable trace logging for performance analysis
export TF_LOG=TRACE
export TF_LOG_PATH=./terraform_trace.log
time terraform apply

# Increase parallelism
terraform apply -parallelism=30
```

#### Version Compatibility Issues
```bash
# Check version constraints
grep -r "required_version\|required_providers" .

# Use tfenv to switch versions
tfenv install 1.5.7
tfenv use 1.5.7
```

### Error Interpretation
```
# Error: Resource already exists
Error: aws_instance.example: Resource already exists

Solution: Import the resource into state:
terraform import aws_instance.example i-abcd1234

# Error: Resource not found
Error: Resource 'aws_instance.example' not found in state.

Solution: Check resource naming or add the resource to configuration.

# Error: Unsupported attribute
Error: Unsupported attribute

Solution: Verify attribute names and provider version compatibility.
```

## Best Practices

### Code Organization

```bash
# Standard project structure
project/
├── main.tf               # Main resources
├── variables.tf          # Input variables
├── outputs.tf            # Output values
├── providers.tf          # Provider configuration
├── backends.tf           # Backend configuration
├── versions.tf           # Terraform version constraints
├── locals.tf             # Local values
├── data.tf               # Data sources
├── modules/              # Local modules
│   └── vpc/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
├── environments/         # Environment-specific configs
│   ├── dev.tfvars
│   ├── staging.tfvars
│   └── prod.tfvars
└── scripts/              # Helper scripts
    └── update_modules.sh
```

### Naming Conventions
```hcl
# Resource naming convention
resource "aws_instance" "web_server" {
  # ...
}

# Variable naming convention
variable "vpc_cidr_block" {
  # ...
}

# Output naming convention
output "load_balancer_dns_name" {
  # ...
}

# Local value naming convention
locals {
  common_tags = {
    Project     = "ExampleProject"
    Environment = var.environment
    ManagedBy   = "Terraform"
  }
}
```

### State Management Best Practices
```hcl
# Remote state with locking and encryption
terraform {
  backend "s3" {
    bucket         = "terraform-state"
    key            = "environment/app/terraform.tfstate"
    region         = "us-west-2"
    encrypt        = true
    dynamodb_table = "terraform-locks"
    kms_key_id     = "arn:aws:kms:us-west-2:111122223333:key/1234abcd"
  }
}

# Output state data for other configurations
output "vpc_id" {
  value = aws_vpc.main.id
}

# Use remote state data from other configurations
data "terraform_remote_state" "network" {
  backend = "s3"
  config = {
    bucket = "terraform-state"
    key    = "environment/network/terraform.tfstate"
    region = "us-west-2"
  }
}

resource "aws_instance" "app" {
  subnet_id = data.terraform_remote_state.network.outputs.subnet_id
}
```

### Module Usage
```hcl
# Root module - keep it simple
module "vpc" {
  source = "./modules/vpc"
  
  cidr_block = var.vpc_cidr
  environment = var.environment
}

module "web_app" {
  source = "./modules/web_app"
  
  vpc_id = module.vpc.vpc_id
  subnets = module.vpc.public_subnets
  environment = var.environment
  
  depends_on = [module.vpc]
}

# Use version constraints for registry modules
module "s3_bucket" {
  source  = "terraform-aws-modules/s3-bucket/aws"
  version = "~> 3.1"
  
  bucket = "my-unique-bucket"
  acl    = "private"
}
```

### Variables and Data Management
```hcl
# Variable defaults and validation
variable "environment" {
  type        = string
  description = "Deployment environment"
  default     = "dev"
  
  validation {
    condition     = contains(["dev", "test", "staging", "prod"], var.environment)
    error_message = "Environment must be one of: dev, test, staging, prod."
  }
}

# Use locals for derived values
locals {
  name_prefix = "${var.project}-${var.environment}"
  
  common_tags = {
    Project     = var.project
    Environment = var.environment
    ManagedBy   = "Terraform"
  }
  
  is_production = var.environment == "prod" ? true : false
}

# Apply consistent tagging
resource "aws_instance" "web" {
  # ... other configuration ...
  
  tags = merge(
    local.common_tags,
    {
      Name = "${local.name_prefix}-web"
      Role = "WebServer"
    }
  )
}
```

### Documentation
```hcl
# Document modules
/**
 * # VPC Module
 *
 * This module creates a VPC with public and private subnets across
 * multiple availability zones.
 *
 * ## Features
 * - Multi-AZ deployment
 * - NAT gateways for private subnet internet access
 * - Flow logs for network monitoring
 *
 * ## Usage
 * ```hcl
 * module "vpc" {
 *   source = "./modules/vpc"
 *   
 *   cidr_block = "10.0.0.0/16"
 *   environment = "prod"
 * }
 * ```
 */

# Document variables
variable "cidr_block" {
  type        = string
  description = "The CIDR block for the VPC. Default is 10.0.0.0/16."
  default     = "10.0.0.0/16"
}

# Document outputs
output "vpc_id" {
  description = "The ID of the VPC"
  value       = aws_vpc.main.id
}
```

### Performance Optimization
```bash
# Reduce plan/apply time
terraform apply -parallelism=20

# Use -target for large infrastructures
terraform plan -target=module.critical_component
terraform apply -target=module.critical_component

# Optimize provider configuration
provider "aws" {
  region = "us-west-2"
  
  # Increase retries for API rate limiting
  retries {
    max_attempts = 10
    min_interval_seconds = 1
  }
  
  # Skip metadata service lookup on instances
  skip_metadata_api_check     = true
  skip_region_validation      = true
  skip_credentials_validation = true
}
```

### Security Practices
```hcl
# Use provider assumption roles
provider "aws" {
  region = "us-west-2"
  assume_role {
    role_arn     = "arn:aws:iam::123456789012:role/TerraformExecutionRole"
    session_name = "Terraform"
    external_id  = "TerraformExternalID"  # Additional security
  }
}

# Store sensitive values in environment variables
variable "db_password" {
  type      = string
  sensitive = true
}

# Use external secrets management
data "aws_secretsmanager_secret_version" "db_credentials" {
  secret_id = "db-credentials"
}

locals {
  db_creds = jsondecode(data.aws_secretsmanager_secret_version.db_credentials.secret_string)
}

# Use lifecycle blocks to protect resources
resource "aws_instance" "critical" {
  # ... configuration ...
  
  lifecycle {
    prevent_destroy = true  # Prevent accidental destruction
  }
}
```

### Automation Tips
```bash
# Pre-commit hooks
# .pre-commit-config.yaml
repos:
- repo: https://github.com/antonbabenko/pre-commit-terraform
  rev: v1.80.0
  hooks:
    - id: terraform_fmt
    - id: terraform_validate
    - id: terraform_docs
    - id: terraform_tflint
    - id: terraform_checkov

# Automated testing script
#!/bin/bash
# test.sh
set -e

echo "Running terraform fmt check..."
terraform fmt -check -recursive

echo "Running terraform validate..."
terraform validate

echo "Running tflint..."
tflint

echo "Running terratest..."
cd test && go test -v ./...
```

---

This comprehensive cheatsheet covers Terraform CLI commands and best practices from version 1.0.0 through 1.6.x. For the most up-to-date information, please refer to the [official Terraform documentation](https://www.terraform.io/docs/cli/commands/index.html).

For additional resources:
- [Terraform Registry](https://registry.terraform.io/)
- [Terraform Language Documentation](https://www.terraform.io/docs/language/index.html)
- [Terraform Best Practices](https://www.terraform-best-practices.com/)