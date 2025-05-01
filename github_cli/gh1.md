# GitHub CLI Cheatsheet

A comprehensive guide to using the GitHub Command Line Interface (CLI) tool.

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

# Create a new repository with a custom name from the current directory
gh repo create [new-repo-name] --public --source=. --push

# Create a new public repository with description from current directory
gh repo create new-repo-name --public --source=. --push --description "Your description here"

# View repository details
gh repo view [repository]

# View repository in web browser
gh repo view [repository] --web

# List repositories for a user or organization
gh repo list [owner] --limit 100

# Fork a repository
gh repo fork [repository]

# Edit repository settings
gh repo edit --description "New description"
gh repo edit --homepage "https://example.com"
gh repo edit --visibility private|public|internal
gh repo edit --default-branch main

# Delete a repository
gh repo delete owner/repo

# Archive a repository
gh repo archive

# Unarchive a repository
gh repo unarchive

# Mirror (copy) a repository
gh repo create new-repo --template owner/template-repo

# Set topics (tags) for the repository
gh repo edit --add-topic topic1 --add-topic topic2

# Remove a topic from repository
gh repo edit --remove-topic old-topic

# List contributors (via REST API + jq)
gh api repos/owner/repo/contributors | jq '.[].login'

# Enable/disable issues and wiki
gh repo edit --enable-issues=false
gh repo edit --enable-wiki=false
```

## Pull Request Commands

```bash
# Create a pull request
gh pr create

# List pull requests
gh pr list

# Check out a pull request locally
gh pr checkout {number}

# View a pull request
gh pr view {number}

# View a pull request in browser
gh pr view {number} --web

# Merge a pull request
gh pr merge {number}

# Review a pull request
gh pr review {number} --approve|--comment|--request-changes

# Close a pull request
gh pr close {number}

# Reopen a pull request
gh pr reopen {number}

# Check pull request status
gh pr status
```

## Issue Commands

```bash
# Create an issue
gh issue create

# List issues
gh issue list

# View an issue
gh issue view {number}

# View an issue in browser
gh issue view {number} --web

# Close an issue
gh issue close {number}

# Reopen an issue
gh issue reopen {number}

# Add a comment to an issue
gh issue comment {number} --body "comment body"
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

# Download workflow run logs
gh run download {id}
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

## Environment Variables

- `GH_TOKEN` - Authentication token
- `GH_REPO` - Repository to use
- `GH_ENTERPRISE_TOKEN` - GitHub Enterprise authentication token
- `GH_ENTERPRISE_HOST` - GitHub Enterprise hostname
- `GH_HOST` - GitHub hostname
- `GH_EDITOR` - Editor to use

For complete documentation, visit: https://cli.github.com/manual/