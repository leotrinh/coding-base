# Git Branching Strategy & Source Code Integration 

**Author:** Leo

## 1. Purpose
To unify and standardize source code management across the development team.

## 2. Preparation

### Prerequisites
1.  **Git Proficiency**: Developers must understand how to work with Git.
2.  **Resources**:
    *   Git Basics (Vietnamese): https://handbook.tinhtd.info/books/git/page/co-ban-ve-git or https://backlog.com/git-tutorial/vn/intro/intro1_1.html
    *   SSH Key Setup: https://blog.tinhtd.info/2021/06/tao-ssh-key-local-va-add-vao-git-account.html

### Daily Workflow
~~~mermaid
graph TD
    Start([Start]) --> A[Checkout develop]
    A -->|git checkout -b feat/...| B[Create Feature Branch]
    B --> C[Development]
    C -->|git commit| D[Commit Work]
    D -->|git pull origin develop| E[Pull latest develop]
    E --> F{Conflicts?}
    F -- Yes --> G[Resolve Conflicts]
    G -->|Commit Merge| H[Ready to Push]
    F -- No --> H
    H -->|Push & Create PR| End([Create PR to develop])
    
    style Start fill:#f9f,stroke:#333
    style End fill:#9f9,stroke:#333
~~~
![Daily Workflow][image5]

*Note: Always pull from the working branch (`develop`) daily to ensure you have the latest code and resolve conflicts early.*

### Recommended Extensions
*   **GitLens**: https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens
*   **Local History**: https://marketplace.visualstudio.com/items?itemName=xyz.local-history

---

## 3. Branching Strategy


We follow a **Trunk-Based** development flow where `develop` is the default working branch.

### General Flow
1.  Create a new branch from **develop**.
2.  Merge completed work back to **develop** via Pull Request.
3.  Merge to **staging/test/release** branches from **develop** for testing.
4.  Merge to **main** from **staging/test/release** for production releases.

---

### 🔄 Sync Latest Code from `develop` (Merge vs Rebase)

During development, developers usually sync code in 2 ways depending on preference and experience.

---

#### ✅ Option 1: Merge (Safe & Recommended)

~~~bash
git checkout develop
git pull origin develop

git checkout <your-branch>
git merge develop
~~~

**Example:**
~~~bash
git checkout develop
git pull origin develop

git checkout feat/login
git merge develop
~~~

**Result:**
- Creates a merge commit
- Keeps full history (branch structure)
- Easy & safe for team collaboration

---

#### 🚀 Option 2: Rebase (Cleaner History)

~~~bash
git checkout <your-branch>
git fetch origin
git rebase origin/develop
~~~

**Example:**
~~~bash
git checkout feat/login
git fetch origin
git rebase origin/develop
~~~

**If conflict:**
~~~bash
git add .
git rebase --continue
~~~

**Abort if needed:**
~~~bash
git rebase --abort
~~~

**Result:**
- Linear commit history
- No merge commit
- Cleaner log but requires Git understanding

---

#### ⚖️ Comparison

| Criteria        | Merge                  | Rebase                  |
|----------------|-----------------------|-------------------------|
| Ease           | Easy                  | Medium                  |
| History        | Branching             | Linear                  |
| Safety         | High                  | Risk if misused         |
| Recommended    | Default               | Advanced users          |

---

#### 💡 Best Practice

- Use **Merge** by default for team consistency
- Use **Rebase** if you understand Git well
- ❗ Do NOT rebase shared branches

---

#### 🧠 Real Case Mapping

**Case 1 (Merge):**
~~~bash
git checkout develop
git pull

git checkout feat/xxx
git merge develop
~~~

**Case 2 (Rebase):**
~~~bash
git checkout feat/xxx
git fetch
git rebase origin/develop
~~~

---

### Branch Naming Conventions

1.  **feat/***
2.  **bugfix/***
3.  **hotfix/***
4.  **release/***
5.  **refactor/***
6.  **chore/***
7.  **sprint/***

---

## 4. Commit Messages & Pull Request Conventions

### Commit Messages

Format:
`#<TaskID> - <type>(<module/feature>): <Commit Message>`

---

[image4]: ../static/images/pr-review.png
[image5]: ../static/images/daily-git-workflow.png