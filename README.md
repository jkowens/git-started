# Intro to Git Rebase

Before doing a rebase, an essential first step is to checkout the main (master, dev, etc) branch and pull down the latest changes:

```
git checkout main
git pull main
```
\
Then switch back to the feature branch to do the rebase:

```
git checkout feature
git rebase main
```
\
If there are conflicts that need to be resolved, git will show which files have merge conflicts. Resolve the conflicts and stage the files using `git add`. Then continue the rebase with `git rebase --continue`.

```
git add .
git rebase --continue
```

*NOTE:* If the commit that creates a conflict is no longer needed, it can be dropped by using the `--skip` option instead:

```
git rebase --skip
```

\
As git applies each commit to the tip of the main branch, there is a chance for a conflict so you may need to repeat the previous step multiple times.


Once the rebase is complete, you can confirm your commits have been applied to the latest commit on main by using `git log`.

```
git log --oneline
```

## What if things go wrong?

During a rebase, you can always abort the rebase operation and revert to the last commit before attempting the rebase.

```
git rebase --abort
```

#### The rebase completed but something isn't right

```
git reflog
```

You will see a history of local changes to the repository. Look for the last good commit before the rebase and copy the commit id (SHA). You can then use `git reset`:

```
git reset --hard <last good SHA>
```

## Interactive Rebase

Git rebase can also be used in interactive mode to modify commits in a range. Commits can be dropped or squashed and commit messages can be modified. As developers we like to commit frequently, but when it comes time to merge our feature into the main branch, it can be beneficial to squash our commits into a few or even a single commit.

```
git rebase --interactive HEAD~<number of commits>
```

## Pushing to Github

If a feature branch has been pushed to Github and then you do a rebase, you will need to use a force push since the commit history has changed:

```
git push origin feature --force
```

*NOTE:* Force pushing to your own feature branch is safe, but if force pushing to master or a branch that is shared it should be considered dangerous.

## References

* [Git Rebase](https://git-scm.com/docs/git-rebase)
* [Merging vs Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
* [Demystifying Git Rebase](https://www.thinktecture.com/en/tools/demystifying-git-rebase)
* [Always Squash and Rebase Your Git Commits](https://blog.carbonfive.com/always-squash-and-rebase-your-git-commits)
