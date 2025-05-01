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
- [Git Ignore](#git-ignore)
- [Git Diff](#git-diff)
- [Git Revert](#git-revert)
- [Git Workflow Strategies](#git-workflow-strategies)
- [Troubleshooting](#troubleshooting)
- [Git Large File Storage (LFS)](#git-large-file-storage-lfs)
- [Sparse Checkout](#sparse-checkout)
- [Git Internals](#git-internals)
- [Git Patch](#git-patch)
- [Collaboration](#collaboration)
- [Git Tools and Extensions](#git-tools-and-extensions)

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

## Git Ignore

### Basic .gitignore
```bash
# Create a .gitignore file
touch .gitignore

# Common patterns for .gitignore
# Ignore specific file
filename.txt

# Ignore all files with extension
*.log
*.tmp

# Ignore specific directory
/node_modules/
/build/
/dist/

# Ignore all files in a directory but keep the directory
logs/*
!logs/.gitkeep

# Negate a pattern
!important.log

# Ignore files with specific patterns
**/debug.log
```

### Global .gitignore
```bash
# Create a global .gitignore for all repositories
git config --global core.excludesfile ~/.gitignore_global

# Edit global gitignore
nano ~/.gitignore_global
```

### Ignoring Tracked Files
```bash
# Stop tracking a file but keep it locally
git rm --cached filename.txt

# Stop tracking a directory
git rm -r --cached directory/
```

## Git Diff

### Advanced Diff Commands
```bash
# Show changes in working directory since last commit
git diff

# Show staged changes
git diff --staged
# or
git diff --cached

# Show diff for specific file
git diff -- path/to/file

# Show diff between two commits
git diff commit1..commit2

# Show diff between current branch and another branch
git diff branch1..branch2

# Show diff with summary only
git diff --summary

# Show word-by-word diff instead of line-by-line
git diff --word-diff

# Show unified diff with more context lines
git diff -U5

# Show diff with color
git diff --color-words

# Show just filenames that changed
git diff --name-only

# Show summary of insertions and deletions
git diff --stat

# Compare branches showing only changes in specific directory
git diff branch1..branch2 -- path/to/directory
```

### External Diff Tools
```bash
# Configure external diff tool
git config --global diff.tool <tool>  # e.g., vimdiff, meld, kdiff3

# Launch external diff tool
git difftool

# Launch specific diff tool
git difftool -t meld
```

## Git Revert

### Reverting Commits in Detail
```bash
# Revert a commit (creates new commit that undoes changes)
git revert commit-hash

# Revert without automatic commit (stage changes only)
git revert --no-commit commit-hash

# Revert a merge commit (must specify parent)
git revert -m 1 merge-commit-hash

# Revert multiple commits
git revert commit1^..commit2

# Abort a revert operation
git revert --abort

# Continue a revert operation after resolving conflicts
git revert --continue

# Skip current revert in a multi-revert operation
git revert --skip
```

## Git Workflow Strategies

### Git Flow
```bash
# Initialize Git Flow
git flow init

# Start a new feature
git flow feature start feature_name

# Finish a feature
git flow feature finish feature_name

# Start a release
git flow release start 1.0.0

# Finish a release
git flow release finish 1.0.0

# Start a hotfix
git flow hotfix start hotfix_name

# Finish a hotfix
git flow hotfix finish hotfix_name
```

### GitHub Flow
```bash
# Create a feature branch
git checkout -b feature-name

# Push branch to remote
git push -u origin feature-name

# Create Pull Request (via GitHub interface)

# After PR is merged, delete branch
git branch -d feature-name
git push origin --delete feature-name
```

### Trunk-Based Development
```bash
# Get latest from main/trunk
git checkout main
git pull

# Create short-lived feature branch
git checkout -b quick-feature

# Merge to main frequently
git checkout main
git merge quick-feature
git push

# Or use rebase to maintain linear history
git checkout quick-feature
git rebase main
git checkout main
git merge quick-feature
git push
```

## Troubleshooting

### Common Issues
```bash
# Fix "fatal: refusing to merge unrelated histories"
git pull origin main --allow-unrelated-histories

# Fix detached HEAD state
git checkout branch-name

# Fix conflict markers in files after failed merge
git checkout --ours path/to/file  # Keep your changes
git checkout --theirs path/to/file  # Keep their changes
git add path/to/file  # Mark as resolved

# Recover lost commits
git reflog
git checkout commit-hash

# Fix "error: failed to push some refs"
git pull --rebase origin main
git push origin main

# Fix credentials issues
git config --global credential.helper store

# Reset file permissions changes
git config core.fileMode false

# Fix line ending issues
git config --global core.autocrlf true  # Windows
git config --global core.autocrlf input  # Mac/Linux
```

### Repository Maintenance
```bash
# Check repository for corruption
git fsck

# Optimize repository
git gc

# Aggressive optimization
git gc --aggressive

# Remove unreachable objects
git prune

# Clean and optimize in one command
git gc --prune=now

# Verify objects in database
git fsck --full

# Recover corrupted objects
git fsck --lost-found
```

## Git Large File Storage (LFS)

### Setup and Basic Commands
```bash
# Install Git LFS
# (varies by system, e.g., apt-get install git-lfs, brew install git-lfs)

# Initialize Git LFS
git lfs install

# Track large file types
git lfs track "*.psd"
git lfs track "*.zip"

# Check tracked patterns
git lfs track

# Add .gitattributes after tracking
git add .gitattributes

# Clone repository with LFS content
git lfs clone https://github.com/username/repo.git

# Pull with LFS content
git lfs pull

# Check LFS status
git lfs status
```

### Advanced LFS Commands
```bash
# List all LFS objects
git lfs ls-files

# Fetch LFS objects
git lfs fetch

# Fetch specific LFS files
git lfs fetch --include="path/to/file"

# Prune old LFS objects
git lfs prune

# Migrate normal Git files to LFS
git lfs migrate import --include="*.psd" --everything
```

## Sparse Checkout

### Basic Sparse Checkout
```bash
# Initialize sparse checkout
git sparse-checkout init

# Set which directories/files to include
git sparse-checkout set "directory1/" "directory2/file.txt"

# List sparse checkout patterns
git sparse-checkout list

# Disable sparse checkout
git sparse-checkout disable
```

### Advanced Sparse Checkout
```bash
# Clone with sparse checkout
git clone --no-checkout https://github.com/username/repo.git
cd repo
git sparse-checkout init --cone
git sparse-checkout set "directory1" "directory2"
git checkout main

# Add more directories later
git sparse-checkout add "directory3"

# Sparse checkout with depth limit
git clone --depth=1 --filter=blob:none --sparse https://github.com/username/repo.git
cd repo
git sparse-checkout set "directory1" "directory2"
```

## Git Internals

### Objects and References
```bash
# Show contents of a blob
git cat-file -p blob-hash

# Show type of an object
git cat-file -t object-hash

# List all objects
git rev-list --objects --all

# Show content of a tree object
git ls-tree tree-hash

# Examine object database
git count-objects -v

# Verify all objects
git fsck

# List all references
git show-ref

# Show symbolic references
git symbolic-ref HEAD
```

### Low-level Commands
```bash
# Create a tree object from index
git write-tree

# Create a commit object
git commit-tree tree-hash -m "Message" -p parent-hash

# Create a blob object
echo "content" | git hash-object -w --stdin

# Update index with file
git update-index --add --cacheinfo 100644 blob-hash filename

# Pack objects
git pack-objects --stdout > pack-file

# Unpack objects
git unpack-objects < pack-file
```

## Git Patch

### Creating and Applying Patches
```bash
# Create a patch for the last commit
git format-patch -1

# Create patches for a range of commits
git format-patch -3  # Last 3 commits
git format-patch master..feature-branch  # All commits in feature branch not in master

# Create patch with binary files
git format-patch --binary -1

# Apply a patch file
git apply patch-file.patch

# Apply a patch as a commit (with author info)
git am patch-file.patch

# Apply a series of patches
git am *.patch

# Check if a patch applies cleanly
git apply --check patch-file.patch

# Apply with more context
git apply -C3 patch-file.patch

# Apply with fallback to 3-way merge
git am --3way patch-file.patch
```

### Email Patches
```bash
# Send patches by email (requires setup)
git send-email *.patch

# Create patch with cover letter
git format-patch -n --cover-letter

# Sign-off patches
git format-patch --signoff -1
```

## Collaboration

### Code Review Commands
```bash
# Show last commit
git show

# Show changes in specific commit
git show commit-hash

# Show specific file in a commit
git show commit-hash:path/to/file

# Review changes since branching
git log --no-merges master..feature-branch

# Find author of specific lines
git blame -L 10,20 filename

# Find who changed what and when in a file
git log -p filename

# Show statistics for changes
git shortlog -sn --all  # All commits by author
git shortlog -sn --since="1 month ago"  # Recent commits by author
```

### Pull Requests (GitHub CLI)
```bash
# Install GitHub CLI (gh)
# Create a pull request
gh pr create --title "Title" --body "Description"

# List pull requests
gh pr list

# Check out a pull request locally
gh pr checkout PR-number

# Review a pull request
gh pr review PR-number --approve
gh pr review PR-number --comment -b "Comment"
gh pr review PR-number --request-changes -b "Changes needed"
```

### Forks and Upstreams
```bash
# Add upstream remote
git remote add upstream https://github.com/original-owner/repo.git

# Fetch from upstream
git fetch upstream

# Merge from upstream
git merge upstream/main

# Update fork and keep changes
git checkout main
git pull upstream main
git push origin main
```

## Git Tools and Extensions

### Git GUI Clients
- **GitKraken**: `gitkraken --path /path/to/repo`
- **Sourcetree**: `sourcetree -r /path/to/repo`
- **GitHub Desktop**: `github /path/to/repo`
- **Git GUI** (built-in): `git gui`
- **Gitk** (built-in): `gitk --all`

### Git Extensions
```bash
# Git Flow
git flow feature start new-feature

# Git LFS
git lfs install
git lfs track "*.psd"

# Git Subtree
git subtree add --prefix=lib/dependency https://github.com/user/dependency.git main --squash

# Git Filter-repo (requires installation)
git filter-repo --path path/to/file --invert-paths  # Remove file from history

# Git Credential Manager
git credential-manager install

# Git Absorb (requires installation)
git absorb  # Automatically fixup commits
```

### Git Aliases and Scripts
```bash
# Set up useful aliases
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
git config --global alias.please 'push --force-with-lease'
git config --global alias.commend 'commit --amend --no-edit'
git config --global alias.stash-all 'stash save --include-untracked'
git config --global alias.aliases "config --get-regexp ^alias\."
```

## Tips and Best Practices

1. **Commit often**: Make small, focused commits that address a single issue.
2. **Write meaningful commit messages**: Use clear and descriptive messages.
3. **Follow commit message conventions**: Consider using formats like Conventional Commits (feat:, fix:, docs:, etc.).
4. **Pull before push**: Always pull the latest changes before pushing to avoid conflicts.
5. **Create branches**: Use branches for new features or bug fixes.
6. **Don't commit generated files**: Use .gitignore to exclude build artifacts, dependencies, etc.
7. **Review changes before committing**: Use `git diff` to see what you're about to commit.
8. **Keep your local repo clean**: Regularly delete merged branches.
9. **Backup your work**: Push to remote repositories frequently.
10. **Use SSH instead of HTTPS** when possible for more secure authentication.
11. **Learn interactive rebase**: It's powerful for cleaning up commit history.
12. **Squash related commits**: Use `git rebase -i` to combine related commits before merging.
13. **Use feature flags**: Hide incomplete features in production while still integrating code.
14. **Set up CI/CD**: Automate testing and deployment for every commit.
15. **Document branch strategy**: Create guidelines for your team about branch naming and workflow.
16. **Avoid large binary files**: Use Git LFS for large files or keep them out of the repository.
17. **Protect your main branch**: Set up branch protection rules to require reviews.
18. **Rebase instead of merge** to maintain a linear, clean history where appropriate.
19. **Use meaningful branch names**: Include feature description or ticket numbers in branch names.
20. **Configure global gitignore**: For editor files, OS files, and personal settings.
