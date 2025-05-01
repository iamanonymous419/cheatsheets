# Helm CLI Cheatsheet

## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Configuration](#configuration)
- [Chart Management](#chart-management)
- [Repository Management](#repository-management)
- [Release Management](#release-management)
- [Templating](#templating)
- [Advanced Templating](#advanced-templating)
- [Plugin Management](#plugin-management)
- [Environment Variables](#environment-variables)
- [Common Flags](#common-flags)
- [Chart Development](#chart-development)
- [Chart Best Practices](#chart-best-practices)
- [Security](#security)
- [Performance Optimization](#performance-optimization)
- [Troubleshooting](#troubleshooting)
- [CI/CD Integration](#cicd-integration)
- [Helm 3 vs Helm 2](#helm-3-vs-helm-2)
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

## Advanced Templating

### Template Functions and Pipelines
```bash
# Common functions
{{ quote .Values.someValue }}  # Add quotes around a value
{{ trim .Values.someString }}  # Remove whitespace
{{ default "default" .Values.key }}  # Set default value
{{ toYaml .Values.resources }}  # Convert to YAML
{{ fromYaml .Files.Get "config.yaml" }}  # Parse YAML file
{{ include "mychart.labels" . | indent 4 }}  # Include template with indent

# Data type conversion
{{ int64 .Values.replicas }}  # Convert to integer
{{ toString .Values.port }}  # Convert to string

# String operations
{{ upper .Values.app.name }}  # Convert to uppercase
{{ lower .Values.app.name }}  # Convert to lowercase
{{ replace "-" "_" .Values.name }}  # Replace strings
{{ trunc 63 .Values.name }}  # Truncate string
{{ b64enc .Values.secret }}  # Base64 encode
{{ b64dec .Values.encodedData }}  # Base64 decode

# Date functions
{{ now | date "2006-01-02" }}  # Format current date
{{ now | htmlDate }}  # Format as HTML date

# Flow control
{{ if eq .Values.service.type "LoadBalancer" }}
# LoadBalancer config
{{ else }}
# ClusterIP config
{{ end }}

# Loops
{{ range .Values.configFiles }}
filename: {{ .name }}
{{ end }}

# With blocks
{{ with .Values.resources }}
resources:
  limits:
    cpu: {{ .limits.cpu }}
{{ end }}
```

### Named Templates and Includes
```yaml
# Define a template in _helpers.tpl
{{- define "mychart.labels" -}}
app: {{ .Chart.Name }}
release: {{ .Release.Name }}
{{- end -}}

# Use the template in deployment.yaml
metadata:
  labels:
    {{- include "mychart.labels" . | nindent 4 }}
```

### Working with Files
```yaml
# Access files from the Files object
{{ .Files.Get "config.ini" }}

# Iterate through files
{{ range $path, $bytes := .Files.Glob "files/*" }}
{{ $path }}: {{ $bytes | b64enc }}
{{ end }}

# Include a file as a configmap
data:
  config.json: |-
{{ .Files.Get "config.json" | indent 4 }}
```

### Scoping and Variables
```yaml
# Set a variable
{{- $releaseName := .Release.Name -}}

# Scope within range
{{- range $index, $service := .Values.services }}
{{- $servicePort := int $service.port }}
{{- end }}
```

## Chart Development

### Chart Structure
```
mychart/
  ├── Chart.yaml           # Chart metadata
  ├── values.yaml          # Default configuration values
  ├── values.schema.json   # JSON Schema for values validation
  ├── charts/              # Directory for dependent charts
  ├── crds/                # Custom Resource Definitions
  ├── templates/           # Directory for template files
  │   ├── NOTES.txt        # Installation notes
  │   ├── _helpers.tpl     # Template helpers
  │   ├── deployment.yaml  # Kubernetes resource templates
  │   └── ...
  └── templates/tests/     # Test templates
      └── test-connection.yaml
```

### Chart.yaml Fields
```yaml
apiVersion: v2              # Helm chart API version (v2 for Helm 3)
name: mychart               # Name of the chart
version: 1.2.3              # Chart version (SemVer 2)
appVersion: "1.16.0"        # Version of the app being deployed
description: My application # Chart description
type: application           # application or library
dependencies:               # Chart dependencies
  - name: postgresql
    version: "10.5.3"
    repository: "https://charts.bitnami.com/bitnami"
    condition: postgresql.enabled
maintainers:                # Chart maintainers
  - name: John Doe
    email: john@example.com
icon: "https://example.com/icon.png"  # URL to chart icon
home: "https://example.com"           # Project home page
keywords:                             # Keywords for charts
  - database
  - nosql
```

### Starterpack
```bash
# Create a starter chart template
helm create --starter=custom-starter mychart

# Creating your own starter
# 1. Create a chart with the structure you want
# 2. Place it in $HELM_HOME/starters/
# 3. Use it with the --starter flag
```

### Chart Hooks
```yaml
# Create a hook in templates/pre-install-hook.yaml
metadata:
  annotations:
    "helm.sh/hook": pre-install
    "helm.sh/hook-weight": "5"      # Order of execution
    "helm.sh/hook-delete-policy": hook-succeeded

# Available hook types:
# pre-install, post-install
# pre-upgrade, post-upgrade
# pre-delete, post-delete
# pre-rollback, post-rollback
# test
```

## Chart Best Practices

### General Best Practices
```yaml
# Use specific image tags, not 'latest'
image:
  repository: nginx
  tag: 1.21.6  # Not 'latest'

# Provide default resource limits
resources:
  limits:
    cpu: 100m
    memory: 128Mi
  requests:
    cpu: 100m
    memory: 128Mi

# Add pod anti-affinity for high availability
affinity:
  podAntiAffinity:
    preferredDuringSchedulingIgnoredDuringExecution:
      - weight: 100
        podAffinityTerm:
          topologyKey: kubernetes.io/hostname
```

### Values File Practices
```yaml
# Group related settings
service:
  type: ClusterIP
  port: 80
  annotations: {}

# Use camelCase for values
storageClass: standard

# Document values with comments
# -- Number of replicas for the deployment
replicaCount: 1

# Provide sensible defaults
livenessProbe:
  enabled: true
  initialDelaySeconds: 30
  periodSeconds: 10
  
# Use conditionals to make features optional
metrics:
  enabled: false
  serviceMonitor:
    enabled: false
```

### Template Best Practices
```yaml
# Use helpers for common labels
{{- define "mychart.labels" -}}
app.kubernetes.io/name: {{ include "mychart.name" . }}
app.kubernetes.io/instance: {{ .Release.Name }}
app.kubernetes.io/version: {{ .Chart.AppVersion | quote }}
app.kubernetes.io/managed-by: {{ .Release.Service }}
{{- end -}}

# Indent properly
metadata:
  name: {{ include "mychart.fullname" . }}
  {{- with .Values.annotations }}
  annotations:
    {{- toYaml . | nindent 4 }}
  {{- end }}

# Use the NOTES.txt template
# templates/NOTES.txt:
Application {{ .Chart.Name }} installed.
Access it at: http://{{ .Values.hostname }}:{{ .Values.service.port }}
```

## Security

### Secure Chart Development
```yaml
# Set securityContext at pod level
securityContext:
  runAsNonRoot: true
  runAsUser: 1000
  fsGroup: 2000

# Set resource limits
resources:
  limits:
    cpu: 100m
    memory: 128Mi
  requests:
    cpu: 100m
    memory: 128Mi

# Use network policies
networkPolicy:
  enabled: true
  ingressRules:
    - from:
        - podSelector:
            matchLabels:
              app: frontend
```

### Sensitive Data Handling
```bash
# Use Secrets for sensitive data
# Store encrypted values with helm-secrets plugin
helm secrets enc secrets.yaml

# Use external secret management
# With external-secrets operator or Vault

# Store minimal secrets in values
# DON'T:
postgresql:
  password: "insecure-password"
# DO:
postgresql:
  existingSecret: "my-postgresql-secret"
```

### Chart Provenance and Verification
```bash
# Sign your chart
helm package --sign --key 'John Doe' ./mychart

# Verify a chart
helm verify ./mychart-1.0.0.tgz

# Install only verified charts
helm install --verify my-release ./mychart-1.0.0.tgz
```

## Performance Optimization

### Resource Management
```yaml
# Set appropriate resource requests/limits
resources:
  requests:
    cpu: 10m    # Minimum required CPU
    memory: 64Mi # Minimum required memory
  limits:
    cpu: 100m    # Maximum CPU
    memory: 128Mi # Maximum memory

# Use horizontal pod autoscaling
autoscaling:
  enabled: true
  minReplicas: 1
  maxReplicas: 10
  targetCPUUtilizationPercentage: 80
```

### Helm Performance
```bash
# Speed up helm operations
helm list --max 100  # Limit number of releases

# Use helm with large releases
export HELM_MAX_HISTORY=5  # Limit history size

# Optimize helm chart size
# Exclude unnecessary files with .helmignore
```

### Kubernetes Integration
```yaml
# Use pod disruption budgets
pdb:
  enabled: true
  minAvailable: 1

# Set pod topology spread constraints
topologySpreadConstraints:
  - maxSkew: 1
    topologyKey: kubernetes.io/hostname
    whenUnsatisfiable: DoNotSchedule
    labelSelector:
      matchLabels:
        app: {{ template "app.name" . }}
```

## Troubleshooting

### Common Issues and Solutions
```bash
# Error: UPGRADE FAILED: cannot patch "resource" because it is being deleted
# Solution: Wait for resource deletion or use --force flag
helm upgrade --force my-release ./mychart

# Error: UPGRADE FAILED: rendered manifests contain a resource that already exists
# Solution: Use --force or delete conflicting resources
kubectl delete deployment my-deployment
helm upgrade my-release ./mychart

# Error: Error: YAML parse error
# Solution: Run helm lint to find YAML errors
helm lint ./mychart
```

### Debugging Commands
```bash
# Debug installation
helm install my-release ./mychart --debug

# Debug rendering issues
helm template ./mychart --debug

# Check resources created by a release
kubectl get all -l release=my-release

# Describe failing resources
kubectl describe pod -l app.kubernetes.io/instance=my-release

# Get pod logs
kubectl logs -l app.kubernetes.io/instance=my-release

# Force resource recreation
helm upgrade my-release ./mychart --force
```

### Rollback Issues
```bash
# View revision history
helm history my-release

# Rollback to specific revision
helm rollback my-release 1

# Debug rollback failure
helm rollback my-release 1 --debug

# Force rollback
helm rollback my-release 1 --force
```

## CI/CD Integration

### GitOps Workflow
```bash
# ArgoCD Application for Helm Chart
kubectl apply -f - <<EOF
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: my-app
spec:
  source:
    repoURL: https://github.com/org/repo.git
    path: charts/mychart
    targetRevision: HEAD
    helm:
      valueFiles:
      - values-prod.yaml
  destination:
    server: https://kubernetes.default.svc
    namespace: default
EOF
```

### CI Pipeline Examples
```bash
# GitHub Actions workflow
name: Helm Chart CI
on: [push]
jobs:
  lint-chart:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Lint Chart
        run: helm lint ./chart
      - name: Package Chart
        run: helm package ./chart
      - name: Install Chart (dry-run)
        run: helm install --dry-run my-release ./chart
```

### Flux CD Integration
```yaml
# HelmRelease resource for Flux v2
apiVersion: helm.toolkit.fluxcd.io/v2beta1
kind: HelmRelease
metadata:
  name: my-release
  namespace: default
spec:
  interval: 1m
  chart:
    spec:
      chart: mychart
      version: '>=1.0.0 <2.0.0'
      sourceRef:
        kind: HelmRepository
        name: my-repo
  values:
    replicaCount: 2
```

## Helm 3 vs Helm 2

### Key Differences
```
# Helm 2                          | Helm 3
---------------------------------|---------------------------------
Tiller component in cluster      | No Tiller (client-only)
global release names             | release names scoped to namespace
helm init to setup              | no initialization needed
helm delete (keeps history)     | helm uninstall (removes all)
helm delete --purge             | helm uninstall
helm inspect                    | helm show
helm fetch                      | helm pull
no default release namespace    | default to current context namespace
chart apiVersion: v1           | chart apiVersion: v2
requirements.yaml for deps     | dependencies in Chart.yaml
crd-install hook               | crds/ directory
```

### Migration from Helm 2
```bash
# Install migration plugin
helm plugin install https://github.com/helm/helm-2to3

# Migrate Helm v2 configuration
helm 2to3 move config

# Migrate Helm v2 releases
helm 2to3 convert RELEASE_NAME

# Check for errors
helm 2to3 convert --dry-run RELEASE_NAME

# Clean up Helm v2 data
helm 2to3 cleanup --skip-confirmation
```

## Tips and Tricks

### Working with Multiple Environments
```bash
# Using different value files for environments
helm install my-release ./mychart -f values.yaml -f values-production.yaml

# Using Helmfile for environment management
# helmfile.yaml:
environments:
  development:
    values:
      - env/dev.yaml
  production:
    values:
      - env/prod.yaml

# Using multiple namespaces
helm list --all-namespaces
```

### Debugging Charts
```bash
# Show rendered templates without installing
helm template ./mychart --debug

# Show what would be installed
helm install my-release ./mychart --dry-run --debug

# Show differences between releases
helm diff revision my-release 1 2

# Debug with kubeval validation
helm template ./mychart | kubeval
```

### Managing Large Values Files
```bash
# Split values into multiple files
helm install my-release ./mychart -f common.yaml -f database.yaml -f frontend.yaml

# Use schema validation
# (add a values.schema.json to your chart for validation)

# External values from URL
helm install -f https://example.com/values.yaml my-release ./mychart
```

### Release Management Best Practices
```bash
# Always version your charts
# In Chart.yaml:
# version: 1.0.0  (chart version)
# appVersion: "1.16.0" (application version)

# Use semantic versioning for chart versions
# major.minor.patch

# Keep a changelog for your chart
# Create a CHANGELOG.md file in your chart
```

### Security Best Practices
```bash
# Validate chart before installing
helm lint ./mychart
helm template ./mychart | kubectl apply --dry-run=client -f -

# Use atomic installations to prevent partial failures
helm install my-release ./mychart --atomic

# Set resource limits in values.yaml

# Use network policies to restrict traffic
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

# Check for chart updates
helm list -o yaml | grep 'chart:' | sort | uniq

# Search multiple repos at once
helm search repo -r '^prometheus


# Get total resources from a release
helm get manifest my-release | grep -c "kind:"

# Dump values from running release
helm get values my-release -o yaml > current-values.yaml
```