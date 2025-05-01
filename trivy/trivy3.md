# Trivy Terraform CLI Cheatsheet

## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Basic Commands](#basic-commands)
- [Scanning Terraform Files](#scanning-terraform-files)
- [Configuration](#configuration)
- [Filtering Results](#filtering-results)
- [Output Formats](#output-formats)
- [CI/CD Integration](#cicd-integration)
- [Advanced Usage](#advanced-usage)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## Introduction

[Trivy](https://aquasecurity.github.io/trivy/) is a comprehensive security scanner that can scan Terraform files for vulnerabilities and misconfigurations. This cheatsheet provides a quick reference for using Trivy with Terraform infrastructure-as-code (IaC).

## Installation

### Linux
```bash
sudo apt-get install wget apt-transport-https gnupg lsb-release
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy
```

### macOS
```bash
brew install trivy
```

### Windows
```powershell
scoop install trivy
# or
choco install trivy
```

### Docker
```bash
docker pull aquasec/trivy
docker run --rm aquasec/trivy --version
```

## Basic Commands

### Check Trivy Version
```bash
trivy version
```

### Update Vulnerability Database
```bash
trivy --download-db-only
```

### Basic Help
```bash
trivy --help
```

### Command-Specific Help
```bash
trivy config --help
```

## Scanning Terraform Files

### Scan a Single Terraform File
```bash
trivy config main.tf
```

### Scan a Directory of Terraform Files
```bash
trivy config ./terraform-project/
```

### Scan Multiple Directories
```bash
trivy config dir1/ dir2/ dir3/
```

### Scan with Terraform Modules
```bash
trivy config --tf-exclude-downloaded-modules=false ./terraform-project/
```

### Use Specific Terraform Variable Files
```bash
trivy config --tf-vars-file=./terraform.tfvars ./terraform-project/
```

## Configuration

### Config File
```bash
# Use a configuration file
trivy config --config=trivy.yaml ./terraform-project/
```

Example `trivy.yaml`:
```yaml
format: table
exit-code: 1
severity: CRITICAL,HIGH
output: trivy-results.txt
```

### Environment Variables
```bash
# Set severity through environment variable
TRIVY_SEVERITY=HIGH,CRITICAL trivy config ./terraform-project/
```

### Hidden Config Files
Trivy automatically looks for `.trivyignore` file in the scanned directory to exclude specific vulnerabilities.

Example `.trivyignore`:
```
# Ignore specific misconfig ID
AVD-AWS-0001
# Ignore with a comment
AVD-AWS-0002 # This is acceptable in our environment
```

## Filtering Results

### Filter by Severity
```bash
trivy config --severity HIGH,CRITICAL ./terraform-project/
```

### Filter by Security Checks
```bash
trivy config --security-checks vuln,config,secret ./terraform-project/
```

### Filter by Terraform-specific Checks
```bash
trivy config --tf-vars="environment=production,region=us-west-2" ./terraform-project/
```

### Ignore Specified Paths
```bash
trivy config --skip-dirs "modules/,examples/" ./terraform-project/
```

### Ignore Specific Files
```bash
trivy config --skip-files "obsolete.tf,test.tf" ./terraform-project/
```

### Only Show Failed Checks
```bash
trivy config --ignore-unfixed ./terraform-project/
```

## Output Formats

### Table Format (Default)
```bash
trivy config --format table ./terraform-project/
```

### JSON Format
```bash
trivy config --format json ./terraform-project/
```

### SARIF Format (for IDE integration)
```bash
trivy config --format sarif --output results.sarif ./terraform-project/
```

### HTML Format
```bash
trivy config --format template --template "@html.tpl" --output results.html ./terraform-project/
```

### ASFF Format (AWS Security Finding Format)
```bash
trivy config --format asff --output results.asff.json ./terraform-project/
```

### JUnit Format (for test integration)
```bash
trivy config --format junit --output junit-results.xml ./terraform-project/
```

### Custom Templates
```bash
trivy config --format template --template "@custom-template.tpl" ./terraform-project/
```

## CI/CD Integration

### Exit Code for CI Pipelines
```bash
# Exit with code 1 if HIGH or CRITICAL vulnerabilities are found
trivy config --exit-code 1 --severity HIGH,CRITICAL ./terraform-project/
```

### GitLab CI Example
```yaml
terraform-scan:
  image: aquasec/trivy:latest
  script:
    - trivy config --format json --output trivy-results.json --exit-code 1 --severity HIGH,CRITICAL ./terraform-project/
  artifacts:
    paths:
      - trivy-results.json
```

### GitHub Actions Example
```yaml
- name: Scan Terraform files
  uses: aquasecurity/trivy-action@master
  with:
    scan-type: 'config'
    scan-ref: './terraform-project/'
    format: 'sarif'
    output: 'trivy-results.sarif'
    exit-code: '1'
    severity: 'CRITICAL,HIGH'
```

### Jenkins Pipeline Example
```groovy
stage('Security Scan') {
    steps {
        sh 'trivy config --format table --output trivy-results.txt --exit-code 0 ./terraform-project/'
    }
    post {
        always {
            archiveArtifacts artifacts: 'trivy-results.txt', fingerprint: true
        }
    }
}
```

## Advanced Usage

### Show All Details About Detected Misconfigurations
```bash
trivy config --severity HIGH,CRITICAL --debug ./terraform-project/
```

### Check for Secrets in Terraform Files
```bash
trivy config --secret ./terraform-project/
```

### Deep Scan Terraform State
```bash
trivy fs --security-checks secret,config --tf-state ./terraform.tfstate
```

### Cache Management
```bash
# Clear cache
trivy --clear-cache

# Specify cache directory
trivy config --cache-dir /path/to/cache ./terraform-project/
```

### Offline Scanning
```bash
# Download DB for offline use
trivy --download-db-only

# Use offline mode
trivy config --offline-scan ./terraform-project/
```

### Custom Policies with Open Policy Agent (OPA)
```bash
trivy config --policy ./custom-policies/ ./terraform-project/
```

## Best Practices

1. **Include in CI/CD**: Automate scanning in your pipeline
2. **Create Baseline**: Generate an initial scan and address critical issues
3. **Ignore with Caution**: Document reason when ignoring vulnerabilities
4. **Scan Early**: Run scans locally during development
5. **Version Management**: Keep Trivy updated
6. **Custom Policies**: Develop organization-specific policies when needed
7. **Filter Noise**: Focus on high-severity issues first
8. **Include Variables**: Use `--tf-vars` to provide context for scans
9. **Scan State Files**: Periodically check state files for secrets

## Troubleshooting

### Common Issues
- **Version Mismatch**: Make sure to use compatible Trivy versions with your Terraform files
- **Missing Dependencies**: Some scans require additional tools
- **Permissions**: Ensure proper permissions for cache and DB directories
- **Memory Issues**: For large projects, increase available memory

### Debug Mode
```bash
trivy config --debug ./terraform-project/ 2> debug.log
```

### Timeout Issues
```bash
# Increase timeout for large projects
trivy config --timeout 10m ./terraform-project/
```

### Trace Mode for Detailed Analysis
```bash
trivy config --trace ./terraform-project/ 2> trace.log
```