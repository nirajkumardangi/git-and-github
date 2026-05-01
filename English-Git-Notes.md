# Git Master Class - Complete Notes in Easy English 🚀

---

## 0:00 - Introduction

Git is a **Version Control System (VCS)**. This means it **tracks every change** you make in your code.

**Think of it this way:**
You are writing an essay. You wrote the first draft, then made changes, then made more changes. What if you want to go back to an older draft? Normally you would create files like "essay_v1", "essay_v2", "essay_final", "essay_final_final". Git handles all this **automatically**. It keeps a record of every change, and you can go back to any old version anytime.

**Why is Git important?**
- It maintains the **history** of your code
- **Multiple people** can work together on the same project
- If you make a mistake, you can **go back to an older version**
- **Branching** lets you work on different features without disturbing each other

**Git vs GitHub/GitLab:**
- **Git** = A tool installed on your computer (works locally)
- **GitHub/GitLab** = Online platforms where you upload (push) your Git repository so others can also see and work on it

---

## 1:03 - Verify Git Installation

First, check if Git is installed on your system or not.

**Command:**
```bash
git --version
```

If installed, the output will be something like:
```
git version 2.42.0
```

If not installed:
- **Windows:** Download from [git-scm.com](https://git-scm.com)
- **Mac:** `brew install git`
- **Linux:** `sudo apt install git`

---

## 3:01 - Setting up Personal Info on Git (PREREQUISITE)

Whenever you make a **commit** (save a change) in Git, Git needs to know **who** made the change. That is why setting your name and email is necessary.

**Commands:**
```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

**What does `--global` mean?**
This setting will apply to your **entire system**. This means every Git project will use this name and email. If you want a different name for a specific project, just remove `--global`.

**To check your settings:**
```bash
git config --global user.name
git config --global user.email
```

Or to see all settings at once:
```bash
git config --list
```

**Theory behind this:**
Git is a **distributed** system. Every developer has their own local copy. When multiple people are working, Git needs to know which change was made by whom. That is why this identity setup is important. This information gets permanently stored with every commit.

---

## 5:54 - Git Basic Commands | Study with Me

Here we will understand the basic workflow of Git. This is a very important section.

### Git's Basic Workflow - Three Stages

In Git, every file goes through **three stages**. Understanding this is **very important**:

```
Working Directory  →  Staging Area  →  Repository
     (git add)          (git commit)
```

**1. Working Directory (Workspace):**
- This is the folder where you are actually working
- When you create or edit a file, those changes are here
- Git does not know about these changes yet (untracked/modified)

**2. Staging Area (Index):**
- This is a **preparation area** — a middle zone
- When you do `git add`, the file moves from Working Directory to the Staging Area
- It means: "Yes, I want to save these changes"
- **Analogy:** Imagine you are shopping. The items you put in your **trolley** are like the staging area. The bill has not been paid yet (not committed), but you have decided you want these items.

**3. Repository (Local Repo / .git folder):**
- When you do `git commit`, all data from the staging area gets **permanently saved** in the repository
- This becomes your project's **history**
- Each commit is a **snapshot** — a complete photo of your project at that moment
- **Analogy:** You took the items from the trolley to the **billing counter** and paid. Now it is final.

**Why are there 3 stages? Why not save directly?**
Suppose you changed 10 files. But you want to save only 3 files right now. So you will add only those 3 files to the staging area and commit them. The remaining 7 files will stay in the working directory. This gives you **fine control** over what gets saved.

### Important Basic Commands:

```bash
# Create a new Git repository
git init

# Move files to the staging area
git add filename.txt        # A specific file
git add .                   # All files in the current directory

# Permanently save staged files
git commit -m "Write here what you changed"

# See current status (which file is where)
git status

# See history/log
git log
```

---

## 33:09 - Understanding git init

The **`git init`** command starts a new Git repository.

**What happens when you run `git init`?**

```bash
mkdir my-project
cd my-project
git init
```

Output:
```
Initialized empty Git repository in /path/my-project/.git/
```

When this command runs, a **hidden folder called `.git`** is created inside your folder. This `.git` folder is the **actual Git repository**. Inside it, Git keeps all its data — commits, branches, config, everything.

**What is inside the `.git` folder?**
```
.git/
├── HEAD            → Pointer to the current branch
├── config          → Project-specific settings
├── objects/        → All data (commits, files, trees) stored here
├── refs/           → Pointers for branches and tags
├── hooks/          → Automation scripts
└── ...more files
```

**Important Theory Points:**

1. **Run `git init` only once in a folder.** If you run it again, the existing repository will be re-initialized (data usually does not get lost, but avoid it).

2. **`git init` only creates a local repository.** It does not connect to GitHub/GitLab. That happens later with `git remote add`.

3. **You can turn any folder into a Git repository.** Whether the folder is empty or already has files, `git init` works on both.

4. **Avoid nested git init.** Do not go inside a git repo and run `git init` again. This creates confusion.

5. **If you delete the `.git` folder, your entire Git history will disappear.** So never touch the `.git` folder manually (unless you are an expert).

---

## 43:02 - Understanding git status

The **`git status`** command tells you the **current situation** of your project. It is the most frequently used command.

```bash
git status
```

**This command tells you 4 things:**

### 1. Untracked Files (New files)
```
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        newfile.txt
```
- These are files you have **newly created**
- Git has never tracked them before
- They appear in **red** color
- Git is saying: "I do not know about this file. If you want me to track it, do `git add`"

### 2. Modified Files (Changes in old files)
```
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   oldfile.txt
```
- These are files that Git was already tracking, but you have **changed something** in them
- These changes are **not in the staging area** yet
- They also appear in **red** color

### 3. Staged Files (Ready for commit)
```
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   staged_file.txt
```
- These are files that you have moved to the **staging area** using `git add`
- They appear in **green** color
- They will be included in the next commit

### 4. Clean Working Tree
```
nothing to commit, working tree clean
```
- This means there are no pending changes
- Everything has been committed
- **All sorted!**

**File Lifecycle in Git:**
```
Untracked → Staged → Committed → Modified → Staged → Committed → ...
    ↑                                          ↑
  (new file)                              (edit existing)
```

**Theory: Git's 4 File States:**

| State | Meaning |
|-------|---------|
| **Untracked** | Git does not know about this file |
| **Tracked - Unmodified** | Git is tracking it, no changes made |
| **Tracked - Modified** | Being tracked, changed but not staged |
| **Tracked - Staged** | Change is in staging area, waiting for commit |

**Pro tip:** Run `git status` before and after every command. This way you will always know what is happening.

---

## Advanced Git Commit: Deep Dive

`git commit` is not just about saving code; it is the primary pillar of your project's **history** and **documentation**.

---

### 🏗 1. Conventional Commits (Industry Standard)
Professional teams use a standardized format so that automated tools (like Semantic Release) can automatically determine when to increment version numbers.

**Format:** `<type>(<scope>): <description>`

| Type | Meaning | Example |
| :--- | :--- | :--- |
| **`feat`** | Adding a new feature | `feat(auth): add JWT token validation` |
| **`fix`** | Fixing a bug | `fix(api): resolve null pointer in user-route` |
| **`refactor`** | Code cleanup (neither a bug fix nor a feature) | `refactor: simplify database connection logic` |
| **`docs`** | Changes to documentation | `docs: update README with API endpoints` |
| **`style`** | Formatting (commas, semicolons, spacing) | `style: linting fixes in home component` |
| **`perf`** | Code that improves performance | `perf: optimize image loading speed` |
| **`chore`** | Updating build tools or dependencies | `chore: upgrade tailwind to v4.0` |

---

### 🛠 2. Advanced Commit Clauses & Commands

**A. Modifying the Recent Past (`--amend`)**
If you have already committed but forgot something (e.g., missed a file or a typo), there is no need to create a new commit.
```bash
# To change only the message
git commit --amend -m "Updated correct message"

# To add a forgotten file
git add .
git commit --amend --no-edit
```
> **Rule:** Never `--amend` a commit that has already been **Pushed**. This can break the remote history for others.

**B. Interactive Patch Commits (`-p`)**
Imagine you wrote 50 lines in `index.js`, but you want 25 lines to go into one commit and the remaining 25 into another.
```bash
git commit -p
```
Git will show you code **hunks** (sections). You can choose `y` (yes), `n` (no), or `s` (split) to decide exactly which parts of the code to commit.

**C. Signing Commits (`-S`)**
In open-source and high-security projects, commits are signed with GPG keys. This displays a "Verified" badge on platforms like GitHub.
```bash
git commit -S -m "Secure and verified commit"
```

---

### 📝 3. Anatomy of a Great Commit Message
For significant changes, always use a **Multi-line Commit**:

```bash
git commit
```
*(When the editor opens, use the following format)*

```text
Summarize changes in around 50 characters (Subject Line)

More detailed explanatory text, if necessary. Wrap it to 
about 72 characters. Focus on:
- WHY this change was made.
- HOW it addresses the issue.
- Side effects or breaking changes.

Fixes #402 (Link to the issue)
```

---

### 💡 4. Expert Pro-Tips

**Atomic Commits**
Always follow the **"One Logical Change = One Commit"** rule. 
*   **Bad:** "Fixed Navbar, connected DB, and fixed Typo" in a single commit.
*   **Good:** Three separate, small commits for each task. This makes `git revert` much easier if something goes wrong.

**Empty Commits**
Sometimes you need to commit without any actual code changes (e.g., to trigger a CI/CD deployment pipeline).
```bash
git commit --allow-empty -m "Chore: trigger deployment pipeline"
```

**Verbose Mode**
If you want to see exactly what changes are being included while writing your message:
```bash
git commit -v
```
This displays the full **diff** at the bottom of the editor so you can double-check your work.

---

### 📊 Summary Table

| Feature | Command | Benefits |
| :--- | :--- | :--- |
| **Quick Fix** | `git commit --amend` | Keeps history clean. |
| **Partial Save** | `git commit -p` | Useful for splitting mixed code changes. |
| **Shortcut** | `git commit -am` | Add and commit in one step (for tracked files). |
| **Automation** | `feat/fix/...` | Generates professional changelogs. |

---

## 1:45:00 - Understanding git log (PREREQUISITE)

The **`git log`** command shows you the **complete history** of your project — all commits that have been made so far.

```bash
git log
```

**The output looks something like this:**
```
commit a1b2c3d4e5f67890abcdef1234567890abcdef12 (HEAD -> main)
Author: Jatin <jatin@email.com>
Date:   Wed Dec 25 10:30:00 2024 +0530

    Add user authentication feature

commit 9x8y7z6w5v4u3t2s1r0qponmlkjihgfedcba98
Author: Jatin <jatin@email.com>
Date:   Tue Dec 24 15:00:00 2024 +0530

    Initial commit - project setup
```

### What each commit shows:
- **commit hash** — Unique ID (40 characters)
- **HEAD -> main** — This tells you which is the current branch and where HEAD is pointing
- **Author** — Who made the commit
- **Date** — When the commit was made
- **Message** — What was done (commit message)

### What is HEAD?

**HEAD** is a **pointer** that tells your **current position** in Git history.

**Analogy:** Imagine a book with a **bookmark** in it. The bookmark is on the page where you currently are. HEAD is that bookmark in Git. It tells you which commit you are currently on.

Normally HEAD is on the latest commit, but you can also move it to older commits (that is an advanced topic).

### Different Variations of git log:

```bash
# Simple one-line view (very useful)
git log --oneline
# Output:
# a1b2c3d (HEAD -> main) Add user authentication
# 9x8y7z6 Initial commit

# Graph view (to visualize branches)
git log --oneline --graph
# Output:
# * a1b2c3d (HEAD -> main) Add authentication
# * 9x8y7z6 Initial commit

# See only last N commits
git log -3          # Last 3 commits
git log -5          # Last 5 commits

# History of a particular file
git log filename.txt

# Commits by a specific author
git log --author="Jatin"

# Graph with all branches
git log --oneline --graph --all

# With detailed diff
git log -p
```

### Theory: Why is git log important?

1. **Debugging:** To find out when a bug was introduced
2. **Code Review:** To see who changed what
3. **Revert/Reset:** You need the hash to go back to an old commit
4. **Understanding:** To understand the evolution of the project

---

## 2:00:33 - Undo Commits with git reset

**`git reset`** is used to **undo commits**. It lets you **travel back in time** in your Git history.

### 3 Modes of git reset:

Understanding this is **very important**. Each mode handles the undone changes differently.

### 1. `git reset --soft <commit-hash>`

```bash
git reset --soft HEAD~1
```

**What happens:**
- The commit gets **undone**
- The changes **come back to the staging area** (green)
- No change in the working directory
- Basically only the commit is removed, everything else stays the same

```
BEFORE: Working Dir → Staging → [Commit C] ← HEAD
AFTER:  Working Dir → [Staging has C's changes] → [Commit B] ← HEAD
```

**Analogy:** You packed a parcel and gave it to the courier counter (commit). `--soft` means you took the parcel back from the counter, but the parcel is still packed (it is in the staging area). Only the courier entry was cancelled.

**When to use:** When the commit message is wrong or you forgot to add some more changes.

### 2. `git reset --mixed <commit-hash>` (DEFAULT)

```bash
git reset HEAD~1
# or
git reset --mixed HEAD~1
```

**What happens:**
- The commit gets **undone**
- The changes **come back to the working directory** (red/untracked)
- The staging area becomes **empty**
- If you write just `git reset` without any flag, it is **`--mixed` by default**

```
BEFORE: Working Dir → Staging → [Commit C] ← HEAD
AFTER:  [Working Dir has C's changes] → Empty Staging → [Commit B] ← HEAD
```

**Analogy:** You took the parcel back from the courier counter AND opened it (unstaged). Now the items are lying open with you.

**When to use:** When you want to undo the commit and decide which files to stage again.

### 3. `git reset --hard <commit-hash>`

```bash
git reset --hard HEAD~1
```

**What happens:**
- The commit gets **undone**
- The staging area becomes **empty**
- The working directory also **goes back to that commit's state**
- **CHANGES ARE PERMANENTLY DELETED!** ⚠️

```
BEFORE: Working Dir → Staging → [Commit C] ← HEAD
AFTER:  [Everything is like Commit B] → [Commit B] ← HEAD
```

**Analogy:** You took the parcel back, opened it, and **threw everything in the trash**. Now nothing can come back.

**When to use:** When you are absolutely sure you do not want those changes. **Use very carefully!**

### What does HEAD~1 mean?

```
HEAD~1  → 1 commit back
HEAD~2  → 2 commits back
HEAD~3  → 3 commits back
```

Or you can directly give a **commit hash**:
```bash
git reset --soft a1b2c3d
```

### Summary Table:

| Mode | Commit | Staging Area | Working Directory |
|------|--------|-------------|-------------------|
| `--soft` | ❌ Undone | ✅ Changes stay | ✅ Changes stay |
| `--mixed` | ❌ Undone | ❌ Gets empty | ✅ Changes stay |
| `--hard` | ❌ Undone | ❌ Gets empty | ❌ Changes DELETED |

### ⚠️ Important Warning:
`git reset` **changes history**. If you have already pushed commits to a remote repository (GitHub), then resetting and pushing again can be **problematic** in a team. In such cases, `git revert` is better.

---

## 2:11:36 - Undoing Commits with git revert

**`git revert`** also undoes commits, but **safely**. It does not delete the old commit. Instead, it creates a **new commit** that **reverses** the old changes.

```bash
git revert <commit-hash>
```

### Reset vs Revert - Key Difference

**`git reset`** = **Erases** history (commit disappears)
**`git revert`** = **Adds to** history (a new commit comes that cancels the old one)

```
git reset scenario:
A → B → C (reset to B)
A → B ← HEAD  (C is gone!)

git revert scenario:
A → B → C (revert C)
A → B → C → C' ← HEAD  (C' = opposite of C's changes)
```

### Analogy:
- **Reset** = Your exam paper was wrong, so you **tore the paper** (erased history)
- **Revert** = Your exam paper was wrong, so you wrote on a new sheet "Answer of Q3 was wrong, the correct answer is this" (added a new entry)

### Example:

Suppose you committed "Added wrong config" and its hash is `abc123`:

```bash
git revert abc123
```

This will create a **new commit** in which all changes of `abc123` will be **reversed**. The old commit will remain in the history (it will not be deleted), but its effects will be cancelled.

### When to use Revert vs Reset?

| Situation | Use |
|-----------|-----|
| Local commits (not pushed yet) | `git reset` ✅ |
| Already pushed commits (working with a team) | `git revert` ✅ |
| Want to keep history clean | `git reset` |
| Want a safe undo | `git revert` |

### Theory:
`git revert` is **safe** because:
1. No history gets deleted
2. No conflict arises in the team
3. There is a **record** of what was undone
4. If the revert was wrong, you can even revert the revert!

---

## 2:23:04 - Understanding Branches in Git

Branches are Git's **most powerful feature**. Understanding this is **very important**.

### What is a Branch?

A branch is a **separate line of development**. Imagine you are walking on a road (main branch). Now a fork comes and a new road is formed (new branch). Work can happen on both roads separately without disturbing each other.

### Why do we use Branches?

**Real-life scenario:**
You are building a website. The website is live (on the main branch). Now you need to:
- Add a login feature
- Build a payment system
- Fix a bug

If you do all three directly on the main branch:
- Code can break
- Incomplete features can go live
- Everything becomes a mess

**Solution: Branches!**
```
                    ← feature/login (separate branch)
main → A → B → C 
                    ← feature/payment (separate branch)
                    ← bugfix/header (separate branch)
```

Create a separate branch for each task, complete the work, test it, then merge it into the main branch.

### Default Branch:
- When you do `git init`, a default branch is created
- Previously it was called **`master`**, now mostly it is called **`main`**
- This is your **production/stable** branch

### Branch Commands:

```bash
# See all branches
git branch

# Create a new branch
git branch feature-login

# Switch to a branch (go to it)
git checkout feature-login
# Or (newer command)
git switch feature-login

# Create a new branch AND switch to it (2 tasks in 1 command)
git checkout -b feature-login
# Or
git switch -c feature-login

# Delete a branch
git branch -d feature-login

# Forcefully delete a branch (unmerged branch)
git branch -D feature-login
```

### How does a branch work internally?

A branch is actually just a **pointer** that points to a commit. When you create a new branch, a new pointer is created that points to the **same commit** where you currently are.

```
main → C3
feature → C3   (both are at the same place right now)
HEAD → feature  (you are on the feature branch)
```

When you make a new commit on the feature branch:
```
main → C3
feature → C4 (moved ahead)
HEAD → feature
```

The main branch is still at C3, feature has moved to C4. **Both are independent.**

### Relationship between HEAD and Branch:

**HEAD** always points to the **current branch**. When you switch branches, HEAD moves to that branch.

```bash
# HEAD → main
git switch feature
# HEAD → feature
git switch main
# HEAD → main
```

### Practical Example:

```bash
# You are on the main branch
git branch          # * main

# Create a new branch
git branch feature-login

# Switch to it
git switch feature-login

# Do some work
echo "login code" > login.js
git add .
git commit -m "Add login feature"

# Go back to main
git switch main
# Here login.js will NOT be visible! Because it is on the feature branch

# Go to the feature branch
git switch feature-login
# login.js is back!
```

**This is the magic of branches** — each branch has its own separate state.

---

## 2:50:12 - Understanding Revisiting Branch

This section is about understanding branches **more deeply**.

### Branch Pointer Movement:

```
Initial State:
main: A → B → C ← HEAD

Create feature branch:
main: A → B → C ← HEAD
feature:        ↑ (pointing to the same commit C)

Switch to feature and make a commit:
main: A → B → C
                 ↘
feature:          D ← HEAD

Make another commit on feature:
main: A → B → C
                 ↘
feature:          D → E ← HEAD

Switch back to main and make a commit:
main: A → B → C → F ← HEAD
                 ↘
feature:          D → E
```

Now main and feature have **diverged** — both went in different directions.

### Important Concepts:

1. **Creating a branch is free** — it takes no extra space (it is just a pointer)
2. **When you switch branches, files change** — the working directory updates according to that branch
3. **Carrying uncommitted changes** — If you have not committed your changes and switch branches, Git will either carry the changes with you or give an error (if there is a conflict)

### Detached HEAD State:

```bash
git checkout <commit-hash>
```

If you directly switch to an old **commit** (not a branch), you enter the **"detached HEAD"** state. This means HEAD is not pointing to any branch, it is directly pointing to a commit.

Commits made in this state can be **lost** if you switch back to a branch without creating a new one.

---

## 3:24:01 - Understanding Git Merging

**Merging** means **combining** the work from two branches together.

### Why Merge?

You worked on a feature branch, testing is done, everything is correct. Now you need to bring these changes into the main branch. This process is **merging**.

### How to merge?

**Rule:** Go to the branch you want to merge INTO first, then give the merge command.

```bash
# Go to the main branch
git switch main

# Merge the feature branch into main
git merge feature-login
```

### Types of Merge (Scenarios):

### Scenario 1: Fast-Forward Merge

```
BEFORE:
main: A → B → C
                 ↘
feature:          D → E

(no new commits on main after C)

AFTER merge:
main: A → B → C → D → E ← HEAD
```

**What happened?** The main branch pointer simply moved forward to the latest commit of feature. No new merge commit was created. This is the **simplest** merge.

**When does this happen?** When there are no new commits on the main branch after the feature branch was created. Main can simply move forward.

**Analogy:** You are standing in a line. Nobody is ahead of you. So you simply walk forward. No conflict.

---

## 3:37:51 - Git Merging Scenario 2 Important

### Scenario 2: Three-Way Merge (Recursive Merge)

```
BEFORE:
main: A → B → C → F → G
                 ↘
feature:          D → E

(new commits have come on main too — F, G)

AFTER merge:
main: A → B → C → F → G → M (merge commit) ← HEAD
                 ↘         ↗
feature:          D → E
```

**What happened?** Changes have been made on both branches (F, G on main and D, E on feature). Git combines changes from both and creates a **new merge commit (M)**. This merge commit has **2 parents** — the last commit of main and the last commit of feature.

**When does this happen?** When both branches have different commits and have diverged.

**Why is it called Three-Way?** Git compares three things:
1. **Common ancestor** (C — where both branches separated)
2. **Latest of main branch** (G)
3. **Latest of feature branch** (E)

By comparing these three, Git understands what to merge.

**Analogy:** Two people take a copy of the same document and make different changes separately. Now you need to merge both their changes into one document. So you need to compare with the original document (ancestor) to understand who changed what.

---

## 3:51:45 - Git Merge Scenario Implementation

Practical implementation:

```bash
# Step 1: Initial commits on main branch
git switch main
echo "Hello World" > index.html
git add .
git commit -m "Initial commit"

# Step 2: Create a feature branch
git switch -c feature-navbar

# Step 3: Work on the feature branch
echo "<nav>Navbar</nav>" > navbar.html
git add .
git commit -m "Add navbar"

# Step 4: Go back to main and do some work
git switch main
echo "<footer>Footer</footer>" > footer.html
git add .
git commit -m "Add footer"

# Step 5: Merge the feature branch into main
git switch main
git merge feature-navbar
# This will be a three-way merge because both branches have commits
# A merge commit will be created
```

---

## 4:02:34 - Understanding How to Resolve Merge Conflict in Branches

### What is a Merge Conflict?

When **the same line of the same file** has been edited differently in both branches, Git gets confused — "Whose change should I keep?" This situation is a **merge conflict**.

```
main branch:    line 5 → "Hello World"
feature branch: line 5 → "Hello Git"
```

Git thinks: "Both have changed line 5. How do I know which one is correct?"

So Git **stops the merge** and tells you: "You need to decide this yourself."

### What does a conflict look like?

When a conflict happens, Git puts **markers** in the conflicted file:

```
<<<<<<< HEAD
Hello World
=======
Hello Git
>>>>>>> feature-branch
```

**Explanation:**
- From `<<<<<<< HEAD` to `=======` → Code from the **current branch (main)**
- From `=======` to `>>>>>>> feature-branch` → Code from the **incoming branch (feature)**

### How to resolve a conflict?

**Step 1:** Open the file and decide what to keep:

```
# Option A: Keep main's version
Hello World

# Option B: Keep feature's version
Hello Git

# Option C: Keep both
Hello World
Hello Git

# Option D: Write something new
Hello Everyone
```

**Step 2:** Remove all conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)

**Step 3:** Save the file

**Step 4:** Stage and commit
```bash
git add .
git commit -m "Resolve merge conflict in index.html"
```

### Theory: Why do conflicts happen?

- When **the same lines of the same file** are changed in both branches
- When a file is **deleted** in one branch and **edited** in another
- Git can only automatically merge changes that are in **different files or different lines**

### How to avoid conflicts?

1. **Make small branches** — The less time a branch stays separate, the less chance of conflict
2. **Regularly pull from main** — Keep bringing main's changes into your feature branch
3. **Communication** — Talk to your team about who is working on which file
4. **Make small commits** — Easier to resolve

---

## 4:17:17 - Picking Just Particular Commits with git cherry-pick

**`git cherry-pick`** is a very interesting command. With this, you can pick **just one specific commit** from another branch and apply it to your current branch.

### Normal Merge vs Cherry-pick:

- **Merge:** Brings all commits from the entire branch
- **Cherry-pick:** Brings only one (or a few specific) commits

### Command:
```bash
git cherry-pick <commit-hash>
```

### Example:

```
main: A → B → C ← HEAD
feature: A → B → D → E → F
```

You only want commit **E** on the main branch (not D and F):

```bash
git switch main
git cherry-pick <hash-of-E>
```

Result:
```
main: A → B → C → E' ← HEAD
```

**E'** is a new commit with the same changes as E but a different hash (because the parent is different).

### Analogy:

Imagine a basket full of fruits (commits). You do not want the whole basket (merge), you just want to pick one apple (cherry-pick). 🍒

### When to use?
- You need just one specific bug fix from another branch
- You want only a particular feature's commit from the feature branch
- You accidentally committed on the wrong branch, so cherry-pick it to the right branch

---

## 4:19:01 - Git Revision Part 1 - Study with Me

This is a revision section where all the concepts covered so far are reviewed:

### Quick Recap:

```
1. git init          → Start a new repo
2. git status        → Current situation
3. git add           → Put in staging area
4. git commit        → Permanently save
5. git log           → See history
6. git reset         → Undo commits (changes history)
   --soft            → Changes go to staging
   --mixed           → Changes go to working dir (default)
   --hard            → Changes get DELETED (DANGEROUS!)
7. git revert        → Safe undo (by creating a new commit)
8. git branch        → Manage branches
9. git switch/checkout → Switch branches
10. git merge        → Combine branches
11. git cherry-pick  → Pick a specific commit
```

### Workflow Diagram:
```
Working Directory
      ↓ git add
Staging Area (Index)
      ↓ git commit
Local Repository (.git)
      ↓ git push (we will learn later)
Remote Repository (GitHub/GitLab)
```

---

## 5:12:28 - Understanding Remote Repository

Everything we did until now was **local** — on your computer. Now we will understand **remote repositories**.

### What is a Remote Repository?

A remote repository is a copy of your Git project **hosted on a server**. It is on the internet so that:

1. **Backup** — Even if your computer crashes, the code is safe
2. **Collaboration** — Team members can access it
3. **Sharing** — You can show your code to others

### Popular Remote Hosting Platforms:

| Platform | URL |
|----------|-----|
| **GitHub** | github.com |
| **GitLab** | gitlab.com |
| **Bitbucket** | bitbucket.org |

### Local vs Remote:

```
Your Computer (Local)              Internet (Remote)
┌──────────────────┐              ┌──────────────────┐
│  Working Dir     │              │                  │
│  Staging Area    │  ──push──→   │  Remote Repo     │
│  Local Repo      │  ←──pull──   │  (GitHub/GitLab) │
│  (.git folder)   │              │                  │
└──────────────────┘              └──────────────────┘
```

### Theory: Distributed Version Control

Git is **distributed**, meaning:
- Every developer has a **complete copy** of the repository (full history)
- The remote server also has a complete copy
- Any developer can work offline
- When you get internet, sync with the remote

This is different from **centralized** systems (like SVN) where only the server had the complete code.

---

## 5:19:40 - Creating Account in GitLab

GitLab is a platform where you can host your remote repositories.

**Steps:**
1. Go to [gitlab.com](https://gitlab.com)
2. Sign up (email, username, password)
3. Verify your account
4. On the dashboard, you can create a new repository

(The same process works for GitHub — go to [github.com](https://github.com) and sign up)

---

## 5:20:01 - Understanding git remote add and git push

### git remote add

This command **connects** your local repository to a remote repository.

```bash
git remote add origin https://gitlab.com/username/project-name.git
```

**Breakdown:**
- `git remote add` → Add a remote connection
- `origin` → Name of the remote (the convention is to name it "origin", but you can name it anything)
- `URL` → The address of the remote repository (you get this from GitLab/GitHub)

**What is `origin`?**
- It is just a **nickname** for the remote URL
- Instead of typing the full URL every time, you just write "origin"
- You can also add multiple remotes with different names

```bash
# See remote connections
git remote -v

# Output:
# origin  https://gitlab.com/username/project.git (fetch)
# origin  https://gitlab.com/username/project.git (push)
```

### git push

This command **sends** your local commits to the remote repository.

```bash
git push origin main
```

**Breakdown:**
- `git push` → Send
- `origin` → Where to send (name of the remote)
- `main` → Which branch to send

**When pushing for the first time:**
```bash
git push -u origin main
```

`-u` (or `--set-upstream`) means **set up a tracking relationship**. After this, you only need to write `git push` from now on — you do not need to type the branch and remote name again.

### Flow of Push:

```
Local Repo → (git push) → Remote Repo
Commits that are on local but not on remote → Reach the remote
```

### Theory Points:
1. Push **only sends committed changes** (not staging area or working directory changes)
2. If someone else has already pushed to the remote, you will need to **pull** first (we will learn later)
3. Push requires **authentication** (username/password or SSH key)

---

## 5:45:55 - Revisiting git log for a moment!

After working with remotes, `git log` shows some new things:

```bash
git log --oneline
```

```
a1b2c3d (HEAD -> main, origin/main) Add feature
9x8y7z6 Initial commit
```

**New terms:**
- **HEAD -> main** → You are on the local main branch
- **origin/main** → The remote's (origin) main branch is also at this commit

If you have made a local commit but have not pushed it:
```
b3c4d5e (HEAD -> main) New local commit
a1b2c3d (origin/main) Add feature
```

See — `HEAD -> main` is ahead and `origin/main` is behind. This means there is one extra commit on local that has not gone to the remote yet.

```bash
git push  # After this, both will be the same
```

---

## 5:49:51 - Understanding git clone

The **`git clone`** command downloads a **complete copy** of a remote repository to your computer.

```bash
git clone https://gitlab.com/username/project-name.git
```

### What happens when you clone?

1. A **new folder** is created with the project's name
2. **All files** come into it
3. The **entire Git history** comes (all branches, all commits)
4. The **remote connection** (origin) is **automatically set up**
5. It **checks out** to the default branch

### Clone vs Init:

| `git init` | `git clone` |
|------------|-------------|
| Creates a **new** empty repo | Creates a **copy** of an existing repo |
| No files come | All files + history come |
| Remote must be set up manually | Remote is automatically set up |
| You are starting a project | You are joining someone else's project |

### Analogy:
- `git init` = Bought a new diary, it is blank, start writing now
- `git clone` = Made a **photocopy** of someone's diary, all pages are there

### Clone with a custom folder name:
```bash
git clone https://gitlab.com/username/project-name.git my-folder-name
```

---

## 5:59:04 - Understanding git pull and git fetch

Both of these commands **bring changes from remote to local**, but there is a **fundamental difference** between them.

### Overall Concept:

```
Remote Repo (GitHub/GitLab)
     ↓
git fetch → Only downloads, does NOT merge
git pull  → Downloads + Merges both
```

**Key Formula:**
```
git pull = git fetch + git merge
```

---

## 6:13:31 - Understanding git fetch

**`git fetch`** downloads the latest changes from the remote repository, but it makes **no changes** to your working code.

```bash
git fetch origin
# Or simply
git fetch
```

### What happens during fetch?

1. New commits on the remote get **downloaded**
2. The `origin/main` pointer gets **updated**
3. Your local `main` branch **stays the same** (no changes)
4. Your working directory is **safe**

```
BEFORE fetch:
Remote:  A → B → C → D → E
Local:   A → B → C (origin/main is also here)

AFTER fetch:
Remote:  A → B → C → D → E
Local:   A → B → C ← main (HEAD)
                  ↓
         origin/main → E  (pointer got updated)
```

### To see what came from remote:

```bash
# What came from remote
git log origin/main

# Difference between local and remote
git diff main origin/main
```

### If you want to merge, do it manually:

```bash
git merge origin/main
```

### Analogy:
**Fetch** = A parcel arrived from Amazon, and the **delivery person left it downstairs** in your building (downloaded). Nothing has come into your home (working directory) yet. If you want, go downstairs and pick it up (merge). Or do not.

### When to use?
- When you want to see what is new on the remote **without disturbing your code**
- When you are working with a team and want to review what changes have come before applying them
- When you want a **safe** approach

---

## 6:27:21 - Understanding git pull

**`git pull`** **downloads + merges** changes from the remote together in one step.

```bash
git pull origin main
# Or simply
git pull
```

### What happens during pull?

1. Latest changes get **downloaded** from the remote (fetch)
2. Those changes get **automatically merged** into your current branch
3. Your working directory gets **updated**

```
BEFORE pull:
Remote:  A → B → C → D → E
Local:   A → B → C ← main (HEAD)

AFTER pull:
Remote:  A → B → C → D → E
Local:   A → B → C → D → E ← main (HEAD)
```

### Analogy:
**Pull** = A parcel arrived from Amazon and it got **delivered straight to your home**. Now you have it.

### Fetch vs Pull - Comparison:

| Feature | `git fetch` | `git pull` |
|---------|-------------|------------|
| Download changes | ✅ | ✅ |
| Auto merge | ❌ | ✅ |
| Working dir changes | ❌ | ✅ |
| Safe? | More safe | Slightly risky (conflicts can happen) |
| Control | More control | Less control |
| When to use? | Review first | Need it quickly |

### ⚠️ Conflicts can happen during pull!

If you have also made changes locally and someone else has edited the same file on the remote, a **merge conflict** can happen during pull. You will need to resolve it the same way you resolve conflicts during branch merging.

### Best Practice:
```bash
# First fetch
git fetch

# See what came
git log --oneline origin/main

# If everything looks fine, merge
git merge origin/main

# Or just pull directly if you trust it
git pull
```

---

## 6:33:36 - Store changes temporarily using git stash

**`git stash`** **temporarily saves** your uncommitted changes without committing them. It is like putting them in a safe.

### The problem that stash solves:

You are working on a feature branch, and your work is half done (not ready to commit). Suddenly your boss says "Fix an urgent bug on the main branch!"

Now the problem is:
- You cannot switch branches because your changes are uncommitted
- You do not want to commit because the work is half done
- You do not want to delete the changes either

**Solution: `git stash`!**

### Commands:

```bash
# Stash your changes (temporarily save)
git stash
# Or with a message
git stash save "work in progress on login"

# See the stash list
git stash list
# Output:
# stash@{0}: WIP on feature: abc123 work in progress on login
# stash@{1}: WIP on feature: def456 some other stash

# Bring stash back (and remove from stash)
git stash pop

# Bring stash back (but keep it in stash too)
git stash apply

# Apply a specific stash
git stash apply stash@{1}

# Delete a stash
git stash drop stash@{0}

# Delete all stashes
git stash clear
```

### Flow of Stash:

```
1. There are changes in the Working Directory (uncommitted)
2. git stash → Changes TEMPORARILY disappear, directory becomes clean
3. Switch branch, fix the bug, commit
4. Come back to the original branch
5. git stash pop → Changes are BACK!
```

### Analogy:
You are cooking in the kitchen (feature development). The doorbell rings (urgent task). You **put everything in the fridge** (stash). You go to the door and handle the task. You come back and **take everything out of the fridge** (stash pop) and continue cooking.

### Theory Points:
1. Stash follows a **stack** data structure (LIFO — Last In First Out)
2. You can have multiple stashes
3. Stash is **branch-independent** — you can stash on one branch and pop on another
4. **Tracked files** are stashed by default. For untracked files, use the `-u` flag:
   ```bash
   git stash -u
   ```

---

## 6:40:15 - Ignore Files using .gitignore

### The Problem:
Every project has some files that you should **not track** in Git:
- `node_modules/` (very large folder, comes back with npm install)
- `.env` (passwords, API keys — sensitive information)
- Log files (`.log`)
- OS files (`.DS_Store` on Mac, `Thumbs.db` on Windows)
- Build folders (`dist/`, `build/`)
- IDE settings (`.vscode/`, `.idea/`)

If these files get into Git:
- The repository size will increase greatly
- Sensitive data can leak
- Unnecessary changes will be tracked

### What is a .gitignore file?

It is a special file in which you write **which files/folders Git should ignore**.

### How to create it?

Create a file named `.gitignore` in the **root folder** of your project:

```bash
touch .gitignore
```

### What to write in .gitignore?

```gitignore
# This is a comment

# Ignore a specific file
secret.txt
.env

# Ignore a specific folder (put / at the end)
node_modules/
dist/
build/

# Ignore all files of a particular extension
*.log
*.tmp
*.cache

# Pattern matching
*.pyc
__pycache__/

# Exception - DO track this file (negate with !)
!important.log

# Ignore a file in a nested folder
logs/debug.log

# Ignore any .env file in any folder
**/.env
```

### Important Rules:

1. **The `.gitignore` file itself should be committed** — so that everyone on the team ignores the same files
2. **Already tracked files will not be ignored** — If a file is already being tracked, just adding it to `.gitignore` will not ignore it. You need to untrack it first:
   ```bash
   git rm --cached filename.txt
   ```
   `--cached` means remove only from Git, do not delete from the file system.

3. **You can also create a global gitignore:**
   ```bash
   git config --global core.excludesfile ~/.gitignore_global
   ```

### Theory: Why is it important?

| Ignore this | Reason |
|-------------|--------|
| `node_modules/` | Very large, comes back with `npm install` |
| `.env` | Passwords, API keys — **security risk!** |
| `*.log` | Temporary files, different on every machine |
| `.DS_Store` | OS-specific, different on every machine |
| `build/` | Generated files, can be recreated from source |

---

## 🎯 COMPLETE SUMMARY — Everything at a Glance

```
LOCAL COMMANDS:
├── git init            → Start a new repo
├── git status          → See current situation
├── git add             → Put in staging area
├── git commit          → Permanently save
├── git log             → See history
├── git reset           → Undo commits (changes history)
│   ├── --soft          → Changes go to staging
│   ├── --mixed         → Changes go to working dir
│   └── --hard          → Changes get DELETED!
├── git revert          → Safe undo (new commit)
├── git branch          → Manage branches
├── git switch          → Switch branches
├── git merge           → Combine branches
├── git cherry-pick     → Pick a specific commit
├── git stash           → Temporarily save changes
└── .gitignore          → Ignore files

REMOTE COMMANDS:
├── git remote add      → Connect to a remote
├── git push            → Send Local → Remote
├── git clone           → Copy Remote → Local
├── git fetch           → Download (no merge)
└── git pull            → Download + Merge (fetch + merge)
```

### Complete Workflow:
```
1. git init / git clone
2. Create/edit files
3. git add .
4. git commit -m "message"
5. git push origin main
6. (Other people) git pull
7. Repeat 2-6
```

