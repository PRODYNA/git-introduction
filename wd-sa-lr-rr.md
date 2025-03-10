# Working Directory, Staging Area, Local Repository, Remote Repository

```mermaid
sequenceDiagram
    participant WD as Working Directory
    participant SA as Staging Area (Index)
    participant LR as Local Repository
    participant RR as Remote Repository

    WD->>WD: Modify files (edit, delete, create)
    WD->>SA: git add <file>
    SA->>LR: git commit -m "message"
    LR->>RR: git push origin <branch>
    RR-->>LR: Acknowledgment of push

    RR->>LR: git fetch (fetches changes)
    LR->>WD: git merge (merges into working directory)
    LR->>WD: git rebase (reapplies commits)

    WD->>SA: git rm --cached <file> (unstage file)
    SA->>WD: git reset HEAD <file> (unstage but keep changes)
    SA->>WD: git reset --hard HEAD (discard changes)

    LR->>WD: git checkout <branch> (switch branch)
    WD->>WD: git stash (save changes temporarily)
    WD->>WD: git stash pop (restore changes)

    RR->>LR: git clone <repo-url> (copy repository)
    LR->>WD: git checkout -b <new-branch> (create new branch)
    WD->>LR: git commit --amend (modify last commit)

    LR->>LR: git revert <commit> (undo commit safely)
    LR->>LR: git reset --hard HEAD~1 (delete last commit)
    LR->>RR: git push --force (force update)

    RR->>LR: git pull origin <branch> (fetch and merge changes)
