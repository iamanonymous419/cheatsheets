Here’s an expanded version of the GitHub CLI Cheat Sheet in **README.md** format with detailed explanations and examples. You can copy and paste this into a `README.md` file:

---

# 📘 GitHub CLI Cheat Sheet

Master GitHub's command line tool with this comprehensive guide to `gh`, organized by category for quick reference and practical usage.

---

## ⚙️ Getting Started

```bash
gh auth login         # Authenticate with GitHub
gh version            # Check installed version
gh help               # General help
```

---

## 📁 Repositories

### Create a Repository
```bash
gh repo create
```
Interactive setup: prompts for name, visibility, and remote setup.

### Clone a Repository
```bash
gh repo clone user/repo-name
```

### Fork a Repository
```bash
gh repo fork user/repo-name
```

### View Repository Info
```bash
gh repo view          # In current directory
gh repo view user/repo-name --web
```

### List Repositories
```bash
gh repo list user --limit 10
```

---

## 🐞 Issues

### List Issues
```bash
gh issue list
gh issue list --label "bug" --state open
```

### View an Issue
```bash
gh issue view 123
```

### Create an Issue
```bash
gh issue create --title "Bug Found" --body "Details here" --label "bug"
```

### Comment on an Issue
```bash
gh issue comment 123 --body "Working on this!"
```

### Close or Reopen
```bash
gh issue close 123
gh issue reopen 123
```

---

## 🔀 Pull Requests (PRs)

### List Pull Requests
```bash
gh pr list
gh pr list --state open --author "@me"
```

### View PR Details
```bash
gh pr view 45
gh pr view 45 --web
```

### Create a PR
```bash
gh pr create --base main --head feature-branch --title "Add login" --body "Implements login feature"
```

### Checkout a PR
```bash
gh pr checkout 45
```

### Comment on a PR
```bash
gh pr comment 45 --body "Great work!"
```

### Merge a PR
```bash
gh pr merge 45 --merge     # Use --squash or --rebase for other strategies
```

### Close a PR
```bash
gh pr close 45
```

---

## ⚡ GitHub Actions

### List Workflow Runs
```bash
gh run list
```

### View a Workflow Run
```bash
gh run view 987654321
```

### Stream a Run Log (Live Output)
```bash
gh run watch 987654321
```

### List Workflows
```bash
gh workflow list
```

### View Workflow Details
```bash
gh workflow view "CI"
```

---

## 📊 GitHub Projects

### List Projects
```bash
gh project list
```

### View a Project
```bash
gh project view "My Project"
```

### Create a Project
```bash
gh project create --title "My Project" --format beta
```

---

## 🧰 Gists

### List Gists
```bash
gh gist list
```

### View a Gist
```bash
gh gist view <gist-id> --web
```

### Create a Gist
```bash
gh gist create file.txt --public --desc "My snippet"
```

### Delete a Gist
```bash
gh gist delete <gist-id>
```

---

## 🧠 Aliases

Simplify repetitive commands.

### Create an Alias
```bash
gh alias set co 'pr checkout'
gh co 123     # Same as `gh pr checkout 123`
```

### List Aliases
```bash
gh alias list
```

### Delete an Alias
```bash
gh alias delete co
```

---

## 🔌 Extensions

Enhance the CLI with community extensions.

### List Extensions
```bash
gh extension list
```

### Install an Extension
```bash
gh extension install <owner>/<repo>
```

### Use an Installed Extension
```bash
gh <extension-name>
```

---

## 🧪 JSON + jq (Advanced)

Use structured JSON output and `jq` for scripting.

```bash
gh issue list --json number,title,state \
  --jq '.[] | select(.state=="OPEN") | "\(.number): \(.title)"'
```

---

## 🆙 Upgrade GitHub CLI

```bash
gh upgrade
```

---

## 📎 Tips

- Use `--web` to open any resource in the browser.
- Use `--help` with any command for flags and examples.
  ```bash
  gh pr create --help
  ```
- Combine with shell scripting for automation.

---

## ✅ Example Daily Workflow

```bash
# Start your day
gh pr list
gh issue list

# Work on an issue
gh issue view 101
gh issue comment 101 --body "Starting work on this."

# Push changes and create PR
gh pr create --base main --head fix-issue101 --title "Fix: Issue #101"
```

---

## 📚 Official Resources

- 📖 [GitHub CLI Docs](https://cli.github.com/manual/)
- 📄 [GitHub CLI Release Notes](https://github.com/cli/cli/releases)
- 🧩 [Community Extensions](https://github.com/topics/gh-extension)

