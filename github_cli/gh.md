Here’s a comprehensive **GitHub CLI Cheat Sheet** to help you master the `gh` command line tool efficiently:

---

## 🧾 GitHub CLI Cheat Sheet

> ✅ Run `gh auth login` first to authenticate with GitHub.

---

### 📁 REPOSITORIES

| Command                             | Description                        |
|-------------------------------------|------------------------------------|
| `gh repo create`                    | Create a new repository            |
| `gh repo clone <user>/<repo>`       | Clone a repository                 |
| `gh repo fork <user>/<repo>`        | Fork a repository                  |
| `gh repo view`                      | View current repo details          |
| `gh repo view --web`                | Open repo in browser               |
| `gh repo list <user>`               | List all user's repositories       |

---

### 🛠️ ISSUES

| Command                             | Description                        |
|-------------------------------------|------------------------------------|
| `gh issue list`                     | List issues                        |
| `gh issue view <number>`            | View a specific issue              |
| `gh issue create`                   | Create a new issue                 |
| `gh issue comment <number>`         | Add comment to issue               |
| `gh issue close <number>`           | Close an issue                     |
| `gh issue reopen <number>`          | Reopen a closed issue              |

---

### 🔀 PULL REQUESTS

| Command                             | Description                        |
|-------------------------------------|------------------------------------|
| `gh pr list`                        | List pull requests                 |
| `gh pr view <number>`               | View a pull request                |
| `gh pr checkout <number>`           | Checkout a PR branch               |
| `gh pr create`                      | Create a new pull request          |
| `gh pr merge <number>`              | Merge a pull request               |
| `gh pr close <number>`              | Close a PR                         |
| `gh pr comment <number>`            | Add a comment to a PR              |

---

### ⚙️ WORKFLOWS / ACTIONS

| Command                             | Description                        |
|-------------------------------------|------------------------------------|
| `gh run list`                       | List recent GitHub Actions runs    |
| `gh run view <run-id>`              | View a specific run                |
| `gh run watch <run-id>`             | Watch the live log                 |
| `gh workflow list`                  | List workflows                     |
| `gh workflow view <name>`           | View a workflow details            |

---

### 📊 PROJECTS

| Command                             | Description                        |
|-------------------------------------|------------------------------------|
| `gh project list`                   | List projects                      |
| `gh project view <name>`            | View a project                     |
| `gh project create`                 | Create a new project               |

---

### 🧠 ALIASES

| Command                             | Description                        |
|-------------------------------------|------------------------------------|
| `gh alias list`                     | List all aliases                   |
| `gh alias set co 'pr checkout'`     | Create shortcut `gh co`            |
| `gh alias delete <alias>`           | Remove an alias                    |

---

### 📦 GISTS

| Command                             | Description                        |
|-------------------------------------|------------------------------------|
| `gh gist list`                      | List gists                         |
| `gh gist view <id>`                 | View a gist                        |
| `gh gist create file.txt`           | Create a gist                      |
| `gh gist delete <id>`               | Delete a gist                      |

---

### 🧰 MISCELLANEOUS

| Command                             | Description                        |
|-------------------------------------|------------------------------------|
| `gh help`                           | Show help                          |
| `gh extension install <name>`       | Install a `gh` extension           |
| `gh upgrade`                        | Upgrade GitHub CLI                 |
