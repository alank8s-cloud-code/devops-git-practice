# Day 22 – Introduction to Git: Your First Repository

A deep-dive walkthrough of Git fundamentals: what each concept is, why it exists, and how to actually do it. Everything you need — explanations, commands, and the deliverable files — lives in this one document.

---

## Table of Contents

1. [What is Git and Why It Matters](#1-what-is-git-and-why-it-matters)
2. [Task 1: Install and Configure Git](#task-1-install-and-configure-git)
3. [Task 2: Create Your Git Project](#task-2-create-your-git-project)
4. [Task 3: Git Commands Reference (`git-commands.md`)](#task-3-git-commands-reference-git-commandsmd)
5. [Task 4: Stage and Commit](#task-4-stage-and-commit)
6. [Task 5: Make More Changes and Build History](#task-5-make-more-changes-and-build-history)
7. [Task 6: Understand the Git Workflow (`day-22-notes.md`)](#task-6-understand-the-git-workflow-day-22-notesmd)
8. [Expected Output Checklist](#expected-output-checklist)

---

## 1. What is Git and Why It Matters

### What
Git is a **distributed version control system (VCS)**. It tracks changes to files over time, letting you record snapshots of a project ("commits"), move between those snapshots, branch off to try new ideas, and merge work back together — all without overwriting anyone's history.

"Distributed" means every developer has a **full copy of the entire project history** on their own machine, not just the latest files. There's no single point of failure like there is with older centralized systems (e.g., SVN, CVS).

### Why
- **History and accountability**: every change is recorded with who made it, when, and why (via the commit message). You can always go back to any previous state.
- **Collaboration without chaos**: multiple people can work on the same codebase simultaneously using branches, then merge their work safely.
- **Experimentation is safe**: you can create a branch, try something risky, and throw it away if it doesn't work — the main codebase is untouched.
- **Foundation of DevOps**: CI/CD pipelines, infrastructure-as-code, GitOps, code reviews, deployment triggers — nearly all of it is built on top of Git events (a push, a merge, a tag). You cannot meaningfully work in DevOps without fluency in Git.
- **Speed and offline work**: because history is local, most operations (commit, log, diff, branch) don't need a network connection.

### How (conceptually)
Git manages three areas for every file in a repository:

| Area | Purpose |
|---|---|
| **Working Directory** | The actual files you see and edit on disk. |
| **Staging Area (Index)** | A "waiting room" where you place exactly the changes you want to include in the next commit. |
| **Repository (.git directory / local history)** | The permanent, saved history of committed snapshots. |

A typical flow: edit a file in the **working directory** → `git add` it to the **staging area** → `git commit` it into the **repository**.

---

## Task 1: Install and Configure Git

### What
Before using Git, you need it installed on your machine and configured with an identity (name + email) so every commit you make is properly attributed to you.

### Why
Git attaches an author to every single commit. If it's not configured, Git will refuse to commit (or use a generic/incorrect identity), which makes history useless for collaboration and blame-tracking.

### How

**1. Verify Git is installed**
```bash
git --version
```
Expected output looks like `git version 2.43.0`. If you get "command not found," install Git for your OS (e.g., `sudo apt install git` on Ubuntu, `brew install git` on macOS, or the installer from git-scm.com on Windows).

**2. Set your Git identity**
```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```
`--global` applies this identity to every repository on your machine. Omit `--global` (use it inside a repo folder) if you want a different identity for a specific project (common when mixing work/personal repos).

**3. Verify your configuration**
```bash
git config --list
```
or check individual values:
```bash
git config user.name
git config user.email
```
You can also inspect where each setting comes from:
```bash
git config --list --show-origin
```

---

## Task 2: Create Your Git Project

### What
A Git repository ("repo") is a project folder that Git is actively tracking. Turning a plain folder into a repo is called **initializing** it.

### Why
Until you run `git init`, Git knows nothing about your folder — it's just files on disk. Initializing creates the hidden `.git/` directory, which is where Git stores the *entire* history, configuration, and metadata for that project. Delete `.git/`, and the folder becomes a normal, untracked directory again (see Task 6, Q4).

### How

**1. Create the project folder**
```bash
mkdir devops-git-practice
cd devops-git-practice
```

**2. Initialize it as a Git repository**
```bash
git init
```
Output: `Initialized empty Git repository in .../devops-git-practice/.git/`

**3. Check the status**
```bash
git status
```
On a fresh repo, this tells you:
- You're on branch `main` (or `master`, depending on Git version/config).
- "No commits yet."
- "nothing to commit (create/copy files and use 'git add' to track)"

This is Git's way of telling you the working directory is clean and empty — there's nothing to snapshot yet.

**4. Explore the hidden `.git/` directory**
```bash
ls -la .git/
```
Key things you'll find:
| Item | What it is |
|---|---|
| `HEAD` | A pointer to your current branch (e.g., `ref: refs/heads/main`) |
| `config` | Repo-specific settings (remotes, user overrides, etc.) |
| `objects/` | The actual database of your project — every commit, tree, and file blob, stored as compressed objects |
| `refs/` | Pointers to branches and tags |
| `hooks/` | Scripts that can run automatically on events like commit or push |
| `index` | The staging area's internal representation (appears after your first `git add`) |

This directory *is* the repository. Everything Git does revolves around reading and writing to it.

---

## Task 3: Git Commands Reference (`git-commands.md`)

### What
A living reference document where you log every Git command you learn, organized by category, with a one-line explanation and an example.

### Why
Git has a large surface area. Writing your own reference — instead of only relying on memory or external docs — reinforces learning (active recall) and gives you a fast, personalized cheat sheet you'll actually use, since you wrote it in your own words with your own examples.

### How
Create the file:
```bash
touch git-commands.md
```

Below is a starter version. Copy this into `git-commands.md` and keep appending to it in later days.

```markdown
# Git Commands Reference

## Setup & Config

### `git --version`
Checks which version of Git is installed.
Example: `git --version`

### `git config --global user.name "Name"`
Sets the name attached to your commits.
Example: `git config --global user.name "Jane Doe"`

### `git config --global user.email "email"`
Sets the email attached to your commits.
Example: `git config --global user.email "jane@example.com"`

### `git config --list`
Shows all current Git configuration values.
Example: `git config --list`

## Basic Workflow

### `git init`
Turns the current folder into a Git repository by creating a `.git/` directory.
Example: `git init`

### `git add <file>`
Moves changes from the working directory into the staging area, marking them for the next commit.
Example: `git add git-commands.md`

### `git add .`
Stages all changed files in the current directory and subdirectories.
Example: `git add .`

### `git commit -m "message"`
Saves a permanent snapshot of everything currently staged, with a descriptive message.
Example: `git commit -m "Add initial git commands reference"`

## Viewing Changes

### `git status`
Shows the current state of the working directory and staging area (what's modified, staged, or untracked).
Example: `git status`

### `git diff`
Shows line-by-line changes in the working directory that are NOT yet staged.
Example: `git diff git-commands.md`

### `git diff --staged`
Shows line-by-line changes that ARE staged but not yet committed.
Example: `git diff --staged`

### `git log`
Shows the full commit history (hash, author, date, message).
Example: `git log`

### `git log --oneline`
Shows a compact, one-line-per-commit version of the history.
Example: `git log --oneline`
```

---

## Task 4: Stage and Commit

### What
The process of turning your edited file into a permanent, recorded snapshot in history.

### Why
This is the core Git loop you'll repeat thousands of times: **edit → stage → commit**. Staging lets you choose precisely what goes into a commit; committing locks it into history with a message explaining the "why."

### How

**1. Stage your file**
```bash
git add git-commands.md
```

**2. Check what's staged**
```bash
git status
```
You'll see `git-commands.md` listed under "Changes to be committed," in green. This confirms Git knows exactly what will be included in the next commit.

**3. Commit with a meaningful message**
```bash
git commit -m "Add initial git-commands.md with setup, workflow, and viewing-changes commands"
```
A good commit message is short, present-tense, and explains *what* changed and *why* — not just "update file."

**4. View your commit history**
```bash
git log
```
You'll see the commit hash, author, date, and message. This is your first entry in a growing, permanent history.

---

## Task 5: Make More Changes and Build History

### What
Repeating the edit → check → stage → commit cycle multiple times to build a real, multi-commit history.

### Why
A single commit doesn't teach you much about how Git *tracks change over time*. Doing this repeatedly is how you internalize the workflow and start seeing Git as a timeline rather than a single save button. In real projects, you'll do this dozens of times a day.

### How (repeat this cycle at least 3 times)

**1. Edit `git-commands.md`** — add a new command you've discovered (e.g., `git diff`, `git log --oneline`, `git show`).

**2. Check what changed since the last commit**
```bash
git diff
```
This shows exactly which lines were added/removed compared to the last commit, before you stage anything.

**3. Stage and commit with a distinct, descriptive message**
```bash
git add git-commands.md
git commit -m "Add git diff and git status commands to reference"
```

Example progression across commits:
- `"Add initial git-commands.md with setup, workflow, and viewing-changes commands"`
- `"Add git diff usage examples"`
- `"Document git log --oneline for compact history view"`
- `"Add staged vs unstaged diff commands"`

**4. View the full history in compact form**
```bash
git log --oneline
```
Output example:
```
a1b2c3d Add staged vs unstaged diff commands
e4f5g6h Document git log --oneline for compact history view
i7j8k9l Add git diff usage examples
m0n1o2p Add initial git-commands.md with setup, workflow, and viewing-changes commands
```
Each line is one commit: a short hash + its message. This is the view you'll use most often day-to-day to scan history quickly.

---

## Task 6: Understand the Git Workflow (`day-22-notes.md`)

### What
A short reflection file where you answer core conceptual questions in your own words, cementing *why* Git works the way it does (not just the commands).

### Why
Memorizing commands without understanding the model behind them (working directory → staging → repository) leads to confusion later, especially with more advanced operations like `reset`, `stash`, or resolving merge conflicts. Understanding *why* the staging area exists, for example, makes those later topics click much faster.

### How
Create the file:
```bash
touch day-22-notes.md
```

Below are model answers you can adapt into your own words inside `day-22-notes.md`:

```markdown
# Day 22 Notes

## 1. What is the difference between `git add` and `git commit`?
`git add` moves changes from the working directory into the staging area — it's
a preview/selection step, not a save. `git commit` takes whatever is currently
staged and permanently records it as a snapshot in the repository's history,
along with a message. Nothing is saved to history until you commit; staging
only prepares it.

## 2. What does the staging area do? Why doesn't Git just commit directly?
The staging area lets you build a commit piece by piece instead of all-or-nothing.
You might change five files but only want two of those changes in this commit
(the other three are unrelated or unfinished). Staging lets you review and
choose exactly what goes into each snapshot, which keeps commit history clean,
logical, and easy to understand later. Without it, every save would bundle
unrelated changes together, making history messy and hard to review or revert.

## 3. What information does `git log` show you?
For each commit: a unique hash (identifier), the author's name and email, the
date and time it was committed, and the commit message. This gives a full,
chronological audit trail of every snapshot ever taken — who changed what,
when, and (via the message) why.

## 4. What is the `.git/` folder and what happens if you delete it?
`.git/` is the actual database of the repository — it stores all commits,
branches, tags, configuration, and the staging index. The files you see in
your project folder are just the current working snapshot; the *real* history
lives inside `.git/`. If you delete `.git/`, you permanently lose all commit
history, branches, and version tracking. The folder reverts to a plain,
untracked directory — your current files remain, but every past version and
all commit messages are gone forever (unless backed up elsewhere, e.g., a
remote like GitHub).

## 5. Difference between working directory, staging area, and repository
- **Working directory**: the actual files on disk that you see and edit right now.
- **Staging area (index)**: a holding area where you place exactly the changes
  you want included in the next commit — a bridge between editing and saving.
- **Repository**: the permanent, saved history stored in `.git/` — every commit
  ever made, forming the full timeline of the project.

Flow: Working Directory --(git add)--> Staging Area --(git commit)--> Repository
```

---

## Expected Output Checklist

- [x] Local Git repo `devops-git-practice/` initialized with `git init`
- [x] Clean, multi-commit history (4+ commits) viewable via `git log` / `git log --oneline`
- [x] `git-commands.md` — categorized, growing command reference
- [x] `day-22-notes.md` — conceptual answers in your own words

**Quick command recap for the whole day:**
```bash
git --version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --list

mkdir devops-git-practice && cd devops-git-practice
git init
git status
ls -la .git/

touch git-commands.md day-22-notes.md
# ...edit files...

git add git-commands.md
git status
git commit -m "Add initial git-commands.md"

# repeat: edit -> git diff -> git add -> git commit
git log
git log --oneline
```
