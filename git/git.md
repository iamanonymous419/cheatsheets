Here’s a complete **Git CLI Cheatsheet** written in a structured way for a `README.md` file, covering everything you shared and organized clearly for quick reference:

---

# Git CLI Cheatsheet

## Configuration

```
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
git config --list                      # View current configuration
git config --global --unset credential.helper
```

## File & Directory Basics

```bash
mkdir <dirname>                       # Create a folder
cd <dirname>                          # Change directory
ls                                    # List files
ls -a                                 # Show hidden files (like .git)
```

## Initialize & Clone

```bash
git init                              # Initialize Git in current folder
git clone <repo-url>                  # Clone repository
```

## Remote Repositories

```bash
git remote add origin <repo-url>     # Add remote origin
git remote -v                         # View remote URLs
git remote remove origin              # Remove origin
git remote set-url origin <new-url>  # Update origin URL
```

## Branches

```bash
git branch                            # List branches
git branch -M main                    # Rename current branch to main
git checkout <branch>                 # Switch to existing branch
git checkout -b <new-branch>          # Create and switch to new branch
git branch -d <branch>                # Delete branch
```

## Status & Tracking

```bash
git status                            # Show file status
git log                               # View commit history
git diff                              # Show changes
git diff <branchname>                 # Compare branches
```

### Git File States

- **Untracked**: Git doesn't know the file yet
- **Modified**: Changes made but not staged
- **Staged**: Ready to be committed
- **Committed (Unmodified)**: Saved in history, no changes

Workflow:  
`Untracked → Modified → Staged → Committed → Unmodified`

## Adding & Committing

```bash
git add <filename>                    # Stage a file
git add .                             # Stage all changes in current directory
git add --all                         # Stage all changes (tracked + untracked)

git commit -m "Commit message"       # Commit staged changes
git commit --amend -m "New message"  # Change last commit message
```

## Pushing & Pulling

```bash
git push origin main                  # Push to main branch
git push -u origin main               # Push and set upstream for future use
git push                              # Short push after upstream is set

git pull origin main                  # Pull latest changes
git pull --rebase origin main         # Pull with rebase
```

## Resetting

```bash
git reset                             # Unstage all staged files
git reset <filename>                  # Unstage specific file
git reset HEAD~1                      # Undo last commit (keep changes)
git reset <commit-hash>               # Move HEAD to specific commit
git reset --hard <commit-hash>        # Reset to specific commit and discard all changes
```

## Merging

```bash
git merge <branchname>               # Merge branch into current branch
```

## Tags

### Lightweight Tag

```bash
git tag <tagname>                    # Create lightweight tag
```

### Annotated Tag

```bash
git tag -a <tagname> -m "message"   # Create annotated tag
```

### Push & Delete Tags

```bash
git push --tags                      # Push all tags to remote
git push origin --delete <tagname>  # Delete tag from remote
git tag -d <tagname>                # Delete tag locally
```

### Show & List Tags

```bash
git show <tagname>                  # Show tag details
git tag                             # List tags
git tag -n                          # List tags with messages
```

## Additional Tips

- **Alias remote:**  
  ```bash
  git remote add learn <url>         # Add alias remote
  git push learn main                # Push using alias
  ```

- **Access repo with token:**  
  ```bash
  git remote set-url origin https://<token>@github.com/username/repo.git
  ```

---

> This cheatsheet provides all essential Git CLI commands with clear syntax and comments for daily development tasks. Use it as your quick Git reference!
```

