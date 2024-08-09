### **branch - create**

1. Checkout the branch you want to create from

```
   git checkout branch_name
```

2. Check that branch is up to date

```
   git pull
```

3. Create the new branch

```
   git checkout -b new_branch_name
```

4. Push the new branch to remote

```
   git push -u origin new_branch_name
```

### **branch - delete**

1. Checkout an alternative branch - git won't allow deletion FROM a branch you want to delete

```
   git checkout alternative_branch
```

2.  List both local and remote branches

```
   git branch -a
```

3. Delete (safe) local branch

```
   git branch -d branch_name
```

4. Delete remote branch

```
   git push origin --delete branch_name
```

**Delete local and remote in one line**

```
   git push branch -d branch_name && git push origin --delete branch_name
```

**Force delete a branch using -D will delete a branch with unmerged changes**

```
   git branch -D branch_name
```

### **branch - prune**

**Fetch all branches and prune the stale branches that no longer exist on the remote**

```
git fetch - p
```

**Prune without fetching all updates**

```
git remote prune origin
```

### **commit - add**

1. Add the changes:

```
   git add .
```

2. Commit the changes to the branch

```
   git commit -m "message"
```

3. Push the commit to remote branch

```
   git push
```

### **commit - delete/hard reset**

1. Delete specified commit from local HEAD

```
git reset --hard  HASHCODE
```

2. Alternatively, delete last commit from local HEAD

```
git reset --hard~1
```

3. Push after git reset to force deletion of the latest commit on remote branch

```
git push --force
```

### **merge**

1. Checkout branch you want to merge into

```
   git checkout branch_name
```

2. Make sure local branch is up to date with remote

```
   git pull && git status
```

3. Merge a branch into your checked out branch

```
   git merge merge_branch_name
```

4. Push the merge to remote:

```
   git push
```

### **stash**

Stash changes

```
git stash
```

Apply most recent stash

```
 git stash apply
```

List all stashes

```
git stash list
```

Delete all stashes

```
git stash clear
```

Apply a specific stash in list

```
git stash apply stash@{index number in list}
```

Delete specific stash from the list using index

```
git stash drop stash@{index number in list}
```

### **repo - create**

Create remote - CLI

```
curl --request POST \
     --header "PRIVATE-TOKEN: token_here" \
     --data "name=example" \
     --data "namespace_id=123456" \
     "https://gitlab.com/api/v4/projects/"
```

```
curl --request POST --header "PRIVATE-TOKEN: glpat-c2EFK-Y2Ryy5F2fSGCoC" --data "name=example" --data "namespace_id=77579999" "https://gitlab.com/api/v4/projects/"
```

Push local to remote

```
cd project_folder
git init --initial-branch=main
git remote add origin https://gitlab.com/el-fly/example.git
touch README.md
git add .
git commit -m "init"
git push -u origin main
```

### **repo - clone**

Clone existing/active repo - example

```
   cd documents
   ls
   cd gitlab
   git clone https://gitlab.com/el-fly/example.git
```

Clone and push to blank repo - example

```
cd project_folder
git clone https://gitlab.com/el-fly/example.git
git switch --create main
touch README.md
git add .
git commit -m "init"
git push -u origin main
```

### **repo - delete**

```
curl --request DELETE --header "PRIVATE-TOKEN: token_here" "https://gitlab.com/api/v4/projects/example"
```

### **other**

List local branches

```
git branch
```

List remote branches

```
git branch -r
```

List local and remote branches

```
git branch -a
```

Check branch status

```
git status
```

Check branch commit history

```
git log
```

Show changes in working directory

```
git diff
```

Unstage alle changes

```
git reset
```
