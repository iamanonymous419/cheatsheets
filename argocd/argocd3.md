# ArgoCD CLI Cheatsheet

## Table of Contents

- [ArgoCD CLI Cheatsheet](#argocd-cli-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [Installation](#installation)
    - [Install ArgoCD CLI](#install-argocd-cli)
    - [Check Version and Build Information](#check-version-and-build-information)
    - [Enable Command Completion](#enable-command-completion)
  - [Login and Configuration](#login-and-configuration)
    - [Login to ArgoCD Server](#login-to-argocd-server)
    - [Managing Sessions](#managing-sessions)
    - [Configuration Files](#configuration-files)
  - [Applications](#applications)
    - [App Creation](#app-creation)
    - [App Management](#app-management)
    - [App Sync Options](#app-sync-options)
    - [App Configuration](#app-configuration)
    - [App Resources](#app-resources)
  - [Projects](#projects)
    - [Project Creation and Management](#project-creation-and-management)
    - [Project Policy Management](#project-policy-management)
    - [Project Role Management](#project-role-management)
  - [Repository Management](#repository-management)
    - [Repository Types](#repository-types)
    - [Repository Credentials](#repository-credentials)
  - [Clusters](#clusters)
    - [Cluster Authentication](#cluster-authentication)
    - [Namespaces](#namespaces)
  - [Context Management](#context-management)
  - [RBAC and Account Management](#rbac-and-account-management)
    - [User Management](#user-management)
    - [Role Management](#role-management)
    - [Policy Management](#policy-management)
  - [Certificate Management](#certificate-management)
  - [GPG Key Management](#gpg-key-management)
  - [Server Management](#server-management)
    - [Server Administration](#server-administration)
    - [Notifications](#notifications)
    - [Resource Hooks](#resource-hooks)
  - [ApplicationSets](#applicationsets)
  - [Troubleshooting Commands](#troubleshooting-commands)
    - [Diagnostics](#diagnostics)
    - [Logs and Events](#logs-and-events)
    - [Network Testing](#network-testing)
  - [Help and Advanced Topics](#help-and-advanced-topics)
    - [Getting Help](#getting-help)
    - [Environment Variables](#environment-variables)
    - [Performance Tuning](#performance-tuning)
    - [Output Formatting](#output-formatting)
    - [Scripting with ArgoCD CLI](#scripting-with-argocd-cli)
    - [Advanced Authentication](#advanced-authentication)
    - [Integration with Kubernetes](#integration-with-kubernetes)
    - [Resource Health Assessment](#resource-health-assessment)
    - [Custom Diffing and Resource Management](#custom-diffing-and-resource-management)
    - [Secret Management](#secret-management)
    - [Webhooks and CI/CD Integration](#webhooks-and-cicd-integration)
    - [Custom Resource Definitions (CRDs)](#custom-resource-definitions-crds)
    - [High Availability (HA) Mode](#high-availability-ha-mode)
    - [Backup and Restore](#backup-and-restore)
  - [GitOps and Configuration Management](#gitops-and-configuration-management)
    - [ArgoCD Config Management Plugins](#argocd-config-management-plugins)
    - [Kustomize Integration](#kustomize-integration)
    - [Helm Integration](#helm-integration)
    - [JsonNet Integration](#jsonnet-integration)
  - [Sync Strategies and Wave Management](#sync-strategies-and-wave-management)
    - [Sync Strategies](#sync-strategies)
    - [Wave and Sync Hooks](#wave-and-sync-hooks)
  - [Resource Management](#resource-management)
    - [Resource Customization](#resource-customization)
    - [Resource Exclusions and Inclusions](#resource-exclusions-and-inclusions)
  - [Monitoring and Debugging](#monitoring-and-debugging)
    - [Prometheus Metrics](#prometheus-metrics)
    - [Advanced Logging](#advanced-logging)
    - [Performance Analysis](#performance-analysis)
  - [Security Best Practices](#security-best-practices)
    - [Role-Based Access Control](#role-based-access-control)
    - [Certificate Management](#certificate-management-1)
    - [Sensitive Data Protection](#sensitive-data-protection)

## Installation

### Install ArgoCD CLI

```bash
# Mac (using Homebrew)
brew install argocd

# Linux (direct download)
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64

# Linux (via apt for Ubuntu/Debian)
curl -sSL -o setup-argocd.sh https://github.com/argoproj/argo-cd/releases/latest/download/install.sh
sudo bash setup-argocd.sh

# Windows (using Chocolatey)
choco install argocd-cli

# Windows (using Scoop)
scoop install argocd

# Install specific version
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/download/v2.8.0/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
```

### Check Version and Build Information

```bash
# Check version
argocd version

# Check version and build details
argocd version --client
argocd version --short

# Check version against server
argocd version --server
```

### Enable Command Completion

```bash
# Bash
source <(argocd completion bash)
echo "source <(argocd completion bash)" >> ~/.bashrc

# Zsh
source <(argocd completion zsh)
echo "source <(argocd completion zsh)" >> ~/.zshrc

# Fish
argocd completion fish > ~/.config/fish/completions/argocd.fish
```

## Login and Configuration

### Login to ArgoCD Server

```bash
# Basic username/password login
argocd login <ARGOCD_SERVER>
argocd login <ARGOCD_SERVER> --username <USERNAME> --password <PASSWORD>

# Single Sign-On login
argocd login <ARGOCD_SERVER> --sso
argocd login <ARGOCD_SERVER> --sso-port <PORT>

# Token-based login
argocd login <ARGOCD_SERVER> --auth-token <TOKEN>

# Skip TLS verification (insecure)
argocd login <ARGOCD_SERVER> --insecure

# Specify custom certificate
argocd login <ARGOCD_SERVER> --certificate-file <CERT_FILE>

# Login with kubeconfig context
argocd login <ARGOCD_SERVER> --kube-context <CONTEXT_NAME>

# Set custom HTTP headers
argocd login <ARGOCD_SERVER> --header <KEY>:<VALUE>

# Login using grpc-web
argocd login <ARGOCD_SERVER> --grpc-web
```

### Managing Sessions

```bash
# Logout from a server
argocd logout <ARGOCD_SERVER>

# Check current session information
argocd session info
```

### Configuration Files

```bash
# View current configuration
argocd config

# Set configuration values
argocd config set server <SERVER_URL>
argocd config set server.core <SERVER_CORE_URL>
argocd config set timeout <TIMEOUT_SECONDS>

# Unset configuration values
argocd config unset server.core
```

## Applications

### App Creation

```bash
# Create application from directory
argocd app create <APP_NAME> \
  --repo <GIT_REPO> \
  --path <PATH_IN_REPO> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE>

# Create application from Helm chart in Git
argocd app create <APP_NAME> \
  --repo <GIT_REPO> \
  --path <PATH_TO_CHART> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE> \
  --helm-set <KEY1>=<VALUE1> \
  --helm-set <KEY2>=<VALUE2>

# Create application from public Helm chart repository
argocd app create <APP_NAME> \
  --repo <HELM_REPO_URL> \
  --helm-chart <CHART_NAME> \
  --revision <CHART_VERSION> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE>

# Create application with Kustomize
argocd app create <APP_NAME> \
  --repo <GIT_REPO> \
  --path <PATH_IN_REPO> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE> \
  --kustomize-image <IMAGE_NAME>:<TAG>

# Create application from JsonNet
argocd app create <APP_NAME> \
  --repo <GIT_REPO> \
  --path <PATH_IN_REPO> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE> \
  --jsonnet-ext-var <VAR_NAME>=<VAR_VALUE>

# Create from a YAML or JSON file
argocd app create -f <PATH_TO_FILE>
argocd app create -f - < app.yaml

# Create application with specific revision
argocd app create <APP_NAME> \
  --repo <GIT_REPO> \
  --path <PATH_IN_REPO> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE> \
  --revision <COMMIT_SHA_OR_BRANCH_OR_TAG>

# Create application in a project
argocd app create <APP_NAME> \
  --repo <GIT_REPO> \
  --path <PATH_IN_REPO> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE> \
  --project <PROJECT_NAME>

# Create application with sync policy
argocd app create <APP_NAME> \
  --repo <GIT_REPO> \
  --path <PATH_IN_REPO> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE> \
  --sync-policy automated \
  --auto-prune \
  --self-heal

# Create application with sync options
argocd app create <APP_NAME> \
  --repo <GIT_REPO> \
  --path <PATH_IN_REPO> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE> \
  --sync-option CreateNamespace=true \
  --sync-option Replace=true

# Create application with resource tracking method
argocd app create <APP_NAME> \
  --repo <GIT_REPO> \
  --path <PATH_IN_REPO> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE> \
  --tracking-method annotation
```

### App Management

```bash
# List applications
argocd app list
argocd app list -o name
argocd app list -o wide
argocd app list -o yaml
argocd app list -o json
argocd app list -l <LABEL_SELECTOR>
argocd app list -p <PROJECT_NAME>

# Get application details
argocd app get <APP_NAME>
argocd app get <APP_NAME> -o yaml
argocd app get <APP_NAME> -o json
argocd app get <APP_NAME> --refresh

# Delete application
argocd app delete <APP_NAME>
argocd app delete <APP_NAME> --cascade  # Cascade delete resources
argocd app delete <APP_NAME> --cascade=false  # Keep resources
argocd app delete <APP_NAME> -y  # No confirmation prompt

# Manage multiple applications
argocd app list -l <LABEL_SELECTOR> | cut -f1 -d ' ' | xargs argocd app delete
```

### App Sync Options

```bash
# Sync application
argocd app sync <APP_NAME>

# Sync with advanced options
argocd app sync <APP_NAME> --force  # Force sync (disregards differences)
argocd app sync <APP_NAME> --dry-run  # Show what would happen
argocd app sync <APP_NAME> --prune  # Prune resources
argocd app sync <APP_NAME> --async  # Don't wait for sync to complete
argocd app sync <APP_NAME> --retry-limit <NUM>  # Retry failed sync up to N times
argocd app sync <APP_NAME> --retry-backoff-duration <DURATION>  # Retry backoff time
argocd app sync <APP_NAME> --timeout <SECONDS>  # Set timeout
argocd app sync <APP_NAME> --strategy <apply|hook>  # Sync strategy

# Selective sync
argocd app sync <APP_NAME> --resource <GROUP:KIND:NAME>  # Sync specific resource
argocd app sync <APP_NAME> --label <KEY>=<VALUE>  # Sync resources with label
argocd app sync <APP_NAME> --local <PATH>  # Use local manifests for sync
argocd app sync <APP_NAME> --local=out-of-sync-only  # Sync only out-of-sync resources

# Sync with replace instead of apply (recreate resources)
argocd app sync <APP_NAME> --replace

# Sync with specific revision
argocd app sync <APP_NAME> --revision <COMMIT_SHA_OR_BRANCH>
```

### App Configuration

```bash
# Set application parameters
argocd app set <APP_NAME> --repo <NEW_REPO>
argocd app set <APP_NAME> --path <NEW_PATH>
argocd app set <APP_NAME> --dest-namespace <NEW_NAMESPACE>
argocd app set <APP_NAME> --dest-server <NEW_SERVER>
argocd app set <APP_NAME> --revision <NEW_REVISION>
argocd app set <APP_NAME> --project <NEW_PROJECT>

# Set Helm specific parameters
argocd app set <APP_NAME> --helm-set <KEY>=<VALUE>
argocd app set <APP_NAME> --helm-set-string <KEY>=<VALUE>
argocd app set <APP_NAME> --helm-set-file <KEY>=<FILE_PATH>
argocd app set <APP_NAME> --helm-values <VALUES_FILE_PATH>

# Set Kustomize specific parameters
argocd app set <APP_NAME> --kustomize-image <IMAGE>=<TAG>
argocd app set <APP_NAME> --kustomize-patch <PATCH_FILE_PATH>
argocd app set <APP_NAME> --kustomize-common-label <KEY>=<VALUE>

# Set JsonNet specific parameters
argocd app set <APP_NAME> --jsonnet-ext-var <VAR>=<VALUE>
argocd app set <APP_NAME> --jsonnet-tla <VAR>=<VALUE>

# Set sync options
argocd app set <APP_NAME> --sync-policy automated  # Enable auto-sync
argocd app set <APP_NAME> --sync-policy none  # Disable auto-sync
argocd app set <APP_NAME> --sync-option <OPTION>=<VALUE>  # Add sync option
argocd app set <APP_NAME> --auto-prune  # Auto prune resources
argocd app set <APP_NAME> --no-prune  # Disable auto prune
argocd app set <APP_NAME> --self-heal  # Enable self healing
argocd app set <APP_NAME> --no-self-heal  # Disable self healing

# Unset parameters
argocd app unset <APP_NAME> --parameter <NAME>
argocd app unset <APP_NAME> --helm-set <NAME>

# Patch application
argocd app patch <APP_NAME> --patch <PATCH> --type merge
argocd app patch <APP_NAME> --patch <PATCH> --type json

# Patch resource in an application
argocd app patch-resource <APP_NAME> \
  --group <GROUP> \
  --kind <KIND> \
  --resource-name <RESOURCE_NAME> \
  --namespace <NAMESPACE> \
  --patch <PATCH> \
  --patch-type <json|merge|strategic>
```

### App Resources

```bash
# Application history
argocd app history <APP_NAME>
argocd app history <APP_NAME> -o wide

# Rollback to a specific version
argocd app rollback <APP_NAME> <ID>
argocd app rollback <APP_NAME> <ID> --prune

# View application manifests
argocd app manifests <APP_NAME>
argocd app manifests <APP_NAME> --source <SOURCE> --revision <REVISION>
argocd app manifests <APP_NAME> | kubectl apply -f -

# View application resources
argocd app resources <APP_NAME>
argocd app resources <APP_NAME> -o wide
argocd app resources <APP_NAME> -o tree

# View resource tree
argocd app resource-tree <APP_NAME>

# View specific resource
argocd app resource <APP_NAME> <GROUP:KIND:NAME>
argocd app resource <APP_NAME> <GROUP:KIND:NAME> -o yaml
argocd app resource <APP_NAME> <GROUP:KIND:NAME> --action <ACTION_NAME>

# Application diff
argocd app diff <APP_NAME>
argocd app diff <APP_NAME> --local <PATH>
argocd app diff <APP_NAME> --revision <REVISION>

# Application wait operations
argocd app wait <APP_NAME>
argocd app wait <APP_NAME> --health  # Wait for app to be healthy
argocd app wait <APP_NAME> --sync  # Wait for app to be synced
argocd app wait <APP_NAME> --operation  # Wait for pending operations
argocd app wait <APP_NAME> --suspended=false  # Wait until not suspended
argocd app wait <APP_NAME> --timeout <SECONDS>  # Set timeout

# Terminate ongoing operations
argocd app terminate-op <APP_NAME>

# Actions on applications and resources
argocd app actions <APP_NAME> list
argocd app actions <APP_NAME> run <ACTION_NAME>
argocd app actions <APP_NAME> run <ACTION_NAME> -p <PARAM_NAME>=<PARAM_VALUE>
```

## Projects

### Project Creation and Management

```bash
# List projects
argocd proj list
argocd proj list -o wide
argocd proj list -o yaml
argocd proj list -o json

# Create project
argocd proj create <PROJECT_NAME>
argocd proj create <PROJECT_NAME> --description <DESCRIPTION>
argocd proj create -f <PROJECT_FILE.yaml>

# Get project details
argocd proj get <PROJECT_NAME>
argocd proj get <PROJECT_NAME> -o yaml
argocd proj get <PROJECT_NAME> -o json

# Delete project
argocd proj delete <PROJECT_NAME>
```

### Project Policy Management

```bash
# Add allowed source repositories
argocd proj add-source <PROJECT_NAME> <REPO_URL>
argocd proj add-source <PROJECT_NAME> "*"  # Allow all repositories

# Remove source repositories
argocd proj remove-source <PROJECT_NAME> <REPO_URL>

# Add destination clusters/namespaces
argocd proj add-destination <PROJECT_NAME> <CLUSTER_URL> <NAMESPACE>
argocd proj add-destination <PROJECT_NAME> "*" "*"  # Allow all clusters and namespaces

# Remove destination
argocd proj remove-destination <PROJECT_NAME> <CLUSTER_URL> <NAMESPACE>

# Allow cluster-scoped resources
argocd proj allow-cluster-resource <PROJECT_NAME> <GROUP> <KIND> <ACTION>
argocd proj allow-cluster-resource <PROJECT_NAME> "*" "*" "*"  # Allow all resources

# Deny cluster-scoped resources
argocd proj deny-cluster-resource <PROJECT_NAME> <GROUP> <KIND> <ACTION>

# Add namespace resource whitelist
argocd proj add-namespace-resource-whitelist <PROJECT_NAME> <GROUP> <KIND>

# Remove namespace resource whitelist
argocd proj remove-namespace-resource-whitelist <PROJECT_NAME> <GROUP> <KIND>

# Add resource blacklist
argocd proj add-resource-blacklist <PROJECT_NAME> <GROUP> <KIND>

# Remove resource blacklist
argocd proj remove-resource-blacklist <PROJECT_NAME> <GROUP> <KIND>

# Set signature verification requirements
argocd proj set <PROJECT_NAME> --signature-keys <KEY_ID>
```

### Project Role Management

```bash
# Create project role
argocd proj role create <PROJECT_NAME> <ROLE_NAME>
argocd proj role create <PROJECT_NAME> <ROLE_NAME> --description <DESCRIPTION>

# Delete project role
argocd proj role delete <PROJECT_NAME> <ROLE_NAME>

# List project roles
argocd proj role list <PROJECT_NAME>

# Get project role details
argocd proj role get <PROJECT_NAME> <ROLE_NAME>

# Add policy to role
argocd proj role add-policy <PROJECT_NAME> <ROLE_NAME> <ACTION> <OBJECT> <PERMISSION>
argocd proj role add-policy <PROJECT_NAME> <ROLE_NAME> "get" "applications" "allow"
argocd proj role add-policy <PROJECT_NAME> <ROLE_NAME> "*" "*" "allow"  # Admin access

# Remove policy from role
argocd proj role remove-policy <PROJECT_NAME> <ROLE_NAME> <ACTION> <OBJECT> <PERMISSION>

# Add user/group to role
argocd proj role add-group <PROJECT_NAME> <ROLE_NAME> <GROUP>
argocd proj role add-user <PROJECT_NAME> <ROLE_NAME> <USER>

# Remove user/group from role
argocd proj role remove-group <PROJECT_NAME> <ROLE_NAME> <GROUP>
argocd proj role remove-user <PROJECT_NAME> <ROLE_NAME> <USER>

# Create JWT token for a role
argocd proj role create-token <PROJECT_NAME> <ROLE_NAME>
argocd proj role create-token <PROJECT_NAME> <ROLE_NAME> --ttl <DURATION>  # Set token TTL
argocd proj role create-token <PROJECT_NAME> <ROLE_NAME> --id <TOKEN_ID>  # Set token ID

# Delete JWT token
argocd proj role delete-token <PROJECT_NAME> <ROLE_NAME> <TOKEN_ID>

# List JWT tokens
argocd proj role list-tokens <PROJECT_NAME> <ROLE_NAME>
```

## Repository Management

### Repository Types

```bash
# List repositories
argocd repo list
argocd repo list -o wide
argocd repo list -o yaml
argocd repo list -o json

# Add Git repository
argocd repo add <REPO_URL>
argocd repo add <REPO_URL> --name <DISPLAY_NAME>
argocd repo add <REPO_URL> --project <PROJECT_NAME>

# Add Helm repository
argocd repo add <REPO_URL> --type helm
argocd repo add <REPO_URL> --type helm --name <REPO_NAME>
argocd repo add <REPO_URL> --type helm --pass-credentials

# Add OCI based Helm repository
argocd repo add <REPO_URL> --type helm --name <REPO_NAME> --enable-oci

# Add Git repository with specific path
argocd repo add <REPO_URL> --path <PATH>

# Get repository details
argocd repo get <REPO_URL>
argocd repo get <REPO_URL> -o yaml

# Remove repository
argocd repo rm <REPO_URL>
```

### Repository Credentials

```bash
# Add Git repository with HTTP/HTTPS credentials
argocd repo add <REPO_URL> --username <USERNAME> --password <PASSWORD>

# Add Git repository with SSH key
argocd repo add <REPO_URL> --ssh-private-key-path <PATH_TO_KEY>
argocd repo add <REPO_URL> --insecure-ignore-host-key  # Skip host key verification
argocd repo add <REPO_URL> --insecure-skip-server-verification  # Skip TLS verification

# Add Git repository with TLS client certificates
argocd repo add <REPO_URL> --tls-client-cert-path <PATH_TO_CERT> --tls-client-cert-key-path <PATH_TO_KEY>

# Add Helm repository with credentials
argocd repo add <REPO_URL> --type helm --username <USERNAME> --password <PASSWORD>
argocd repo add <REPO_URL> --type helm --tls-cert-path <PATH_TO_CERT> --tls-cert-key-path <PATH_TO_KEY>

# Add OCI repository with credentials
argocd repo add <REPO_URL> --type helm --enable-oci --username <USERNAME> --password <PASSWORD>
```

## Clusters

### Cluster Authentication

```bash
# List clusters
argocd cluster list
argocd cluster list -o name
argocd cluster list -o wide
argocd cluster list -o yaml

# Add cluster from kubeconfig
argocd cluster add <CONTEXT_NAME>

# Add in-cluster config (when ArgoCD runs in the same cluster)
argocd cluster add <CONTEXT_NAME> --in-cluster

# Add cluster with specific bearer token
argocd cluster add <CONTEXT_NAME> --bearer-token <TOKEN>

# Add cluster with exec authentication plugin 
argocd cluster add <CONTEXT_NAME> --exec-command <COMMAND> --exec-args <ARGS>

# Add cluster with service account
argocd cluster add <CONTEXT_NAME> --service-account <SA_NAME> --namespace <NAMESPACE>

# Add cluster with specific permissions
argocd cluster add <CONTEXT_NAME> --cluster-resources  # Allow cluster-level resources
argocd cluster add <CONTEXT_NAME> --system-namespace=<NAMESPACE>  # For system-level components

# Get cluster details
argocd cluster get <CLUSTER_URL>
argocd cluster get <CLUSTER_URL> -o yaml

# Remove cluster
argocd cluster rm <CLUSTER_URL>
```

### Namespaces

```bash
# List namespaces in a cluster
argocd cluster namespaces <CLUSTER_URL>

# Add resource exclusions
argocd cluster set <CLUSTER_URL> --resource-exclusions <GROUP/KIND>
```

## Context Management

```bash
# List available contexts
argocd context
argocd context list

# Display current context information
argocd context current

# Switch to another context
argocd context <NUMBER>
argocd context <SERVER_NAME>

# Custom context configuration
argocd context <SERVER_NAME> --name <DISPLAY_NAME>
argocd context <SERVER_NAME> --user <USERNAME>
argocd context <SERVER_NAME> --port <PORT>

# Delete context
argocd context delete <SERVER_NAME>
```

## RBAC and Account Management

### User Management

```bash
# List users
argocd account list
argocd account list --output wide
argocd account list -o yaml

# Get user details
argocd account get <USERNAME>
argocd account get --current

# Update password
argocd account update-password
argocd account update-password --current-password <CURRENT_PW> --new-password <NEW_PW>

# Update another user's password (requires admin)
argocd account update-password --account <USERNAME> --new-password <NEW_PW>

# Generate API token
argocd account generate-token
argocd account generate-token --account <USERNAME>
argocd account generate-token --account <USERNAME> --ttl <DURATION>
argocd account generate-token --account <USERNAME> --id <TOKEN_ID>
argocd account generate-token --account <USERNAME> --scopes <SCOPE1,SCOPE2>

# Delete API token
argocd account delete-token <USERNAME> <TOKEN_ID>

# List API tokens for user
argocd account list-tokens <USERNAME>
```

### Role Management

```bash
# List roles
argocd admin role list
argocd admin role list -o wide

# Get role details
argocd admin role get <ROLE_NAME>
argocd admin role get <ROLE_NAME> -o yaml

# Create role
argocd admin role create <ROLE_NAME>
argocd admin role create <ROLE_NAME> -d <DESCRIPTION>

# Delete role
argocd admin role delete <ROLE_NAME>

# Add policy to role
argocd admin role add-policy <ROLE_NAME> -a <ACTION> -o <OBJECT> -p <PERMISSION>
argocd admin role add-policy <ROLE_NAME> -a "*" -o "*" -p allow  # Admin role

# Remove policy from role
argocd admin role remove-policy <ROLE_NAME> -a <ACTION> -o <OBJECT> -p <PERMISSION>
```

### Policy Management

```bash
# Get current RBAC policy
argocd admin settings rbac

# Update RBAC policy
argocd admin settings rbac --policy.csv <POLICY_FILE>
argocd admin settings rbac --policy.default <ROLE>
```

## Certificate Management

```bash
# List certificates
argocd cert list
argocd cert list -o yaml

# Add TLS certificate
argocd cert add-tls <HOSTNAME> --from <PATH_TO_CERT>
argocd cert add-tls <HOSTNAME> --cert <PATH_TO_CERT> --key <PATH_TO_KEY>

# Add SSH known hosts
argocd cert add-ssh <HOSTNAME>:<PORT>
argocd cert add-ssh <HOSTNAME>:<PORT> --batch

# Remove certificate
argocd cert rm <HOSTNAME>
argocd cert rm <HOSTNAME> --type ssh
```

## GPG Key Management

```bash
# List GPG keys
argocd gpg list
argocd gpg list -o yaml

# Add GPG key
argocd gpg add --from <KEY_PATH>
argocd gpg add --from <KEY_PATH> --name <KEY_NAME>

# Delete GPG key
argocd gpg rm <KEY_ID>

# Import keys from public keyserver
argocd gpg import <KEY_ID>
argocd gpg import <KEY_ID> --keyserver <KEYSERVER_URL>
```

## Server Management

### Server Administration

```bash
# Apply settings
argocd admin settings set <KEY> <VALUE>
argocd admin settings unset <KEY>

# Export cluster configuration
argocd admin export > backup.yaml
argocd admin export --namespace <NAMESPACE> > backup.yaml

# Import cluster configuration
argocd admin import - < backup.yaml
argocd admin import --prune backup.yaml  # Delete resources not in backup

# Cluster maintenance
argocd admin cluster kubeconfig <CONTEXT> > kubeconfig.yaml

# Check server version
argocd admin version
argocd admin version --client
argocd admin version --short

# Initiate server upgrade
argocd admin upgrade
```

### Notifications

```bash
# List notification templates
argocd admin notifications template list
argocd admin notifications template get <TEMPLATE_NAME>

# Create/update notification template
argocd admin notifications template set <TEMPLATE_NAME> --path <PATH>

# Delete notification template
argocd admin notifications template delete <TEMPLATE_NAME>

# List notification triggers
argocd admin notifications trigger list
argocd admin notifications trigger get <TRIGGER_NAME>

# Create/update notification trigger
argocd admin notifications trigger set <TRIGGER_NAME> --path <PATH>

# Delete notification trigger
argocd admin notifications trigger delete <TRIGGER_NAME>

# List notification services
argocd admin notifications service list
argocd admin notifications service get <SERVICE_NAME>

# Create/update notification service
argocd admin notifications service set <SERVICE_NAME> --type <TYPE> --path <PATH>

# Delete notification service
argocd admin notifications service delete <SERVICE_NAME>

# Subscribe to notifications
argocd admin notifications subscription set \
  app=<APP_SELECTOR> \
  --trigger <TRIGGER_NAME> \
  --recipient <RECIPIENT>

# List notification subscriptions
argocd admin notifications subscription list
```

### Resource Hooks

```bash
# List sync hooks
argocd admin hook list
argocd admin hook get <HOOK_NAME>
```

## ApplicationSets

```bash
# List ApplicationSets
argocd appset list
argocd appset list -o wide
argocd appset list -o yaml

# Create ApplicationSet
argocd appset create -f <APPSET_FILE.yaml>

# Get ApplicationSet details
argocd appset get <APPSET_NAME>
argocd appset get <APPSET_NAME> -o yaml

# Delete ApplicationSet
argocd appset delete <APPSET_NAME>

# ApplicationSet operations
argocd appset generate-spec <GENERATOR_TYPE> > appset.yaml
```

## Troubleshooting Commands

### Diagnostics

```bash
# ArgoCD component diagnostics
argocd admin app info <APP_NAME>
argocd admin app stats

# Check controller status
argocd admin app status

# Show sync status
argocd admin app diff <APP_NAME>

# Compare resources with manifests
argocd admin app resources <APP_NAME>

# Check controller processing queue
argocd admin app list-processed
argocd admin app list-unprocessed
```

### Logs and Events

```bash
# View application logs
argocd app logs <APP_NAME>
argocd app logs <APP_NAME> -c <CONTAINER_NAME>
arcocd app logs <APP_NAME> --follow
argocd app logs <APP_NAME> --tail <NUM_LINES>
argocd app logs <APP_NAME> --since <TIME>
argocd app logs <APP_NAME> --group <true|false>

# View application events
argocd app events <APP_NAME>

# View controller logs
argocd admin controller logs
argocd admin controller logs --follow

# View repo server logs
argocd admin repo-server logs
argocd admin repo-server logs --follow

# View API server logs
argocd admin server logs
argocd admin server logs --follow

# View component metrics
argocd admin controller metrics
argocd admin repo-server metrics
argocd admin server metrics
```

### Network Testing

```bash
# Test Redis connectivity
argocd admin redis ping
argocd admin redis info

# Test repository access
argocd repo get <REPO_URL>
argocd repo test <REPO_URL>
argocd repo test <REPO_URL> --username <USERNAME> --password <PASSWORD>

# Test cluster connectivity
argocd cluster get <CLUSTER_URL>
```

## Help and Advanced Topics

### Getting Help

```bash
# General help
argocd --help
argocd -h

# Command-specific help
argocd <COMMAND> --help
argocd app sync --help

# Show all available commands
argocd

# Show version
argocd version
```

### Environment Variables

```bash
# Set server URL
export ARGOCD_SERVER=<SERVER_URL>

# Set authentication token
export ARGOCD_AUTH_TOKEN=<AUTH_TOKEN>

# Skip TLS verification
export ARGOCD_INSECURE=true

# Set custom headers
export ARGOCD_HEADERS="HeaderName:value"

# Set custom grpc-web root path
export ARGOCD_GRPC_WEB_ROOT_PATH=/path

# Set connection timeout
export ARGOCD_TIMEOUT_SECONDS=300
```

### Performance Tuning

```bash
# Set number of concurrent tasks for syncing
argocd app sync <APP_NAME> --sync-concurrency <NUM>

# Set timeout for individual resources during sync
argocd app sync <APP_NAME> --resource-timeout <SECONDS>

# Increase command timeout
argocd --timeout <SECONDS> app sync <APP_NAME>
```

### Output Formatting

```bash
# Output formats
argocd <COMMAND> -o yaml
argocd <COMMAND> -o json
argocd <COMMAND> -o wide
argocd <COMMAND> -o name
argocd <COMMAND> -o table

# Filter output with jq
argocd app list -o json | jq '.items[] | select(.status.sync.status=="OutOfSync")'

# Use custom columns
argocd app list -o custom -c name -c status.sync.status -c status.health.status
```

### Scripting with ArgoCD CLI

```bash
# Wait for application sync and health check
argocd app wait <APP_NAME> --timeout 300 --health --sync --operation

# Get sync status and exit code based on status
argocd app get <APP_NAME> -o json | jq -r '.status.sync.status'
if [ $? -ne 0 ]; then echo "Failed"; fi

# Create multiple applications from templates
for env in dev stage prod; do
  sed "s/{{ENV}}/$env/g" app-template.yaml | argocd app create -f -
done

# Sync all applications in a project
argocd app list -p <PROJECT_NAME> -o name | xargs -I {} argocd app sync {}

# Delete all applications matching a pattern
argocd app list -o name | grep "pattern" | xargs argocd app delete
```

### Advanced Authentication

```bash
# Use OIDC device authorization flow
argocd login <SERVER> --auth-device

# Use single sign-on with custom browser
argocd login <SERVER> --sso --sso-browser <BROWSER_COMMAND>

# Generate and use API tokens
TOKEN=$(argocd account generate-token)
argocd --auth-token $TOKEN app list
```

### Integration with Kubernetes

```bash
# Use ArgoCD with kubectl plugins
kubectl argo cd app list
kubectl argo cd app sync <APP_NAME>

# Use ArgoCD with k9s plugin
k9s plugin install https://raw.githubusercontent.com/derailed/k9s-plugins/master/argocd.yml

# Watch application resources in Kubernetes
kubectl get applications -n argocd -w

# View ArgoCD resources in Kubernetes
kubectl get applications,appprojects -n argocd
```

### Resource Health Assessment

```bash
# Check application health
argocd app get <APP_NAME> --refresh
argocd app get <APP_NAME> -o json | jq '.status.health'

# Health check settings
argocd app set <APP_NAME> --health-check-timeout <SECONDS>
argocd app set <APP_NAME> --health-check <GROUP/KIND>=<HEALTH_CHECK_TYPE>

# Create custom health check
argocd admin settings resource-overrides set <GROUP/KIND> \
  --health-lua="health_status = {status = \"Progressing\", message = \"Custom message\"}"
```

### Custom Diffing and Resource Management

```bash
# Ignore differences in specific fields
argocd app set <APP_NAME> --ignore-difference-fields <JSONPATH>
argocd app set <APP_NAME> --ignore-difference-fields spec.replicas

# Set custom diff options
argocd app diff <APP_NAME> --normal
argocd app diff <APP_NAME> --local <PATH>

# Custom resource actions
argocd admin settings resource-overrides set <GROUP/KIND> \
  --actions-lua="actions = {
    {name = \"my-action\", title = \"My Custom Action\"}
  }"
```

### Secret Management

```bash
# Set secrets for repository
argocd repo add <REPO_URL> \
  --username <USERNAME> \
  --password <PASSWORD> \
  --tls-client-cert-path <PATH> \
  --tls-client-cert-key-path <PATH>

# Create repository credentials from Kubernetes secrets
kubectl create secret generic repo-creds \
  --from-literal=username=<USERNAME> \
  --from-literal=password=<PASSWORD> \
  -n argocd

# Use Helm secret values
argocd app set <APP_NAME> --helm-set-string 'secret=password' 
```

### Webhooks and CI/CD Integration

```bash
# Generate webhook URL
argocd admin settings get url

# Create GitHub webhook secret
WEBHOOK_SECRET=$(openssl rand -hex 16)
argocd admin settings webhook github --secret $WEBHOOK_SECRET

# Test webhook
curl -X POST https://<ARGOCD_SERVER>/api/webhook \
  -H "Content-Type: application/json" \
  -d '{"repository": {"clone_url": "<REPO_URL>"}, "ref": "refs/heads/main"}'
```

### Custom Resource Definitions (CRDs)

```bash
# Export application as CRD
argocd app get <APP_NAME> -o yaml > application.yaml

# Apply application CRD
kubectl apply -f application.yaml

# Export project as CRD
argocd proj get <PROJECT_NAME> -o yaml > appproject.yaml

# Apply project CRD
kubectl apply -f appproject.yaml
```

### High Availability (HA) Mode

```bash
# Check HA status
argocd admin cluster info

# Enable HA mode
argocd admin settings set controller.sharding.enabled true
argocd admin settings set controller.sharding.replicas <NUM_REPLICAS>

# View HA metrics
argocd admin controller metrics | grep ha_
```

### Backup and Restore

```bash
# Backup entire ArgoCD configuration
argocd admin export > argocd-backup.yaml

# Backup only certain resources
argocd admin export --kind Application,AppProject > partial-backup.yaml

# Restore from backup
argocd admin import -f argocd-backup.yaml

# Restore with pruning (dangerous!)
argocd admin import -f argocd-backup.yaml --prune

# Backup to remote storage
argocd admin export | aws s3 cp - s3://bucket/argocd-backup.yaml
```

## GitOps and Configuration Management

### ArgoCD Config Management Plugins

```bash
# List installed config management plugins
argocd admin settings plugins list

# Install new plugin
argocd admin settings plugins add <PLUGIN_NAME> \
  --init-command <INIT_CMD> \
  --generate-command <GEN_CMD>

# Remove plugin
argocd admin settings plugins remove <PLUGIN_NAME>

# Get plugin settings
argocd admin settings plugins get <PLUGIN_NAME>
```

### Kustomize Integration

```bash
# Create application with Kustomize
argocd app create <APP_NAME> \
  --repo <REPO_URL> \
  --path <PATH> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE> \
  --kustomize-common-annotations <KEY>=<VALUE>

# Set Kustomize options
argocd app set <APP_NAME> --kustomize-image <IMAGE>=<TAG>
argocd app set <APP_NAME> --kustomize-common-label <KEY>=<VALUE>
argocd app set <APP_NAME> --kustomize-version <VERSION>
argocd app set <APP_NAME> --kustomize-common-annotation <KEY>=<VALUE>

# View Kustomize generated manifests
argocd app manifests <APP_NAME> --source kustomize
```

### Helm Integration

```bash
# Create application from Helm chart
argocd app create <APP_NAME> \
  --repo <REPO_URL> \
  --helm-chart <CHART_NAME> \
  --helm-chart-version <VERSION> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE>

# Set Helm values
argocd app set <APP_NAME> --helm-set <KEY>=<VALUE>
argocd app set <APP_NAME> --helm-set-file <KEY>=<FILE_PATH>
argocd app set <APP_NAME> --helm-set-string <KEY>=<VALUE>

# Use values files
argocd app set <APP_NAME> --values <VALUES_FILE>
argocd app set <APP_NAME> --values values-prod.yaml,values-common.yaml

# Override Helm parameters
argocd app set <APP_NAME> --helm-version <VERSION>
argocd app set <APP_NAME> --release-name <RELEASE_NAME>
```

### JsonNet Integration

```bash
# Create application with JsonNet
argocd app create <APP_NAME> \
  --repo <REPO_URL> \
  --path <PATH> \
  --dest-server <CLUSTER_URL> \
  --dest-namespace <NAMESPACE> \
  --jsonnet-ext-var-code <VAR>=<CODE>

# Set JsonNet options
argocd app set <APP_NAME> --jsonnet-tla-str <KEY>=<VALUE>
argocd app set <APP_NAME> --jsonnet-tla-code <KEY>=<CODE>
argocd app set <APP_NAME> --jsonnet-libs <PATH>
```

## Sync Strategies and Wave Management

### Sync Strategies

```bash
# Apply sync strategy
argocd app sync <APP_NAME> --strategy <apply|hook>

# Set resource pruning behavior
argocd app set <APP_NAME> --auto-prune  # Enable auto-pruning
argocd app set <APP_NAME> --no-prune    # Disable auto-pruning

# Set selective sync
argocd app sync <APP_NAME> --resource <GROUP:KIND:NAME>
argocd app sync <APP_NAME> --label <KEY>=<VALUE>

# Set sync retry options
argocd app set <APP_NAME> --retry-backoff-duration <DURATION>
argocd app set <APP_NAME> --retry-backoff-max-duration <DURATION>
argocd app set <APP_NAME> --retry-backoff-factor <FACTOR>
```

### Wave and Sync Hooks

```bash
# Sync with waves (resource priority)
argocd app sync <APP_NAME> --resource-version <VERSION>

# List hooks for an application
argocd app resource <APP_NAME> --kind=Hook

# View hook status
argocd app get <APP_NAME> -o json | jq '.status.operationState.syncResult.resources[] | select(.hookType != null)'

# Skip hooks during sync
argocd app sync <APP_NAME> --skip-hooks
```

## Resource Management

### Resource Customization

```bash
# Set resource tracking method
argocd app set <APP_NAME> --tracking-method <label|annotation|resourceName>

# Manage resource finalizers
argocd app set <APP_NAME> --sync-option Replace=true
argocd app set <APP_NAME> --sync-option SkipDryRunOnMissingResource=true

# Resource transformations
argocd admin settings resource-overrides set <GROUP/KIND> \
  --ignore-differences 'jsonPointers=["spec.replicas"]'
```

### Resource Exclusions and Inclusions

```bash
# Exclude resources from sync
argocd app set <APP_NAME> --sync-option Validate=false

# Create namespaces automatically
argocd app set <APP_NAME> --sync-option CreateNamespace=true

# Skip resource validation
argocd app set <APP_NAME> --sync-option Validate=false

# Force resource replace instead of apply
argocd app set <APP_NAME> --sync-option Replace=true
```

## Monitoring and Debugging

### Prometheus Metrics

```bash
# View application metrics
argocd admin app metrics <APP_NAME>

# View controller metrics
argocd admin controller metrics

# View repo server metrics
argocd admin repo-server metrics

# View API server metrics
argocd admin server metrics
```

### Advanced Logging

```bash
# Enable debug logging
argocd app get <APP_NAME> --loglevel debug

# Stream controller logs
argocd admin controller logs --container controller --level debug --follow

# Custom log formatting
argocd admin controller logs --format json
```

### Performance Analysis

```bash
# View application resource usage
argocd admin app resources <APP_NAME>

# Check API server performance
argocd admin server metrics | grep "request_"

# View application processing timing
argocd app sync <APP_NAME> --loglevel debug | grep "time="
```

## Security Best Practices

### Role-Based Access Control

```bash
# Configure RBAC for SSO users
argocd admin settings rbac --policy.default role:readonly
argocd admin settings rbac --scopes read:application

# Assign roles based on group membership
argocd proj role add-group <PROJECT_NAME> <ROLE_NAME> <GROUP_NAME>

# View RBAC permissions
argocd admin settings get server.rbac
```

### Certificate Management

```bash
# Rotate certificates
argocd admin certificate rotate

# Configure certificate expiration
argocd admin settings set server.tls.cert-expiration-warning <DAYS>

# View certificate information
argocd admin certificate info
```

### Sensitive Data Protection

```bash
# Configure repository secret encryption
argocd admin settings set repository.credentials.secretKey <KEY>

# Use external secret management
argocd app set <APP_NAME> --helm-set-file "creds=/path/to/secret.txt"

# Encrypt webhook payloads
argocd admin settings set webhook.github.secret <SECRET>
```