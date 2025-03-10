# Common Git Errors and Fixes

### **1. Committing to the Wrong Branch**
#### **Problem**:
You accidentally commit changes to the wrong branch.

#### **Fix**:
Move the commit to the correct branch.

```sh
# Create and switch to the correct branch if it doesn't exist
git checkout -b correct-branch

# Move the last commit to the correct branch
git cherry-pick <commit-hash>  # Find commit hash using `git log`

# Switch back to the wrong branch and remove the commit
git checkout wrong-branch
git reset --hard HEAD~1
```

---

### **2. Undoing the Last Commit (Before Pushing)**
#### **Problem**:
You made a mistake in the last commit.

#### **Fix**:
To undo the last commit but keep the changes:

```sh
git reset --soft HEAD~1
```

To undo the last commit and discard the changes:

```sh
git reset --hard HEAD~1
```

---

### **3. Undoing the Last Commit (After Pushing)**
#### **Problem**:
You already pushed a commit but need to undo it.

#### **Fix**:
Use a revert (safe) if others have already pulled the commit:

```sh
git revert HEAD
git push origin main
```

Use a reset (force) if you're sure nobody else has pulled it:

```sh
git reset --hard HEAD~1
git push --force
```
⚠️ **Warning**: `--force` can overwrite history, so be cautious.

---

### **4. Staging the Wrong Files**
#### **Problem**:
You accidentally staged a file you didn’t mean to commit.

#### **Fix**:
To unstage a file without losing changes:

```sh
git reset HEAD <file>
```

To unstage all files:

```sh
git reset HEAD
```

---

### **5. Accidentally Deleting a Branch**
#### **Problem**:
You deleted a branch but need it back.

#### **Fix**:
Find the last commit hash:

```sh
git reflog
```

Restore the branch:

```sh
git checkout -b deleted-branch <commit-hash>
```

---

### **6. Overwriting Local Changes with `git pull`**
#### **Problem**:
Running `git pull` causes you to lose local changes.

#### **Fix**:
Use stash before pulling:

```sh
git stash
git pull origin main
git stash pop  # Reapply stashed changes
```

---

### **7. Committing with the Wrong Author Name/Email**
#### **Problem**:
You committed with the wrong user information.

#### **Fix**:
Change author details for the last commit:

```sh
git commit --amend --author="New Name <newemail@example.com>"
```

If already pushed:

```sh
git push --force
```

---

### **8. Merging the Wrong Branch**
#### **Problem**:
You accidentally merged the wrong branch.

#### **Fix**:
If not pushed:

```sh
git reset --hard HEAD~1
```

If pushed:

```sh
git revert -m 1 <merge-commit-hash>
git push origin main
```

---

### **9. Fixing a Merge Conflict**
#### **Problem**:
You get a merge conflict.

#### **Fix**:
1. Check conflicting files:

   ```sh
   git status
   ```

2. Open the files, resolve conflicts manually, and save.

3. Mark them as resolved:

   ```sh
   git add <file>
   git commit
   ```

---

### **10. Recovering a Lost Commit**
#### **Problem**:
You reset a branch and lost a commit.

#### **Fix**:
Find lost commits:

```sh
git reflog
```

Restore a commit:

```sh
git checkout -b recovered-branch <commit-hash>
```

---
