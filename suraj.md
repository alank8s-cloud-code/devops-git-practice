# Git Commands Reference

A living document of Git commands I've learned, organized by category.
I'll keep adding to this as I progress through the DevOps journey.

---

## Setup & Config

### `git --version`
Checks which version of Git is installed.
```
git --version
```

### `git config --global user.name "<name>"`
Sets the name that will be attached to your commits.
```
git config --global user.name "DevOps Learner"
```

### `git config --global user.email "<email>"`
Sets the email that will be attached to your commits.
```
git config --global user.email "devops.learner@example.com"
```

### `git config --list`
Shows all current Git configuration settings (global + local).
```
git config --list
```

---

## Basic Workflow

### `git init`
Turns the current folder into a Git repository by creating a `.git/` directory.
```
git init
```

### `git add <file>`
Moves changes from the working directory into the staging area, marking them ready to commit.
```
git add git-commands.md
```

### `git commit -m "<message>"`
Saves a permanent snapshot of everything currently staged, with a message describing the change.
```
git commit -m "Add initial git commands reference"
```

---

## Viewing Changes

### `git status`
Shows the current state of the working directory and staging area (what's tracked, changed, or staged).
```
git status
```

### `git log`
Shows the commit history, newest first, with full commit hashes, authors, dates, and messages.
```
git log
```

### `git log --oneline`
Shows a compact, one-line-per-commit version of the history.
```
git log --oneline
```

### `git diff`
Shows the exact line-by-line changes in the working directory that are NOT yet staged.
```
git diff
```

### `git diff --staged`
Shows the exact line-by-line changes that ARE staged, comparing them to the last commit.
```
git diff --staged
```

---

## Branching (early notes)

### `git branch`
Lists all local branches, marking the current one with an asterisk.
```
git branch
```

### `git branch <name>`
Creates a new branch pointing at the current commit.
```
git branch feature-login
```

---

## Undo & Inspect

### `git restore <file>`
Discards uncommitted changes in the working directory, reverting a file back to its last committed state.
```
git restore git-commands.md
```

### `git log --oneline --graph`
Shows commit history as a compact, one-line-per-commit list with a visual branch graph.
```
git log --oneline --graph
```

### `git show <commit-hash>`
Shows the full details and diff of a single specific commit.
```
git show ec85edc
```

---

## Remotes (preview — coming soon)

### `git remote add origin <url>`
Links your local repo to a remote repository (e.g. on GitHub) under the name "origin".
```
git remote add origin https://github.com/user/repo.git
```

### `git push origin <branch>`
Uploads your local commits on a branch to the remote repository.
```
git push origin master
```
