# Ultimate Git CLI Cheat Sheet

A comprehensive guide to Git commands for daily use and specific scenarios.

## Table of Contents
- [Configuration](#configuration)
- [Repository Setup](#repository-setup)
- [Basic Commands](#basic-commands)
- [File Status Lifecycle](#file-status-lifecycle)
- [Working with Remotes](#working-with-remotes)
- [Branching and Merging](#branching-and-merging)
- [Commit Management](#commit-management)
- [Undoing Changes](#undoing-changes)
- [Tags](#tags)
- [Git Log and History](#git-log-and-history)
- [Authentication and Security](#authentication-and-security)
- [Advanced Git Commands](#advanced-git-commands)

## Configuration

### User Setup
```bash
# Set username globally
git config --global user.name "Your Name"

# Set email globally
git config --global user.email "your.email@example.com"

# List all configurations
git config --list

# Remove a specific config (like credentials helper)
git config --global --unset credentials.helper
```

### Configuration Levels
```bash
# System-wide configuration
git config --system

# User-level configuration (global)
git config --global

# Repository-specific configuration
git config --local
```

## Repository Setup

### Creating a New Repository
```bash
# Initialize a new Git repository
git init

# Create a new directory and initialize Git
mkdir project-name
cd project-name
git init
```

### Cloning Repositories
```bash
# Clone a repository
git clone https://github.com/username/repository-name.git

# Clone a specific branch
git clone -b branch-name https://github.com/username/repository-name.git

# Clone a repository into a specific directory
git clone https://github.com/username/repository-name.git folder-name
```

## Basic Commands

### Checking Status
```bash
# View the status of your working directory
git status

# Short status output
git status -s
```

### Adding Changes
```bash
# Add a specific file to staging
git add filename.txt

# Add all files in the current directory
git add .

# Add all files (including in subdirectories)
git add --all
# or
git add -A

# Add only modified and deleted files (not new)
git add -u
```

### Committing Changes
```bash
# Commit staged changes with a message
git commit -m "Your commit message here"

# Add all changes and commit in one command
git commit -am "Your commit message here"
```

### Pushing Changes
```bash
# Push to the default remote (origin) and branch (main)
git push

# Push to a specific remote and branch
git push origin main

# Push and set upstream tracking
git push -u origin main

# Force push (use with caution!)
git push --force
```

### Pulling Changes
```bash
# Pull changes from the default remote
git pull

# Pull from a specific remote and branch
git pull origin main

# Pull with rebase instead of merge
git pull --rebase origin main
```

## File Status Lifecycle

Git files go through these states:
1. **Untracked**: New files Git doesn't know about
2. **Tracked**: Files that Git is monitoring
   - **Unmodified**: Tracked files with no changes
   - **Modified**: Tracked files with changes
   - **Staged**: Modified files marked for next commit

```bash
# Check file status
git status

# See what changes are in files
git diff            # Unstaged changes
git diff --staged   # Staged changes
```

## Working with Remotes

### Managing Remote Repositories
```bash
# List all remotes
git remote -v

# Add a remote
git remote add origin https://github.com/username/repo.git

# Add a remote with a different name
git remote add upstream https://github.com/original-owner/repo.git

# Change remote URL
git remote set-url origin https://github.com/username/new-repo.git

# Remove a remote
git remote remove origin

# Using token in remote URL for authentication
git remote set-url origin https://token@github.com/username/repo.git
```

### Fetching and Updating
```bash
# Fetch changes without merging
git fetch origin

# Fetch from all remotes
git fetch --all

# Update local repository to match remote
git fetch origin
git reset --hard origin/main
```

## Branching and Merging

### Basic Branch Commands
```bash
# List all branches
git branch

# List all remote branches
git branch -r

# List all branches (local and remote)
git branch -a

# Create a new branch
git branch branch-name

# Switch to a branch
git checkout branch-name

# Create and switch to a new branch
git checkout -b new-branch-name

# Rename current branch
git branch -M new-name

# Delete a branch (if merged)
git branch -d branch-name

# Force delete a branch (even if not merged)
git branch -D branch-name

# Delete a remote branch
git push origin --delete branch-name
```

### Merging
```bash
# Merge a branch into the current branch
git merge branch-name

# Merge with no fast-forward (creates a merge commit)
git merge --no-ff branch-name

# Abort a merge with conflicts
git merge --abort
```

### Rebasing
```bash
# Rebase current branch onto another
git rebase main

# Interactive rebase
git rebase -i HEAD~3  # Rebase last 3 commits

# Continue rebase after resolving conflicts
git rebase --continue

# Abort rebase
git rebase --abort
```

## Commit Management

### Amending Commits
```bash
# Change the last commit message
git commit --amend -m "New message"

# Add more changes to the last commit
git add forgotten-file.txt
git commit --amend --no-edit
```

### Viewing Commit History
```bash
# View commit history
git log

# Compact log view
git log --oneline

# Graph view
git log --graph --oneline --decorate

# Show changes in each commit
git log -p

# Show stats
git log --stat
```

## Undoing Changes

### Unstaging Files
```bash
# Unstage a file
git restore --staged filename.txt
# or (older syntax)
git reset filename.txt

# Unstage all files
git restore --staged .
# or (older syntax)
git reset
```

### Discarding Changes
```bash
# Discard changes in working directory
git restore filename.txt
# or (older syntax)
git checkout -- filename.txt

# Discard all local changes
git restore .
# or (older syntax)
git checkout -- .
```

### Resetting Commits
```bash
# Soft reset (keep changes, unstage)
git reset --soft HEAD~1  # Reset last commit

# Mixed reset (keep changes, but don't stage)
git reset HEAD~1

# Hard reset (discard all changes)
git reset --hard HEAD~1

# Reset to a specific commit
git reset --hard commit-hash

# Reset to match remote branch
git reset --hard origin/main
```

### Reverting Commits
```bash
# Create a new commit that undoes changes
git revert commit-hash

# Revert multiple commits
git revert older-commit-hash..newer-commit-hash
```

## Tags

### Creating Tags
```bash
# Create a lightweight tag
git tag v1.0.0

# Create an annotated tag with message
git tag -a v1.0.0 -m "Version 1.0.0 release"

# Tag a specific commit
git tag -a v0.9.0 commit-hash -m "Version 0.9.0 beta"
```

### Working with Tags
```bash
# List all tags
git tag

# Show tag details
git show v1.0.0

# Show tag messages
git tag -n

# Delete a local tag
git tag -d v1.0.0

# Push tags to remote
git push origin v1.0.0  # Push specific tag
git push --tags         # Push all tags

# Delete a remote tag
git push origin --delete v1.0.0
```

## Git Log and History

### Advanced Log Commands
```bash
# Search commits by message
git log --grep="bug fix"

# Show commits by author
git log --author="John Doe"

# Show commits between dates
git log --after="2023-01-01" --before="2023-02-01"

# Show commits that changed a specific file
git log -- filename.txt

# Show differences introduced in each commit
git log -p

# Show summary of changes
git log --stat

# Show branching history graphically
git log --graph --oneline --all --decorate
```

### Inspecting Changes
```bash
# Show changes between branches
git diff branch1..branch2

# Show changes in a specific file between branches
git diff branch1..branch2 -- filename.txt

# Show changes introduced by a specific commit
git show commit-hash

# Show who changed each line in a file
git blame filename.txt
```

## Authentication and Security

### Credentials Storage
```bash
# Store credentials in memory temporarily (default: 15 minutes)
git config --global credential.helper cache

# Store credentials for longer (hours)
git config --global credential.helper 'cache --timeout=3600'

# Store credentials on disk
git config --global credential.helper store  # Less secure

# Use credential manager (Windows)
git config --global credential.helper wincred

# Use keychain (macOS)
git config --global credential.helper osxkeychain

# Clear stored credentials
git config --global --unset credential.helper
```

### Working with SSH
```bash
# Generate SSH key
ssh-keygen -t ed25519 -C "your.email@example.com"

# Add SSH key to ssh-agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Use SSH URL for remotes
git remote set-url origin git@github.com:username/repo.git
```

## Advanced Git Commands

### Stashing Changes
```bash
# Stash changes
git stash

# Stash with a message
git stash save "Work in progress on feature X"

# List stashes
git stash list

# Apply most recent stash (keep stash)
git stash apply

# Apply specific stash
git stash apply stash@{2}

# Apply and remove most recent stash
git stash pop

# Remove most recent stash
git stash drop

# Remove specific stash
git stash drop stash@{2}

# Clear all stashes
git stash clear
```

### Cherry-picking
```bash
# Apply specific commit to current branch
git cherry-pick commit-hash

# Cherry-pick without committing
git cherry-pick -n commit-hash
```

### Worktrees
```bash
# Create a new worktree
git worktree add ../path-to-new-worktree branch-name

# List worktrees
git worktree list

# Remove a worktree
git worktree remove ../path-to-worktree
```

### Submodules
```bash
# Add a submodule
git submodule add https://github.com/username/repo.git path/to/submodule

# Initialize submodules after cloning
git submodule init
git submodule update

# Clone repository with submodules
git clone --recurse-submodules https://github.com/username/repo.git

# Update all submodules
git submodule update --remote --merge
```

### Bisect (Finding Bugs)
```bash
# Start bisect
git bisect start

# Mark current commit as bad
git bisect bad

# Mark a known good commit
git bisect good commit-hash

# Mark current commit as good during bisect
git bisect good

# End bisect
git bisect reset
```

### Reflog (Recovery)
```bash
# View reference logs
git reflog

# Recover lost commits
git checkout HEAD@{2}  # Go to specific reflog entry
```

### Git Clean
```bash
# See what would be deleted
git clean -n

# Delete untracked files
git clean -f

# Delete untracked files and directories
git clean -fd

# Remove ignored and untracked files
git clean -fX
```

### Git Hooks
```bash
# View available hooks (in .git/hooks directory)
ls -la .git/hooks

# Make a hook executable
chmod +x .git/hooks/pre-commit
```

### Git Alias
```bash
# Create aliases for complex commands
git config --global alias.st status
git config --global alias.ci "commit -m"
git config --global alias.unstage "reset HEAD --"
git config --global alias.last "log -1 HEAD"
git config --global alias.visual "!gitk"
```

### Git Attributes
```bash
# Create .gitattributes file
echo "*.txt text" > .gitattributes
echo "*.jpg binary" >> .gitattributes
```

### Commit Signing
```bash
# Configure GPG key for signing
git config --global user.signingkey your-gpg-key-id

# Sign commits
git config --global commit.gpgsign true

# Sign individual commit
git commit -S -m "Signed commit message"

# Sign tags
git tag -s v1.0.0 -m "Signed tag"
```

## Tips and Best Practices

1. **Commit often**: Make small, focused commits that address a single issue.
2. **Write meaningful commit messages**: Use clear and descriptive messages.
3. **Pull before push**: Always pull the latest changes before pushing to avoid conflicts.
4. **Create branches**: Use branches for new features or bug fixes.
5. **Don't commit generated files**: Use .gitignore to exclude build artifacts, dependencies, etc.
6. **Review changes before committing**: Use `git diff` to see what you're about to commit.
7. **Keep your local repo clean**: Regularly delete merged branches.
8. **Backup your work**: Push to remote repositories frequently.
9. **Use SSH instead of HTTPS** when possible for more secure authentication.
10. **Learn interactive rebase**: It's powerful for cleaning up commit history.
