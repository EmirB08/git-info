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

#### **repo - create**

Create a repo locally, will need to create an access token to use for the API. If the project page is for a group you need the namespace_id as well. Alternatively the repo can be initialized in remote to skip this.

```
curl --request POST \
     --header "PRIVATE-TOKEN: token_here" \
     --data "name=example" \
     --data "namespace_id=123456" \
     "https://gitlab.com/api/v4/projects/"
```

```
curl --request POST --header "PRIVATE-TOKEN: token_here" --data "name=example" --data "namespace_id=123456" "https://gitlab.com/api/v4/projects/"
```

**Clone existing**

```
cd repo_folder
git clone https://gitlab.com/el-fly/gitcommands.git
git switch --create main
touch README.md
git add .
git commit -m "init"
git push -u origin main
```

**Push an existing folder**

```
cd repo_folder
git init --initial-branch=main
git remote add origin https://gitlab.com/el-fly/example.git
git add .
git commit -m "init"
git push -u origin main
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

**Fetch all branches and prune the stale branches that no longer exist on the remote**

```
git fetch --prune

or

git fetch -p
```

**Prune using git remote prune to explicitly prune without fetching all updates**

```
git remote prune origin
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
