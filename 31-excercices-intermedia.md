
# **Intermediate Git Exercises (11-20)**

```mermaid
graph TD;
    A[Cherry-picking a Commit] --> B[Viewing File History];
    B --> C[Reverting a Commit];
    C --> D[Using Git Aliases];
    D --> E[Interactive Rebase];
    E --> F[Finding a Deleted Branch];
    F --> G[Resetting a Branch to Remote];
    G --> H[Amending the Last Commit];
    H --> I[Tagging Releases];
    I --> J[Pushing Tags to Remote];
```

---

## **Exercise 11: Cherry-picking Commits**

```mermaid
graph TD;
    A[Feature Branch] -->|Pick a commit| B[main branch]; 
```

### **Starting Point Setup**
```sh
git checkout -b cherry-pick-branch  
echo "First commit" > file.txt  
git add file.txt  
git commit -m "Commit A"  
echo "Second commit" >> file.txt  
git commit -am "Commit B"  
echo "Third commit" >> file.txt  
git commit -am "Commit C"  
git checkout main  
```

### **Goal**
Cherry-pick a commit from `cherry-pick-branch` into `main`.

### **Commands**
```sh
git cherry-pick <commit-hash>  
```

### **Verification**
```sh
git log --oneline  
```

---

## **Exercise 12: Viewing File History**

```mermaid
graph TD;
    A[Older Version] -->|git log| B[Recent Version];
```

### **Starting Point Setup**
```sh
echo "File history test" > history.txt  
git add history.txt  
git commit -m "Initial commit"  
echo "Updated content" >> history.txt  
git commit -am "Modified history.txt"  
```

### **Goal**
View the commit history of a file.

### **Commands**
```sh
git log --oneline history.txt  
```

### **Verification**
```sh
git blame history.txt  
```

---

## **Exercise 13: Reverting a Commit**

```mermaid
graph TD;
    A[Bad Commit] -->|git revert| B[New Commit - Undo];
```

### **Starting Point Setup**
```sh
echo "Revert this change" > revert.txt  
git add revert.txt  
git commit -m "Bad commit"  
```

### **Goal**
Revert the last commit without removing the file.

### **Commands**
```sh
git revert HEAD  
```

### **Verification**
```sh
git log --oneline  
```

---

## **Exercise 14: Using Git Aliases**

```mermaid
graph TD;
    A[Normal Git Command] -->|Alias| B[Shorter Command]; 
```

### **Goal**
Create a shortcut for frequently used commands.

### **Commands**
```sh
git config --global alias.last 'log -1 HEAD'  
```

### **Verification**
```sh
git last  
```

---

## **Exercise 15: Interactive Rebase (Squashing Commits)**
(Same as Exercise 11 but squashing multiple commits.)

```mermaid
graph TD;
    A[Commit 1] --> B[Commit 2] --> C[Commit 3];
    C -->|Squash| D[Single Commit];
```

---

## **Exercise 16: Finding a Deleted Branch**

```mermaid
graph TD;
    A[Deleted Branch] -->|git reflog| B[Recovered Branch]; 
```

### **Starting Point Setup**
```sh
git checkout -b recover-branch  
touch recover.txt  
git add recover.txt  
git commit -m "Work in progress"  
git checkout main  
git branch -D recover-branch  
```

### **Goal**
Recover the deleted branch.

### **Commands**
```sh
git reflog  
git checkout -b recover-branch <commit-hash>  
```

---

## **Exercise 17: Resetting a Branch to Remote**

```mermaid
graph TD;
    A[Local Changes] -->|Reset| B[Match Remote];
```

### **Goal**
Reset local changes and match remote.

### **Commands**
```sh
git fetch origin  
git reset --hard origin/main  
```

---

## **Exercise 18: Amending the Last Commit**

```mermaid
graph TD;
    A[Original Commit] -->|Amend| B[Updated Commit];
```

### **Goal**
Modify the last commit message.

### **Commands**
```sh
git commit --amend -m "Updated commit message"  
```

---

## **Exercise 19: Tagging Releases**

```mermaid
graph TD;
    A[Code Version] -->|Tag| B[v1.0];
```

### **Goal**
Create an annotated tag.

### **Commands**
```sh
git tag -a v1.0 -m "Version 1.0 release"  
```

### **Verification**
```sh
git tag  
```

---

## **Exercise 20: Pushing Tags to Remote**

```mermaid
graph TD;
    A[Local Tags] -->|Push| B[Remote Tags];
```

### **Goal**
Push tags to a remote repository.

### **Commands**
```sh
git push origin --tags  
```

---

