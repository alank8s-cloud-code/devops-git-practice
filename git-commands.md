# 📘 Git Commands Reference

> A complete Git command reference covering setup, daily workflow, branching, remotes, merging, rebasing, stash, cherry-pick, reset, and revert.

---

# Table of Contents

1. Git Setup & Configuration
2. Basic Workflow
3. Branching
4. Remote Repository
5. Merge & Rebase
6. Git Stash
7. Git Cherry-pick
8. Git Reset
9. Git Revert
10. Helpful Commands
11. Common Git Flags

---

# 1. Git Setup & Configuration

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git --version` | Shows installed Git version | Verify Git installation |
| `git config --global user.name "Your Name"` | Sets username | Every commit records author name |
| `git config --global user.email "email@example.com"` | Sets email | Links commits to your GitHub account |
| `git config --global init.defaultBranch main` | Sets default branch name | New repositories start with `main` |
| `git config --global core.editor nano` | Sets default editor | Used for commit messages |
| `git config --list` | Displays Git configuration | Verify current settings |
| `git config --global --list` | Shows global configuration | Check user-wide settings |
| `git help <command>` | Opens help page | Learn command usage |
| `git <command> --help` | Detailed documentation | View all options |

---

# 2. Basic Workflow

## Initialize Repository

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git init` | Creates a Git repository | Start version control |
| `git clone <url>` | Downloads existing repository | Work on an existing project |

---

## Check Status

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git status` | Shows repository status | Check modified, staged, and untracked files |
| `git status -s` | Short status | Compact output |
| `git status --short` | Same as `-s` | Quick overview |

---

## Add Files

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git add file.txt` | Stages one file | Prepare file for commit |
| `git add .` | Stages current directory | Add all current changes |
| `git add -A` | Stages all changes | Includes deleted files |
| `git add *` | Adds matching files | Less recommended than `.` |

---

## Commit

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git commit -m "message"` | Creates a commit | Save changes |
| `git commit -am "message"` | Stage tracked files and commit | Faster workflow |
| `git commit --amend` | Edit previous commit | Fix commit message or add forgotten files |
| `git commit --amend --no-edit` | Update last commit without changing message | Add missed files |

---

## View History

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git log` | Shows commit history | View all commits |
| `git log --oneline` | One line per commit | Compact history |
| `git log --graph` | Shows commit graph | Visualize branches |
| `git log --graph --oneline --all` | Complete graph | Best visualization |
| `git log -p` | Shows commit with changes | Inspect modifications |
| `git show` | Displays latest commit | Review last commit |
| `git show <commit>` | Shows specific commit | Inspect commit details |

---

## Compare Changes

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git diff` | Working vs staging | View unstaged changes |
| `git diff --staged` | Staging vs last commit | Check staged changes |
| `git diff HEAD` | Working vs latest commit | View all changes |
| `git diff branch1..branch2` | Compare branches | Review branch differences |

---

# 3. Branching

## View Branches

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git branch` | Lists local branches | View branches |
| `git branch -a` | Lists all branches | Local + remote |
| `git branch -r` | Remote branches | View remote branches |
| `git branch -vv` | Branch tracking info | Check upstream branch |

---

## Create Branch

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git branch feature` | Creates new branch | Separate development |
| `git switch -c feature` | Create and switch | Faster workflow |
| `git checkout -b feature` | Create and switch | Older syntax |

---

## Switch Branch

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git switch main` | Switch branch | Modern method |
| `git checkout main` | Switch branch | Older method |

---

## Rename/Delete Branch

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git branch -m new-name` | Rename current branch | Better naming |
| `git branch -m old new` | Rename another branch | Rename existing branch |
| `git branch -d branch` | Delete merged branch | Clean repository |
| `git branch -D branch` | Force delete | Delete unmerged branch |

---

# 4. Remote Repository

## Add Remote

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git remote add origin <url>` | Adds remote repository | Connect local repo |
| `git remote -v` | Shows remote URLs | Verify remotes |
| `git remote remove origin` | Removes remote | Disconnect remote |
| `git remote rename old new` | Rename remote | Better organization |


---

| Command                                    | What it does                                              | Why we use it                                                |
| ------------------------------------------ | --------------------------------------------------------- | ------------------------------------------------------------ |
| `git remote -v`                            | Lists all configured remote repositories                  | Check existing remotes and their URLs                        |
| `git remote add upstream <repository-url>` | Adds the original repository as `upstream`                | Sync your fork with the original project                     |
| `git remote remove upstream`               | Removes the upstream remote                               | Delete an incorrect or unused upstream                       |
| `git remote rename upstream original`      | Renames the upstream remote                               | Use a different remote name if needed                        |
| `git remote show upstream`                 | Displays detailed information about the upstream remote   | Check tracked branches and fetch/push URLs                   |
| `git fetch upstream`                       | Downloads the latest changes from the upstream repository | Update local references without changing your current branch |
| `git branch -r`                            | Lists all remote branches                                 | View branches available on `origin` and `upstream`           |
| `git checkout main`                        | Switches to the `main` branch                             | Prepare to update your local main branch                     |
| `git switch main`                          | Modern way to switch to `main`                            | Same purpose as `checkout`                                   |
| `git merge upstream/main`                  | Merges upstream changes into the current branch           | Update your local branch while preserving merge history      |
| `git rebase upstream/main`                 | Rebases your branch onto the latest upstream changes      | Keep a clean, linear commit history                          |
| `git push origin main`                     | Pushes updated local `main` to your fork (`origin`)       | Keep your GitHub fork synchronized                           |
| `git pull upstream main`                   | Fetches and merges the latest changes from upstream       | Update directly from the original repository                 |
| `git fetch --all`                          | Fetches changes from all configured remotes               | Update both `origin` and `upstream` simultaneously           |


---

## Push

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git push origin main` | Push branch | Upload commits |
| `git push -u origin main` | Set upstream | Future pushes only need `git push` |
| `git push` | Push current branch | Upload changes |
| `git push --force` | Force overwrite remote | Dangerous, avoid unless necessary |
| `git push --force-with-lease` | Safer force push | Prevent overwriting others' work |
| `git push --all` | Push all branches | Upload every branch |
| `git push --tags` | Push tags | Upload version tags |

---

## Pull

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git pull` | Fetch + merge | Update local repository |
| `git pull origin main` | Pull specific branch | Sync with remote |
| `git pull --rebase` | Fetch + rebase | Cleaner history |

---

## Fetch

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git fetch` | Downloads changes | Doesn't modify working files |
| `git fetch origin` | Fetch from remote | Update references |
| `git fetch --all` | Fetch all remotes | Update every remote |

---

## Clone & Fork

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git clone <url>` | Download repository | Start working |
| `git clone --depth 1 <url>` | Shallow clone | Faster download |
| **Fork** | Copy repository on GitHub | Contribute without repository access |

---

# 5. Merge & Rebase

## Merge

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git merge feature` | Merge branch | Combine work |
| `git merge --no-ff feature` | Force merge commit | Preserve history |
| `git merge --abort` | Cancel merge | Exit merge conflict |

---

## Rebase

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git rebase main` | Move commits | Keep history clean |
| `git pull --rebase` | Update without merge commit | Cleaner history |
| `git rebase --continue` | Continue after resolving conflicts | Finish rebase |
| `git rebase --abort` | Cancel rebase | Restore previous state |
| `git rebase --skip` | Skip problematic commit | Continue rebase |

---

# 6. Git Stash

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git stash` | Save temporary changes | Switch branches safely |
| `git stash push -m "message"` | Named stash | Easier identification |
| `git stash list` | Shows stashes | View saved work |
| `git stash show` | Displays stash summary | Inspect stash |
| `git stash show -p` | Full stash diff | Review changes |
| `git stash apply` | Restore stash | Keep stash saved |
| `git stash pop` | Restore and delete stash | Resume work |
| `git stash drop` | Delete stash | Remove one stash |
| `git stash clear` | Delete all stashes | Cleanup |

---

# 7. Git Cherry-pick

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git cherry-pick <commit>` | Copies one commit | Move a specific change |
| `git cherry-pick A B` | Apply multiple commits | Copy several commits |
| `git cherry-pick --continue` | Continue after conflict | Finish cherry-pick |
| `git cherry-pick --abort` | Cancel cherry-pick | Restore previous state |

---

# 8. Git Reset

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git reset --soft HEAD~1` | Remove commit, keep staged | Edit commit history |
| `git reset --mixed HEAD~1` | Remove commit, unstage | Default reset |
| `git reset --hard HEAD~1` | Remove commit and changes | Dangerous rollback |
| `git reset file.txt` | Unstage file | Remove from staging |
| `git reset --hard origin/main` | Match remote exactly | Discard local work |

---

# 9. Git Revert

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git revert <commit>` | Creates inverse commit | Safely undo changes |
| `git revert HEAD` | Undo latest commit | Keep project history |
| `git revert --no-edit <commit>` | Skip commit message editor | Faster revert |

---

# 10. Helpful Commands

| Command | What it does | Why we use it |
|----------|--------------|---------------|
| `git reflog` | Shows reference history | Recover lost commits |
| `git clean -n` | Preview file deletion | Safe cleanup |
| `git clean -fd` | Delete untracked files | Remove unwanted files |
| `git tag` | List tags | View releases |
| `git tag v1.0` | Create tag | Mark release |
| `git blame file.txt` | Shows line authors | Track code ownership |

---

# 11. Common Git Flags

| Flag | Meaning | Example |
|------|---------|---------|
| `-m` | Commit message | `git commit -m "Initial commit"` |
| `-a` | All tracked files | `git commit -am "Update"` |
| `-A` | Stage everything | `git add -A` |
| `-u` | Set upstream | `git push -u origin main` |
| `-b` | Create branch | `git checkout -b feature` |
| `-c` | Create and switch | `git switch -c feature` |
| `-d` | Delete branch | `git branch -d feature` |
| `-D` | Force delete branch | `git branch -D feature` |
| `-r` | Remote branches | `git branch -r` |
| `-a` | All branches | `git branch -a` |
| `-v` | Verbose output | `git remote -v` |
| `-vv` | Very verbose | `git branch -vv` |
| `-p` | Patch/Detailed diff | `git log -p` |
| `--soft` | Keep staged changes | `git reset --soft HEAD~1` |
| `--mixed` | Keep working files | `git reset --mixed HEAD~1` |
| `--hard` | Remove all changes | `git reset --hard HEAD~1` |
| `--amend` | Modify last commit | `git commit --amend` |
| `--continue` | Continue interrupted operation | `git rebase --continue` |
| `--abort` | Cancel operation | `git merge --abort` |
| `--force` | Force push | `git push --force` |
| `--force-with-lease` | Safe force push | `git push --force-with-lease` |
| `--all` | Include everything | `git fetch --all` |
| `--oneline` | Compact log | `git log --oneline` |
| `--graph` | Commit graph | `git log --graph` |
| `--staged` | Compare staged changes | `git diff --staged` |

---

# Daily Git Workflow

```bash
# Clone repository
git clone <repository-url>

# Enter project
cd project

# Create feature branch
git switch -c feature/login

# Make changes

# Check status
git status

# Stage files
git add .

# Commit
git commit -m "Add login feature"

# Push
git push -u origin feature/login

# Open Pull Request

# After merge
git switch main
git pull origin main

# Delete local feature branch
git branch -d feature/login
```

---

# Git Workflow Summary

```
Working Directory
       │
       ▼
 git add
       │
       ▼
Staging Area
       │
       ▼
 git commit
       │
       ▼
 Local Repository
       │
       ▼
 git push
       │
       ▼
 Remote Repository (GitHub)

Remote → Local
git fetch
git pull
```

---

# Quick Tips

- Commit often with meaningful messages.
- Create a new branch for every feature or bug fix.
- Use `git fetch` before `git pull` if you want to inspect remote changes first.
- Prefer `git push --force-with-lease` over `git push --force`.
- Use `git revert` on shared branches because it preserves history.
- Use `git reset` only when rewriting local history.
- Use `git stash` for temporary work.
- Use `git rebase` to maintain a clean, linear commit history.
- Use `git reflog` to recover accidentally lost commits.
