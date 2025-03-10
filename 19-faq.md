# Git FAQ

## Is it possible to...?

Yes!

## How do I discard all local changes in a file?

To discard all local changes in a file and revert it to the last committed state, use:

```sh
git restore file.txt
```

This command is the modern equivalent of using `git checkout -- file.txt`.

## How do I restore a deleted file?

To restore a deleted file from the last commit, use:

```sh
git restore --source=HEAD~1 file.txt
```

This command restores `file.txt` from the commit before the last one. You can replace `HEAD~1` with any commit reference.

## How do I discard chunks/lines in a file

To discard specific chunks or lines in a file, use:

```sh
git restore -p file.txt
```

This command starts an interactive session where you can choose which changes to keep or discard.

## How do I discard all local changes?

To discard all local changes in your working directory, use:

```sh
git restore .
```

This command reverts all changes in the working directory to the last committed state.

## How do I discard all local changes and commits?

To discard all local changes and commits and revert to the last commit on the current branch, use:

```sh
git reset --hard HEAD
```

This command resets the current branch to the last commit, discarding all changes and commits.

## How do I discard a commit?

To discard the last commit and keep the changes in your working directory, use:

```sh
git reset --soft HEAD~1
```

This command resets the current branch to the commit before the last one, keeping the changes in your working directory.

## How do I discard a commit and all changes?

To discard the last commit and all changes in your working directory, use:

```sh
git reset --hard HEAD~1
```

This command resets the current branch to the commit before the last one, discarding all changes in your working directory.

## How do I undo a commit after pushing?

To undo a commit after pushing it to a remote repository, use:

```sh
git revert HEAD
git push origin <branch>
```

This command creates a new commit that undoes the changes introduced by the last commit. You can then push this new commit to the remote repository.

## How do I undo a commit and changes after pushing?

To undo a commit and all changes after pushing it to a remote repository, use:

```sh
git reset --hard HEAD~1
git push --force
```

This command resets the current branch to the commit before the last one, discarding all changes in your working directory. The `--force` flag is required to update the remote repository with the rewritten history.

## How do I discard a file from the staging area?

To discard a file from the staging area while keeping the changes in your working directory, use:

```sh
git reset HEAD <file>
```

This command unstages the specified file, but keeps the changes in your working directory.

## How do I discard all files from the staging area?

To discard all files from the staging area while keeping the changes in your working directory, use:

```sh
git reset
```

This command unstages all files, but keeps the changes in your working directory.

## How do I discard changes in a specific file?

To discard changes in a specific file and revert it to the last committed state, use:

```sh
git checkout -- file.txt
```

This command reverts `file.txt` to the last committed state, discarding any changes made to it.

## How do I discard all changes in a specific file?

To discard all changes in a specific file and revert it to the last committed state, use:

```sh
git checkout HEAD -- file.txt
```

This command reverts `file.txt` to the last committed state, discarding any changes made to it.

## How do I discard all changes in all files?

To discard all changes in all files and revert them to the last committed state, use:

```sh
git checkout -- .
```

This command reverts all files in the working directory to the last committed state, discarding any changes made to them.

## How to fix the comment of the last commit?

To fix the comment of the last commit, use:

```sh
git commit --amend
```

This command opens an editor to modify the comment of the last commit. Save and close the editor to update the commit message.

## How to fix the author of the last commit?

To fix the author of the last commit, use:

```sh
git commit --amend --author="New Name"
```

This command updates the author of the last commit. Replace `New Name` with the desired author name.

## How do I add a file to the last commit that I have forgotten?

To add a file to the last commit that you have forgotten, use:

```sh
git add forgotten-file.txt
git commit --amend
```

This command stages the forgotten file and opens an editor to modify the last commit. Save and close the editor to add the file to the last commit.

## How do I add changes to the last commit?

To add changes to the last commit without modifying the commit message, use:

```sh
git add .
git commit --amend --no-edit
```

This command stages all changes and adds them to the last commit without changing the commit message.

## How do I revert a commit in the middle of the history?

To revert a commit in the middle of the history, use:

```sh
git revert <commit-hash>
```

This command creates a new commit that undoes the changes introduced by the specified commit. You can then push this new commit to the remote repository.

## How do I delete a commit in the middle of the history?

To delete a commit in the middle of the history and all changes introduced by it, use:

```sh
git rebase -i <commit-hash>^
```

This command opens an interactive rebase session where you can delete the specified commit. Save and close the editor to rewrite the history.

## How do I squash multiple commits into one?

To squash multiple commits into one, use:

```sh
git rebase -i HEAD~<number-of-commits>
```

This command opens an interactive rebase session where you can squash the specified number of commits into one. Save and close the editor to rewrite the history.

## How do I get the changes from a specific commit?

To get the changes from a specific commit without creating a new commit, use:

```sh
git cherry-pick <commit-hash>
```

This command applies the changes introduced by the specified commit to the current branch.

## How do I move a commit to another branch?

To move a commit to another branch, use:

```sh
git cherry-pick <commit-hash>
git checkout <destination-branch>
git cherry-pick <commit-hash>
git checkout <source-branch>
git reset --hard HEAD~1
```

This sequence of commands cherry-picks the specified commit to the destination branch, resets the source branch to the commit before the last one, and discards the commit from the source branch.

## How do I check the current branch name?

To check the current branch name, use:

```sh
git branch --show-current
```

or simply 

```sh
git branch
```

or 

```sh
git status
```

These commands display the current branch name in the output.

## How do I check the remote URL of a repository?

To check the remote URL of a repository, use:

```sh
git remote get-url origin
```

This command displays the URL of the remote repository named `origin`.

## How do I check the remote branch?

To check the remote branch associated with the current branch, use:

```sh
git branch -vv
```

## How do I delete branch?

To delete a branch, use:

```sh
git branch -d <branch-name>
```

## How do I delete a remote branch?

To delete a remote branch, use:

```sh
git push origin --delete <branch-name>
```

## How do I rename a branch?

To rename a branch, use:

```sh
git branch -m <new-branch-name>
```

This command renames the current branch to `new-branch-name`.

## How do I delete branches, that are not on the remote?

To delete branches that are not on the remote, use:

```sh
git fetch --prune
```

This command fetches the latest changes from the remote repository and prunes (deletes) local branches that no longer exist on the remote.

## How do I list all branches?

To list all branches, use:

```sh
git branch -a
```

This command displays both local and remote branches.

## How do I list all remote branches?

To list all remote branches, use:

```sh
git branch -r
```

This command displays only remote branches.

## How do I list all branches with the last commit message?

To list all branches with the last commit message, use:

```sh
git branch -v
```

This command displays the last commit message for each branch.

## How do I display a graph of all commits and branches?

To display a graph of all commits and branches, use:

```sh
git log --oneline --graph --all
```
