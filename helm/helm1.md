# Helm CLI Cheatsheet

Helm is the package manager for Kubernetes. This cheatsheet expands on the essential and advanced Helm CLI operations with examples and best practices.

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
  - [Dependency Management](#dependency-management)
  - [Helm Test](#helm-test)
  - [Helm Hooks](#helm-hooks)
  - [Security](#security)
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
├── .helmignore          # Files to ignore when packaging
└── README.md            # Chart documentation
```

---

## Helm Repositories

```bash
helm repo add <name> <url>
helm repo update
helm search repo <keyword>
helm repo list
helm repo remove <name>
```

Example:
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
```

---

## Chart Creation

```bash
helm create <chart-name>
```
This scaffolds a complete Helm chart structure.

---

## Install & Upgrade Releases

```bash
helm install <release> <chart> [flags]
helm upgrade <release> <chart> [flags]
helm upgrade --install <release> <chart>
```

Examples:
```bash
helm install myapp ./mychart
helm upgrade myapp ./mychart --set image.tag=v2
```

---

## Uninstall Releases

```bash
helm uninstall <release>
```

---

## Values & Configuration

```bash
helm show values <chart>
helm get values <release>
helm get all <release>
helm install -f values.yaml <release> <chart>
helm install --set key=value,... <release>
```

Use `--set-string` for string values:
```bash
helm install myapp ./mychart --set-string env=production
```

---

## Templating & Rendering

```bash
helm template <release> <chart>
helm lint <chart>
```

Lint before installing:
```bash
helm lint ./mychart
```

---

## Release Management

```bash
helm list
helm list --all-namespaces
helm history <release>
helm rollback <release> [revision]
helm status <release>
```

---

## Debugging

```bash
helm install <release> <chart> --debug --dry-run
```
Helps in rendering templates without actually installing.

---

## Packaging & Sharing Charts

```bash
helm package <chart-dir>
helm push <chart.tgz> <repo-name>  # Plugin required
```

---

## Plugins

```bash
helm plugin list
helm plugin install <url>
```

Popular plugins:
- [diff](https://github.com/databus23/helm-diff)
- [push](https://github.com/chartmuseum/helm-push)

---

## Dependency Management

Define dependencies in `Chart.yaml`:
```yaml
dependencies:
  - name: redis
    version: 14.0.0
    repository: "https://charts.bitnami.com/bitnami"
```

Commands:
```bash
helm dependency update
helm dependency build
```

---

## Helm Test

Add test templates:
```yaml
# templates/tests/test-connection.yaml
apiVersion: v1
kind: Pod
metadata:
  name: "{{ include "mychart.fullname" . }}-test"
  annotations:
    "helm.sh/hook": test
spec:
  containers:
    - name: wget
      image: busybox
      command: ['wget']
      args: ['{{ template "mychart.fullname" . }}']
  restartPolicy: Never
```

Run tests:
```bash
helm test <release>
```

---

## Helm Hooks

Helm supports hooks like `pre-install`, `post-install`, `pre-upgrade`, etc.

Example annotation:
```yaml
annotations:
  "helm.sh/hook": pre-install
```

Hooks can be used for jobs like DB migrations, config validation, etc.

---

## Security

- Scan charts using [Trivy](https://github.com/aquasecurity/trivy):
  ```bash
  trivy config --helm ./mychart
  ```
- Avoid sensitive data in `values.yaml`
- Use sealed secrets or external secret managers

---

## Useful Commands

```bash
helm env
helm version
helm status <release>
helm uninstall <release>
helm get manifest <release>
```

---

## References

- [Helm Official Docs](https://helm.sh/docs/)
- [Artifact Hub](https://artifacthub.io/)
- [Helm GitHub](https://github.com/helm/helm)

