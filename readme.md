# Git Tips

This repository is used to record some git commands which are frequently used.

Git Reference Manual >> [Link](https://git-scm.com/docs)

---

## Setup and Config

### Configuration

Set and get git global or repository settings

```
// -- Set global user settings
$ git config --global user.name xxx
$ git config --global user.email xxx@mail.com

// -- Set repository user settings
$ git config user.name xxx
$ git config user.email xxx@mail.com

// -- Remove settings
$ git config --unset user.name

// -- Get settings
$ git config --global --list
$ git config --list

// -- Use alias
$ git config --global alias.br branch
```

Useful Alias
```
alias.br=branch
alias.chp=cherry-pick
alias.fp=fetch --prune
alias.cm=commit
alias.co=checkout
alias.st=status
alias.lg=log --oneline --graph
alias.la=log --graph --all --pretty=format:"%C(auto)%h -%d %s%Creset %C(blue)(%cr)%Creset %C(dim white)<%an>%Creset"
```

---

## Getting and Creating Projects

### Initialization

Create an empty git repository or reinitialize an existing one

```
$ git init
```

### Clone

Clone a repository into a new directory

```
$ git clone [<directory>]
```

---

## Basic Snapshotting

### Status

Show the working tree status

```
$ git status
```

### Add

Add file contents to the index

```
$ git add [<file_path>]

// -- Add all unstaged files in the index
$ git add .
```

### Diff

Show changes between commits, commit and working tree, etc.

```
$ git diff
```

### Commit

Record changes to repository

```
$ git commit

// -- Add and commit all unstaged files with commit message
$ git cm -am [<commit_message>]
```

### Restore

Restore working tree files

```
$ git restore [<file_path>]
```

### Reset

Reset current HEAD to specified state

```
$ git reset [<commit>]
```

---

## Branching and Merging

### Branch

List, create, or delete branches

```
// -- List all branches in your repo, and which branch you're curently in
$ git branch

// -- Create a branch
$ git branch [<branch_name>]

// -- Delete the branch
$ git branch -d [<branch_name>]

// -- Delete the branch (FORCE)
$ git branch -D [<branch_name>]

// -- Change the branch name
$ git branch -m [<older_branch_name>] [<new_branch_name>]
```

### Checkout

Switch branches or restore working tree files

```
// -- Switch to another branch
$ git checkout [<branch_name>]

// -- Create a new branch & switch to it
$ git checkout -b [<branch_name>]

// -- Cancel the changed file
$ git checkout -- [<file>]
```

### Merge

Join two or more histories together

```
$ git merge

// -- Merge without fast-forward
$ git merge --no-ff
```

### Log

Show commit logs

```
$ git log

// -- Specify date
$ git log --before=[<date>] --after=[<date>]

// -- Specifiy author
$ git log --author=[<author_name>]
```

### Stash

Stash the changes in a dirty working directory away

```
$ git stash

// -- List out current stash
$ git stash list

// -- Output your stashed file
$ git stash apply

// -- Output specific stashed file
$ git stash apply [<stash>]

// -- Remove a single stashed state & apply it on top of current working tree state
$ git stash pop

// -- Remove a single stash entry from the list of stash entries
$ git stash drop [<stash>]
```

### Tag

Create, list, delete or verify a tag object signed with GPG

```
$ git tag [<tag_name>]

// -- Delete a tag
$ git tag -d [<tag_name>]
```

---

## Sharing and Updating Projects

### Fetch

Download objects and refs from another repository

```
$ git fetch

// -- Fetch all remote
$ git fetch --all
```

### Push

Update remote refs along with associated objects

```
$ git push

// -- Add upstream reference
$ git push -u | --set-upstream [<remote_name>] [<repository_url>]
```

### Remote

Manage set of tracked repositories

```
// -- Show remote url after name
$ git remote -v

// -- Add remote
$ git remote add [<remote_name>] [<repositoy_url>]

// -- Remove remote
$ git remote remove [<remote_name>] [<repositoy_url>]

// -- Change remote URL
$ git remote set-url [<remote_name>] [<repositoy_url>]
```

---

## Patching

### Cherry-pick

Apply the changes introduced by some existing commits

```
$ git cherry-pick [<commit_hash_1>] [<commit_hash_2>] ...

// -- Pick without commit
$ git cherry-pick [<commit_hash_1>] --no-commit
```

### Rebase

Reapply commits on top of another base tip

```
$ git rebase -i | --interactive [<new_base>]
```

### Revert

Revert some existing commits

```
$ git revert
```

---

## Debugging

### prep

Print lines matching a pattern

```
// -- Search with line number
$ git grep -n [<search_text>]
```

---

## Administration

### Git Reflog

Manage & track reflog information

```
$ git reflog
```

### Git Gitk

Open a Git repository browser

```
$ gitk

// -- Show all references (branches, tags, etc.)
$ gitk --all
```
