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

## Installation & Setup

### Installation
```bash
# MacOS
brew install terraform

# Windows
choco install terraform

# Linux
wget https://releases.hashicorp.com/terraform/1.6.2/terraform_1.6.2_linux_amd64.zip
unzip terraform_1.6.2_linux_amd64.zip
sudo mv terraform /usr/local/bin/
```

### Version Check
```bash
terraform version
```

### Auto-completion Setup
```bash
# Bash
terraform -install-autocomplete

# PowerShell
terraform -install-autocomplete
```

## Basic Commands

### Help
```bash
terraform -help                  # General help
terraform <command> -help        # Command-specific help
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
```

## Initialization

### Initialize Working Directory
```bash
terraform init                   # Initialize directory, download plugins
terraform init -upgrade          # Upgrade plugins to latest version
terraform init -reconfigure      # Reconfigure backend
terraform init -migrate-state    # Reconfigure backend, migrate state
terraform init -backend=false    # Initialize without backend configuration
```

### Backend Configuration
```bash
terraform init -backend-config=<path>     # Load backend settings from file
terraform init -backend-config="key=value" # Set specific backend setting
```

## Planning

### Create Plan
```bash
terraform plan                   # Show execution plan
terraform plan -out=<path>       # Save plan to file
terraform plan -destroy          # Plan for resource destruction
terraform plan -refresh=false    # Skip state refresh
terraform plan -target=<resource> # Plan specific resource only
terraform plan -var 'key=value'  # Set variable
terraform plan -var-file=<file>  # Load variables from file
```

### Plan Options
```bash
terraform plan -compact-warnings # Compact warnings
terraform plan -detailed-exitcode # Return detailed exit code
terraform plan -lock=false       # Don't hold state lock
terraform plan -no-color         # Disable color output
terraform plan -parallelism=<n>  # Limit concurrent operations
```

## Applying Changes

### Apply Changes
```bash
terraform apply                  # Apply changes (prompts for confirmation)
terraform apply -auto-approve    # Apply without confirmation
terraform apply <plan-file>      # Apply saved plan
terraform apply -target=<resource> # Apply specific resource only
terraform apply -var 'key=value' # Set variable
terraform apply -var-file=<file> # Load variables from file
```

### Apply Options
```bash
terraform apply -compact-warnings # Compact warnings
terraform apply -lock=false      # Don't hold state lock
terraform apply -lock-timeout=<duration> # State lock timeout
terraform apply -parallelism=<n> # Limit concurrent operations
terraform apply -refresh=false   # Skip state refresh
terraform apply -replace=<addr>  # Force replacement of resource
```

### Destroy Resources
```bash
terraform destroy                # Destroy all resources (prompts for confirmation)
terraform destroy -auto-approve  # Destroy without confirmation
terraform destroy -target=<resource> # Destroy specific resource only
```

## State Management

### List Resources
```bash
terraform state list             # List resources in state
terraform state list <filter>    # List resources matching filter
```

### Show Resource
```bash
terraform state show <resource>  # Show resource in state
```

### Move Resource
```bash
terraform state mv <source> <destination> # Move resource in state
```

### Remove Resource
```bash
terraform state rm <resource>    # Remove resource from state
```

### Pull State
```bash
terraform state pull             # Pull state from remote backend
terraform state pull > state.tfstate # Pull state to local file
```

### Push State
```bash
terraform state push <path>      # Push state to remote backend
```

### State Refresh
```bash
terraform refresh                # Refresh state
terraform refresh -var 'key=value' # Refresh with variable
```

## Workspace Management

### List Workspaces
```bash
terraform workspace list         # List workspaces
```

### Create Workspace
```bash
terraform workspace new <name>   # Create new workspace
```

### Select Workspace
```bash
terraform workspace select <name> # Switch to workspace
```

### Delete Workspace
```bash
terraform workspace delete <name> # Delete workspace
```

### Show Current Workspace
```bash
terraform workspace show         # Show current workspace
```

## Module Management

### Get Modules
```bash
terraform get                    # Download modules
terraform get -update            # Update modules
```

### Generate Module Documentation
```bash
terraform-docs markdown <dir>    # Generate documentation (requires terraform-docs)
```

## Variables & Outputs

### Set Variables
```bash
terraform apply -var 'key=value' # Set single variable
terraform apply -var-file=<file> # Load variables from file
```

### Environment Variables
```bash
export TF_VAR_name=value         # Set variable via environment
```

### Show Outputs
```bash
terraform output                 # Show all outputs
terraform output <output_name>   # Show specific output
terraform output -json           # Show outputs in JSON format
```

## Import & Export

### Import Resources
```bash
terraform import <resource_addr> <id> # Import existing infrastructure
terraform import -var 'key=value' <resource_addr> <id> # Import with variables
```

### Generate Configuration
```bash
terraform plan -generate-config-out=<path> # Generate config from plan (0.15+)
```

## Providers

### List Providers
```bash
terraform providers              # List providers
```

### Install Provider
```bash
terraform init                   # Install providers needed in configuration
```

### Provider Lock File
```bash
terraform providers lock         # Create provider lock file
terraform providers lock -platform=<os>_<arch> # Lock for specific platform
```

### Provider Mirror
```bash
terraform providers mirror <dir> # Mirror providers to directory
```

## Console & Debugging

### Interactive Console
```bash
terraform console                # Interactive console
terraform console -var 'key=value' # Console with variables
```

### Debug Logs
```bash
export TF_LOG=TRACE              # Set log level (TRACE, DEBUG, INFO, WARN, ERROR)
export TF_LOG_PATH=./terraform.log # Set log file
```

### Crash Log
```bash
terraform crash-log              # Shows crash log (if available)
```

## Formatting & Validation

### Format Code
```bash
terraform fmt                    # Format code in current directory
terraform fmt -recursive         # Format code recursively
terraform fmt -check             # Check formatting
terraform fmt -diff              # Show formatting differences
```

### Validate Configuration
```bash
terraform validate               # Validate configuration
terraform validate -json         # Validate with JSON output
```

## Environment Variables

```bash
TF_CLI_ARGS                      # Additional CLI args for all commands
TF_CLI_ARGS_<command>            # Args for specific command, e.g., TF_CLI_ARGS_plan
TF_DATA_DIR                      # Directory for plugin cache and state (default: .terraform)
TF_IN_AUTOMATION                 # Set to non-empty for automation mode
TF_INPUT                         # Disable/enable interactive prompts (0/1)
TF_LOG                           # Log level (TRACE, DEBUG, INFO, WARN, ERROR)
TF_LOG_PATH                      # Log file path
TF_PLUGIN_CACHE_DIR              # Plugin cache directory
TF_SKIP_PROVIDER_VERIFY          # Skip provider checksum verification (1/0)
TF_VAR_name                      # Value for variable "name"
TF_WORKSPACE                     # Set workspace
```

## Advanced Options

### Terraform Lock
```bash
terraform force-unlock <lock-id> # Force unlock state
```

### Terraform Login
```bash
terraform login                  # Login to Terraform Cloud/Enterprise
terraform logout                 # Log out from Terraform Cloud/Enterprise
```

### Test
```bash
terraform test                   # Run tests in test files (0.15+)
```

### Graph
```bash
terraform graph                  # Generate resource graph
terraform graph | dot -Tsvg > graph.svg # Generate SVG graph
```

### Terraform Cloud/Enterprise
```bash
terraform login                  # Login to Terraform Cloud/Enterprise
terraform logout                 # Log out
terraform taint <resource>       # Mark resource for recreation
terraform untaint <resource>     # Remove taint from resource
```

## Common Workflows

### Typical Development Workflow
```bash
terraform init                   # Initialize
terraform fmt                    # Format code
terraform validate               # Validate syntax
terraform plan                   # Plan changes
terraform apply                  # Apply changes
```

### Clean Workflow
```bash
terraform destroy                # Destroy resources
rm -rf .terraform .terraform.lock.hcl # Remove local state
terraform init                   # Start fresh
```

### Production Workflow
```bash
terraform init                   # Initialize
terraform workspace select prod  # Select workspace
terraform plan -out=prod.plan    # Create plan
terraform apply prod.plan        # Apply plan exactly as planned
```

---

This cheatsheet covers all major Terraform CLI commands through version 1.6.x. For the most up-to-date information, refer to the [official Terraform documentation](https://www.terraform.io/docs/cli/commands/index.html).