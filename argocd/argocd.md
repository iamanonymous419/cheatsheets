Sure! Here's a complete **ArgoCD CLI Cheatsheet** in a `README.md` format that covers the essential commands and topics:

---

# ArgoCD CLI Cheatsheet

This cheatsheet provides quick access to commonly used ArgoCD CLI commands for managing applications, clusters, repositories, and users.

## Table of Contents

- [ArgoCD CLI Cheatsheet](#argocd-cli-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [Login \& Context](#login--context)
  - [Application Management](#application-management)
  - [Sync \& Rollback](#sync--rollback)
  - [Repository Management](#repository-management)
  - [Cluster Management](#cluster-management)
  - [Projects](#projects)
  - [User Management](#user-management)
  - [Secrets \& Config](#secrets--config)
  - [Monitoring \& Status](#monitoring--status)
  - [Exporting \& Importing](#exporting--importing)
  - [Help \& Version](#help--version)
  - [References](#references)

---

## Login & Context

```bash
# Login to ArgoCD server
argocd login <ARGOCD_SERVER> --username <USERNAME> --password <PASSWORD> --insecure

# Set current context
argocd context <ARGOCD_SERVER>
```

---

## Application Management

```bash
# List applications
argocd app list

# Get details of an application
argocd app get <APP_NAME>

# Create a new application
argocd app create <APP_NAME> \
  --repo <REPO_URL> \
  --path <APP_PATH> \
  --dest-server <DEST_SERVER> \
  --dest-namespace <NAMESPACE> \
  --revision <BRANCH>

# Update application
argocd app set <APP_NAME> --repo <REPO_URL> --revision <BRANCH>

# Delete application
argocd app delete <APP_NAME> --cascade

# Rename application
argocd app set <APP_NAME> --name <NEW_APP_NAME>
```

---

## Sync & Rollback

```bash
# Sync application
argocd app sync <APP_NAME>

# Sync with pruning
argocd app sync <APP_NAME> --prune

# Rollback application to a previous revision
argocd app rollback <APP_NAME> <REVISION>

# Wait for sync to complete
argocd app wait <APP_NAME> --sync
```

---

## Repository Management

```bash
# List repositories
argocd repo list

# Add repository
argocd repo add <REPO_URL> \
  --username <USERNAME> --password <PASSWORD> \
  --type git

# Remove repository
argocd repo rm <REPO_URL>

# Update repo credentials
argocd repo update <REPO_URL>
```

---

## Cluster Management

```bash
# List clusters
argocd cluster list

# Add a new cluster
argocd cluster add <CONTEXT_NAME>

# Remove a cluster
argocd cluster rm <SERVER_NAME>
```

---

## Projects

```bash
# List projects
argocd proj list

# Create a new project
argocd proj create <PROJECT_NAME>

# Get project details
argocd proj get <PROJECT_NAME>

# Delete a project
argocd proj delete <PROJECT_NAME>
```

---

## User Management

```bash
# List user info
argocd account get-user-info

# List user tokens
argocd account list-token

# Create a new user token
argocd account generate-token
```

---

## Secrets & Config

```bash
# List configuration
argocd admin settings list

# View current context
argocd context

# Add or update config management plugin
argocd admin cm plugin add ...
```

---

## Monitoring & Status

```bash
# Get application status
argocd app get <APP_NAME>

# Watch application for live updates
argocd app get <APP_NAME> --watch

# Diff application
argocd app diff <APP_NAME>

# View application logs
argocd app logs <APP_NAME> --follow
```

---

## Exporting & Importing

```bash
# Export application manifest as YAML
argocd app export <APP_NAME> -o yaml

# Backup configuration
kubectl get configmap -n argocd -o yaml > config-backup.yaml
```

---

## Help & Version

```bash
# Display help
argocd --help
argocd <COMMAND> --help

# Display version
argocd version
```

---

## References

- [ArgoCD Official Docs](https://argo-cd.readthedocs.io/)
- [GitHub - ArgoCD](https://github.com/argoproj/argo-cd)

