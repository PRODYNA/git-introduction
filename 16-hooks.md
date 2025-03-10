# Git Hooks Manual

## What are Git Hooks?
Git hooks are scripts that run automatically at certain points in the Git workflow. They allow you to enforce rules, automate tasks, and customize Git behavior.

Hooks are stored in the `.git/hooks/` directory inside a Git repository and are executed locally. There are two main types of hooks:

- **Client-side hooks**: Run on developers' machines (e.g., pre-commit, pre-push, post-merge).
- **Server-side hooks**: Run on the remote repository (e.g., pre-receive, post-receive).

## How to Use Git Hooks

1. Navigate to the `.git/hooks/` directory inside your repository.
2. Rename the sample hook (e.g., `pre-commit.sample` to `pre-commit`).
3. Make the script executable: `chmod +x .git/hooks/pre-commit`.
4. Write the script using a supported language (e.g., Bash, Python, or another scripting language).

## Common Git Hooks and Examples

### 1. Pre-commit Hook (Linting & Formatting)
Runs before a commit is created, preventing commits that don’t meet certain criteria.

```bash
#!/bin/bash

# Run linting before committing
if ! flake8; then
  echo "Code does not meet style guidelines. Fix errors before committing."
  exit 1
fi
```

### 2. Pre-push Hook (Prevent Pushing to `main`)
Runs before a `git push` command is executed, allowing you to enforce policies.

```bash
#!/bin/bash

branch=$(git rev-parse --abbrev-ref HEAD)
if [ "$branch" = "main" ]; then
  echo "You cannot push directly to main! Use a feature branch and create a pull request."
  exit 1
fi
```

### 3. Commit-msg Hook (Enforce Commit Message Format)
Ensures that commit messages follow a specific pattern.

```bash
#!/bin/bash

commit_msg_file=$1
commit_msg=$(cat "$commit_msg_file")

if ! [[ "$commit_msg" =~ ^(feat|fix|docs|style|refactor|test|chore): ]]; then
  echo "Commit message must follow the format: <type>: <message> (e.g., feat: add new API)"
  exit 1
fi
```

### 4. Post-merge Hook (Run after a Merge)
Automatically installs dependencies when a merge is completed.

```bash
#!/bin/bash

echo "Running post-merge hook: Installing dependencies"
npm install
```

### 5. Pre-receive Hook (Server-side Hook to Enforce Branch Protection)
Used on remote repositories to validate incoming changes.

```bash
#!/bin/bash

while read oldrev newrev refname; do
  if [[ "$refname" == "refs/heads/main" ]]; then
    echo "Direct commits to main are not allowed!"
    exit 1
  fi
done
```

## Managing Hooks with `core.hooksPath`
By default, hooks are stored in `.git/hooks/`, but you can centralize them using:

```bash
git config core.hooksPath path/to/hooks-directory
```

This allows teams to share hooks in a repository without modifying the local `.git/hooks/` folder.

## Conclusion
Git hooks are a powerful way to enforce rules, automate tasks, and improve workflow efficiency. By implementing them, teams can ensure code quality and streamline their Git operations.


