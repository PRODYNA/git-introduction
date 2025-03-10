# Internals

The `.git` directory is the **heart of a Git repository**. It contains everything Git needs to track changes, manage branches, store commits, and handle configurations.

---

## **1. Overview of `.git` Directory Structure**
When you initialize a Git repository (`git init`), a `.git` directory is created in the root of your project:

```sh
.git/
├── HEAD
├── config
├── description
├── hooks/
├── index
├── info/
│   ├── exclude
├── logs/
│   ├── HEAD
│   ├── refs/
│       ├── heads/
│       ├── remotes/
├── objects/
│   ├── info/
│   ├── pack/
├── refs/
│   ├── heads/
│   ├── remotes/
│   ├── tags/
```

Each file and directory serves a specific purpose.

---

## **2. Detailed Breakdown of `.git` Files and Directories**
Below is an explanation of each file, its format, introspection methods, and equivalent Git commands (if available).

### **2.1 `.git/HEAD` (Current Branch Reference)**
- **Purpose**: Points to the current checked-out branch.
- **Format**:
  ```
  ref: refs/heads/main
  ```
  OR if in detached HEAD state:
  ```
  <commit-hash>
  ```
- **Introspect**:
  ```sh
  cat .git/HEAD
  ```
- **Git Equivalent**:
  ```sh
  git symbolic-ref HEAD  # Show current branch
  git rev-parse HEAD     # Show current commit hash
  ```

---

### **2.2 `.git/config` (Repository Configuration)**
- **Purpose**: Stores repository-specific configurations, such as remotes, user info, and merge settings.
- **Format** (INI-like):
  ```
  [core]
      repositoryformatversion = 0
      filemode = true
      bare = false
  [remote "origin"]
      url = git@github.com:user/repo.git
      fetch = +refs/heads/*:refs/remotes/origin/*
  ```
- **Introspect**:
  ```sh
  cat .git/config
  ```
- **Git Equivalent**:
  ```sh
  git config --list
  ```

---

### **2.3 `.git/description` (Bare Repository Description)**
- **Purpose**: Used by GitWeb (not usually important for normal repositories).
- **Format**:
  ```
  unnamed repository; edit this file to name it for gitweb.
  ```
- **Introspect**:
  ```sh
  cat .git/description
  ```
- **Git Equivalent**: No direct equivalent.

---

### **2.4 `.git/hooks/` (Client-Side Hooks)**
- **Purpose**: Contains shell scripts that run at different Git events (e.g., pre-commit, post-commit).
- **Example Files**:
  ```
  pre-commit
  post-commit
  pre-push
  ```
- **Introspect**:
  ```sh
  ls -l .git/hooks/
  ```
- **Git Equivalent**: No direct equivalent (hooks are user-defined).

---

### **2.5 `.git/index` (Staging Area)**
- **Purpose**: Binary file storing the list of staged files and their hashes.
- **Format**: Binary format (not human-readable).
- **Introspect**:
  ```sh
  git ls-files --stage
  ```
- **Git Equivalent**:
  ```sh
  git status
  git diff --cached
  ```

---

### **2.6 `.git/info/exclude` (Local Git Ignore)**
- **Purpose**: Works like `.gitignore` but only for this repository (not shared).
- **Format**:
  ```
  # Ignore all log files
  *.log
  ```
- **Introspect**:
  ```sh
  cat .git/info/exclude
  ```
- **Git Equivalent**: No direct equivalent.

---

### **2.7 `.git/logs/` (Commit History Logs)**
- **Purpose**: Stores reflog information, tracking movements of HEAD and branches.
- **Example Files**:
  ```
  .git/logs/HEAD
  .git/logs/refs/heads/main
  ```
- **Format**:
  ```
  <old-commit> <new-commit> author <timestamp> <action>
  ```
- **Introspect**:
  ```sh
  cat .git/logs/HEAD
  ```
- **Git Equivalent**:
  ```sh
  git reflog
  ```

---

### **2.8 `.git/objects/` (Git Object Database)**
- **Purpose**: Stores all commits, trees, and blobs as compressed objects.
- **Structure**:
  ```
  .git/objects/
  ├── info/
  ├── pack/
  ├── a7/
  │   ├── 34bd2d...(commit/blob/tree hash)
  ```
- **Introspect**:
  ```sh
  ls -R .git/objects/
  ```
- **Git Equivalent**:
  ```sh
  git cat-file -p <object-hash>
  ```

---

### **2.9 `.git/refs/` (Branch & Tag References)**
- **Purpose**: Stores references to commit hashes for branches and tags.
- **Example Files**:
  ```
  .git/refs/heads/main
  .git/refs/remotes/origin/main
  ```
- **Format**:
  ```
  <commit-hash>
  ```
- **Introspect**:
  ```sh
  cat .git/refs/heads/main
  ```
- **Git Equivalent**:
  ```sh
  git show-ref
  git branch
  ```

---

### **2.10 `.git/packed-refs` (Packed References)**
- **Purpose**: A compact version of refs used when the repository has many branches/tags.
- **Format**:
  ```
  # pack-refs with: peeled fully-peeled
  <commit-hash> refs/tags/v1.0
  ```
- **Introspect**:
  ```sh
  cat .git/packed-refs
  ```
- **Git Equivalent**:
  ```sh
  git show-ref --tags
  ```

---

## **3. How to List and Inspect All Files in `.git`**
To explore everything in `.git`:

```sh
find .git -type f
```

To check each file manually:

```sh
cat .git/HEAD
cat .git/config
git reflog
ls -R .git/objects/
```

---

## **4. Conclusion**
The `.git` directory is where all Git's magic happens. While users mostly interact with Git via commands, **understanding these files helps with debugging, recovery, and advanced Git usage**.

Would you like an example of manually recreating a `.git` structure from scratch? 🚀