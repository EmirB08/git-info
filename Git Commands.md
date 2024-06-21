#### **branch**
1. Checkout the branch you want to create from
```
   git checkout branchname
```
2. Check that branch is up to date
```
   git pull
```
3. Create the new branch
```
   git checkout -b newbranchname
```
4. Push the new branch to remote
```
   git push -u origin newbranchname
```

#### **commit - add**
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


#### **commit - delete**

1. Delete specified commit from local HEAD
```
git reset --hard  HASHCODE
```
2. Alternatively, delete last commit from local HEAD
```
git reset --hard~1
```
3. Push after git reset to force deletion of the latest commit from history
```
git push --force
```

#### **merge**
1. Checkout branch you want to merge into
```
   git checkout checkoutname
```
2. Make sure local branch is up to date with remote
```
   git pull && git status
```
3. Merge a branch into your checked out branch
```
   git merge mergebranchname
```
4. Push the merge to remote:
```
   git push
```

#### **repo**

Easiest way is to just create trough the web GUI and then run the git commands locally

**Create a new repository**
```
git clone https://gitlab.com/el-fly/gitcommands.git
cd gitcommands
git switch --create main
touch README.md
git add README.md
git commit -m "add README"
git push --set-upstream origin main
```

**Push an existing folder**
```
cd existing_folder
git init --initial-branch=main
git remote add origin https://gitlab.com/el-fly/gitcommands.git
git add .
git commit -m "Initial commit"
git push --set-upstream origin main
```

#### **other**

**List local branches**
```
git branch
```

**List remote branches**
```
git branch -r
```

**Check branch status**
```
git status
```

**Check branch commit history**
```
git log
```

**Show changes in working directory**
```
git diff
```

**Safe delete local AND remote branch**
```
git branch -d branchname && git push origin --delete branchname
```

**Stash changes**
```
git stash
```

**Apply most recent stash**

```
 git stash apply
```

**List all stashes**
```
git stash list
```

**Delete all stashes**
```
git stash clear
```

**Apply a specific stash in list**
```
git stash apply stash@{index number in list}
```

**Delete specific stash from the list using index**
```
git stash drop stash@{index number in list}
```


