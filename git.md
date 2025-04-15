---
title: Git Command Reference
description: Comprehensive guide to Git operations
tags:
  - git
  - reference
  - commands
---
# branch

## branch - create

```
# Checkout the branch you want to create from
git checkout branch_name

# Check that branch is up to date
git pull

# Create the new branch
git checkout -b new_branch_name

# Push the new branch to remote
git push -u origin new_branch_name
```

## branch - delete

```
# Checkout an alternative branch - git won't allow deletion FROM a branch you want to delete
git checkout alternative_branch

# List both local and remote branches
git branch -a

# Delete (safe) local branch
git branch -d branch_name

# Delete remote branch
git push origin --delete branch_name

# Delete local and remote in one line
git branch -d branch_name && git push origin --delete branch_name

# Force delete a branch with unmerged changes
git branch -D branch_name
```

## branch - prune

```
# Fetch all branches and prune stale remote branches
git fetch -p

# Prune without fetching all updates
git remote prune origin
```

# commit

## commit - add

```
# Add the changes
git add .

# Commit the changes to the branch
git commit -m "message"

# Push the commit to remote branch
git push
```

## commit - delete/hard reset

```
# Delete specified commit from local HEAD
git reset --hard HASHCODE

# Alternatively, delete last commit from local HEAD
git reset --hard HEAD~1

# Push after git reset to force deletion of the latest commit on remote branch
git push --force
```

# merge

```
# Checkout branch you want to merge into
git checkout branch_name

# Make sure local branch is up to date with remote
git pull && git status

# Merge a branch into your checked out branch
git merge merge_branch_name

# Push the merge to remote
git push
```

# stash

```
# Stash changes
git stash

# Apply most recent stash
git stash apply

# List all stashes
git stash list

# Delete all stashes
git stash clear

# Apply a specific stash in list
git stash apply stash@{index number in list}

# Delete specific stash from the list using index
git stash drop stash@{index number in list}
```

# repository

## repository - create

```
# Create remote - GitLab API
curl --request POST \
     --header "PRIVATE-TOKEN: token_here" \
     --data "name=example" \
     --data "namespace_id=123456" \
     "https://gitlab.com/api/v4/projects/"

# Alternative one-line format
curl --request POST --header "PRIVATE-TOKEN: token_here" --data "name=example" --data "namespace_id=123456" "https://gitlab.com/api/v4/projects/"

# Push local to remote
cd project_folder
git init --initial-branch=main
git remote add origin https://gitlab.com/example/example.git
touch README.md
git add .
git commit -m "init"
git push -u origin main
```

## repository - clone

```
# Clone existing/active repo - example
cd documents
ls
cd gitlab
git clone https://gitlab.com/example/example.git

# Clone and push to blank repo - example
cd project_folder
git clone https://gitlab.com/example/example.git
git switch --create main
touch README.md
git add .
git commit -m "init"
git push -u origin main
```

## repository - delete

```
# Delete repository via GitLab API
curl --request DELETE --header "PRIVATE-TOKEN: token_here" "https://gitlab.com/api/v4/projects/example"
```

# misc

```
# List local branches
git branch

# List remote branches
git branch -r

# List local and remote branches
git branch -a

# Check branch status
git status

# Check branch commit history
git log

# Show changes in working directory
git diff

# Unstage all changes
git reset
```
