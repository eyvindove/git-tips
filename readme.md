# Git Tips

This repository is used to note some git commands down which are frequently used.

[Git Document Reference Manual](https://git-scm.com/docs)

If you like this tips, don't forget to give a star! :star2:

---

## Table of Contents

- [Setup and Config](#setup-and-config)
  - [Configuration](#configuration)
- [Getting and Creating Projects](#getting-and-creating-projects)
  - [Initialization](#initialization)
  - [Clone](#clone)
- [Basic Snap Shotting](#basic-snap-shotting)
  - [Status](#status)
  - [Add](#add)
  - [Commit](#commit)
  - [Diff](#diff)
  - [Restore](#restore)
  - [Reset](#reset)
  - [rm](#rm)
- [Branching and Merging](#branching-and-merging)
  - [Branch](#branch)
  - [Checkout](#checkout)
  - [Merge](#merge)
  - [Log](#log)
  - [Stash](#stash)
  - [Tag](#tag)
- [Sharing and Updating Projects](#sharing-and-updating-projects)
  - [Fetch](#fetch)
  - [Push](#push)
  - [Remote](#remote)
  - [Submodules](#submodules)
- [Patching](#patching)
  - [Cherry-Pick](#cherry-pick)
  - [Rebase](#rebase)
  - [Revert](#revert)
- [Debugging](#debugging)
  - [Grep](#grep)
- [Administration](#administration)
  - [Reflog](#reflog)
  - [Gitk](#gitk)

## Setup and Config

### Configuration

Set and get git global or repository settings

```bash
# Set global user settings
$ git config --global user.name xxx
$ git config --global user.email xxx@mail.com

# Set repository user settings
$ git config user.name xxx
$ git config user.email xxx@mail.com

# Remove settings
$ git config --unset user.name

# Get settings
$ git config --global --list
$ git config --list

# Use alias
$ git config --global alias.br branch

# Avoid line ending problem under cross platform development
$ git config --global core.autocrlf true
```

Useful Alias

```bash
alias.br=branch
alias.chp=cherry-pick
alias.fp=fetch --prune
alias.cm=commit
alias.co=checkout
alias.st=status
alias.lg=log --oneline --graph
alias.la=log --graph --all --pretty=format:"%C(auto)%h -%d %s%Creset %Cblue(%cr)%Creset %C(dim white)<%an>%Creset"
```

---

## Getting and Creating Projects

### Initialization

Create an empty git repository or reinitialize an existing one

```bash
$ git init
```

### Clone

Clone a repository into a new directory

```bash
$ git clone <directory>
```

---

## Basic Snap Shotting

### Status

Show the working tree status

```bash
$ git status
```

### Add

Add file contents to the index

```bash
$ git add <file_path>

# Add all un-staged files in the index
$ git add .
```

### Commit

Record changes to repository

```bash
$ git commit

$ git commit -m <commit_message>

# Add and commit all unstaged files with commit message
$ git commit -am <commit_message>
```

### Diff

Show changes between commits, commit and working tree, etc.

```bash
$ git diff <file_path>

$ git diff HEAD~1

$ git diff <commit_hash_1> <commit_hash_2>

# Compare the difference between index changes and last commit
$ git diff --cached <file_path>
```

### Restore

Restore working tree files

```bash
$ git restore <file_path>

# Restore staged files
$ git restore --staged <file_path>
```

### Reset

Reset current HEAD to specified state

```bash
$ git reset [--soft | --mixed | --hard] <commit>
```

### rm

Remove files from the working tree and from the index

```bash
$ git rm <file_path>
```

---

## Branching and Merging

### Branch

List, create, or delete branches

```bash
# List all branches in your repo, and which branch you're currently in
$ git branch

# Create a branch
$ git branch <branch_name>

# Delete the branch
$ git branch -d <branch_name>

# Delete the branch (FORCE)
$ git branch -D <branch_name>

# Change the branch name
$ git branch -m <older_branch_name> <new_branch_name>
```

### Checkout

Switch branches or restore working tree files

```bash
# Switch to another branch
$ git checkout <branch_name>

# Create a new branch & switch to it
$ git checkout -b <branch_name>

# Cancel the changed file
$ git checkout -- <file>
```

### Merge

Join two or more histories together

```bash
$ git merge <branch>

# Merge without fast-forward
$ git merge --no-ff <branch>
```

### Log

Show commit logs

```bash
$ git log

# Specify date
$ git log --before=<date> --after=<date>

# Specify author
$ git log --author=<author_name>
```

### Stash

Stash the changes in a dirty working directory away

```bash
$ git stash

# List out current stash
$ git stash list

# Push the files wanna stash
$ git stash push

# Output the stashed file
$ git stash apply

# Output specific stashed file
$ git stash apply <stash>

# Remove a single stashed state & apply it on top of current working tree state
$ git stash pop

# Remove a single stash entry from the list of stash entries
$ git stash drop <stash>
```

### Tag

Create, list, delete or verify a tag object signed with GPG

```bash
$ git tag <tag_name>

# Delete a tag
$ git tag -d <tag_name>

# Delete all local tags
$ git tag -l | xargs git tag -d
```

---

## Sharing and Updating Projects

### Fetch

Download objects and refs from another repository

```bash
$ git fetch

# Fetch all remote
$ git fetch --all

# Before fetching, remove any remote-tracking references that no longer exist on the remote
$ git fetch --prune
```

```bash
# Fetch & rebase branch without checkout
$ git fetch origin <remote_branch>:<local_branch>
```

### Push

Update remote refs along with associated objects

```bash
$ git push

# Add upstream reference
$ git push [-u | --set-upstream] <remote_name> <repository_url>
```

### Remote

Manage set of tracked repositories

```bash
# Show remote url after name
$ git remote -v

# Add remote
$ git remote add <remote_name> <repository_url>

# Remove remote
$ git remote remove <remote_name> <repository_url>

# Change remote URL
$ git remote set-url <remote_name> <repository_url>
```

## Submodules

```bash
# Add a submodules
$ git submodule add <repository> <path>

# Occasionally update the submodule to a new version
$ git -C <path> checkout <new-version>
$ git add <path>
$ git commit -m <commit_message>

# Check submodules status
$ git submodule status

# Cloning or pulling a repository containing submodules
$ git submodule init
$ git submodule update
# Shorthand
$ git submodule update --init

# Update recurse into nested submodules
$ git submodule update --recursive <path>

# Unregister the given submodules
$ git submodule deinit <path>

# Remove submodules
$ git rm <path>
```

---

## Patching

### Cherry-Pick

Apply the changes introduced by some existing commits

```bash
$ git cherry-pick <commit_hash_1> <commit_hash_2> ...

# Pick without commit
$ git cherry-pick <commit_hash_1> --no-commit
```

### Rebase

Reapply commits on top of another base tip

```bash
$ git rebase [-i | --interactive] <new_base>
```

### Revert

Revert some existing commits

```bash
$ git revert
```

---

## Debugging

### Grep

Print lines matching a pattern

```bash
# Search with line number
$ git grep -n <search_text>
```

---

## Administration

### Reflog

Manage & track reflog information

```bash
$ git reflog
```

### Gitk

Open a Git repository browser

```bash
$ gitk

# Show all references (branches, tags, etc.)
$ gitk --all
```
