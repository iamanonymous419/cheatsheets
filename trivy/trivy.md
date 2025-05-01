# Trivy CLI Cheatsheet

## Table of Contents
- [Trivy CLI Cheatsheet](#trivy-cli-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Installation](#installation)
    - [Using Package Managers](#using-package-managers)
    - [Binary Installation](#binary-installation)
  - [Basic Usage](#basic-usage)
  - [Scanning Targets](#scanning-targets)
    - [Container Images](#container-images)
    - [Filesystems](#filesystems)
    - [Git Repositories](#git-repositories)
    - [Kubernetes](#kubernetes)
    - [AWS](#aws)
  - [Configuration Options](#configuration-options)
  - [Output Formats](#output-formats)
  - [Filtering Results](#filtering-results)
  - [CI/CD Integration](#cicd-integration)
  - [Cache Management](#cache-management)
  - [Plugin System](#plugin-system)
  - [Advanced Features](#advanced-features)
  - [Common Issues \& Troubleshooting](#common-issues--troubleshooting)

## Overview

Trivy is a comprehensive security scanner that finds vulnerabilities, misconfigurations, secrets, and SBOM in containers, Kubernetes, code repositories, clouds and more.

## Installation

### Using Package Managers

**Homebrew (macOS/Linux)**:
```sh
brew install trivy
```

**APT (Debian/Ubuntu)**:
```sh
sudo apt-get install wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy
```

**YUM (Amazon Linux/CentOS)**:
```sh
sudo rpm -ivh https://github.com/aquasecurity/trivy/releases/download/v[VERSION]/trivy_[VERSION]_Linux-64bit.rpm
```

**Docker**:
```sh
docker pull aquasec/trivy
```

### Binary Installation

```sh
# Download the latest release
curl -sfL https://raw.githubusercontent.com/aquasecurity/trivy/main/contrib/install.sh | sh -s -- -b /usr/local/bin

# Verify installation
trivy --version
```

## Basic Usage

**Basic syntax**:
```sh
trivy [COMMAND] [OPTIONS] TARGET
```

**Common commands**:
- `image`: Scan a container image
- `fs`: Scan a filesystem
- `repo`: Scan a git repository
- `k8s`: Scan Kubernetes resources
- `config`: Scan configuration files
- `aws`: Scan AWS resources
- `plugin`: Manage plugins
- `version`: Show version
- `help`: Show help

## Scanning Targets

### Container Images

**Scan local image**:
```sh
trivy image [IMAGE_NAME]
```

**Scan remote image**:
```sh
trivy image [REGISTRY/IMAGE:TAG]
```

**Scan with custom credentials**:
```sh
trivy image --username [USERNAME] --password [PASSWORD] [REGISTRY/IMAGE:TAG]
```

**Scan image without OS packages**:
```sh
trivy image --security-checks vuln --vuln-type library [IMAGE_NAME]
```

**Scan image without application dependencies**:
```sh
trivy image --security-checks vuln --vuln-type os [IMAGE_NAME]
```

**Scan multiple images**:
```sh
trivy image image1 image2 image3
```

### Filesystems

**Scan local directory**:
```sh
trivy fs [PATH/TO/PROJECT]
```

**Scan specific file**:
```sh
trivy fs [PATH/TO/FILE]
```

**Scan for secrets**:
```sh
trivy fs --security-checks secret [PATH]
```

**Scan for misconfigurations**:
```sh
trivy fs --security-checks config [PATH]
```

### Git Repositories

**Scan remote repository**:
```sh
trivy repo [REPOSITORY_URL]
```

**Scan specific branch or tag**:
```sh
trivy repo --branch [BRANCH] [REPOSITORY_URL]
```

**Scan with depth limit**:
```sh
trivy repo --depth [NUMBER] [REPOSITORY_URL]
```

### Kubernetes

**Scan live Kubernetes cluster**:
```sh
trivy k8s --report summary cluster
```

**Scan specific namespace**:
```sh
trivy k8s --namespace [NAMESPACE] all
```

**Scan specific resource type**:
```sh
trivy k8s --report summary deployment
```

**Scan all resources**:
```sh
trivy k8s --report summary all
```

**Scan YAML files**:
```sh
trivy config [PATH/TO/YAML]
```

**Scan Helm chart**:
```sh
trivy config --input helm [PATH/TO/CHART]
```

### AWS

**Scan AWS account**:
```sh
trivy aws --region [REGION] account
```

**Scan specific service**:
```sh
trivy aws --region [REGION] --service [SERVICE] account
```

**Scan with custom credentials**:
```sh
AWS_ACCESS_KEY_ID=[KEY] AWS_SECRET_ACCESS_KEY=[SECRET] trivy aws account
```

## Configuration Options

**Cache options**:
```sh
# Clear cache
trivy --clear-cache

# Skip cache update
trivy --skip-update 

# Specify cache directory
trivy --cache-dir [PATH] [TARGET]
```

**Scanning options**:
```sh
# Offline scanning
trivy --offline-scan [TARGET]

# Skip specific files/directories
trivy --skip-dirs [DIR1],[DIR2] [TARGET]

# Skip specific files
trivy --skip-files [FILE1],[FILE2] [TARGET]

# Set timeout
trivy --timeout [TIME] [TARGET]
```

**Severity filtering**:
```sh
# Specify severity levels
trivy --severity HIGH,CRITICAL [TARGET]

# Ignore unfixed vulnerabilities
trivy --ignore-unfixed [TARGET]
```

## Output Formats

**Change output format**:
```sh
# JSON format
trivy --format json [TARGET]

# SARIF format
trivy --format sarif [TARGET]

# Table format (default)
trivy --format table [TARGET]

# Template format
trivy --format template --template "@/path/to/template.tpl" [TARGET]

# HTML format 
trivy --format template --template "@contrib/html.tpl" -o report.html [TARGET]

# ASFF format (for AWS Security Hub)
trivy --format asff [TARGET]

# Cyclonedx format
trivy --format cyclonedx [TARGET]

# SPDX format
trivy --format spdx-json [TARGET]
```

**Output to file**:
```sh
trivy --output [FILE_PATH] [TARGET]
```

## Filtering Results

**Filter by severity**:
```sh
trivy --severity HIGH,CRITICAL [TARGET]
```

**Filter by vulnerability ID**:
```sh
trivy --vuln-id [CVE-ID] [TARGET]
```

**Ignore specific vulnerabilities**:
```sh
trivy --ignorefile [PATH_TO_IGNORE_FILE] [TARGET]
```

**Create .trivyignore file**:
```
# Format: [CVE-ID or issue ID]
CVE-2021-44228
CVE-2021-45046
```

**Ignore unfixed vulnerabilities**:
```sh
trivy --ignore-unfixed [TARGET]
```

## CI/CD Integration

**Exit code on vulnerability detection**:
```sh
trivy --exit-code 1 [TARGET]
```

**Limit by severity for CI/CD**:
```sh
trivy --exit-code 1 --severity CRITICAL [TARGET]
```

**Jenkins integration**:
```sh
trivy --format sarif --output trivy-results.sarif [TARGET]
```

**GitHub Actions integration**:
```yaml
- name: Run Trivy vulnerability scanner
  uses: aquasecurity/trivy-action@master
  with:
    image-ref: 'image:tag'
    format: 'sarif'
    output: 'trivy-results.sarif'
```

**GitLab CI integration**:
```yaml
trivy-scan:
  script:
    - trivy image --exit-code 1 --severity HIGH,CRITICAL $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA
```

## Cache Management

**Clear cache**:
```sh
trivy --clear-cache
```

**Skip database update**:
```sh
trivy --skip-update [TARGET]
```

**Specify cache directory**:
```sh
trivy --cache-dir [PATH] [TARGET]
```

**Reset database**:
```sh
trivy --reset [TARGET]
```

## Plugin System

**List available plugins**:
```sh
trivy plugin list
```

**Install plugin**:
```sh
trivy plugin install github.com/user/plugin
```

**Update plugin**:
```sh
trivy plugin update [PLUGIN_NAME]
```

**Uninstall plugin**:
```sh
trivy plugin uninstall [PLUGIN_NAME]
```

**Run plugin**:
```sh
trivy [PLUGIN_NAME] [OPTIONS]
```

## Advanced Features

**Generate SBOM (Software Bill of Materials)**:
```sh
# CycloneDX format
trivy image --format cyclonedx [IMAGE]

# SPDX format
trivy image --format spdx-json [IMAGE]
```

**Show vulnerability details**:
```sh
trivy image --vuln-type os --format json -o results.json [IMAGE]
```

**Scan for license compliance**:
```sh
trivy fs --security-checks license [PATH]
```

**Custom policy scanning**:
```sh
trivy config --policy [PATH_TO_POLICY_DIR] [TARGET]
```

**Air-gapped environment setup**:
```sh
# Download database
trivy --download-db-only

# Use downloaded database
trivy --skip-update --offline-scan [TARGET]
```

**Run server mode**:
```sh
# Start server
trivy server

# Scan using server
trivy client --remote http://localhost:4954 [TARGET]
```

## Common Issues & Troubleshooting

**Debugging**:
```sh
# Enable debug mode
trivy --debug [TARGET]

# Increase verbosity
trivy -v [TARGET]
```

**Common issues**:

1. **Connection issues**:
   ```sh
   # Use proxy
   HTTPS_PROXY=http://proxy:port trivy [TARGET]
   ```

2. **Permission issues**:
   ```sh
   # Run with sudo
   sudo trivy [TARGET]
   ```

3. **Timeout issues**:
   ```sh
   # Increase timeout
   trivy --timeout 10m [TARGET]
   ```

4. **False positives handling**:
   - Create a `.trivyignore` file in your project root
   - Add CVE IDs to ignore, one per line

5. **Resource constraints**:
   ```sh
   # Limit scan to specific directories
   trivy --skip-dirs [DIRS_TO_SKIP] [TARGET]
   ```

6. **Database update failures**:
   ```sh
   # Force DB update
   trivy --reset [TARGET]
   ```