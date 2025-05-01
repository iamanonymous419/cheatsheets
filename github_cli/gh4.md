# GitHub CLI Cheatsheet

A comprehensive guide to using the GitHub Command Line Interface (CLI) tool.

## Table of Contents

- [GitHub CLI Cheatsheet](#github-cli-cheatsheet)
  - [Table of Contents](#table-of-contents)
  - [Getting Started](#getting-started)
  - [Installation](#installation)
  - [Authentication](#authentication)
  - [Repository Commands](#repository-commands)
  - [Pull Request Commands](#pull-request-commands)
  - [Issue Commands](#issue-commands)
  - [Branch Commands](#branch-commands)
  - [Workflow Commands](#workflow-commands)
  - [Actions Commands](#actions-commands)
  - [Release Commands](#release-commands)
  - [Gist Commands](#gist-commands)
  - [Search Commands](#search-commands)
  - [Codespace Commands](#codespace-commands)
  - [Secret Commands](#secret-commands)
  - [SSH Key Commands](#ssh-key-commands)
  - [GPG Key Commands](#gpg-key-commands)
  - [Label Commands](#label-commands)
  - [Project Commands](#project-commands)
  - [Organization Commands](#organization-commands)
  - [Team Commands](#team-commands)
  - [User Commands](#user-commands)
  - [API Commands](#api-commands)
  - [Extension Commands](#extension-commands)
  - [Alias Commands](#alias-commands)
  - [Configuration](#configuration)
  - [Environment Variables](#environment-variables)
  - [Output Formatting](#output-formatting)
  - [Pagination](#pagination)
  - [Troubleshooting](#troubleshooting)

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

# Enable autocomplete for your shell (bash, zsh, fish, PowerShell)
gh completion -s bash > ~/.gh-completion.bash
echo 'source ~/.gh-completion.bash' >> ~/.bashrc
```

## Installation

```bash
# macOS
brew install gh

# Windows
winget install --id GitHub.cli
# or
scoop install gh
# or
choco install gh

# Linux (Debian/Ubuntu)
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh

# Linux (Fedora/RHEL)
sudo dnf install gh

# Linux (Arch)
sudo pacman -S github-cli

# Linux (Alpine)
apk add github-cli
```

## Authentication

```bash
# Login to GitHub
gh auth login

# Login with a specific token
gh auth login --with-token < token.txt

# Login to GitHub Enterprise
gh auth login --hostname enterprise.example.com

# Check auth status
gh auth status

# Refresh auth token
gh auth refresh

# Set GitHub host
gh auth setup-git

# Logout
gh auth logout

# Logout from specific host
gh auth logout --hostname enterprise.example.com
```

## Repository Commands

```bash
# Clone a repository
gh repo clone owner/repo

# Clone a repository to a specific directory
gh repo clone owner/repo path/to/directory

# Create a new repository
gh repo create [name] [flags]

# Create a new public repository
gh repo create --public

# Create a new private repository
gh repo create --private

# Create a new repository from current directory
gh repo create --public --source=. --push

# Create a repository from a template
gh repo create --template=owner/template

# View repository details
gh repo view [repository]

# View repository in web browser
gh repo view [repository] --web

# List repositories
gh repo list [owner]

# List your repositories with specific properties
gh repo list --visibility=public --language=javascript --limit=10

# List starred repositories
gh repo list --starred

# List repositories you contribute to
gh repo list --fork

# Fork a repository
gh repo fork [repository]

# Fork a repository and clone it locally
gh repo fork [repository] --clone

# Archive a repository
gh repo archive [repository]

# Unarchive a repository
gh repo unarchive [repository]

# Delete a repository
gh repo delete [repository]

# Rename a repository
gh repo rename [new-name]

# Add topics to a repository
gh repo edit --add-topic kubernetes,docker

# Set repository visibility
gh repo edit --visibility internal|private|public

# Enable/disable specific features
gh repo edit --enable-issues=false --enable-wiki=true

# Set default branch
gh repo edit --default-branch main

# Create a repository README
gh repo edit --add-readme

# View repository traffic
gh repo traffic [repository]

# Sync a forked repository
gh repo sync
```

## Pull Request Commands

```bash
# Create a pull request
gh pr create

# Create a pull request with title and body
gh pr create --title "Fix bug" --body "This fixes #123"

# Create a pull request and fill details in editor
gh pr create --fill

# Create a pull request for a specific branch
gh pr create --base main --head feature-branch

# Create a draft pull request
gh pr create --draft

# Create a pull request and assign reviewers
gh pr create --reviewer username1,username2

# Create a pull request and add labels
gh pr create --label bug,enhancement

# List pull requests
gh pr list

# List pull requests with specific filters
gh pr list --state=open --assignee=@me --label="bug" --base=main

# List pull requests in JSON format
gh pr list --json number,title,headRefName

# Check out a pull request locally
gh pr checkout {number}

# View a pull request
gh pr view {number}

# View a pull request in browser
gh pr view {number} --web

# View pull request changes
gh pr diff {number}

# Merge a pull request
gh pr merge {number}

# Merge a pull request with a specific method
gh pr merge {number} --merge|--squash|--rebase

# Merge a pull request with a custom commit message
gh pr merge {number} --subject "Custom commit title" --body "Custom body"

# Review a pull request
gh pr review {number} --approve|--comment|--request-changes

# Review a pull request with body
gh pr review {number} --comment -b "Looks good, but consider optimizing"

# Request reviewers for a pull request
gh pr edit {number} --add-reviewer username1,username2

# Add labels to a pull request
gh pr edit {number} --add-label bug,documentation

# Remove labels from a pull request
gh pr edit {number} --remove-label bug

# Set milestone on a pull request
gh pr edit {number} --milestone "v1.0"

# Set assignees for a pull request
gh pr edit {number} --add-assignee username1,username2

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

# Add a code suggestion comment to a pull request
gh pr comment {number} --body "```suggestion
fixed code goes here
```"

# Edit a pull request
gh pr edit {number} --title "New title" --body "Updated description"

# Mark a pull request as ready for review
gh pr ready {number}

# Apply suggested changes from a review
gh pr apply {comment-id}

# Check branch status
gh pr checks {number}

# View CI status for a pull request
gh pr checks {number}

# Wait for CI checks to pass
gh pr checks {number} --watch
```

## Issue Commands

```bash
# Create an issue
gh issue create

# Create an issue with title and body
gh issue create --title "Bug report" --body "Steps to reproduce..."

# Create an issue from a template
gh issue create --template "bug_report.md"

# Create an issue and assign it
gh issue create --assignee @me,username

# Create an issue with labels
gh issue create --label bug,priority

# Create an issue with a milestone
gh issue create --milestone "v1.0"

# Create an issue with a project
gh issue create --project "Project Name"

# List issues
gh issue list

# List issues with specific filters
gh issue list --state=open --assignee=@me --label="bug" --milestone="v1.0"

# List issues created by you
gh issue list --author "@me"

# List issues related to time
gh issue list --created-after="2023-01-01" --created-before="2023-12-31"

# List issues that mention you
gh issue list --mention @me

# View an issue
gh issue view {number}

# View an issue in browser
gh issue view {number} --web

# Edit an issue
gh issue edit {number} --title "Updated title" --body "Updated description"

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

# Remove assignees from an issue
gh issue edit {number} --remove-assignee username1

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
gh issue lock {number} --reason spam|off-topic|too_heated|resolved

# Unlock an issue
gh issue unlock {number}

# List issue comments
gh issue comment list {number}

# Delete a comment
gh issue comment delete {comment-id}

# Edit a comment
gh issue comment edit {comment-id} --body "Updated comment"
```

## Branch Commands

```bash
# List branches
gh api repos/{owner}/{repo}/branches --jq '.[].name'

# Create a branch
gh api repos/{owner}/{repo}/git/refs -f ref="refs/heads/new-branch" -f sha="base-branch-sha"

# Get branch protection rules
gh api repos/{owner}/{repo}/branches/{branch}/protection

# Set branch protection rules
gh api repos/{owner}/{repo}/branches/{branch}/protection --method PUT -f required_status_checks[strict]=true
```

## Workflow Commands

```bash
# List workflows
gh workflow list

# View a workflow
gh workflow view {id|name|filename}

# Run a workflow
gh workflow run {id|name|filename}

# Run a workflow with inputs
gh workflow run {name} -f key=value -f another=value

# Enable a workflow
gh workflow enable {id|name|filename}

# Disable a workflow
gh workflow disable {id|name|filename}

# View workflow runs
gh workflow view {id|name|filename} --view=runs

# List workflow runs
gh run list

# List workflow runs for specific workflow
gh run list --workflow={workflow-name}

# View a specific run
gh run view {id}

# View a run in the browser
gh run view {id} --web

# Download workflow run logs
gh run download {id}

# Watch a run until it completes
gh run watch {id}

# Cancel a workflow run
gh run cancel {id}

# Rerun a failed workflow run
gh run rerun {id}

# Rerun a workflow with failed jobs only
gh run rerun {id} --failed

# List jobs in a run
gh run view {id} --jobs

# View a specific job in a run
gh run view --job={job-id}
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

# List action workflows
gh actions workflows

# List GitHub Actions runners
gh actions runners list

# Add a new runner
gh actions runners add

# Remove a runner
gh actions runners remove {id}

# List secrets
gh actions secrets list

# Set a secret
gh actions secrets set SECRET_NAME --body "secret value"

# Delete a secret
gh actions secrets delete SECRET_NAME
```

## Release Commands

```bash
# Create a release
gh release create v1.0.0

# Create a release with notes
gh release create v1.0.0 --notes "Release notes"

# Create a release with notes from a file
gh release create v1.0.0 --notes-file release-notes.md

# Create a pre-release
gh release create v1.0.0-beta --prerelease

# Create a draft release
gh release create v1.0.0 --draft

# Create a release and upload assets
gh release create v1.0.0 path/to/asset1 path/to/asset2

# List releases
gh release list

# List all releases including drafts
gh release list --limit 100

# View a release
gh release view {tag}

# View a release in browser
gh release view {tag} --web

# Delete a release
gh release delete {tag}

# Download release assets
gh release download {tag}

# Download specific assets
gh release download {tag} --pattern "*.zip" --dir path/to/download

# Upload assets to a release
gh release upload {tag} file1.zip file2.tgz

# Generate release notes automatically
gh release create v1.0.0 --generate-notes

# Create release with specific target
gh release create v1.0.0 --target main
```

## Gist Commands

```bash
# Create a gist
gh gist create file.txt

# Create a gist with description
gh gist create file.txt --desc "My helpful code snippet"

# Create a private gist
gh gist create file.txt --private

# Create a gist from stdin
echo "hello" | gh gist create

# Create a gist from multiple files
gh gist create file1.txt file2.py file3.js

# List your gists
gh gist list

# List all public gists
gh gist list --public

# List someone else's gists
gh gist list {username}

# View a gist
gh gist view {id}

# View a specific file in a gist
gh gist view {id} -f file.txt

# View a gist in browser
gh gist view {id} --web

# Clone a gist locally
gh gist clone {id}

# Clone a gist to a specific directory
gh gist clone {id} path/to/directory

# Edit a gist
gh gist edit {id}

# Update a specific file in a gist
gh gist edit {id} -f file.txt

# Delete a gist
gh gist delete {id}

# Fork a gist
gh gist fork {id}

# Star a gist
gh gist star {id}

# Unstar a gist
gh gist unstar {id}
```

## Search Commands

```bash
# Search for repositories
gh search repos "nodejs framework" --limit 10 --sort stars

# Search repos with specific criteria
gh search repos "game engine" --language=c++ --stars=">1000" --fork=false

# Search for issues
gh search issues "auth bug" --owner=myorg --state=open --limit 20

# Search issues with specific criteria
gh search issues "memory leak" --label=bug --state=open --created=">2023-01-01"

# Search for pull requests
gh search prs "database migration" --label=priority --state=open

# Search pull requests with specific criteria
gh search prs "fix tests" --author=username --merged --base=main

# Search for code
gh search code "function fetchData" --language=javascript

# Search code with specific criteria
gh search code "TODO: fix" --path="src/" --language=python --filename="*.py"

# Search for commits
gh search commits "fix security" --author-email="*@company.com"

# Search for users
gh search users "location:berlin type:user" --limit 10

# Search for topics
gh search topics "machine learning" --limit 15 --sort=repositories

# Search for labels
gh search labels "bug" --repository=owner/repo

# Output search results as JSON
gh search repos "cli tool" --json name,description,stargazers_count
```

## Codespace Commands

```bash
# List your codespaces
gh codespace list

# Create a new codespace
gh codespace create

# Create a codespace for a specific repository
gh codespace create --repo owner/repo

# Create a codespace for a specific branch
gh codespace create --branch feature-branch

# Create a codespace with a specific machine type
gh codespace create --machine medium

# Connect to an existing codespace
gh codespace code [name]

# Delete a codespace
gh codespace delete [name]

# Stop a codespace
gh codespace stop [name]

# SSH into a codespace
gh codespace ssh [name]

# Port forwarding for a codespace
gh codespace ports forward {local-port}:{remote-port} --codespace [name]

# List forwarded ports
gh codespace ports [name]

# View codespace logs
gh codespace logs [name]

# Export a codespace configuration
gh codespace cp [name]:{src-path} {dst-path}

# Import files to a codespace
gh codespace cp {src-path} [name]:{dst-path}

# View codespace info
gh codespace view [name]

# Rename a codespace
gh codespace rename [old-name] [new-name]

# List available machine types
gh codespace machine list
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

# Set an organization secret with specific repositories
gh secret set SECRET_NAME --org=your-org --visibility=selected --repos="repo1,repo2"

# Set a secret for a specific environment
gh secret set SECRET_NAME --env=production --body "secret value"

# List secrets for a specific environment
gh secret list --env=production

# Delete a secret from an environment
gh secret delete SECRET_NAME --env=production
```

## SSH Key Commands

```bash
# List SSH keys in your GitHub account
gh ssh-key list

# Add an SSH key to your GitHub account
gh ssh-key add ~/.ssh/id_ed25519.pub --title "My key"

# Add SSH key from stdin
cat ~/.ssh/id_ed25519.pub | gh ssh-key add --title "Work Laptop"

# Delete an SSH key from your GitHub account
gh ssh-key delete key-id

# Generate an SSH key and add it to GitHub
ssh-keygen -t ed25519 -C "email@example.com" && gh ssh-key add ~/.ssh/id_ed25519.pub --title "New Key"
```

## GPG Key Commands

```bash
# List GPG keys
gh gpg-key list

# Add a GPG key
gh gpg-key add key.asc

# Add a GPG key from stdin
cat key.asc | gh gpg-key add

# Delete a GPG key
gh gpg-key delete key-id
```

## Label Commands

```bash
# List labels in a repository
gh label list

# Create a label
gh label create bug --color FF0000 --description "Something isn't working"

# Clone labels from another repository
gh label clone source-owner/source-repo

# Edit a label
gh label edit bug --color 00FF00 --description "Updated description"

# Delete a label
gh label delete bug

# Delete multiple labels
gh label delete bug feature documentation
```

## Project Commands

```bash
# List projects
gh project list

# List organization projects
gh project list --org=your-org

# View a project
gh project view [number]

# View a project in browser
gh project view [number] --web

# Create a new project
gh project create --title "Project Title" --body "Project Description"

# Create a new organization project
gh project create --org=your-org --title "Org Project"

# Delete a project
gh project delete [number]

# Edit a project
gh project edit [number] --title "New Title" --body "New Description"

# Copy a project
gh project copy [number] --title "Copy of Project"

# Add an issue or PR to a project
gh project item-add [project-number] --issue-id [issue-number]

# List items in a project
gh project item-list [project-number]

# Archive or unarchive a project
gh project archive|unarchive [number]
```

## Organization Commands

```bash
# List organizations you belong to
gh org list

# View organization details
gh org view [org-name]

# List organization members
gh api orgs/{org}/members --jq '.[].login'

# Invite someone to an organization
gh api orgs/{org}/invitations -f email="user@example.com" -f role="direct_member"

# List organization repositories
gh repo list [org-name]

# Create a new repository in an organization
gh repo create [org-name]/[repo-name]

# List organization teams
gh api orgs/{org}/teams --jq '.[].name'

# Create a new team in an organization
gh api orgs/{org}/teams -f name="new-team" -f description="Team description" -f privacy="closed"
```

## Team Commands

```bash
# List teams you're a member of
gh api user/teams --jq '.[].name'

# View team details
gh api orgs/{org}/teams/{team-slug}

# List team members
gh api orgs/{org}/teams/{team-slug}/members --jq '.[].login'

# Add a member to a team
gh api orgs/{org}/teams/{team-slug}/memberships/{username} --method PUT -f role="member"

# Remove a member from a team
gh api orgs/{org}/teams/{team-slug}/memberships/{username} --method DELETE

# List team repositories
gh api orgs/{org}/teams/{team-slug}/repos --jq '.[].name'

# Add a repository to a team
gh api orgs/{org}/teams/{team-slug}/repos/{owner}/{repo} --method PUT -f permission="push"

# Remove a repository from a team
gh api orgs/{org}/teams/{team-slug}/repos/{owner}/{repo} --method DELETE
```

## User Commands

```bash
# View your profile
gh api user

# View someone's profile
gh api users/{username}

# List your followers
gh api user/followers --jq '.[].login'

# List who you're following
gh api user/following --jq '.[].login'

# Follow a user
gh api user/following/{username} --method PUT

# Unfollow a user
gh api user/following/{username} --method DELETE

# Block a user
gh api user/blocks/{username} --method PUT

# Unblock a user
gh api user/blocks/{username} --method DELETE

# List starred repositories
gh api user/starred --jq '.[].full_name'

# Star a repository
gh api user/starred/{owner}/{repo} --method PUT

# Unstar a repository
gh api user/starred/{owner}/{repo} --method DELETE
```

## API Commands

```bash
# Make a custom API request
gh api repos/owner/repo/issues

# Make a custom API request with arguments
gh api repos/owner/repo/issues?state=closed

# Make a custom API POST request with data
gh api repos/owner/repo/issues -f title="Bug report" -f body="There is a bug"

# Make a custom API PATCH request
gh api repos/owner/repo/issues/123 --method PATCH -f state=closed

# Request a different API version
gh api --header "X-GitHub-Api-Version: 2022-11-28" /user

# Output specific fields from JSON response
gh api repos/owner/repo --jq '.name'

# Format the output as table
gh api repos/owner/repo/issues --jq '.[] | {number, title, state}' --template '{{tablerow .number .title .state}}'

# Paginate through results
gh api repos/owner/repo/issues --paginate

# Handle rate limiting
gh api rate_limit
```

## Extension Commands

```bash
# List available extensions
gh extension list

# Browse available extensions
gh extension browse

# Install an extension
gh extension install owner/name

# Upgrade an extension
gh extension upgrade [name]

# Upgrade all extensions
gh extension upgrade --all

# Create a new extension
gh extension create [name]

# Remove an extension
gh extension remove [name]

# Execute an extension
gh [extension-name]
```

## Alias Commands

```bash
# Create custom aliases
gh alias set pv 'pr view'

# Create multi-word aliases
gh alias set bugs 'issue list --label="bug"'

# Create aliases with parameters
gh alias set isu 'issue view $1 --web'

# Create complex aliases with shell commands
gh alias set daily '!gh pr list --author @me --created-after="1 day ago" --json number,title | jq -r ".[] | \"#\(.number) \(.title)\""'

# List aliases
gh alias list

# Delete an alias
gh alias delete pv
```

## Configuration

```bash
# View configuration
gh config get git_protocol

# Set editor
gh config set editor vim

# Set git protocol to use
gh config set git_protocol ssh

# Set browser
gh config set browser firefox

# Set prompt
gh config set prompt enabled

# Enable or disable features
gh config set feature_flag feature_name true|false

# Set a host
gh config set -h github.com git_protocol https

# Set preferred pager
gh config set pager less
```

## Environment Variables

```bash
# Common environment variables
export GH_TOKEN="your-token"              # Authentication token
export GH_ENTERPRISE_TOKEN="your-token"   # GitHub Enterprise authentication token
export GH_HOST="github.com"               # GitHub hostname
export GH_ENTERPRISE_HOST="github.example.com"  # GitHub Enterprise hostname
export GH_REPO="owner/repo"               # Repository to use
export GH_EDITOR="vim"                    # Editor to use
export GH_BROWSER="firefox"               # Browser to use for web commands
export GH_DEBUG="1"                       # Enable debug output
export GH_PAGER="less"                    # Override the pager program
export NO_COLOR="1"                       # Disable color output
export GH_FORCE_TTY="1"                   # Force TTY output
export GH_NO_UPDATE_NOTIFIER="1"          # Disable update checks
```

## Output Formatting

```bash
# Format as JSON
gh issue list --json number,title,body

# Format with templates
gh pr list --json number,title --template '{{range .}}#{{.number}} {{.title}}{{"\n"}}{{end}}'

# Format as CSV
gh issue list --json number,title,state --jq '.[] | [.number, .title, .state] | @csv'

# Format as table
gh pr list --json number,title,headRefName --template \
  '{{tablerow "NUMBER" "TITLE" "BRANCH"}}{{range .}}{{tablerow .number .title .headRefName}}{{end}}'

# Use custom formatting with JQ
gh issue list --json number,title --jq '.[] | "#\(.number): \(.title)"'
```

## Pagination

```bash
# Paginate through results
gh api repos/owner/repo/issues --paginate

# Paginate with a specific page size
gh api repos/owner/repo/issues --paginate --per-page 100

# Paginate with a maximum number of items
gh api repos/owner/repo/issues --paginate --paginate-limit 500
```

## Troubleshooting

```bash
# Enable debug mode
GH_DEBUG=1 gh issue list

# Check GitHub CLI version
gh --version

# Check GitHub API status
gh api https://www.githubstatus.com/api/v2/status.json

# Check authentication status
gh auth status

# Print environment information
gh --version --show-host

# Refresh authentication
gh auth refresh

# Check rate limits
gh api rate_limit
```

For complete documentation, visit: https://cli.github.com/manual/