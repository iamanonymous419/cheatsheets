# GitHub CLI Cheatsheet

A comprehensive guide to using the GitHub Command Line Interface (CLI) tool.

## Getting Started

```bash
# Check GitHub CLI version
gh --version

# Show general help
gh help

# Show help for a specific command
gh <command> --help

# Display GitHub CLI environment info
gh --version --show-host
```

## Installation

```bash
# macOS
brew install gh

# Windows
winget install --id GitHub.cli

# Linux (Debian/Ubuntu)
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh
```

## Authentication

```bash
# Login to GitHub
gh auth login

# Check auth status
gh auth status

# Logout
gh auth logout
```

## Repository Commands

```bash
# Clone a repository
gh repo clone owner/repo

# Create a new repository
gh repo create [name] [flags]

# Create a new repository from current directory
gh repo create --public --source=. --push

# View repository details
gh repo view [repository]

# View repository in web browser
gh repo view [repository] --web

# List repositories
gh repo list [owner]

# Fork a repository
gh repo fork [repository]
```

## Pull Request Commands

```bash
# Create a pull request
gh pr create

# Create a pull request with title and body
gh pr create --title "Fix bug" --body "This fixes #123"

# Create a draft pull request
gh pr create --draft

# List pull requests
gh pr list

# List pull requests with specific filters
gh pr list --state=open --assignee=@me --label="bug" --base=main

# Check out a pull request locally
gh pr checkout {number}

# View a pull request
gh pr view {number}

# View a pull request in browser
gh pr view {number} --web

# Merge a pull request
gh pr merge {number}

# Merge a pull request with a specific method
gh pr merge {number} --merge|--squash|--rebase

# Review a pull request
gh pr review {number} --approve|--comment|--request-changes

# Request reviewers for a pull request
gh pr edit {number} --add-reviewer username1,username2

# Add labels to a pull request
gh pr edit {number} --add-label bug,documentation

# Close a pull request
gh pr close {number}

# Reopen a pull request
gh pr reopen {number}

# Check pull request status
gh pr status

# Diff a pull request
gh pr diff {number}

# Check out PR branch and show diff
gh pr checkout {number} && gh pr diff

# List pull request comments
gh pr comment list {number}

# Add a comment to a pull request
gh pr comment {number} --body "Looking good!"

# Edit a pull request
gh pr edit {number} --title "New title" --body "Updated description"

# Mark a pull request as ready for review
gh pr ready {number}
```

## Issue Commands

```bash
# Create an issue
gh issue create

# Create an issue with title and body
gh issue create --title "Bug report" --body "Steps to reproduce..."

# Create an issue from a template
gh issue create --template "bug_report.md"

# List issues
gh issue list

# List issues with specific filters
gh issue list --state=open --assignee=@me --label="bug" --milestone="v1.0"

# List issues created by you
gh issue list --author "@me"

# View an issue
gh issue view {number}

# View an issue in browser
gh issue view {number} --web

# Close an issue
gh issue close {number}

# Close multiple issues
gh issue close {number1} {number2} {number3}

# Reopen an issue
gh issue reopen {number}

# Add a comment to an issue
gh issue comment {number} --body "comment body"

# Add assignees to an issue
gh issue edit {number} --add-assignee username1,username2

# Add labels to an issue
gh issue edit {number} --add-label bug,documentation

# Remove labels from an issue
gh issue edit {number} --remove-label bug

# Set milestone on an issue
gh issue edit {number} --milestone "v1.0"

# Transfer an issue to another repository
gh issue transfer {number} owner/repo

# Pin an issue
gh issue pin {number}

# Unpin an issue
gh issue unpin {number}

# Lock an issue
gh issue lock {number} --reason spam

# Unlock an issue
gh issue unlock {number}
```

## Gist Commands

```bash
# Create a gist
gh gist create file.txt

# Create a gist from stdin
echo "hello" | gh gist create

# List your gists
gh gist list

# View a gist
gh gist view {id}

# Clone a gist locally
gh gist clone {id}
```

## Release Commands

```bash
# Create a release
gh release create v1.0.0

# List releases
gh release list

# View a release
gh release view {tag}

# Download release assets
gh release download {tag}

# Upload assets to a release
gh release upload {tag} file1.zip file2.tgz
```

## Workflow Commands

```bash
# List workflows
gh workflow list

# View a workflow
gh workflow view {id|name|filename}

# Run a workflow
gh workflow run {id|name|filename}

# View workflow runs
gh workflow view {id|name|filename} --view=runs

# List workflow runs
gh run list

# View a specific run
gh run view {id}

# Download workflow run logs
gh run download {id}

# Watch a run until it completes
gh run watch {id}

# Cancel a workflow run
gh run cancel {id}

# Rerun a failed workflow run
gh run rerun {id}
```

## Actions Commands

```bash
# List all available actions
gh actions cache list

# View details of a specific cache
gh actions cache view {id}

# Delete a cache
gh actions cache delete {id}

# Run a custom action
gh actions run action-name [flags]
```

## Alias Commands

```bash
# Create custom aliases
gh alias set pv 'pr view'

# List aliases
gh alias list

# Delete an alias
gh alias delete pv
```

## Configuration

```bash
# Set editor
gh config set editor vim

# Set git protocol to use
gh config set git_protocol ssh

# Set browser
gh config set browser firefox
```

## Additional Tips

- Most commands accept a `--help` flag for more information
- Use `--json` flag with many commands to output in JSON format
- Use `--web` with many commands to open the GitHub web interface

## Search Commands

```bash
# Search for repositories
gh search repos "nodejs framework" --limit 10 --sort stars

# Search for issues
gh search issues "auth bug" --owner=myorg --state=open --limit 20

# Search for pull requests
gh search prs "database migration" --label=priority --state=open

# Search for code
gh search code "function fetchData" --language=javascript
```

## Codespace Commands

```bash
# List your codespaces
gh codespace list

# Create a new codespace
gh codespace create

# Connect to an existing codespace
gh codespace code [name]

# Delete a codespace
gh codespace delete [name]

# Stop a codespace
gh codespace stop [name]

# SSH into a codespace
gh codespace ssh [name]
```

## Secret Commands

```bash
# Set a repository secret
gh secret set SECRET_NAME --body "secret value"

# Set a repository secret from a file
gh secret set SECRET_FILE < file.txt

# List repository secrets
gh secret list

# Delete a repository secret
gh secret delete SECRET_NAME

# Set an organization secret
gh secret set SECRET_NAME --org=your-org --body "secret value"
```

## SSH Key Commands

```bash
# List SSH keys in your GitHub account
gh ssh-key list

# Add an SSH key to your GitHub account
gh ssh-key add ~/.ssh/id_ed25519.pub --title "My key"

# Delete an SSH key from your GitHub account
gh ssh-key delete key-id
```

## Project Commands

```bash
# List projects
gh project list

# View a project
gh project view [number]

# Create a new project
gh project create --title "Project Title" --body "Project Description"

# Delete a project
gh project delete [number]
```

## API Commands

```bash
# Make a custom API request
gh api repos/owner/repo/issues

# Make a custom API POST request with data
gh api repos/owner/repo/issues -f title="Bug report" -f body="There is a bug"

# Request a different API version
gh api --header "X-GitHub-Api-Version: 2022-11-28" /user

# Output specific fields from JSON response
gh api repos/owner/repo --jq '.name'
```

## Environment Variables

- `GH_TOKEN` - Authentication token
- `GH_REPO` - Repository to use
- `GH_ENTERPRISE_TOKEN` - GitHub Enterprise authentication token
- `GH_ENTERPRISE_HOST` - GitHub Enterprise hostname
- `GH_HOST` - GitHub hostname
- `GH_EDITOR` - Editor to use
- `GH_BROWSER` - Browser to use for web commands
- `GH_DEBUG` - Enable debug output (set to any value)
- `GH_PAGER` - Override the pager program
- `NO_COLOR` - Disable color output

For complete documentation, visit: https://cli.github.com/manual/