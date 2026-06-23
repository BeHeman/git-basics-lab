# Module 02 · Setup & Init

⏱️ ~10 minutes · You'll install/verify Git, set your identity, and create your project repository.

---

## Step 1 — Check if Git is installed

Open your terminal (Git Bash on Windows; Terminal on macOS/Linux) and run:

```bash
git --version
```

**Expected output** (version number may differ):

```
git version 2.43.0
```

- ✅ If you see a version → Git is installed. Skip to Step 2.
- ❌ If you see `command not found` → install Git:
  - **Windows / macOS:** download from <https://git-scm.com/downloads> and run the installer (accept all defaults).
  - **Linux (Debian/Ubuntu):** `sudo apt-get install git`
  - Then re-run `git --version` to confirm.

---

## Step 2 — Configure your identity (one-time setup)

Every commit records **who** made it. Tell Git your name and email **once**, and it applies to all your projects. Use the **same email as your GitHub account**.

```bash
git config --global user.name "Asha Verma"
git config --global user.email "asha.verma@example.com"
```

> 🔁 Replace the name and email with **your own**. The email should match your GitHub sign-up email so your commits link to your profile.

**Verify it worked:**

```bash
git config --global --list
```

**Expected output:**

```
user.name=Asha Verma
user.email=asha.verma@example.com
```

> 💡 `--global` means "for every project on this computer." You only do this once per machine.

*(Optional but recommended — set `main` as the default branch name for new repos):*

```bash
git config --global init.defaultBranch main
```

---

## Step 3 — Create your project folder

Create a folder for the profile project and move into it.

```bash
# macOS / Linux / Git Bash
mkdir cloud-profile
cd cloud-profile
```

You're now **inside** an empty folder called `cloud-profile`. Confirm with:

```bash
pwd
```

It should end in `/cloud-profile`.

---

## Step 4 — Initialize the repository

This is the moment your folder becomes a **Git repository**:

```bash
git init
```

**Expected output:**

```
Initialized empty Git repository in /Users/asha/cloud-profile/.git/
```

🎉 **What just happened?** Git created a hidden folder called `.git` inside `cloud-profile`. That folder *is* your repository — it will store the entire history of every change you make. You never edit `.git` directly; Git manages it for you.

**See the hidden folder** (proof it exists):

```bash
ls -a
```

**Expected output:**

```
.    ..    .git
```

> ⚠️ **Never delete the `.git` folder** — deleting it throws away all your version history and turns the project back into an ordinary, untracked folder.

---

## Step 5 — Check the status

`git status` is the command you'll run **constantly**. It tells you what Git currently sees.

```bash
git status
```

**Expected output:**

```
On branch main

No commits yet

nothing to commit (working tree clean)
```

Read that carefully:
- `On branch main` → you're on the default `main` branch.
- `No commits yet` → you haven't saved any snapshots.
- `nothing to commit` → there are no files for Git to track *yet*.

---

## ✅ Checkpoint

You should now have:

- [x] `git --version` returns a version number
- [x] `git config --global --list` shows your name and email
- [x] A `cloud-profile` folder containing a hidden `.git` folder
- [x] `git status` says `On branch main` / `No commits yet`

If all four are true, your environment is ready. 🚀

---

## 🧠 Try it

Run `git status` once more and read every line out loud. Get comfortable — you'll run this command more than any other in Git.

---

➡️ **Next:** Open `03-Staging-and-Commits.md` — you'll create the profile page and make your first commits.
