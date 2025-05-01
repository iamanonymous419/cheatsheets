
# 📘 GitHub CLI Full Cheat Sheet

Master GitHub from your terminal using the `gh` command. This cheat sheet covers **all core topics** and commands supported by GitHub CLI.

---

## ⚙️ Getting Started

```bash
gh auth login           # Authenticate GitHub CLI
gh auth logout          # Log out
gh auth status          # Show current authentication
gh config set <key> <value>  # Set config
gh config get <key>     # Get config
gh version              # Show CLI version
gh help                 # Show CLI help
```

---

## 📁 Repository Commands

```bash
gh repo create                  # Create new repo
gh repo clone <user>/<repo>     # Clone repo
gh repo fork <repo>             # Fork repo
gh repo list <user/org>         # List repos
gh repo view [<repo>]           # View repo info
gh repo edit                    # Edit repo metadata
gh repo archive                 # Archive a repo
gh repo delete <repo>           # Delete a repo
```

---

## 🐛 Issues

```bash
gh issue list                   # List issues
gh issue view <number>          # View issue
gh issue create                 # Create issue
gh issue edit <number>          # Edit issue
gh issue close <number>         # Close issue
gh issue reopen <number>        # Reopen issue
gh issue comment <number>       # Comment on issue
gh issue status                 # Issues assigned to or opened by you
```

---

## 🔀 Pull Requests

```bash
gh pr list                      # List PRs
gh pr view [<number>]           # View PR
gh pr create                    # Create PR
gh pr checkout <number>         # Checkout PR branch
gh pr diff <number>             # Show PR diff
gh pr edit <number>             # Edit PR
gh pr merge <number>            # Merge PR
gh pr close <number>            # Close PR
gh pr reopen <number>           # Reopen PR
gh pr comment <number>          # Comment on PR
gh pr status                    # Show current repo PR activity
```

---

## ⚡ GitHub Actions (Workflows)

```bash
gh run list                     # List runs
gh run view <id>                # View run
gh run watch <id>               # Stream logs
gh run download <id>            # Download artifacts
gh workflow list                # List workflows
gh workflow view <name>         # View workflow
gh workflow run <name>          # Trigger workflow
```

---

## 📊 Projects (Beta or Classic)

```bash
gh project list                 # List projects
gh project view <name/id>       # View project
gh project create               # Create project
gh project edit <name/id>       # Edit project
gh project delete <name/id>     # Delete project
```

---

## 🧰 Gists

```bash
gh gist list                    # List gists
gh gist view <id>               # View gist
gh gist create <file>           # Create gist
gh gist edit <id>               # Edit gist
gh gist delete <id>             # Delete gist
```

---

## 🔌 Extensions

```bash
gh extension list               # List extensions
gh extension install <repo>     # Install extension
gh extension upgrade <repo>     # Upgrade extension
gh extension remove <repo>      # Remove extension
```

---

## 🧠 Aliases

```bash
gh alias list                   # List aliases
gh alias set <name> <cmd>       # Set alias
gh alias delete <name>          # Delete alias
```

---

## 📄 Releases

```bash
gh release list                 # List releases
gh release view <tag>           # View release
gh release create <tag>         # Create release
gh release edit <tag>           # Edit release
gh release delete <tag>         # Delete release
```

---

## 📎 Markdown & Output

```bash
gh <command> --json <fields>    # Output JSON
gh <command> --jq <jq-query>    # Parse with jq
gh <command> --template <tpl>   # Output with Go template
```

---

## 🔐 SSH & Auth Helpers

```bash
gh ssh-key add <path> --title <title>    # Add SSH key
gh auth login --with-token               # Login using token
```

---

## 🧪 Misc Commands

```bash
gh label list                    # List labels
gh label create <name>           # Create label
gh label delete <name>           # Delete label

gh codespace list                # List codespaces
gh codespace create              # Create codespace
gh codespace delete              # Delete codespace
```

---

## 📚 Resources

- [Official Docs](https://cli.github.com/manual)
- [gh GitHub Repo](https://github.com/cli/cli)
- [Explore Extensions](https://github.com/topics/gh-extension)

---

## ✅ Tip: Use --help with any command

```bash
gh issue create --help
gh pr merge --help
```

This gives full details, flags, and examples.
