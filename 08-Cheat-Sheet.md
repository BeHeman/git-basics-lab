# Module 08 · Git Cheat Sheet

One-page reference for everything in this lab. Keep it open while you work.

---

## 🔧 One-time setup

```bash
git --version                              # check Git is installed
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global --list                 # verify your settings
```

## 🌱 Start a repository

```bash
git init                    # turn current folder into a repo
git clone <url>             # copy an existing remote repo to your machine
```

## 📋 Inspect what's going on (use constantly)

```bash
git status                  # what's changed / staged / untracked
git diff                    # exact line changes (unstaged)
git diff --staged           # line changes that are staged
git log                     # full commit history
git log --oneline           # compact one-line-per-commit history
git log --oneline --graph   # history with a visual branch graph
```

## 💾 The core loop: stage → commit

```bash
git add <file>              # stage one file
git add .                   # stage everything changed (check status first!)
git commit -m "message"     # commit staged changes
git commit -am "message"    # stage tracked files + commit (skips new files)
```

## ☁️ Work with GitHub (remotes)

```bash
git remote add origin <url> # link local repo to a remote named "origin"
git remote -v               # show configured remotes
git branch -M main          # rename current branch to main
git push -u origin main     # first push (sets upstream)
git push                    # push after upstream is set
git pull                    # download + merge remote changes
git fetch                   # download remote changes WITHOUT merging
```

## 🌿 Branching & merging

```bash
git branch                       # list branches (* = current)
git switch -c <name>             # create + switch to a new branch
git switch <name>                # switch to an existing branch
git checkout -b <name>           # older syntax: create + switch
git merge <branch>               # merge <branch> INTO current branch
git branch -d <name>             # delete a merged branch
git push -u origin <branch>      # push a branch to GitHub (to open a PR)
```

## ↩️ Undo & rollback

```bash
# --- not pushed yet (safe to rewrite local history) ---
git restore <file>               # discard uncommitted changes to a file
git restore --staged <file>      # unstage a file (keep the edits)
git commit --amend -m "new msg"  # fix the last commit's message
git commit --amend --no-edit     # add staged files to last commit
git reset --soft  HEAD~1         # undo last commit, keep changes STAGED
git reset --mixed HEAD~1         # undo last commit, keep changes UNSTAGED (default)
git reset --hard  HEAD~1         # ☢️ undo last commit AND DELETE changes

# --- already pushed (don't rewrite shared history) ---
git revert <commit>              # ✅ new commit that undoes <commit>, then: git push
```

## 🕵️ Look at the past (read-only)

```bash
git checkout <commit-hash>       # view an old snapshot (detached HEAD)
git switch main                  # return to the present
git show <commit-hash>           # show what a specific commit changed
```

---

## 🧭 Mental model

```
Working Directory  --(git add)-->  Staging Area  --(git commit)-->  Local Repo  --(git push)-->  GitHub
       ^                                                                  |                          |
       └──────────────────────── git restore ────────────────────────────┘                          |
                                                                          └────── git pull ──────────┘
```

## 🔑 Key terms in one line each

- **repo** — a project tracked by Git (`.git` folder holds the history)
- **commit** — a saved snapshot + message
- **staging area** — where you choose what goes into the next commit
- **branch** — an independent line of work
- **`main`** — the default primary branch
- **`origin`** — the default name for your remote (GitHub)
- **push / pull** — upload / download commits to/from the remote
- **merge** — combine one branch's changes into another
- **pull request (PR)** — a proposal to merge a branch, with review
- **revert** — undo a pushed commit by adding an opposite commit (safe)
- **reset** — move the branch back / remove local commits (local only)

---

## ⭐ The two loops to memorize

**Solo daily loop:**
```
edit → git add → git commit → git push
```

**Team feature loop (with PR):**
```
git switch main && git pull
git switch -c feature/x
edit → git add → git commit
git push -u origin feature/x
→ open PR on GitHub → review → merge
git switch main && git pull
```

---

➡️ Teaching this? See `09-Instructor-Guide.md`.
