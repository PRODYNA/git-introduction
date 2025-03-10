# Pipelines

## **Integrating CI/CD Pipelines with Git Workflows in GitHub & GitLab**
To optimize CI/CD pipelines in **GitHub Actions** or **GitLab CI/CD**, you should align automation with your **Git workflow philosophy** (feature branching, GitFlow, trunk-based, etc.). Pipelines should trigger at the right points, enforce quality gates, and support efficient development.

---

## **1. General Best Practices for CI/CD in Git Workflows**
✅ **Run CI/CD on Pull Requests (PRs) or Merge Requests (MRs)**  
✅ **Fail fast** on linting, tests, and security scans  
✅ **Use branch-based deployment policies**  
✅ **Auto-cancel redundant pipelines on new commits**  
✅ **Enforce required checks before merging**

---

## **2. CI/CD Pipeline Design for Different Git Workflows**
### **A. Feature Branching Workflow (Common Agile Teams)**
#### **Philosophy**:
- Developers work on **feature branches**.
- CI/CD runs **on PRs** before merging.
- Merging to `main` triggers **deployment**.

#### **Pipeline Strategy**:
🔹 Run **build + tests** on **feature branches**.  
🔹 Require **CI checks to pass** before merging to `main`.  
🔹 Deploy only on **merges to `main`**.  
🔹 Auto-delete **feature branches** after merging.

#### **GitHub Actions Workflow (`.github/workflows/ci.yml`)**
```yaml
name: CI Pipeline

on:
  push:
    branches:
      - main
      - develop
  pull_request:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install dependencies
        run: npm install
      - name: Run tests
        run: npm test
```

#### **GitLab CI/CD (`.gitlab-ci.yml`)**
```yaml
stages:
  - test
  - deploy

test:
  script:
    - npm install
    - npm test
  only:
    - merge_requests
    - main

deploy:
  script:
    - echo "Deploying..."
  only:
    - main
```

🔹 **Why?** Ensures that PRs get tested, and `main` deployments happen only after passing tests.

---

### **B. Trunk-Based Development**
#### **Philosophy**:
- All developers commit directly to `main` or use **short-lived branches**.
- CI/CD runs **on every commit** to `main`.
- Feature flags control unfinished work.

#### **Pipeline Strategy**:
🔹 **Strict tests on all pushes to `main`**.  
🔹 Deploy **small, incremental changes** automatically.  
🔹 Use **feature flags** instead of long-lived branches.

#### **GitHub Actions Workflow**
```yaml
name: Trunk-Based CI/CD

on:
  push:
    branches:
      - main

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm install
      - run: npm test

  deploy:
    needs: build-and-test
    runs-on: ubuntu-latest
    if: success()
    steps:
      - name: Deploy application
        run: ./deploy.sh
```

🔹 **Why?** Ensures that every commit to `main` is stable and deployable.

---

### **C. GitFlow (Enterprise Projects)**
#### **Philosophy**:
- Development happens in `develop`.
- Releases go through `release/*` branches.
- **Hotfixes** go into `hotfix/*` and merge back to `main`.

#### **Pipeline Strategy**:
🔹 CI/CD **runs on `develop`, `release/*`, `hotfix/*`**.  
🔹 **Deploy to staging** from `release/*`.  
🔹 **Deploy to production** when merged into `main`.

#### **GitHub Actions Workflow**
```yaml
name: GitFlow CI/CD

on:
  push:
    branches:
      - develop
      - release/*
      - hotfix/*
  pull_request:
    branches:
      - main
      - develop

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm install
      - run: npm test

  deploy-staging:
    if: github.ref == 'refs/heads/release/*'
    runs-on: ubuntu-latest
    steps:
      - run: ./deploy-staging.sh

  deploy-production:
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - run: ./deploy-production.sh
```

🔹 **Why?** This ensures only stable versions get to production, following GitFlow.

---

### **D. Forking Workflow (Open Source)**
#### **Philosophy**:
- Contributors work in **forks**.
- **Pull Requests (PRs)** trigger CI/CD.
- Only **trusted maintainers** deploy.

#### **Pipeline Strategy**:
🔹 **Run CI on external PRs** but block deployments.  
🔹 **Deploy only when PRs are merged by maintainers**.

#### **GitHub Actions Workflow**
```yaml
name: Forking Workflow CI

on:
  pull_request:
    branches:
      - main
  push:
    branches:
      - main

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm install
      - run: npm test

  deploy:
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - run: ./deploy.sh
```

🔹 **Why?** Ensures contributions are tested but only maintainers can deploy.

---

## **3. Enforcing CI/CD in Git Workflows**
💡 **GitHub Settings**
- **Require CI checks before merging** in branch protection rules.
- **Disallow force pushes** to `main`.
- **Use CODEOWNERS** for mandatory reviews.

💡 **GitLab Settings**
- **Set required jobs in `Settings > CI/CD > General Pipelines`**.
- **Enable "Merge only if pipeline succeeds"**.
- **Use protected branches for production**.

---

## **4. Summary Table: CI/CD for Git Workflows**
| Workflow                | Run CI on PRs? | Auto Deploy? | Special Configs? |
|-------------------------|---------------|--------------|------------------|
| Feature Branching       | ✅ Yes        | ✅ On Merge | PRs require tests |
| Trunk-Based Development | ✅ Yes        | ✅ On Commit | Small frequent merges |
| GitFlow                 | ✅ Yes        | ✅ Only on `release/*`, `main` | Staging deployments |
| Forking Workflow        | ✅ Yes        | ❌ No, maintainers deploy | Restrict external forks |

---

## **Final Thoughts**
🚀 **GitHub Actions / GitLab CI/CD should mirror your Git workflow.**  
📌 Enforce **CI checks before merging** to maintain quality.  
📌 Use **branch-based deployment** to avoid accidental releases.  
📌 **Rebase often, avoid long-lived branches** unless following GitFlow.

Would you like help setting up advanced pipeline conditions, such as **dynamic environments per branch**? 😊