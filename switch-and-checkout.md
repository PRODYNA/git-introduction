The difference between `git checkout` and `git switch` comes down to **scope** and **clarity**:

1. **`git switch` is dedicated to branch switching**
    - Introduced in Git 2.23 to make branch operations more intuitive.
    - Specifically used to switch branches or create new ones.
    - Cannot be used to checkout individual files.

   Example usage:
   ```sh
   git switch my-branch  # Switch to an existing branch
   git switch -c new-branch  # Create and switch to a new branch
   ```

2. **`git checkout` is more general-purpose**
    - Can switch branches **or** restore individual files.
    - Often considered overloaded and confusing.
    - Can lead to unintended consequences if used without care.

   Example usage:
   ```sh
   git checkout my-branch  # Switch to an existing branch
   git checkout -- file.txt  # Restore file.txt to its last committed state
   ```

### When to use what?
- **Use `git switch`** when you only need to change branches.
- **Use `git checkout`** if you need to restore files or if using an older Git version.

Sure! Let’s break it down further with edge cases and how to create a new branch using both commands.

---

### **Key Differences & Edge Cases**

| Action | `git switch` | `git checkout` | Notes |
|--------|-------------|---------------|-------|
| **Switch to an existing branch** | `git switch my-branch` | `git checkout my-branch` | Both work the same. |
| **Create a new branch and switch to it** | `git switch -c new-branch` | `git checkout -b new-branch` | Both create a branch and switch to it. |
| **Switch to a branch with uncommitted changes (conflict-free)** | ✅ Allowed | ✅ Allowed | Won't discard changes if they don’t conflict. |
| **Switch to a branch with conflicting uncommitted changes** | ❌ Prevented (unless using `-f`) | ❌ Prevented (unless using `--force`) | Use `-f` or `--force` to override. |
| **Restore a file to its last committed state** | ❌ Not supported | ✅ `git checkout -- file.txt` | `git switch` does NOT support file-level operations. Use `git restore` instead. |
| **Checkout a specific commit (detached HEAD)** | ❌ Not supported | ✅ `git checkout <commit>` | Use `git switch --detach <commit>` instead. |
| **Switch to a remote-tracking branch** | `git switch my-branch` (if tracking is set) | `git checkout my-branch` | `git switch` requires upstream tracking or `-c` to create it. |
| **Detach HEAD (checkout a commit without a branch)** | `git switch --detach <commit>` | `git checkout <commit>` | `git switch --detach` is the recommended way. |

---

### **Creating a New Branch and Switching to It**
#### **Using `git switch` (Recommended)**
```sh
git switch -c new-branch
```
- The `-c` flag stands for "create".
- Creates `new-branch` and switches to it.

#### **Using `git checkout` (Older Method)**
```sh
git checkout -b new-branch
```
- The `-b` flag stands for "branch".
- Does the same as `git switch -c`, but `git switch` is more explicit.

---

### **Detached HEAD Mode**
- A **detached HEAD** means Git is not on any branch, just at a specific commit.
- This is useful for checking out an old version of the code without modifying branches.

#### **Using `git switch`**
```sh
git switch --detach <commit-hash>
```
#### **Using `git checkout`**
```sh
git checkout <commit-hash>
```
- Both will place you in a detached HEAD state.
- To return to a branch, use `git switch <branch>` or `git checkout <branch>`.

---

### **Restoring a File**
If you want to revert a file to the last committed version:

#### **Using `git restore` (Newer)**
```sh
git restore file.txt
```
#### **Using `git checkout` (Older)**
```sh
git checkout -- file.txt
```
- `git restore` is the modern equivalent of using `checkout` for files.

---

### **When to Use Which Command?**
- **Use `git switch`** when changing branches—it’s safer and clearer.
- **Use `git restore`** instead of `git checkout` for files.
- **Use `git checkout` only if necessary**, like checking out commits or working with older Git versions.

---

### **Final Recommendation**
- If you’re switching branches, use `git switch`!
- If you’re restoring files, use `git restore`.
- If you’re working with commits, `git checkout` (or `git switch --detach`) is fine.

Let me know if you need more details or real-world examples! 🚀