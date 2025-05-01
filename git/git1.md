Certainly! Here's an expanded and comprehensive **Git CLI Cheatsheet** in Markdown format, suitable for inclusion in a `README.md` file. This guide covers essential and advanced Git commands, providing a valuable reference for developers at all levels.

---


# 🧠 Git CLI Cheatsheet

A comprehensive guide to Git commands for efficient version control and collaboration.

---

## ⚙️ Configuration

```bash
git config --global user.name "Your Name"           # Set global username
git config --global user.email "you@example.com"    # Set global email
git config --list                                   # List all configurations
git config --global --unset credential.helper       # Unset credential helper
```

---

## 📁 Repository Setup

```bash
git init                                            # Initialize a new Git repository
git clone <repo-url>                                # Clone an existing repository
```

---

## 📂 Directory Navigation

```bash
mkdir <directory>                                   # Create a new directory
cd <directory>                                      # Change into directory
ls                                                  # List files
ls -a                                               # List all files, including hidden
```

---

## 🔄 File States

- **Untracked**: New files not yet tracked by Git
- **Modified**: Tracked files with changes not staged
- **Staged**: Changes marked to be committed
- **Committed**: Changes saved in the repository

```bash
git status                                          # Show the working tree status
git add <file>                                      # Stage a specific file
git add .                                           # Stage all changes in current directory
git add --all                                       # Stage all changes
git reset <file>                                    # Unstage a specific file
git reset                                           # Unstage all files
```

---

## 📝 Committing Changes

```bash
git commit -m "Commit message"                      # Commit staged changes
git commit --amend -m "New message"                 # Amend the last commit
```

---

## 🚀 Pushing and Pulling

```bash
git push origin main                                # Push to the main branch
git push -u origin main                             # Push and set upstream
git pull origin main                                # Pull latest changes from main
git pull --rebase origin main                       # Pull with rebase
```

---

## 🌿 Branching

```bash
git branch                                          # List branches
git branch -a                                       # List all branches (local and remote)
git branch <branch-name>                            # Create a new branch
git branch -d <branch-name>                         # Delete a branch
git branch -M <new-name>                            # Rename current branch
git checkout <branch-name>                          # Switch to a branch
git checkout -b <branch-name>                       # Create and switch to a new branch
git checkout -                                       # Switch to the previous branch
```

---

## 🔁 Merging and Rebasing

```bash
git merge <branch-name>                             # Merge specified branch into current
git rebase <branch-name>                            # Rebase current branch onto specified
```

---

## 🧹 Stashing Changes

```bash
git stash                                           # Stash changes
git stash list                                      # List stashed changes
git stash apply                                     # Apply stashed changes
git stash drop                                      # Drop the latest stash
git stash clear                                     # Clear all stashes
```

---

## 🧭 Remote Repositories

```bash
git remote add origin <repo-url>                    # Add remote repository
git remote -v                                       # List remote repositories
git remote set-url origin <new-url>                 # Change remote URL
git remote remove origin                            # Remove remote
```

---

## 🕵️ Viewing History

```bash
git log                                             # View commit history
git log --oneline                                   # View concise commit history
git log --graph --all --decorate                    # View graphical commit history
git show <commit-hash>                              # Show details of a specific commit
```

---

## 🔍 Comparing Changes

```bash
git diff                                            # Show unstaged changes
git diff --staged                                   # Show staged changes
git diff <branch1>..<branch2>                       # Show differences between branches
```

---

## 🧪 Debugging Tools

```bash
git blame <file>                                    # Show who changed what and when
git bisect start                                    # Start bisecting
git bisect bad                                      # Mark current commit as bad
git bisect good <commit>                            # Mark a known good commit
git bisect reset                                    # End bisecting
```

---

## 🧼 Resetting and Reverting

```bash
git reset <file>                                    # Unstage a file
git reset --hard                                    # Reset working directory and index
git reset --hard <commit-hash>                      # Reset to specific commit
git revert <commit-hash>                            # Revert a specific commit
```

---

## 🏷️ Tagging

```bash
git tag <tagname>                                   # Create a lightweight tag
git tag -a <tagname> -m "Message"                   # Create an annotated tag
git tag                                             # List all tags
git show <tagname>                                  # Show tag details
git tag -d <tagname>                                # Delete a local tag
git push origin <tagname>                           # Push a tag to remote
git push origin --delete <tagname>                  # Delete a remote tag
```

---

## 🧰 Miscellaneous

```bash
git help <command>                                  # Get help for a specific command
git gc                                              # Cleanup unnecessary files and optimize
git fsck                                            # Check repository for errors
git reflog                                          # Show history of HEAD
git cherry-pick <commit>                            # Apply changes from a specific commit
```

---

## 📄 .gitignore

- Create a `.gitignore` file to exclude files from being tracked
- Example entries:
  ```
  node_modules/
  *.log
  .env
  ```

---

## 🔐 Authentication

- Use SSH keys or personal access tokens for authentication
- Example of setting remote with token:
  ```bash
  git remote set-url origin https://<token>@github.com/username/repo.git
  ```

---

## 🧪 Advanced Tools

- **Git Hooks**: Automate tasks with scripts triggered by Git events
- **Git Submodules**: Include external repositories within a repository
- **Git LFS**: Manage large files efficiently

---

> 📝 This cheatsheet provides a comprehensive overview of Git commands for daily development tasks. Keep it handy for quick reference!


