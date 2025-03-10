# Advanced Git Features

### **1. Binary Handling & Large File Support**
- **Git Large File Storage (LFS)**: Replaces large files (e.g., videos, images, datasets) with pointers and stores them separately to avoid bloating the repository.
- **Git Annex**: Alternative to LFS, allowing managing large/binary files outside Git while keeping track of them.
- **Delta Compression & `core.bigFileThreshold`**: Git handles binary files poorly due to diff-based storage; this setting optimizes performance for large binaries.

### **2. Submodules & Subtrees**
- **Git Submodules**: Enables linking another repository within a repository (useful for dependencies, libraries).
    - Requires manual updates (`git submodule update --init --recursive`).
    - Challenges: Version tracking, nested submodules, and additional complexity.
- **Git Subtree**: An alternative that allows merging and splitting subprojects into a main repository with easier management (`git subtree add/push/pull`).

### **3. Worktrees**
- **Git Worktrees**: Allows working on multiple branches simultaneously in different directories without cloning the repo multiple times (`git worktree add`).
- **Use cases**: Parallel feature development, handling hotfixes while working on a big feature branch.

### **4. Refs, Reflogs, and the Git Object Model**
- **Reflogs (`git reflog`)**: Tracks branch movements and allows recovery of lost commits.
- **Loose & Packed Objects**: Understanding blobs, trees, commits, and tags.
- **Alternate Object Storage (`.git/objects/info/alternates`)**: Allows sharing objects between repositories.

### **5. Advanced History Manipulation**
- **Interactive Rebase (`git rebase -i`)**: Rewriting commit history (squash, fixup, reordering).
- **Filter-Branch & `git filter-repo`**: Cleaning repository history (e.g., removing sensitive data).
- **Commit Graph (`git commit-graph` and `git gc`)**: Improves performance for large repositories.

### **6. Sparse Checkouts & Partial Clones**
- **Sparse Checkout (`git sparse-checkout`)**: Allows working with only a subset of a repository’s files (useful for monorepos).
- **Partial Clone (`git clone --filter=blob:none`)**: Clones a repo without downloading all blobs initially, fetching them on-demand.

### **7. Git Hooks & Custom Workflows**
- **Client-side Hooks (`.git/hooks/`)**: Automation before/after commits, pushes, merges (e.g., linting, security checks).
- **Server-side Hooks**: Enforcing policies on a shared repository (e.g., preventing force pushes).
- **Custom Merge Drivers**: Handling specific merge scenarios for non-text files.

### **8. Signed Commits & Secure Collaboration**
- **Signed Commits (`git commit -S`)**: Verifying commit authorship (GPG/SSH signatures).
- **Signed Tags (`git tag -s`)**: Ensuring tag authenticity.
- **Git Verify & `git fsck`**: Checking repository integrity.

### **9. Bisecting & Debugging**
- **Git Bisect (`git bisect start`)**: Finding the commit that introduced a bug by binary search.
- **Git Blame (`git blame`)**: Tracking changes in a file to specific commits/authors.
- **Git Grep (`git grep`)**: Searching efficiently within a repository.

### **10. Alternative Backends & Experimental Features**
- **Reftables (Experimental)**: Aims to improve reference storage performance.
- **Git with Different Backends**: Git can store objects in alternative formats (e.g., SQLite, SHA-256 support).
- **Using `git update-index --skip-worktree` vs. `assume-unchanged`**: Ignoring local file changes.

