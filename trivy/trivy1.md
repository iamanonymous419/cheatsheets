
# 🛡️ Trivy CLI Full Cheat Sheet

Trivy is a comprehensive and fast vulnerability and misconfiguration scanner for containers, Kubernetes, and other artifacts. This cheat sheet covers all core functionalities and usage examples.

---

## 🚀 Installation

```bash
brew install aquasecurity/trivy/trivy         # macOS
sudo apt install trivy                        # Ubuntu/Debian
choco install trivy                           # Windows
```

---

## 🐳 Container Image Scanning

```bash
trivy image <image_name>                      # Scan container image
trivy image --severity HIGH,CRITICAL <image>  # Filter by severity
trivy image --format json -o result.json <image>  # JSON output
trivy image --ignore-unfixed <image>          # Ignore unfixed vulns
```

---

## 📦 Filesystem Scanning

```bash
trivy fs <path>                               # Scan local files
trivy fs --scan-hidden <path>                 # Scan hidden files
trivy fs --skip-dirs .git,node_modules <path> # Skip dirs
```

---

## 🧱 SBOM Scanning

```bash
trivy sbom <sbom_file.spdx|cyclonedx|syft>    # Scan SBOM file
```

---

## 🎛️ Config File Scanning (IaC)

```bash
trivy config <path>                           # Scan IaC for misconfigurations
trivy config --severity HIGH,CRITICAL <path>  # Filter by severity
trivy config --policy <rego-dir> <path>       # Custom policies
```

---

## ☸️ Kubernetes Scanning

```bash
trivy k8s --report summary cluster            # Scan full cluster
trivy k8s --namespace default all             # Scan namespace
trivy k8s pod <pod-name>                      # Scan a pod
trivy k8s node <node-name>                    # Scan a node
```

---

## 📋 Kubernetes Manifest File Scanning

```bash
trivy config <manifest.yaml>                  # Scan YAML manifests
```

---

## 🧩 Repository Scanning (VCS)

```bash
trivy repo https://github.com/user/repo       # Scan remote Git repo
```

---

## 🔐 Secret Scanning

```bash
trivy fs --scanners secret <path>             # Scan secrets in files
trivy repo --scanners secret <repo>           # Scan secrets in repo
trivy image --scanners secret <image>         # Scan secrets in image
```

---

## 📝 License Scanning

```bash
trivy fs --scanners license <path>            # Scan for license compliance
trivy image --scanners license <image>        # Scan licenses in image
```

---

## ⚙️ SBOM Generation

```bash
trivy image --format cyclonedx -o sbom.json <image>  # Generate CycloneDX SBOM
trivy image --format spdx-json -o sbom.json <image>  # Generate SPDX SBOM
```

---

## 📦 Dependency Scanning

```bash
trivy fs --scanners vuln,secret,license <path>     # Scan dependencies in code
```

---

## 🛠️ Caching and DB Update

```bash
trivy --download-db-only                   # Download latest DB
trivy image --skip-db-update <image>       # Skip DB update
```

---

## 📤 Output Formats

```bash
trivy image --format table                 # Default (table)
trivy image --format json -o result.json   # JSON
trivy image --format sarif -o result.sarif # SARIF for GitHub Code Scanning
```

---

## 📊 Filtering Results

```bash
trivy image --severity CRITICAL,HIGH <image>     # Filter by severity
trivy image --vuln-type os,library <image>       # Filter vuln types
```

---

## 🔍 Ignoring Vulnerabilities

```bash
trivy image --ignorefile .trivyignore <image>    # Use .trivyignore
```

---

## 📡 Trivy Server Mode

```bash
trivy server                             # Start Trivy in server mode
trivy client --remote http://localhost:4954 image <image>  # Use client mode
```

---

## 🔐 Authentication (Git, Registry)

```bash
trivy image --username foo --password bar <image>     # Auth for registries
trivy repo --token <GITHUB_TOKEN> <repo_url>          # Auth for GitHub
```

---

## 📚 Resources

- [Official Docs](https://aquasecurity.github.io/trivy/)
- [Trivy GitHub](https://github.com/aquasecurity/trivy)
- [Trivy VS Code Extension](https://marketplace.visualstudio.com/items?itemName=AquaSecurity.trivy-vulnerability-scanner)

---

## ✅ Pro Tip: Use `--help`

```bash
trivy image --help
trivy config --help
```

This provides full options and advanced usage.

---

Happy Scanning! 🔍
