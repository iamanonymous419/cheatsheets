

# 🛡️ Trivy CLI Cheat Sheet

Trivy is a comprehensive and versatile security scanner that can detect vulnerabilities, misconfigurations, secrets, and licenses across various targets like container images, file systems, repositories, and Kubernetes clusters.

---

## 📦 Installation

Trivy can be installed via package managers or used directly as a Docker image:


```bash
# macOS
brew install aquasecurity/trivy/trivy

# Ubuntu/Debian
sudo apt install trivy

# Windows (using Chocolatey)
choco install trivy

# Docker
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy image python:3.4-alpine
```


For more installation options, refer to the [official documentation](https://aquasecurity.github.io/trivy/v0.33/docs/installation/).

---

## 🔍 Basic Usage


```bash
# Scan a container image
trivy image python:3.4-alpine

# Scan a local file system
trivy fs /path/to/project

# Scan a Git repository
trivy repo https://github.com/user/repo

# Scan configuration files for misconfigurations
trivy config /path/to/config

# Scan a Kubernetes cluster
trivy k8s --report summary cluster
```


---

## 🐳 Container Image Scanning


```bash
# Scan an image
trivy image alpine:3.15

# Scan an image tar archive
trivy image --input ruby-3.1.tar

# Filter by severity
trivy image --severity HIGH,CRITICAL alpine:3.15

# Ignore unfixed vulnerabilities
trivy image --ignore-unfixed alpine:3.15

# Output in JSON format
trivy image --format json --output result.json alpine:3.15

# Output in CycloneDX format
trivy image --format cyclonedx --output result.cdx alpine:3.15
```


---

## 📁 File System Scanning


```bash
# Scan current directory
trivy fs .

# Scan with specific security checks
trivy fs --security-checks vuln,config .

# Skip specific directories
trivy fs --skip-dirs .git,node_modules .

# Skip specific files
trivy fs --skip-files secret.txt,config.yaml .
```


---

## 🧾 SBOM Scanning


```bash
# Scan an SBOM file
trivy sbom sbom.spdx

# Generate SBOM in CycloneDX format
trivy image --format cyclonedx --output sbom.cdx.json alpine:3.15

# Generate SBOM in SPDX format
trivy image --format spdx-json --output sbom.spdx.json alpine:3.15
```


---

## 🛠️ Configuration File Scanning (IaC)


```bash
# Scan configuration files
trivy config /path/to/config

# Filter by severity
trivy config --severity HIGH,CRITICAL /path/to/config

# Use custom Rego policies
trivy config --policy /path/to/rego /path/to/config
```


---

## ☸️ Kubernetes Scanning


```bash
# Scan the entire cluster
trivy k8s --report summary cluster

# Scan a specific namespace
trivy k8s --namespace default all

# Scan a specific resource
trivy k8s deployment my-deployment

# Filter by severity
trivy k8s --severity CRITICAL deployment my-deployment

# Output in JSON format
trivy k8s --format json --output result.json cluster
```


---

## 🔐 Secret Scanning


```bash
# Scan for secrets in a file system
trivy fs --scanners secret /path/to/project

# Scan for secrets in a repository
trivy repo --scanners secret https://github.com/user/repo

# Scan for secrets in a container image
trivy image --scanners secret alpine:3.15
```


---

## 📄 License Scanning


```bash
# Scan for licenses in a file system
trivy fs --scanners license /path/to/project

# Scan for licenses in a container image
trivy image --scanners license alpine:3.15
```


---

## 🧩 Plugin Management


```bash
# List installed plugins
trivy plugin list

# Install a plugin
trivy plugin install aquasecurity/trivy-plugin-example

# Uninstall a plugin
trivy plugin uninstall trivy-plugin-example

# Run a plugin
trivy plugin run trivy-plugin-example
```


---

## ⚙️ Server and Client Mode


```bash
# Start Trivy in server mode
trivy server

# Use Trivy in client mode
trivy client --remote http://localhost:4954 image alpine:3.15
```


---

## 📤 Output Formats


```bash
# Default table format
trivy image alpine:3.15

# JSON format
trivy image --format json --output result.json alpine:3.15

# SARIF format (for GitHub integration)
trivy image --format sarif --output result.sarif alpine:3.15

# CycloneDX format
trivy image --format cyclonedx --output result.cdx alpine:3.15

# SPDX format
trivy image --format spdx-json --output result.spdx.json alpine:3.15
```


---

## 🎛️ Global Options


```bash
--quiet, -q           # Suppress progress bar and log output
--debug, -d           # Enable debug mode
--cache-dir <dir>     # Specify cache directory
--help, -h            # Show help
--version, -v         # Show version
```


---

## 📚 Resources

- [Official Documentation](https://aquasecurity.github.io/trivy/)
- [GitHub Repository](https://github.com/aquasecurity/trivy)
- [Trivy Cheat Sheet PDF](https://cheat-sheets.nth-root.nl/trivy-cheat-sheet.pdf)

