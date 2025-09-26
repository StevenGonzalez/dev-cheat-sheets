# Git Cheat Sheet

## Table of Contents
- [Configuration](#configuration)
- [Repository Initialization](#repository-initialization)
- [Basic Commands](#basic-commands)
- [Branching](#branching)
- [Remote Repositories](#remote-repositories)
- [Viewing History](#viewing-history)
- [Undoing Changes](#undoing-changes)
- [Stashing](#stashing)
- [Advanced Commands](#advanced-commands)
- [Git Aliases](#git-aliases)
- [Tips & Best Practices](#tips--best-practices)

## Configuration

### First-time Setup
```bash
# Set global username and email
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Set default branch name
git config --global init.defaultBranch main

# Set default editor
git config --global core.editor "code --wait"  # VS Code
git config --global core.editor "vim"          # Vim
```

### View Configuration
```bash
# View all config settings
git config --list

# View specific setting
git config user.name
git config user.email
```

## Repository Initialization

### Create New Repository
```bash
# Initialize new repository
git init

# Initialize with specific branch name
git init -b main
```

### Clone Repository
```bash
# Clone repository
git clone <repository-url>

# Clone to specific directory
git clone <repository-url> <directory-name>

# Clone specific branch
git clone -b <branch-name> <repository-url>
```

## Basic Commands

### Status and Information
```bash
# Check repository status
git status

# Short status format
git status -s

# Show current branch
git branch --show-current
```

### Adding and Committing
```bash
# Add specific file
git add <filename>

# Add all changes
git add .

# Add all tracked files
git add -u

# Interactive add
git add -i

# Commit with message
git commit -m "Your commit message"

# Add and commit in one step
git commit -am "Your commit message"

# Amend last commit
git commit --amend
```

## Branching

### Create and Switch Branches
```bash
# Create new branch
git branch <branch-name>

# Switch to branch
git checkout <branch-name>

# Create and switch to new branch
git checkout -b <branch-name>

# Create and switch (newer syntax)
git switch -c <branch-name>

# Switch to existing branch
git switch <branch-name>
```

### Branch Management
```bash
# List all branches
git branch

# List all branches (including remote)
git branch -a

# Delete branch
git branch -d <branch-name>

# Force delete branch
git branch -D <branch-name>

# Rename current branch
git branch -m <new-name>
```

### Merging
```bash
# Merge branch into current branch
git merge <branch-name>

# Create merge commit even for fast-forward
git merge --no-ff <branch-name>

# Abort merge
git merge --abort
```

## Remote Repositories

### Remote Management
```bash
# Add remote repository
git remote add origin <repository-url>

# View remotes
git remote -v

# Remove remote
git remote remove <remote-name>

# Rename remote
git remote rename <old-name> <new-name>
```

### Push and Pull
```bash
# Push to remote
git push origin <branch-name>

# Push and set upstream
git push -u origin <branch-name>

# Push all branches
git push --all

# Pull changes
git pull

# Pull specific branch
git pull origin <branch-name>

# Fetch without merging
git fetch

# Fetch all remotes
git fetch --all
```

## Viewing History

### Log Commands
```bash
# View commit history
git log

# One line per commit
git log --oneline

# Show last n commits
git log -n 5

# Show commits with files changed
git log --stat

# Show commits with diffs
git log -p

# Graphical representation
git log --graph --oneline --decorate --all

# Search commits by message
git log --grep="search term"

# Show commits by author
git log --author="Author Name"
```

### Diff Commands
```bash
# Show unstaged changes
git diff

# Show staged changes
git diff --staged

# Compare branches
git diff <branch1>..<branch2>

# Compare specific files between branches
git diff <branch1>..<branch2> -- <filename>
```

## Undoing Changes

### Unstaging and Reverting
```bash
# Unstage file
git reset HEAD <filename>

# Unstage all files
git reset HEAD

# Discard unstaged changes
git checkout -- <filename>

# Discard all unstaged changes
git checkout -- .

# Restore file (newer syntax)
git restore <filename>

# Unstage file (newer syntax)
git restore --staged <filename>
```

### Reset Commands
```bash
# Soft reset (keep changes staged)
git reset --soft HEAD~1

# Mixed reset (default, unstage changes)
git reset HEAD~1

# Hard reset (discard all changes)
git reset --hard HEAD~1

# Reset to specific commit
git reset --hard <commit-hash>
```

### Revert Commits
```bash
# Revert specific commit
git revert <commit-hash>

# Revert merge commit
git revert -m 1 <merge-commit-hash>
```

## Stashing

### Basic Stashing
```bash
# Stash current changes
git stash

# Stash with message
git stash push -m "Work in progress"

# List stashes
git stash list

# Apply latest stash
git stash apply

# Apply specific stash
git stash apply stash@{0}

# Pop latest stash (apply and remove)
git stash pop

# Drop specific stash
git stash drop stash@{0}

# Clear all stashes
git stash clear
```

### Advanced Stashing
```bash
# Stash including untracked files
git stash -u

# Stash only specific files
git stash push <filename>

# Create branch from stash
git stash branch <branch-name>
```

## Advanced Commands

### Rebasing
```bash
# Rebase current branch onto main
git rebase main

# Interactive rebase
git rebase -i HEAD~3

# Continue rebase after resolving conflicts
git rebase --continue

# Abort rebase
git rebase --abort
```

### Cherry-picking
```bash
# Cherry-pick specific commit
git cherry-pick <commit-hash>

# Cherry-pick multiple commits
git cherry-pick <commit1> <commit2>

# Cherry-pick without committing
git cherry-pick -n <commit-hash>
```

### Tagging
```bash
# Create lightweight tag
git tag <tag-name>

# Create annotated tag
git tag -a <tag-name> -m "Tag message"

# List tags
git tag

# Push tags
git push origin --tags

# Delete tag
git tag -d <tag-name>
git push origin --delete <tag-name>
```

## Git Aliases

Add these to your `.gitconfig` file or use `git config --global alias.<alias-name> '<command>'`:

```bash
# Useful aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

## Tips & Best Practices

### Commit Messages
- Use imperative mood: "Add feature" not "Added feature"
- Keep first line under 50 characters
- Use blank line before detailed description
- Reference issues: "Fix #123: Update user validation"

### Workflow Tips
- Pull before pushing
- Use meaningful branch names
- Keep commits small and focused
- Review changes before committing
- Use `.gitignore` to exclude unnecessary files

### Common .gitignore Patterns
```gitignore
# Dependencies
node_modules/
*.log

# Build outputs
dist/
build/
*.min.js

# Environment files
.env
.env.local

# IDE files
.vscode/
.idea/
*.swp
*.swo

# OS files
.DS_Store
Thumbs.db
```

### Emergency Commands
```bash
# Oh no, I committed to the wrong branch!
git reset HEAD~ --soft
git stash
git checkout correct-branch
git stash pop
git add .
git commit

# I need to remove a file from Git but keep it locally
git rm --cached <filename>

# Undo the last commit but keep changes
git reset --soft HEAD~1
```

### Performance Tips
- Use `git fetch` regularly to stay updated
- Clean up old branches: `git branch -d <branch-name>`
- Use `git gc` occasionally to optimize repository
- Consider using `git worktree` for multiple working directories

---

*Remember: Git is powerful but can be complex. When in doubt, make backups and consult the documentation with `git help <command>`.*