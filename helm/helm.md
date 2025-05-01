Here's a complete **Helm CLI Cheatsheet** in `README.md` format, covering all essential and advanced topics, including installation, chart creation, templating, values, repositories, upgrades, rollbacks, and more.

---

### `README.md` — **Helm CLI Cheatsheet**


# Helm CLI Cheatsheet

Helm is the package manager for Kubernetes. This cheatsheet covers commonly used Helm CLI commands.

---

## Table of Contents

- [Helm CLI Cheatsheet](#helm-cli-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [Installation](#installation)
  - [Helm Chart Structure](#helm-chart-structure)
  - [Helm Repositories](#helm-repositories)
  - [Chart Creation](#chart-creation)
  - [Install \& Upgrade Releases](#install--upgrade-releases)
  - [Uninstall Releases](#uninstall-releases)
  - [Values \& Configuration](#values--configuration)
  - [Templating \& Rendering](#templating--rendering)
  - [Release Management](#release-management)
  - [Debugging](#debugging)
  - [Packaging \& Sharing Charts](#packaging--sharing-charts)
  - [Plugins](#plugins)
  - [Useful Commands](#useful-commands)
  - [References](#references)

---

## Installation

```bash
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```

---

## Helm Chart Structure

```
mychart/
├── charts/              # Subcharts
├── templates/           # Kubernetes manifests (YAML)
├── Chart.yaml           # Chart metadata
├── values.yaml          # Default config values
└── .helmignore          # Files to ignore when packaging
```

---

## Helm Repositories

```bash
helm repo add <name> <url>         # Add a repo
helm repo update                   # Update all repos
helm search repo <keyword>         # Search charts in repos
helm repo list                     # List configured repos
helm repo remove <name>            # Remove a repo
```

Example:

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

---

## Chart Creation

```bash
helm create <chart-name>           # Scaffold a new chart
```

---

## Install & Upgrade Releases

```bash
helm install <release> <chart> [flags]           # Install new release
helm upgrade <release> <chart> [flags]           # Upgrade existing release
helm upgrade --install <release> <chart>         # Install if not exists
```

Examples:

```bash
helm install myapp ./mychart
helm upgrade myapp ./mychart --set image.tag=v2
```

---

## Uninstall Releases

```bash
helm uninstall <release>          # Uninstall a release
```

---

## Values & Configuration

```bash
helm show values <chart>                         # Show default values
helm get values <release>                        # Show configured values
helm get all <release>                           # All release data
helm install -f values.yaml <release> <chart>    # Use custom values
helm install --set key=value,... <release>       # Override inline
```

---

## Templating & Rendering

```bash
helm template <release> <chart>          # Render templates locally
helm lint <chart>                        # Validate chart syntax
```

---

## Release Management

```bash
helm list                                # List all releases
helm history <release>                   # Show release history
helm rollback <release> [revision]       # Rollback to revision
```

---

## Debugging

```bash
helm install <release> <chart> --debug --dry-run
```

---

## Packaging & Sharing Charts

```bash
helm package <chart-dir>                     # Package chart into .tgz
helm push <chart.tgz> <repo-name>            # Push to repo (plugin required)
```

---

## Plugins

```bash
helm plugin list                             # List installed plugins
helm plugin install <url>                    # Install a plugin
```

---

## Useful Commands

```bash
helm env                                     # Show Helm environment info
helm version                                 # Helm version
helm status <release>                        # Release status
helm uninstall <release>                     # Remove release
```

---

## References

- [Helm Docs](https://helm.sh/docs/)
- [Artifact Hub](https://artifacthub.io/)
```
