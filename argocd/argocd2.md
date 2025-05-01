# ArgoCD CLI Cheatsheet

## Table of Contents

- [Installation](#installation)
- [Login and Configuration](#login-and-configuration)
- [Applications](#applications)
- [Projects](#projects)
- [Repository Management](#repository-management)
- [Clusters](#clusters)
- [Context Management](#context-management)
- [RBAC and Account Management](#rbac-and-account-management)
- [Certificate Management](#certificate-management)
- [GPG Key Management](#gpg-key-management)
- [Server Management](#server-management) 
- [Troubleshooting Commands](#troubleshooting-commands)

## Installation

### Install ArgoCD CLI
```bash
# Mac (using Homebrew)
brew install argocd

# Linux
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64

# Windows (using Chocolatey)
choco install argocd-cli
```

### Check Version
```bash
argocd version
```

## Login and Configuration

### Login to ArgoCD Server
```bash
# Using username/password
argocd login <ARGOCD_SERVER> [--username <USERNAME> --password <PASSWORD>]

# Using SSO
argocd login <ARGOCD_SERVER> --sso

# Insecure connection (skip TLS verification)
argocd login <ARGOCD_SERVER> --insecure
```

### Logout
```bash
argocd logout <ARGOCD_SERVER>
```

### List Contexts
```bash
argocd context
```

### Switch Contexts
```bash
argocd context <NAME>
```

### Add Context
```bash
argocd context <NAME> --server <SERVER> --user <USER> --project <PROJECT>
```

### Set Default Context
```bash
argocd context --current --server <SERVER> --user <USER> --project <PROJECT>
```

## Applications

### List Applications
```bash
# List all applications
argocd app list

# List applications in a specific project
argocd app list -p <PROJECT_NAME>

# Output in different formats
argocd app list -o wide
argocd app list -o yaml
argocd app list -o json
```

### Create Application
```bash
# Basic create
argocd app create <APP_NAME> \
  --repo <GIT_REPO> \
  --path <PATH_IN_REPO> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE>

# From Helm chart
argocd app create <APP_NAME> \
  --repo <GIT_REPO> \
  --helm-chart <CHART_NAME> \
  --revision <CHART_VERSION> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE>

# From Kustomize
argocd app create <APP_NAME> \
  --repo <GIT_REPO> \
  --path <PATH_IN_REPO> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE> \
  --kustomize-common-label=<KEY>=<VALUE>

# Create from a YAML file
argocd app create -f app.yaml
```

### Get Application Details
```bash
argocd app get <APP_NAME>

# Get output in different formats
argocd app get <APP_NAME> -o yaml
argocd app get <APP_NAME> -o json
```

### Sync Application
```bash
# Basic sync
argocd app sync <APP_NAME>

# Force sync
argocd app sync <APP_NAME> --force

# Sync with specific revision
argocd app sync <APP_NAME> --revision <COMMIT_SHA_OR_BRANCH>

# Prune resources
argocd app sync <APP_NAME> --prune

# Apply only certain resources
argocd app sync <APP_NAME> --resource <GROUP:KIND:NAME>

# Sync only resources that are out of sync
argocd app sync <APP_NAME> --local=out-of-sync-only

# Replace resources instead of applying
argocd app sync <APP_NAME> --replace
```

### Delete Application
```bash
# Basic delete
argocd app delete <APP_NAME>

# Force delete without confirmation
argocd app delete <APP_NAME> --cascade

# Delete without cascade (keep the deployed resources)
argocd app delete <APP_NAME> --cascade=false
```

### Application History and Rollback
```bash
# View application history
argocd app history <APP_NAME>

# Rollback to a previous version
argocd app rollback <APP_NAME> <ID>
```

### Application Set and Unset Parameters
```bash
# Set parameters
argocd app set <APP_NAME> --parameter <KEY>=<VALUE>
argocd app set <APP_NAME> --helm-set <KEY>=<VALUE>
argocd app set <APP_NAME> --kustomize-image <IMAGE>=<TAG>

# Set app sync policy
argocd app set <APP_NAME> --sync-policy automated
argocd app set <APP_NAME> --sync-policy none

# Enable/disable auto-pruning
argocd app set <APP_NAME> --auto-prune
argocd app set <APP_NAME> --no-prune

# Enable/disable self-healing
argocd app set <APP_NAME> --self-heal
argocd app set <APP_NAME> --no-self-heal
```

### Application Diff and Patch
```bash
# View differences between live and desired state
argocd app diff <APP_NAME>

# Patch application
argocd app patch <APP_NAME> --patch <PATCH> --type json
```

### Application Actions
```bash
# Refresh application status
argocd app refresh <APP_NAME>

# Wait for synchronization to complete
argocd app wait <APP_NAME> --health

# Terminate ongoing operations
argocd app terminate-op <APP_NAME>

# Show application resources
argocd app resources <APP_NAME>

# Show application manifests
argocd app manifests <APP_NAME>
```

## Projects

### List Projects
```bash
argocd proj list
```

### Create Project
```bash
# Basic create
argocd proj create <PROJECT_NAME>

# Create from YAML file
argocd proj create -f project.yaml
```

### Delete Project
```bash
argocd proj delete <PROJECT_NAME>
```

### Get Project Details
```bash
argocd proj get <PROJECT_NAME>
```

### Project Add/Remove Destinations
```bash
# Add allowed destination
argocd proj add-destination <PROJECT_NAME> <CLUSTER_URL> <NAMESPACE>

# Remove destination
argocd proj remove-destination <PROJECT_NAME> <CLUSTER_URL> <NAMESPACE>
```

### Project Add/Remove Sources
```bash
# Add allowed source repository
argocd proj add-source <PROJECT_NAME> <REPO_URL>

# Remove source repository
argocd proj remove-source <PROJECT_NAME> <REPO_URL>
```

### Project Resource Management
```bash
# Allow resource
argocd proj allow-cluster-resource <PROJECT_NAME> <GROUP> <KIND> <ACTION>

# Deny resource
argocd proj deny-cluster-resource <PROJECT_NAME> <GROUP> <KIND> <ACTION>
```

### Project Role Management
```bash
# Create role
argocd proj role create <PROJECT_NAME> <ROLE_NAME>

# Add policy to role
argocd proj role add-policy <PROJECT_NAME> <ROLE_NAME> <ACTION> <OBJECT> <PERMISSION>

# Add user/group to role
argocd proj role add-group <PROJECT_NAME> <ROLE_NAME> <GROUP>
argocd proj role add-token <PROJECT_NAME> <ROLE_NAME> <TOKEN>

# Remove user/group from role
argocd proj role remove-group <PROJECT_NAME> <ROLE_NAME> <GROUP>
argocd proj role remove-token <PROJECT_NAME> <ROLE_NAME> <TOKEN>
```

## Repository Management

### List Repositories
```bash
argocd repo list
```

### Add Repository
```bash
# Add Git repository
argocd repo add <REPO_URL> --username <USERNAME> --password <PASSWORD>

# Add private repository using SSH key
argocd repo add <REPO_URL> --ssh-private-key-path <PATH_TO_KEY>

# Add Helm repository
argocd repo add <REPO_URL> --type helm --name <REPO_NAME> --username <USERNAME> --password <PASSWORD>

# Add OCI based Helm repository
argocd repo add <REPO_URL> --type helm --name <REPO_NAME> --enable-oci --username <USERNAME> --password <PASSWORD>
```

### Remove Repository
```bash
argocd repo rm <REPO_URL>
```

### Get Repository Details
```bash
argocd repo get <REPO_URL>
```

## Clusters

### List Clusters
```bash
argocd cluster list
```

### Add Cluster
```bash
# Add cluster using current kubeconfig context
argocd cluster add <CONTEXT_NAME>

# Add cluster with specific RBAC privileges
argocd cluster add <CONTEXT_NAME> --namespace <NAMESPACE> --in-cluster
```

### Remove Cluster
```bash
argocd cluster rm <CLUSTER_URL>
```

### Get Cluster Details
```bash
argocd cluster get <CLUSTER_URL>
```

## Context Management

### List Contexts
```bash
argocd context
```

### Switch Context
```bash
argocd context <SERVER_NAME>
```

### Delete Context
```bash
argocd context delete <SERVER_NAME>
```

## RBAC and Account Management

### List Users
```bash
argocd account list
```

### Get User Details
```bash
argocd account get <USERNAME>
```

### Update Password
```bash
# Update current user's password
argocd account update-password

# Update another user's password (requires admin)
argocd account update-password --account <USERNAME> --current-password <ADMIN_PASSWORD> --new-password <NEW_PASSWORD>
```

### Create Token
```bash
argocd account generate-token --account <USERNAME>
```

### Manage RBAC
```bash
# Get RBAC permissions
argocd admin settings rbac

# Update RBAC policy
argocd admin settings rbac --policy <POLICY_FILE>
```

## Certificate Management

### Add Certificate
```bash
argocd cert add-tls <HOSTNAME> --from <SOURCE>
```

### List Certificates
```bash
argocd cert list
```

### Remove Certificate
```bash
argocd cert rm <HOSTNAME>
```

## GPG Key Management

### List GPG Keys
```bash
argocd gpg list
```

### Add GPG Key
```bash
argocd gpg add --from <KEY_PATH>
```

### Delete GPG Key
```bash
argocd gpg rm <KEY_ID>
```

## Server Management

### Admin Settings
```bash
# View current settings
argocd admin settings 

# Update settings
argocd admin settings --update-file <FILE_PATH>
```

### Server Version
```bash
argocd admin version
```

### Export/Import
```bash
# Export all ArgoCD configurations
argocd admin export > backup.yaml

# Import ArgoCD configurations
argocd admin import - < backup.yaml
```

### Notifications
```bash
# Get notifications settings
argocd admin notifications settings

# Get notification templates
argocd admin notifications template get <TEMPLATE_NAME>

# Get notification triggers
argocd admin notifications trigger get <TRIGGER_NAME>
```

## Troubleshooting Commands

### App Status and Events
```bash
# View application events 
argocd app events <APP_NAME>

# View application logs
argocd app logs <APP_NAME>

# Check application health
argocd app get <APP_NAME> --refresh
```

### System Diagnostics
```bash
# Check ArgoCD component status
argocd admin app status

# View controller logs
argocd admin controller logs

# View repo server logs
argocd admin repo-server logs

# View application controller metrics
argocd admin controller metrics
```

### Connection Testing
```bash
# Test Redis connectivity
argocd admin redis ping

# Test repository connection
argocd repo get <REPO_URL>
```

### Resource Management
```bash
# View resource tree
argocd app resource-tree <APP_NAME>

# View specific resource
argocd app resource <APP_NAME> <GROUP:KIND:NAME>
```