Here's a combined **Trivy Cheatsheet** and a **Terraform CLI Reference**, neatly formatted for a `README.md` file. This is ideal for DevSecOps or Infrastructure-as-Code (IaC) engineers using both tools.

---

### ✅ Would you like me to create a downloadable `.md` file or push this into a GitHub-ready structure too?

---

## 📄 `README.md` – Trivy + Terraform CLI Cheatsheet

```
# 🔐 Trivy + ⚙️ Terraform CLI Cheatsheet

## 📦 Trivy - Vulnerability Scanner

Trivy is a comprehensive and easy-to-use vulnerability scanner for:

- OS packages
- Containers
- IaC (Terraform, Kubernetes YAML)
- Git Repositories
- SBOM and more

### 🧪 1. Install Trivy

```bash
# macOS
brew install aquasecurity/trivy/trivy

# Linux
sudo apt install wget -y
wget https://github.com/aquasecurity/trivy/releases/latest/download/trivy_0.50.1_Linux-64bit.deb
sudo dpkg -i trivy_0.50.1_Linux-64bit.deb
```

---

### 🔍 2. Scan Container Images

```bash
trivy image nginx:latest
trivy image --severity CRITICAL,HIGH ubuntu:22.04
```

---

### 📁 3. Scan File System / Directories

```bash
trivy fs .
trivy fs --severity HIGH,CRITICAL --exit-code 1 .
```

---

### 📜 4. Scan IaC files (Terraform, Kubernetes YAML)

```bash
trivy config .
trivy config ./terraform
trivy config --severity HIGH,CRITICAL --exit-code 1 .
```

---

### 🔐 5. Scan Git Repositories (Secrets + Misconfig)

```bash
trivy repo https://github.com/your-org/your-repo
```

---

### 📦 6. Generate SBOM (Software Bill of Materials)

```bash
trivy sbom --format cyclonedx --output sbom.json nginx:latest
```

---

### 🧪 7. CI/CD Integration (example)

```bash
# fail pipeline if vulnerabilities of HIGH/CRITICAL are found
trivy image --severity HIGH,CRITICAL --exit-code 1 nginx:latest
```

---

### 🛠 8. Useful Options

| Option | Description |
|--------|-------------|
| `--format table|json|sarif` | Output format |
| `--ignore-unfixed` | Ignore unfixed vulnerabilities |
| `--exit-code N` | Exit with N on detection |
| `--download-db-only` | Just download DB |
| `--skip-dirs` | Skip certain directories |

---

## ☁️ Terraform CLI Cheatsheet

Terraform CLI helps you manage infrastructure as code (IaC) efficiently.

---

### 📦 1. Terraform Setup

```bash
# Install using tfenv (recommended)
brew install tfenv
tfenv install latest
tfenv use latest
```

---

### 🛠 2. Basic Commands

```bash
terraform init      # Initialize Terraform working directory
terraform validate  # Check syntax
terraform plan      # Show execution plan
terraform apply     # Apply changes
terraform destroy   # Destroy infrastructure
```

---

### 📁 3. State Management

```bash
terraform state list                          # List resources in state
terraform state show aws_instance.my_server   # Show specific resource
terraform state rm aws_instance.my_server     # Remove from state
```

---

### 🔄 4. Refresh / Output / Graph

```bash
terraform refresh        # Update state
terraform output          # Show output values
terraform graph | dot -Tpng > graph.png
```

---

### 🔐 5. Workspaces

```bash
terraform workspace list
terraform workspace new dev
terraform workspace select dev
```

---

### ⚙️ 6. Modules

```hcl
module "vpc" {
  source = "./modules/vpc"
  ...
}
```

```bash
terraform get      # Download modules
```

---

### 🧪 7. Debugging

```bash
TF_LOG=DEBUG terraform plan
TF_LOG_PATH=./debug.log terraform apply
```

---

### 🔐 8. Useful Flags

| Command              | Purpose                               |
|----------------------|----------------------------------------|
| `-auto-approve`      | Skip approval step                    |
| `-lock=false`        | Don't lock state file                 |
| `-var`               | Override variable                     |
| `-target`            | Apply/destroy specific resource       |

---

## 📚 References

- [Trivy GitHub](https://github.com/aquasecurity/trivy)
- [Terraform CLI Docs](https://developer.hashicorp.com/terraform/cli)
```

---

Would you like a `.zip` or `.md` download for this, or should I prepare it as a GitHub-ready project structure?