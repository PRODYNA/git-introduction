Here's a table comparing common Subversion (SVN) and Git commands to help users transitioning from SVN to Git.

| **Action**                     | **SVN Command**                     | **Git Command**                               | **Notes** |
|---------------------------------|-------------------------------------|----------------------------------------------|----------|
| **Check repository URL**       | `svn info`                          | `git remote -v`                             | SVN tracks a central repo, Git tracks multiple remotes. |
| **Clone/checkout repository**  | `svn checkout <URL>`               | `git clone <URL>`                           | `git clone` gets the full repo history, unlike `svn checkout`. |
| **Update working copy**        | `svn update`                        | `git pull`                                  | `git pull` fetches and merges changes. |
| **Commit changes**             | `svn commit -m "Message"`           | `git commit -m "Message"`                   | Git commits locally first. |
| **Push changes**               | *(N/A in SVN - implicit on commit)* | `git push`                                  | In Git, commits must be explicitly pushed. |
| **Add files**                  | `svn add <file>`                    | `git add <file>`                            | Git stages changes before committing. |
| **Remove files**               | `svn delete <file>`                 | `git rm <file>`                             | Git tracks removals explicitly. |
| **Revert changes**             | `svn revert <file>`                 | `git checkout -- <file>` (before Git 2.23) / `git restore <file>` (Git 2.23+) | Git has more granular rollback options. |
| **Show log/history**           | `svn log`                           | `git log`                                   | Git log is local; SVN requires server access. |
| **Show file changes**          | `svn diff`                          | `git diff`                                  | Works similarly in both. |
| **Show repository status**     | `svn status`                        | `git status`                                | `git status` is only local. |
| **Move/rename files**          | `svn move <source> <destination>`   | `git mv <source> <destination>`             | Git tracks renames heuristically. |
| **Create branch**              | `svn copy <URL>/trunk <URL>/branches/<branch>` | `git branch <branch>`                      | Git branches are local by default. |
| **Switch branch**              | `svn switch <URL>/branches/<branch>` | `git checkout <branch>` / `git switch <branch>` (Git 2.23+) | SVN switch updates the working copy from the server. |
| **Merge branch**               | `svn merge <branch>`                | `git merge <branch>`                        | Git merging happens locally. |
| **List branches**              | `svn list <URL>/branches`           | `git branch -a`                             | Git lists local and remote branches separately. |
| **Delete branch**              | `svn delete <URL>/branches/<branch>` | `git branch -d <branch>` / `git push origin --delete <branch>` | Git requires a separate push to delete remote branches. |
| **Create tag**                 | `svn copy <URL>/trunk <URL>/tags/<tag>` | `git tag <tag>` / `git push origin <tag>` | SVN tags are just copies; Git uses lightweight or annotated tags. |
| **List tags**                  | `svn list <URL>/tags`               | `git tag`                                   | Git tags are local until pushed. |
| **Delete tag**                 | `svn delete <URL>/tags/<tag>`       | `git tag -d <tag>` / `git push origin --delete <tag>` | Same as branch deletion in Git. |
| **Resolve conflicts**          | `svn resolve <file>`                | Manually edit file, then `git add <file>` and commit | Git requires manual conflict resolution. |
| **Ignore files**               | Edit `.svnignore`                   | Edit `.gitignore`                           | Similar concepts but different syntax. |
| **View file blame**            | `svn blame <file>`                  | `git blame <file>`                          | Shows line-by-line commit history. |
| **Stash changes**              | *(No direct equivalent)*            | `git stash`                                 | Temporarily saves uncommitted changes. |
| **Show remote repositories**   | `svn info`                          | `git remote -v`                             | Git allows multiple remotes. |
| **Change commit message**      | `svn propedit --revprop -r <rev> svn:log` | `git commit --amend`                        | Git amends local commits. |
| **Undo last commit**           | *(Difficult in SVN)*                | `git reset --soft HEAD~1`                   | Git allows rewriting history. |
| **Hard reset to previous state** | *(Difficult in SVN)*                | `git reset --hard <commit>`                 | Git allows discarding local changes. |

