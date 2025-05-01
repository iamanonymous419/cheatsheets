# Helm CLI Cheatsheet

## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Configuration](#configuration)
- [Chart Management](#chart-management)
- [Repository Management](#repository-management)
- [Release Management](#release-management)
- [Templating](#templating)
- [Plugin Management](#plugin-management)
- [Environment Variables](#environment-variables)
- [Common Flags](#common-flags)
- [Tips and Tricks](#tips-and-tricks)

## Introduction

Helm is the package manager for Kubernetes. It helps you define, install, and upgrade even the most complex Kubernetes applications using "charts" - packages of pre-configured Kubernetes resources.

## Installation

### Binary Installation
```bash
# macOS (using Homebrew)
brew install helm

# Windows (using Chocolatey)
choco install kubernetes-helm

# Linux (using snap)
sudo snap install helm --classic

# Using script
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```

### Verify Installation
```bash
helm version
```

## Configuration

### Init Configuration
```bash
# Set namespace for commands
helm --namespace kube-system

# Set kubeconfig file
helm --kubeconfig=/path/to/kubeconfig

# Add bash/zsh completion
helm completion bash > /etc/bash_completion.d/helm
```

## Chart Management

### Create a New Chart
```bash
# Create a new chart with default structure
helm create mychart

# Create a starter chart from a template
helm create mychart --starter=mychart
```

### Package a Chart
```bash
# Package a chart directory into a chart archive
helm package ./mychart

# Package with specific version
helm package --version 1.2.3 ./mychart

# Package with app version
helm package --app-version 1.2.3 ./mychart

# Package and sign
helm package --sign --key 'mykey' --keyring ~/.gnupg/secring.gpg ./mychart
```

### Chart Validation
```bash
# Validate chart
helm lint ./mychart

# Validate chart with values
helm lint --values custom-values.yaml ./mychart

# Show chart info
helm show chart ./mychart
helm show all ./mychart
helm show values ./mychart
helm show readme ./mychart
```

### Chart Dependencies
```bash
# Update chart dependencies
helm dependency update ./mychart

# List chart dependencies
helm dependency list ./mychart

# Build chart dependencies
helm dependency build ./mychart
```

## Repository Management

### Repository Commands
```bash
# Add a chart repository
helm repo add bitnami https://charts.bitnami.com/bitnami

# Update repositories
helm repo update

# List repositories
helm repo list

# Remove a repository
helm repo remove bitnami

# Search repositories
helm search repo nginx

# Search for all versions
helm search repo nginx --versions
```

### OCI Registry Commands
```bash
# Log in to a registry
helm registry login registry.example.com

# Log out from a registry
helm registry logout registry.example.com

# Push chart to registry
helm push mychart-0.1.0.tgz oci://registry.example.com/charts
```

## Release Management

### Install Commands
```bash
# Install a chart
helm install my-release bitnami/nginx

# Install from a local path
helm install my-release ./mychart

# Install with custom values
helm install my-release bitnami/nginx --values=custom-values.yaml

# Install with values from command line
helm install my-release bitnami/nginx --set service.type=LoadBalancer

# Install with multiple value files
helm install my-release bitnami/nginx -f values1.yaml -f values2.yaml

# Install with string values
helm install my-release bitnami/nginx --set-string image.tag=latest

# Generate name automatically
helm install bitnami/nginx --generate-name

# Install a specific version
helm install my-release bitnami/nginx --version 9.3.0

# Perform a dry run
helm install my-release bitnami/nginx --dry-run

# Render templates locally
helm install my-release bitnami/nginx --debug --dry-run

# Wait for resources to be ready
helm install my-release bitnami/nginx --wait

# Install with timeout
helm install my-release bitnami/nginx --timeout 5m

# Install in specific namespace
helm install my-release bitnami/nginx --namespace my-namespace

# Install with dependency update
helm install my-release bitnami/nginx --dependency-update

# Create namespace if it doesn't exist
helm install my-release bitnami/nginx --create-namespace

# Install from an OCI registry
helm install my-release oci://registry.example.com/charts/nginx
```

### Upgrade Commands
```bash
# Upgrade a release
helm upgrade my-release bitnami/nginx

# Install if not exists, upgrade if exists
helm upgrade --install my-release bitnami/nginx

# Perform atomic upgrade (rollback on failure)
helm upgrade my-release bitnami/nginx --atomic

# Force resource updates through delete/recreate
helm upgrade my-release bitnami/nginx --force

# Clean up old release versions
helm upgrade my-release bitnami/nginx --cleanup-on-fail

# Reset values to chart's original values
helm upgrade my-release bitnami/nginx --reset-values

# Reuse the last release's values
helm upgrade my-release bitnami/nginx --reuse-values
```

### Rollback Commands
```bash
# Rollback to the previous release
helm rollback my-release 1

# Rollback and wait for completion
helm rollback my-release 2 --wait

# Rollback with timeout
helm rollback my-release 2 --timeout 5m

# Clean up on rollback failure
helm rollback my-release 2 --cleanup-on-fail
```

### Release Info Commands
```bash
# List all releases
helm list
helm ls

# List all releases in all namespaces
helm list --all-namespaces
helm ls -A

# List releases with a specific status
helm list --deployed
helm list --failed
helm list --pending
helm list --uninstalled
helm list --superseded

# Filter releases by regexp
helm list --filter 'web-*'

# Show release history
helm history my-release

# Get release details
helm get all my-release

# Get release values
helm get values my-release

# Get computed values
helm get values my-release --all

# Get release manifest (K8s resources)
helm get manifest my-release

# Get release notes
helm get notes my-release

# Get release hooks
helm get hooks my-release

# Show status of release
helm status my-release
```

### Uninstall Commands
```bash
# Uninstall a release
helm uninstall my-release

# Uninstall multiple releases
helm uninstall my-release1 my-release2

# Keep history and release name
helm uninstall my-release --keep-history

# Uninstall with dry run
helm uninstall my-release --dry-run
```

## Templating

### Template Commands
```bash
# Render chart templates locally
helm template ./mychart

# Render with release name
helm template my-release ./mychart

# Render with custom values
helm template my-release ./mychart --values=custom-values.yaml

# Render with specific values
helm template my-release ./mychart --set service.type=NodePort

# Render a specific template
helm template my-release ./mychart --show-only templates/deployment.yaml

# Output in YAML format
helm template my-release ./mychart --output-dir ./rendered

# Validate rendered templates against API server
helm template my-release ./mychart --validate
```

### Test Commands
```bash
# Run tests for a release
helm test my-release

# Run tests with logs
helm test my-release --logs

# Run specific tests
helm test my-release --filter 'test-connection'
```

## Plugin Management

### Plugin Commands
```bash
# List installed plugins
helm plugin list

# Update plugins
helm plugin update [plugin]

# Install a plugin
helm plugin install https://github.com/helm/helm-mapkubeapis

# Uninstall a plugin
helm plugin uninstall mapkubeapis
```

### Common Plugins
```bash
# Install helm-diff plugin
helm plugin install https://github.com/databus23/helm-diff

# Install helm-secrets plugin
helm plugin install https://github.com/jkroepke/helm-secrets

# Install helm-mapkubeapis plugin
helm plugin install https://github.com/helm/helm-mapkubeapis
```

## Environment Variables

Helm uses the following environment variables:

- `HELM_CACHE_HOME`: Path to the cache directory
- `HELM_CONFIG_HOME`: Path to the config directory
- `HELM_DATA_HOME`: Path to the data directory
- `HELM_DEBUG`: Enable verbose output (0 or 1)
- `HELM_DRIVER`: Storage backend (configmap, secret, memory, sql)
- `HELM_MAX_HISTORY`: Maximum number of release versions saved per release
- `HELM_NAMESPACE`: Namespace scope for the request
- `HELM_NO_PLUGINS`: Disable plugins (0 or 1)
- `HELM_PLUGINS`: Path to the plugins directory
- `HELM_REGISTRY_CONFIG`: Path to the registry config file
- `HELM_REPOSITORY_CACHE`: Path to the repository cache directory
- `HELM_REPOSITORY_CONFIG`: Path to the repositories file
- `KUBECONFIG`: Path to the Kubernetes config file

## Common Flags

These flags work across many Helm commands:

- `--debug`: Enable verbose output
- `--kube-apiserver`: The Kubernetes API server address
- `--kube-as-group`: Group to impersonate for the operation
- `--kube-as-user`: Username to impersonate for the operation
- `--kube-ca-file`: The certificate authority file for the Kubernetes API server connection
- `--kube-context`: Name of the kubeconfig context to use
- `--kube-token`: Bearer token used for authentication
- `--kubeconfig`: Path to the kubeconfig file
- `--namespace/-n`: Namespace scope for the request
- `--registry-config`: Path to the registry config file
- `--repository-cache`: Path to the repository cache directory
- `--repository-config`: Path to the repositories file

## Tips and Tricks

### Working with Multiple Environments
```bash
# Using different value files for environments
helm install my-release ./mychart -f values.yaml -f values-production.yaml

# Using multiple namespaces
helm list --all-namespaces
```

### Debugging Charts
```bash
# Show rendered templates without installing
helm template ./mychart --debug

# Show what would be installed
helm install my-release ./mychart --dry-run --debug
```

### Managing Large Values Files
```bash
# Split values into multiple files
helm install my-release ./mychart -f common.yaml -f database.yaml -f frontend.yaml

# Use schema validation
# (add a values.schema.json to your chart for validation)
```

### Release Management Best Practices
```bash
# Always version your charts
# In Chart.yaml:
# version: 1.0.0  (chart version)
# appVersion: "1.16.0" (application version)

# Use semantic versioning for chart versions
# major.minor.patch
```

### Security Best Practices
```bash
# Validate chart before installing
helm lint ./mychart
helm template ./mychart | kubectl apply --dry-run=client -f -

# Use atomic installations to prevent partial failures
helm install my-release ./mychart --atomic

# Set resource limits in values.yaml
```

### Helpful One-liners
```bash
# List all charts in a repository
helm search repo bitnami

# Find deprecated charts
helm search repo bitnami --deprecated

# Find charts with specific keyword
helm search repo database

# Show all chart versions
helm search repo nginx --versions

# Render and validate a chart
helm template ./mychart | kubeval

# Export all release manifests
helm get manifest my-release > release.yaml
```