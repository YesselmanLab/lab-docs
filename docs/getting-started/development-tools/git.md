# Git Guide

Git is a distributed version control system that tracks changes in your code and enables collaboration. It's essential for managing code, tracking history, and working with others.

---

## What is Version Control? (For Complete Beginners)

If you've never used version control before, think of it like this:

### The Problem Without Version Control

Imagine you're writing a paper and you save it as `paper.doc`. Then you make changes and save it as `paper_v2.doc`. Then more changes become `paper_final.doc`, then `paper_final_really.doc`, and so on. You end up with:
- Multiple confusing file versions
- No clear record of what changed and when
- Risk of losing work
- Hard to collaborate with others

### How Version Control Solves This

Version control is like having a **time machine for your files**. It:
- **Saves snapshots** of your project at different points in time
- **Tracks what changed** between versions
- **Lets you go back** to any previous version
- **Allows multiple people** to work on the same files without conflicts
- **Keeps everything organized** in one place

### Real-World Analogy

Think of Git like a **sophisticated save system in a video game**:
- Each "save" is a **commit** (snapshot of your project)
- You can load any previous save
- You can create different "save slots" (branches) for experiments
- You can see what changed between saves
- Multiple players (collaborators) can work on the same game

---

## What is Git?

Git is a version control system that:
- **Tracks changes** in your files over time
- **Enables collaboration** by allowing multiple people to work on the same project
- **Preserves history** so you can revert to previous versions
- **Manages branches** for parallel development
- **Integrates with GitHub/GitLab** for remote repositories

### Why Use Git?

Even if you work alone, Git is valuable because:
1. **Safety net**: Never lose your work - you can always go back
2. **Experimentation**: Try new things without fear - you can always undo
3. **Documentation**: See what you changed and when
4. **Organization**: Keep your project organized and clean
5. **Collaboration**: Essential when working with others
6. **Professional standard**: Used by virtually all software projects

---

## Installation

### macOS Installation

```bash
# Install via Homebrew (recommended), might not be necessary as it usually comes on a mac
brew install git

# Verify installation
git --version
```

### Initial Configuration

After installation, configure Git with your information:

```bash
# Set your name
git config --global user.name "Your Name"

# Set your email
git config --global user.email "your.email@example.com"

# Verify configuration
git config --list
```

### Additional Configuration

```bash
# Set default branch name to 'main'
git config --global init.defaultBranch main

# Set default editor (VS Code)
git config --global core.editor "code --wait"

# Or use Cursor
git config --global core.editor "cursor --wait"

# Or use vim
git config --global core.editor "vim"

# Enable colored output
git config --global color.ui auto

# Set default push behavior
git config --global push.default simple
```

---

## Basic Concepts (Explained Simply)

### Repository (Repo)

A **repository** (or "repo") is simply a folder that Git is tracking. It contains:
- Your project files (code, data, documents, etc.)
- A hidden `.git` folder that stores all the history

Think of it like a **special folder** where Git watches everything you do.

**Types of repositories:**
- **Local**: On your computer (the folder on your Mac)
- **Remote**: On a server like GitHub or GitLab (backup/collaboration)

### Commit

A **commit** is a saved snapshot of your project. Think of it like:
- A **save point** in a video game
- A **photograph** of your project at a moment in time
- A **checkpoint** you can return to

Each commit includes:
- **What changed**: Which files were modified
- **When**: Timestamp
- **Who**: Your name (from Git config)
- **Why**: Your commit message explaining the changes
- **Unique ID**: A hash like `a1b2c3d` (like a fingerprint)

**Important**: A commit is permanent, but you can always create new commits that undo changes.

### Branch

A **branch** is like a parallel timeline. Imagine:
- **Main branch**: Your "official" version (like the main story)
- **Feature branch**: A copy where you experiment (like a "what if" scenario)

You can:
- Work on features without affecting the main code
- Switch between branches instantly
- Merge branches together when ready

**Analogy**: Like having multiple drafts of a paper - you keep the main one safe while you experiment with a copy.

### The Three States: Understanding Git's Workflow

Git has three important "areas" where your files can be:

1. **Working Directory** (Your Files)
   - This is your normal folder with your files
   - You edit files here normally
   - Git sees these changes but hasn't saved them yet

2. **Staging Area** (Ready to Save)
   - Files you've marked as "ready to commit"
   - Like putting items in a shopping cart before checkout
   - You choose which changes to include

3. **Repository** (Saved History)
   - Committed snapshots (the saved history)
   - Permanent record of your project
   - This is what Git tracks

**The Flow:**
```
Edit files → Stage changes → Commit → History saved!
```

**Visual Example:**
```
Working Directory          Staging Area           Repository
─────────────────         ────────────          ──────────
file1.py (modified)  →    file1.py (staged)  →  commit #1
file2.py (modified)        (not staged)           commit #2
file3.py (unchanged)       (not staged)           commit #3
```

---

## Your First Git Repository: Step-by-Step Tutorial

Let's create your first Git repository from scratch. Follow along!

### Step 1: Create a Project Folder

```bash
# Create a new folder for your project
mkdir my-first-project
cd my-first-project

# Verify you're in the right place
pwd
# Should show: /Users/yourname/my-first-project
```

### Step 2: Initialize Git Repository

```bash
# Turn this folder into a Git repository
git init
```

**What just happened?**
- Git created a hidden `.git` folder in your directory
- This folder stores all Git's history and configuration
- Your folder is now a Git repository!

**Verify it worked:**
```bash
# Check if .git folder exists (it's hidden, so use -a flag)
ls -la
# You should see a .git folder
```

### Step 3: Create Your First File

```bash
# Create a simple Python file
echo 'print("Hello, Git!")' > hello.py

# Or create it with your editor
# code hello.py  # or cursor hello.py
```

### Step 4: Check What Git Sees

```bash
# See the status of your repository
git status
```

**What you'll see:**
```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        hello.py

nothing added to commit but untracked files present (use "git add" to track)
```

**Understanding the output:**
- "No commits yet": You haven't saved any snapshots yet
- "Untracked files": Git sees `hello.py` but isn't tracking it yet
- Git is telling you what to do next: use `git add`

### Step 5: Stage Your File (Add to Staging Area)

```bash
# Tell Git to track this file (add to staging area)
git add hello.py
```

**What just happened?**
- Git added `hello.py` to the **staging area**
- The file is now "ready to be committed"
- Think of it like putting an item in your shopping cart

**Check status again:**
```bash
git status
```

**Now you'll see:**
```
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   hello.py
```

**Notice the change:**
- File moved from "Untracked" to "Changes to be committed"
- Git is ready to save this file

### Step 6: Make Your First Commit

```bash
# Save this snapshot with a message
git commit -m "Add hello.py - my first file"
```

**What just happened?**
- Git created your first commit (snapshot)
- Your file is now permanently saved in Git's history
- The `-m` flag lets you add a message describing what you did

**Check status again:**
```bash
git status
```

**You'll see:**
```
On branch main
nothing to commit, working tree clean
```

**This means:**
- Everything is saved
- No changes pending
- Your working directory is "clean"

### Step 7: View Your History

```bash
# See your commit history
git log
```

**You'll see something like:**
```
commit a1b2c3d4e5f6... (HEAD -> main)
Author: Your Name <your.email@example.com>
Date:   Mon Jan 15 10:30:00 2024

    Add hello.py - my first file
```

**Understanding the output:**
- **commit**: The unique ID of this snapshot
- **Author**: Who made this commit (you!)
- **Date**: When it was made
- **Message**: What you wrote describing the change
- **(HEAD -> main)**: This is your current position

### Step 8: Make Changes and Commit Again

```bash
# Edit your file
echo 'print("Hello, Git!")
print("This is my second commit!")' > hello.py

# Check what changed
git status
```

**You'll see:**
```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   hello.py
```

**See what actually changed:**
```bash
# See the exact differences
git diff
```

**You'll see:**
```
diff --git a/hello.py b/hello.py
index 1234567..abcdefg 100644
--- a/hello.py
+++ b/hello.py
@@ -1 +1,2 @@
 print("Hello, Git!")
+print("This is my second commit!")
```

**The `+` means a line was added.**

**Now commit the change:**
```bash
# Stage the change
git add hello.py

# Commit it
git commit -m "Add second print statement to hello.py"
```

**View your history:**
```bash
git log --oneline
```

**You'll see:**
```
a1b2c3d Add second print statement to hello.py
f9e8d7c Add hello.py - my first file
```

**Notice:**
- Two commits now
- Most recent is at the top
- Each has a unique ID

---

## Understanding the Basic Workflow

Now that you've done it once, here's the pattern you'll use every day:

### The Daily Git Workflow

```
1. Edit files (in your working directory)
   ↓
2. Check what changed: git status
   ↓
3. Stage changes: git add <files>
   ↓
4. Commit: git commit -m "Description"
   ↓
5. Repeat!
```

### Detailed Commands

#### Check Status

```bash
# See what files have changed
git status

# Short, compact status
git status -s
# Shows: M  modified_file.py (M = modified)
#        ?? new_file.py      (?? = untracked)
```

**When to use:** Always check status before committing to see what will be saved.

#### Add Files to Staging

```bash
# Add a specific file
git add filename.py

# Add all files in current directory (most common)
git add .

# Add all files in entire repository
git add -A

# Add files interactively (choose parts of files)
git add -p
```

**What happens:**
- Files move from "working directory" to "staging area"
- They're now ready to be committed
- You can stage multiple files before committing

**Example:**
```bash
# You edited 3 files
git status
# Shows: modified: file1.py, file2.py, file3.py

# Stage all of them
git add .

# Or stage just one
git add file1.py
git status
# Now shows: file1.py staged, file2.py and file3.py still modified
```

#### Commit Changes

```bash
# Commit with a message (most common)
git commit -m "Add new feature"

# Commit with detailed message
git commit -m "Add new feature" -m "This feature does X, Y, and Z"

# Commit all tracked files (skip staging - use carefully!)
git commit -am "Quick commit"
# Note: This only works for files Git already tracks
```

**Commit messages should:**
- Be clear and descriptive
- Explain **what** you changed and **why**
- Be written in present tense: "Add feature" not "Added feature"

**Good commit messages:**
```bash
git commit -m "Fix bug in data loading function"
git commit -m "Add error handling for missing files"
git commit -m "Update documentation for installation"
```

**Bad commit messages:**
```bash
git commit -m "fix"           # Too vague
git commit -m "stuff"         # Meaningless
git commit -m "asdf"          # Random characters
git commit -m "Fixed it"     # Past tense, vague
```

### View History

```bash
# View commit history (detailed)
git log

# One-line format (easier to read)
git log --oneline

# Graph view (shows branches)
git log --graph --oneline --all

# Show changes in commits
git log -p

# Search commits by message
git log --grep="keyword"

# Limit number of commits shown
git log -5  # Show last 5 commits
```

**Understanding `git log` output:**

Full format shows:
```
commit a1b2c3d4e5f6789... (HEAD -> main)
Author: Your Name <email@example.com>
Date:   Mon Jan 15 10:30:00 2024 -0500

    Your commit message here
```

- **commit**: Unique identifier (hash)
- **HEAD**: Points to your current commit
- **main**: The branch you're on
- **Author**: Who made the commit
- **Date**: When it was made
- **Message**: What you wrote

### View Changes

```bash
# See unstaged changes (what you edited but haven't staged)
git diff

# See staged changes (what's ready to commit)
git diff --staged

# See changes in a specific commit
git show <commit-hash>

# See changes between two commits
git diff commit1 commit2
```

**Understanding `git diff` output:**

```diff
diff --git a/file.py b/file.py
index 1234567..abcdefg 100644
--- a/file.py
+++ b/file.py
@@ -1,3 +1,4 @@
 print("Hello")
+print("New line added")
 print("World")
```

- Lines starting with `-` were removed (red)
- Lines starting with `+` were added (green)
- Lines without `-` or `+` are context (unchanged)

**Common scenarios:**

```bash
# "What did I change but haven't staged?"
git diff

# "What am I about to commit?"
git diff --staged

# "What changed in the last commit?"
git show HEAD

# "What changed 3 commits ago?"
git show HEAD~3
```

---

## Branching: Working on Different Versions

### What is a Branch? (For Beginners)

Think of branches like **parallel timelines** or **different drafts**:

- **Main branch**: Your "official" version (like a final draft)
- **Feature branch**: A copy where you experiment (like a rough draft)

**Why use branches?**
- Work on new features without breaking working code
- Experiment safely - you can always delete a branch
- Multiple people can work on different things simultaneously
- Keep your main code stable while developing

**Real-world analogy:**
Imagine writing a paper:
- **Main branch**: Your final, polished version
- **Feature branch**: A copy where you try a new section
- If the new section doesn't work, you just delete that copy
- If it works, you add it to the main version

### Understanding Your Current Branch

```bash
# See what branch you're on
git branch
```

**Output:**
```
* main
```

The `*` shows you're on the `main` branch.

### Create and Switch Branches

```bash
# Create a new branch (but stay on current branch)
git branch feature-branch

# Switch to a branch
git checkout feature-branch

# Create and switch in one command (most common)
git checkout -b feature-branch

# Modern way (Git 2.23+) - clearer command
git switch -c feature-branch

# List all local branches
git branch

# List remote branches
git branch -r

# List all branches (local and remote)
git branch -a
```

### Your First Branch: Step-by-Step

Let's create a branch to add a new feature:

```bash
# 1. Make sure you're on main and everything is committed
git status
# Should say: "working tree clean"

# 2. Create and switch to a new branch
git checkout -b add-greeting-feature

# 3. Verify you're on the new branch
git branch
# Should show: * add-greeting-feature (with *)

# 4. Make changes
echo 'def greet(name):
    return f"Hello, {name}!"' > greeting.py

# 5. Commit the changes
git add greeting.py
git commit -m "Add greeting function"

# 6. View your branches
git branch
# Shows both: main and add-greeting-feature (with * on current)

# 7. Switch back to main
git checkout main
# Notice: greeting.py is gone! (it's only in the branch)

# 8. Switch back to your feature branch
git checkout add-greeting-feature
# greeting.py is back!
```

**Key insight:** Each branch is like a separate folder. Files in one branch don't exist in another until you merge them.

### Merge Branches: Combining Your Work

**What is merging?**
Merging takes changes from one branch and adds them to another. It's like copying your new section from your rough draft into your final paper.

**Step-by-step merge:**

```bash
# 1. Make sure your feature branch is complete and committed
git checkout add-greeting-feature
git status
# Should be clean

# 2. Switch to the branch you want to merge INTO (usually main)
git checkout main

# 3. Merge the feature branch
git merge add-greeting-feature
```

**What happens:**
- Git combines the changes from `add-greeting-feature` into `main`
- If there are no conflicts, Git does it automatically
- You'll see a message like: "Merge made by the 'recursive' strategy"

**After merging:**
```bash
# Your greeting.py is now in main!
ls
# Should show greeting.py

# View the history
git log --oneline --graph
# Shows the merge commit
```

**Merge with a message:**
```bash
git merge feature-branch -m "Merge feature branch: add greeting function"
```

**Common merge scenarios:**

**Fast-forward merge** (simple case):
- Your feature branch has new commits
- Main branch hasn't changed
- Git just moves the pointer forward
- No merge commit needed

**Three-way merge** (more complex):
- Both branches have new commits
- Git creates a merge commit
- Combines changes from both branches

### Delete Branches

```bash
# Delete local branch
git branch -d feature-branch

# Force delete (if not merged)
git branch -D feature-branch

# Delete remote branch
git push origin --delete feature-branch
```

---

## Remote Repositories: Backing Up and Sharing

### What is a Remote Repository?

A **remote** is a copy of your repository stored somewhere else (usually on GitHub or GitLab). Think of it as:
- A **backup** of your code
- A place to **share** your code with others
- A way to **collaborate** on projects

**Local vs Remote:**
- **Local**: On your computer (`~/my-project/`)
- **Remote**: On a server (`github.com/username/repo`)

### Setting Up a Remote (First Time)

**Step 1: Create repository on GitHub/GitLab**
1. Go to GitHub.com (or GitLab.com)
2. Click "New repository"
3. Name it (e.g., "my-first-project")
4. Don't initialize with README (you already have files)
5. Click "Create repository"

**Step 2: Connect your local repo to remote**

```bash
# Add the remote (GitHub will show you this command)
git remote add origin https://github.com/your-username/my-first-project.git

# Verify it was added
git remote -v
```

**Output:**
```
origin  https://github.com/your-username/my-first-project.git (fetch)
origin  https://github.com/your-username/my-first-project.git (push)
```

**What is "origin"?**
- `origin` is just a nickname for your remote
- You can name it anything, but `origin` is the convention
- It's like a bookmark to the remote URL

**Step 3: Push your code**

```bash
# Push your main branch to remote (first time)
git push -u origin main
```

**What just happened?**
- Your local commits were uploaded to GitHub
- The `-u` flag sets up tracking (so next time you can just use `git push`)
- Your code is now backed up and visible on GitHub!

**Step 4: Verify on GitHub**
- Refresh your GitHub page
- You should see your files!

### Managing Remotes

```bash
# View all remotes
git remote -v

# View details about a remote
git remote show origin

# Rename a remote
git remote rename origin upstream

# Remove a remote
git remote remove origin

# Change remote URL
git remote set-url origin https://github.com/new-url.git
```

### Push to Remote: Uploading Your Changes

**What is pushing?**
Pushing uploads your local commits to the remote repository. It's like saving your work to the cloud.

**First time push:**
```bash
# Push and set up tracking
git push -u origin main
```

**What the flags mean:**
- `-u` (or `--set-upstream`): Sets up tracking so Git remembers where to push
- `origin`: The remote name
- `main`: The branch to push

**After first push:**
```bash
# Just push (Git remembers where to go)
git push

# Or be explicit
git push origin main
```

**Push a different branch:**
```bash
# Push your feature branch
git push origin feature-branch

# Push and set up tracking for new branch
git push -u origin feature-branch
```

**Force push (DANGER - use carefully!):**
```bash
# Only use if you know what you're doing
git push --force
```

**When you might need force push:**
- You rewrote history (amended commits)
- You want to overwrite remote with your local version
- **Warning**: This can delete other people's work! Only use on your own branches.

### Pull from Remote: Downloading Changes

**What is pulling?**
Pulling downloads changes from the remote and merges them into your local repository. It's like syncing your work.

**Basic pull:**
```bash
# Download and merge latest changes
git pull
```

**What `git pull` does:**
1. Downloads changes from remote (`git fetch`)
2. Merges them into your current branch (`git merge`)

**Pull from specific remote and branch:**
```bash
git pull origin main
```

**Safer approach (see changes first):**
```bash
# First, just download (don't merge yet)
git fetch origin

# See what changed
git log HEAD..origin/main

# Then merge when ready
git merge origin/main
```

**Common scenario:**
```bash
# Someone else pushed changes to GitHub
# You want to get them:

# Option 1: Quick way
git pull

# Option 2: Safer way (see what changed first)
git fetch
git log HEAD..origin/main  # See what's new
git merge origin/main      # Merge when ready
```

### Clone Repository: Getting Someone Else's Code

**What is cloning?**
Cloning downloads an entire repository from a remote. It's like downloading a complete project.

**Basic clone:**
```bash
# Clone a repository
git clone https://github.com/username/repo.git
```

**What happens:**
- Creates a new folder with the repository name
- Downloads all files and history
- Sets up the remote automatically
- You can start working immediately!

**Clone to specific directory:**
```bash
# Clone into a folder with a different name
git clone https://github.com/username/repo.git my-project-name
```

**Clone specific branch:**
```bash
# Only clone a particular branch (saves time/space)
git clone -b branch-name https://github.com/username/repo.git
```

**After cloning:**
```bash
cd repo-name
git status
# You're ready to work!
```

---

## Undoing Changes: Fixing Mistakes

### Common Scenarios and How to Fix Them

#### Scenario 1: "I staged a file but don't want to commit it"

**Problem:** You ran `git add file.py` but changed your mind.

**Solution: Unstage the file**
```bash
# Unstage a file (keep your changes)
git restore --staged filename.py

# Or older syntax
git reset HEAD filename.py

# Unstage all files
git restore --staged .
```

**What happens:**
- File moves from staging area back to working directory
- Your changes are still there (not lost!)
- File shows as "modified" in `git status` again

#### Scenario 2: "I made changes but want to discard them"

**Problem:** You edited a file but want to go back to the last committed version.

**Solution: Discard changes**
```bash
# Discard changes in a file (CAREFUL - this deletes your edits!)
git restore filename.py

# Or older syntax
git checkout -- filename.py

# Discard ALL changes (very careful!)
git restore .
```

**Warning:** This permanently deletes your uncommitted changes! Make sure you really want to discard them.

**Safer approach:**
```bash
# First, see what you'd lose
git diff

# If you're sure, then discard
git restore filename.py
```

#### Scenario 3: "I staged changes but want to unstage them"

**Problem:** You staged a file but want to unstage it (keep changes).

**Solution:**
```bash
# Unstage but keep changes
git restore --staged filename.py

# Now the file is modified but not staged
git status
# Shows: modified: filename.py (not staged)
```

#### Scenario 4: "I want to see what I'd lose before discarding"

**Always check first:**
```bash
# See unstaged changes
git diff

# See staged changes
git diff --staged

# See all changes (staged + unstaged)
git diff HEAD
```

### Understanding the Commands

**`git restore`** (modern, recommended):
```bash
git restore filename.py           # Discard unstaged changes
git restore --staged filename.py  # Unstage file (keep changes)
```

**`git reset`** (older, still works):
```bash
git reset HEAD filename.py  # Unstage file (keep changes)
```

**`git checkout`** (old way, being phased out):
```bash
git checkout -- filename.py  # Discard changes (old syntax)
```

### Revert Commits: Undoing Saved Changes

**Important distinction:**
- **Discard uncommitted changes**: Use `git restore` (see above)
- **Undo a commit**: Use `git reset` or `git revert` (see below)

#### Scenario 5: "I just committed but want to undo it (keep my changes)"

**Problem:** You made a commit but want to undo it, keeping your file changes.

**Solution: Soft reset**
```bash
# Undo last commit, keep changes staged
git reset --soft HEAD~1

# Or undo and unstage (keep changes in working directory)
git reset HEAD~1
```

**What `HEAD~1` means:**
- `HEAD` = your current commit
- `~1` = one commit before
- So `HEAD~1` = the commit before your last one

**After soft reset:**
- Your commit is gone
- Your changes are still there (staged or unstaged)
- You can edit and recommit

#### Scenario 6: "I want to completely undo my last commit and lose the changes"

**Problem:** You committed something and want to completely remove it.

**Solution: Hard reset (DANGEROUS)**
```bash
# Undo last commit and discard all changes
git reset --hard HEAD~1
```

**Warning:** This permanently deletes your commit AND your changes! Only use if you're absolutely sure.

**Safer approach:**
```bash
# First, see what you'd lose
git show HEAD

# Create a backup branch first
git branch backup-branch

# Then reset
git reset --hard HEAD~1

# If you change your mind, you can get it back:
# git checkout backup-branch
```

#### Scenario 7: "I want to undo a commit but keep it in history"

**Problem:** You want to undo changes but keep a record that you did.

**Solution: Revert (creates new commit)**
```bash
# Create a new commit that undoes the last commit
git revert HEAD
```

**What happens:**
- Git creates a NEW commit that undoes the changes
- History is preserved (you can see both commits)
- Safe for shared repositories

**Example:**
```bash
# Commit 1: Added feature
git commit -m "Add login feature"

# Oops, want to remove it
git revert HEAD
# Creates: Commit 2: "Revert 'Add login feature'"

# Now login feature is gone, but history shows both commits
```

#### Scenario 8: "I want to go back to a specific commit"

**Problem:** You want to return to an earlier state of your project.

**Solution:**
```bash
# First, find the commit you want
git log --oneline

# Reset to that commit
git reset --hard <commit-hash>
```

**Example:**
```bash
git log --oneline
# a1b2c3d Latest commit
# d4e5f6a Middle commit  
# g7h8i9j Old commit

# Go back to middle commit
git reset --hard d4e5f6a
```

**Warning:** This deletes all commits after that point! Use with caution.

**Recovery:**
If you reset and change your mind:
```bash
# View reflog (history of all Git actions)
git reflog

# Find the commit you lost
# Reset back to it
git reset --hard <commit-hash>
```

---

## .gitignore: Telling Git What to Ignore

### What is .gitignore?

The `.gitignore` file tells Git which files to **ignore** (not track). This is important because you don't want to commit:
- Temporary files
- Personal settings
- Large data files
- Compiled code
- Secrets/passwords

### Why Use .gitignore?

**Without .gitignore:**
```bash
git status
# Shows: modified: __pycache__/file.pyc
#       modified: .DS_Store
#       modified: secret_key.txt  # Oops! Don't commit this!
```

**With .gitignore:**
```bash
git status
# Clean! Git ignores those files automatically
```

### Creating .gitignore

```bash
# Create .gitignore in your project root
touch .gitignore

# Or create and edit it
code .gitignore  # or cursor .gitignore
```

Common `.gitignore` patterns:

```
# Python
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
venv/
env/
ENV/
*.egg-info/
dist/
build/

# Jupyter Notebooks
.ipynb_checkpoints
*.ipynb

# IDEs
.vscode/
.idea/
*.swp
*.swo
*~

# OS
.DS_Store
Thumbs.db

# Environment variables
.env
.env.local

# Data files (if large)
*.csv
*.h5
*.hdf5
data/
```

---

## Best Practices for Beginners

### 1. Commit Often (But Meaningfully)

**Why:** Small commits are easier to understand and undo if needed.

**Good practice:**
```bash
# Good: Small, focused commits
git add file1.py
git commit -m "Add data loading function"

git add file2.py
git commit -m "Add data processing function"

# Each commit does one thing - easy to understand!
```

**Bad practice:**
```bash
# Bad: One large commit with everything
git add .
git commit -m "Update everything"
# What changed? Hard to tell!
```

**How often?**
- Commit when you complete a logical unit of work
- Don't commit broken code (but it's OK to commit work-in-progress)
- Aim for multiple commits per day, not one giant commit per week

### 2. Write Clear Commit Messages

**Why:** Good messages help you (and others) understand what changed and why.

**Format:**
```
<type>: <short description>

<optional longer explanation>
```

**Good commit messages:**
```bash
git commit -m "fix: resolve memory leak in data processing"
git commit -m "feat: add user authentication system"
git commit -m "docs: update installation instructions"
git commit -m "refactor: simplify data loading function"
```

**Bad commit messages:**
```bash
git commit -m "fix"           # Too vague - fix what?
git commit -m "stuff"          # Meaningless
git commit -m "asdf"           # Random characters
git commit -m "Fixed it"      # Past tense, vague
git commit -m "WIP"            # Work in progress - but what?
```

**Commit message types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Formatting (no code change)
- `refactor`: Code restructuring
- `test`: Adding tests
- `chore`: Maintenance tasks

### 3. Use Branches for New Work

**Why:** Keeps your main branch stable while you experiment.

**When to create a branch:**
- Starting a new feature
- Fixing a bug
- Experimenting with something
- Any time you're not sure if it will work

**Good practice:**
```bash
# Always create a branch for new work
git checkout -b feature/user-login
# ... work on feature ...
git commit -m "feat: add login functionality"
git push origin feature/user-login

# When done, merge to main
git checkout main
git merge feature/user-login
```

**Branch naming:**
```bash
git checkout -b feature/user-authentication  # New feature
git checkout -b fix/memory-leak              # Bug fix
git checkout -b experiment/new-algorithm     # Experiment
git checkout -b docs/update-readme          # Documentation
```

### 4. Keep Main Branch Working

**Rule:** Only merge code into `main` that works and is tested.

**Workflow:**
```bash
# 1. Create feature branch
git checkout -b feature/new-feature

# 2. Work and commit
git add .
git commit -m "feat: add new feature"

# 3. Test it works!

# 4. Push to remote
git push origin feature/new-feature

# 5. Merge to main (when ready)
git checkout main
git pull  # Get latest changes
git merge feature/new-feature
git push
```

### 5. Always Pull Before Push

**Why:** Someone else might have pushed changes while you were working.

**Good habit:**
```bash
# Before pushing, always pull first
git pull
# If there are conflicts, resolve them
git push
```

**What can happen:**
- If remote has new commits, Git will merge them
- If there are conflicts, Git will ask you to resolve them
- After resolving, you can push

### 6. Review Before Committing

**Always check what you're committing:**

```bash
# See what files changed
git status

# See what actually changed
git diff              # Unstaged changes
git diff --staged     # Staged changes

# Review, then commit
git commit -m "Your message"
```

**Common mistake:**
```bash
# Don't do this blindly:
git add .
git commit -m "Update"
# You might commit files you didn't mean to!
```

**Better:**
```bash
# Check first
git status
git diff --staged

# Then commit
git commit -m "Clear message"
```

### 7. Don't Commit Secrets

**Never commit:**
- Passwords
- API keys
- Personal information
- Large data files

**Use .gitignore:**
```bash
# Add to .gitignore
echo ".env" >> .gitignore
echo "secrets.txt" >> .gitignore
echo "*.key" >> .gitignore
```

### 8. Commit Related Changes Together

**Good:**
```bash
# All related to data loading
git add data_loader.py
git add data_utils.py
git commit -m "feat: add data loading functionality"
```

**Bad:**
```bash
# Unrelated changes together
git add data_loader.py
git add user_auth.py
git add README.md
git commit -m "Update stuff"  # What is this commit about?
```

---

## Collaboration Workflow

### Fork and Clone

```bash
# 1. Fork repository on GitHub/GitLab
# 2. Clone your fork
git clone https://github.com/your-username/repo.git
cd repo

# 3. Add upstream remote
git remote add upstream https://github.com/original-owner/repo.git

# 4. Create feature branch
git checkout -b feature/my-feature
```

### Keep Fork Updated

```bash
# Fetch from upstream
git fetch upstream

# Merge upstream changes
git checkout main
git merge upstream/main

# Push to your fork
git push origin main
```

### Pull Requests

1. Push your branch to your fork
2. Create pull request on GitHub/GitLab
3. Address review comments
4. Merge after approval

---

## Advanced Features

### Stashing

Save changes temporarily without committing:

```bash
# Stash current changes
git stash

# Stash with message
git stash save "Work in progress"

# List stashes
git stash list

# Apply most recent stash
git stash apply

# Apply and remove stash
git stash pop

# Apply specific stash
git stash apply stash@{0}

# Delete stash
git stash drop
```

### Tagging

Mark important points in history:

```bash
# Create lightweight tag
git tag v1.0.0

# Create annotated tag
git tag -a v1.0.0 -m "Release version 1.0.0"

# List tags
git tag

# Push tags to remote
git push origin v1.0.0

# Push all tags
git push origin --tags
```

### Rebasing

Reapply commits on top of another base:

```bash
# Rebase current branch onto main
git checkout feature-branch
git rebase main

# Interactive rebase (edit last 3 commits)
git rebase -i HEAD~3

# Abort rebase
git rebase --abort
```

### Cherry-picking

Apply specific commits to current branch:

```bash
# Apply a commit from another branch
git cherry-pick <commit-hash>

# Apply multiple commits
git cherry-pick <commit1> <commit2>
```

---

## GitHub/GitLab Integration

### SSH Keys

Set up SSH keys for passwordless authentication:

```bash
# Generate SSH key (if not already done)
ssh-keygen -t ed25519 -C "your.email@example.com"

# Add to SSH agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Copy public key to clipboard
pbcopy < ~/.ssh/id_ed25519.pub

# Add to GitHub: Settings → SSH and GPG keys → New SSH key
# Add to GitLab: Settings → SSH Keys → Add SSH key
```

### Clone with SSH

```bash
# Use SSH URL instead of HTTPS
git clone git@github.com:username/repo.git
```

### GitHub CLI

```bash
# Install GitHub CLI
brew install gh

# Authenticate
gh auth login

# Clone repository
gh repo clone username/repo

# Create pull request
gh pr create
```

---

## Troubleshooting: Common Problems and Solutions

### Issue: Merge Conflicts (Most Common Problem)

**What is a merge conflict?**
When Git can't automatically combine changes from two branches, it asks you to decide.

**When it happens:**
- You and someone else edited the same lines
- You're merging branches with conflicting changes

**How to resolve:**

**Step 1: See what's conflicted**
```bash
git status
# Shows: "Unmerged paths" with conflicted files
```

**Step 2: Open the conflicted file**
You'll see markers like this:
```python
<<<<<<< HEAD
print("My version")
=======
print("Their version")
>>>>>>> branch-name
```

**Understanding the markers:**
- `<<<<<<< HEAD`: Start of your changes
- `=======`: Separator
- `>>>>>>> branch-name`: End of their changes

**Step 3: Choose what to keep**
You have three options:
1. Keep your version (delete their section)
2. Keep their version (delete your section)
3. Keep both (combine them)

**Example resolution:**
```python
# Before (conflicted):
<<<<<<< HEAD
print("Hello")
=======
print("Hi")
>>>>>>> feature-branch

# After (resolved - keeping both):
print("Hello")
print("Hi")
```

**Step 4: Mark as resolved**
```bash
# After editing the file, stage it
git add resolved-file.py

# Complete the merge
git commit
# Git will open an editor with a default merge message
```

**Step 5: Verify**
```bash
git status
# Should say: "working tree clean"
```

**Tips:**
- Use VS Code/Cursor - they have great merge conflict tools
- When in doubt, ask the person who made the other changes
- Test your code after resolving conflicts

### Issue: Accidentally Committed Wrong Files

**Problem**: You ran `git commit` but included files you didn't mean to.

**Solution 1: Undo commit, keep changes (most common)**
```bash
# Undo the commit, keep your changes staged
git reset --soft HEAD~1

# Now unstage the files you don't want
git restore --staged wrong-file.py

# Commit again with only the files you want
git commit -m "Correct commit message"
```

**Solution 2: Undo commit, unstage everything**
```bash
# Undo commit, unstage files, keep changes
git reset HEAD~1

# Now stage only what you want
git add correct-file.py
git commit -m "Correct commit message"
```

**Solution 3: Amend the commit (if you haven't pushed yet)**
```bash
# Remove the wrong file from last commit
git restore --staged wrong-file.py
git commit --amend --no-edit
```

**If you already pushed:**
- You'll need to force push (dangerous if others are using the repo)
- Better to make a new commit that removes the file

### Issue: Lost Commit or Accidentally Reset

**Problem**: You reset or deleted a commit and want it back.

**Solution: Use reflog (Git's safety net)**
```bash
# View reflog - shows ALL Git actions (even "deleted" commits)
git reflog

# Output shows:
# a1b2c3d HEAD@{0}: reset: moving to HEAD~1
# d4e5f6a HEAD@{1}: commit: Your lost commit message
# ...

# Recover the commit
git checkout d4e5f6a

# Create a branch to keep it
git checkout -b recovered-branch

# Or merge it back
git checkout main
git merge recovered-branch
```

**What is reflog?**
- Git keeps a log of EVERYTHING you do
- Even "deleted" commits are here for ~30 days
- It's like Git's "undo history"

### Issue: Committed to Wrong Branch

**Problem**: You made commits on `main` but meant to put them on a feature branch.

**Solution: Move the commit**
```bash
# Step 1: Note the commit hash
git log --oneline -1
# Output: a1b2c3d Your commit message

# Step 2: Remove it from current branch (but keep the changes)
git reset HEAD~1
# Or if you want to keep it staged:
git reset --soft HEAD~1

# Step 3: Switch to correct branch
git checkout feature-branch

# Step 4: Apply the commit here
git cherry-pick a1b2c3d
# Or if you used --soft reset, just commit:
git commit -m "Your commit message"
```

**Alternative: Create branch from current position**
```bash
# If you just committed to main by mistake:
# Create a branch from here (includes your commit)
git checkout -b feature-branch

# Now remove it from main
git checkout main
git reset HEAD~1
```

### Issue: "Your branch is ahead of 'origin/main' by X commits"

**Problem**: You have local commits that aren't on the remote yet.

**Solution**: Just push!
```bash
git push
```

**If you get an error about tracking:**
```bash
git push -u origin main
```

### Issue: "Your branch is behind 'origin/main' by X commits"

**Problem**: Remote has commits you don't have locally.

**Solution**: Pull the changes
```bash
git pull
```

**If there are conflicts, resolve them (see merge conflicts above).**

### Issue: Authentication Failed When Pushing

**Problem**: Git asks for password or authentication fails.

**Solutions:**
1. **Use SSH instead of HTTPS** (recommended):
   ```bash
   # Change remote URL to SSH
   git remote set-url origin git@github.com:username/repo.git
   ```

2. **Set up SSH keys** (see SSH Keys guide)

3. **Use personal access token** (if using HTTPS):
   - GitHub: Settings → Developer settings → Personal access tokens
   - Use token as password when pushing

### Issue: Large Files

**Problem**: Trying to commit large files

**Solution**:
```bash
# Use Git LFS for large files
brew install git-lfs
git lfs install
git lfs track "*.h5"
git add .gitattributes
git add large-file.h5
git commit -m "Add large file with LFS"
```

---

## Quick Reference: Commands You'll Use Daily

### Setup (Do Once)

```bash
# Configure your identity
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Set default branch name
git config --global init.defaultBranch main
```

### Daily Workflow Commands

```bash
# Check what's changed
git status

# See what actually changed
git diff

# Stage files
git add filename.py        # One file
git add .                  # All files in current directory

# Commit
git commit -m "Clear message describing changes"

# View history
git log --oneline          # Compact view
git log                    # Detailed view
```

### Branch Commands

```bash
# Create and switch to new branch
git checkout -b feature-name

# Switch branches
git checkout branch-name
git switch branch-name     # Modern way

# List branches
git branch

# Merge branch
git checkout main
git merge feature-name
```

### Remote Commands

```bash
# Push to remote
git push                   # After first: git push -u origin main

# Pull from remote
git pull

# View remotes
git remote -v
```

### Undo Commands

```bash
# Unstage a file
git restore --staged filename.py

# Discard changes (CAREFUL!)
git restore filename.py

# Undo last commit (keep changes)
git reset HEAD~1

# Undo last commit (lose changes - DANGEROUS!)
git reset --hard HEAD~1
```

### Getting Help

```bash
# Get help for any command
git help <command>
git <command> --help

# Examples
git help status
git help commit
git log --help
```

### Common Workflows

```bash
# Daily workflow
git pull
# ... make changes ...
git add .
git commit -m "Description"
git push

# Feature workflow
git checkout -b feature/new-feature
# ... work ...
git add .
git commit -m "feat: add feature"
git push origin feature/new-feature
# Create pull request

# Fix workflow
git checkout -b fix/bug-name
# ... fix ...
git add .
git commit -m "fix: resolve bug"
git push origin fix/bug-name
```

---

## Related Guides

- **[SSH Keys Guide](ssh-keys.md)** - Set up SSH keys for Git authentication
- **[VS Code/Cursor Guide](vscode-cursor.md)** - Configure Git in your editor
- **[Development Tools Overview](index.md)** - All development tools guides
- **[Command Line Guide](../command-line-guide.md)** - Terminal basics

---

*Last updated: {{ git_revision_date_localized }}*

