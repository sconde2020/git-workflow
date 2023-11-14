# Git Workflow for Feature Branches

The following is an example workflow for developing on a temporary branch and merging back to the main branch squashing all commits into a single commit.  This assumes you already have a branch named ``branch-xyz`` and have finished the work on that branch.

## Step 1: Checkout the feature branch

```
git checkout branch-xyz
```

## Step 2: Rebase the branch to the master branch
This will replay all commits on the feature branch on top of the latest code from the master branch.  This makes it look like the feature branch was copied from the master branch and all commits laid on top, even if other commits happened on the master.  This makes merging later on easy.  This assumes that master is up to date with your remote repository.  If not, make sure to do a ``git pull`` on the master branch to bring it up to date.

```
git rebase master
```

## Step 3: Resolve conflicts
If any conflicts occurred while rebasing, you will need to resolve those conflicts before proceeding.  To resolve the conflicts, open the conflicting files in an editor and update the demarked lines.  You  may need to repeat these steps as necessary until all rebasing has been completed.

```
[update file1 file2 etc]
git add file1 file2 etc
git rebase --continue
```

## Step 4: Checkout master
At this point, the feature branch is up to date with master, so we can checkout master again to get ready to merge.

```
git checkout master
```

## Step 5: Merge the feature branch
We can now merge the feature branch into master squashing all commits into a single commit.  This allows you to commit early and often on the feature branch and only update the main code base as if only one commit happened keeping a nice and clean history.

```
git merge --squash branch-xyz
```

## Step 6: Commit
At this point you can commit the merged updates.  When you commit, it will give you a prefilled commit message containing all the merged commits.  You can simply delete those lines and create a new line that describes the update or the bug fix.  Optionally, you can choose to push the commits back to the remote repository.

```
git commit
git push
```

## Step 7: Finish
You are now done.  You can choose to delete the branch, although deleting the branch will remove all the individual logged commits on the branch since they were squashed on the master branch.