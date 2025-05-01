# ArgoCD CLI Cheatsheet

This expanded cheatsheet covers all important aspects of ArgoCD's CLI usage for managing applications, clusters, projects, repositories, users, settings, and more.

---

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
  - [Application History](#application-history)
  - [Application Deletion and Orphaned Resources](#application-deletion-and-orphaned-resources)
  - [Hooks and Lifecycle Management](#hooks-and-lifecycle-management)
  - [Custom Health Checks](#custom-health-checks)
  - [Resource Actions and Patching](#resource-actions-and-patching)
  - [RBAC and Access Control](#rbac-and-access-control)
  - [Miscellaneous](#miscellaneous)
  - [Help \& Version](#help--version)
  - [References](#references)

---

## Login & Context
```bash
argocd login <ARGOCD_SERVER> --username <USERNAME> --password <PASSWORD> --insecure
argocd context <ARGOCD_SERVER>
```

## Application Management
```bash
argocd app list
argocd app get <APP_NAME>
argocd app create <APP_NAME> \
  --repo <REPO_URL> \
  --path <APP_PATH> \
  --dest-server <DEST_SERVER> \
  --dest-namespace <NAMESPACE> \
  --revision <BRANCH>
argocd app set <APP_NAME> --repo <REPO_URL> --revision <BRANCH>
argocd app delete <APP_NAME> --cascade
argocd app rename <APP_NAME> <NEW_NAME>
```

## Sync & Rollback
```bash
argocd app sync <APP_NAME>
argocd app sync <APP_NAME> --prune
argocd app wait <APP_NAME> --sync
argocd app rollback <APP_NAME> <REVISION>
```

## Repository Management
```bash
argocd repo list
argocd repo add <REPO_URL> --username <USERNAME> --password <PASSWORD>
argocd repo rm <REPO_URL>
argocd repo update <REPO_URL>
```

## Cluster Management
```bash
argocd cluster list
argocd cluster add <CONTEXT_NAME>
argocd cluster rm <SERVER_NAME>
```

## Projects
```bash
argocd proj list
argocd proj create <PROJECT_NAME>
argocd proj get <PROJECT_NAME>
argocd proj delete <PROJECT_NAME>
argocd proj allow-cluster-resource <PROJECT_NAME> <GROUP> <KIND>
argocd proj allow-ns-resource <PROJECT_NAME> <GROUP> <KIND>
```

## User Management
```bash
argocd account get-user-info
argocd account list-token
argocd account generate-token
```

## Secrets & Config
```bash
argocd admin settings list
argocd context
argocd admin cm plugin add ...
kubectl get secrets -n argocd
```

## Monitoring & Status
```bash
argocd app get <APP_NAME> --watch
argocd app diff <APP_NAME>
argocd app logs <APP_NAME> --follow
```

## Exporting & Importing
```bash
argocd app export <APP_NAME> -o yaml
kubectl get configmap -n argocd -o yaml > config-backup.yaml
```

## Application History
```bash
argocd app history <APP_NAME>
argocd app rollback <APP_NAME> <REVISION>
```

## Application Deletion and Orphaned Resources
```bash
argocd app delete <APP_NAME> --cascade
argocd app delete <APP_NAME> --orphans
```

## Hooks and Lifecycle Management
Documentation: https://argo-cd.readthedocs.io/en/stable/user-guide/resource_hooks/
```yaml
# Define PreSync, Sync, PostSync hooks in manifests
```

## Custom Health Checks
Docs: https://argo-cd.readthedocs.io/en/stable/operator-manual/health/

## Resource Actions and Patching
```bash
argocd app patch-resource <APP_NAME> --kind <KIND> --resource-name <NAME> --patch <JSON_PATCH>
```

## RBAC and Access Control
```bash
# View RBAC settings
kubectl -n argocd get configmap argocd-rbac-cm -o yaml
```

## Miscellaneous
```bash
argocd version
argocd login --grpc-web
```

## Help & Version
```bash
argocd --help
argocd <COMMAND> --help
argocd version
```

## References
- [ArgoCD Docs](https://argo-cd.readthedocs.io/)
- [ArgoCD GitHub](https://github.com/argoproj/argo-cd)
- [CLI Reference](https://argo-cd.readthedocs.io/en/stable/cli_installation/)

