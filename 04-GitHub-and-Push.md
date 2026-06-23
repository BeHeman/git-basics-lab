# Module 04 · GitHub & Push

⏱️ ~15 minutes · So far everything lives **only on your computer**. Now you'll publish it to GitHub so it's backed up, shareable, and ready for collaboration.

---

## Concept — what is a "remote"?

Right now your commits live in the `.git` folder on your laptop. If the laptop dies, they're gone, and no teammate can see them.

A **remote** is a copy of your repository hosted somewhere else — on GitHub, in this case. The standard name for your primary remote is **`origin`**.

```
   YOUR LAPTOP (local)                         GITHUB (remote)
┌──────────────────────┐     git push      ┌──────────────────────┐
│  cloud-profile/.git  │  ───────────────▶ │  origin/cloud-profile│
│  (your commits)      │  ◀─────────────── │  (cloud copy)        │
└──────────────────────┘     git pull      └──────────────────────┘
```

- **`git push`** = upload your local commits to the remote.
- **`git pull`** = download commits from the remote to your local repo.

---

## A quick word: Git vs. GitHub

| | **Git** | **GitHub** |
|---|---------|------------|
| What | A version-control tool | A website that hosts Git repos |
| Runs | On your computer | In the cloud / browser |
| Needs internet? | No | Yes |
| Made by | Linus Torvalds (2005) | A company (now Microsoft) |

> GitHub adds **collaboration, backup, pull requests, issues, and CI/CD** on top of Git. Alternatives include GitLab and Azure DevOps — they all speak the same Git underneath.

---

## Step 1 — Create an empty repository on GitHub

1. Go to <https://github.com> and sign in.
2. Click the **+** in the top-right → **New repository**.
3. Fill in:
   - **Repository name:** `cloud-profile`
   - **Description:** *(optional)* "My cloud engineer profile page"
   - **Public** (so you can share it) or **Private** — your choice.
4. ⚠️ **Do NOT** check "Add a README", "Add .gitignore", or "Choose a license." You want a **completely empty** repo, because your local project already has files. (Adding them now causes an avoidable conflict.)
5. Click **Create repository**.

GitHub now shows a page titled *"…or push an existing repository from the command line"* with commands. You'll use those next.

---

## Step 2 — Connect your local repo to the remote

Copy the repository URL from that GitHub page. It looks like:

```
https://github.com/YOUR-USERNAME/cloud-profile.git
```

Back in your terminal (inside `cloud-profile`), tell Git about the remote:

```bash
git remote add origin https://github.com/YOUR-USERNAME/cloud-profile.git
```

> 🔁 Replace `YOUR-USERNAME` with your actual GitHub username.

**Verify the remote was added:**

```bash
git remote -v
```

**Expected output:**

```
origin  https://github.com/YOUR-USERNAME/cloud-profile.git (fetch)
origin  https://github.com/YOUR-USERNAME/cloud-profile.git (push)
```

> 💡 `origin` is just a **nickname** for that long URL, so you can type `origin` instead of the full address every time.

---

## Step 3 — Make sure your branch is named `main`

```bash
git branch -M main
```

This renames your current branch to `main` (the `-M` forces the rename). GitHub expects `main` as the default.

---

## Step 4 — Push to origin

```bash
git push -u origin main
```

The first time, GitHub will ask you to **authenticate** (sign in via browser, or with a Personal Access Token). Follow the prompt.

**Expected output:**

```
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Writing objects: 100% (9/9), 1.10 KiB | 1.10 MiB/s, done.
Total 9 (delta 0), reused 0 (delta 0)
To https://github.com/YOUR-USERNAME/cloud-profile.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
```

🎉 **Your profile page is now on GitHub!**

> 🔑 The `-u` flag (short for `--set-upstream`) links your local `main` to `origin/main`. After this **first** push, you can just type `git push` and `git pull` — Git remembers where to send things.

---

## Step 5 — Verify in the browser

Refresh your GitHub repository page. You should now see:

- `index.html` listed
- Your **three commits** (click the "commits" link or the clock icon)
- Each commit message you wrote

Click `index.html` → you can read your code right in GitHub.

---

## Step 6 — The daily loop, now with push

From here on, the everyday workflow is:

```bash
# 1. edit files in your editor ...
git status                       # see what changed
git add index.html               # stage
git commit -m "Describe change"  # commit locally
git push                         # publish to GitHub
```

Try it now — make a tiny edit (e.g., add a `<footer>` before `</body>`):

```html
  <footer>
    <p>&copy; 2026 Asha Verma</p>
  </footer>
```

Then:

```bash
git add index.html
git commit -m "Add page footer with copyright"
git push
```

Refresh GitHub — the footer commit appears within seconds.

---

## ✅ Checkpoint

- [x] `git remote -v` shows `origin` pointing to your GitHub URL
- [x] Your repo on GitHub.com shows `index.html` and all your commits
- [x] A fresh `git push` after a new commit succeeds without errors

---

## 🧠 Try it / Discuss

1. What does `origin` actually refer to? What does `main` refer to?
2. Why did we create the GitHub repo **empty** (no README)?
3. Your laptop's hard drive fails tomorrow. Where is your work safe — and how would you get it back? *(Hint: `git clone`.)*

---

➡️ **Next:** Open `05-Branching-and-Merging.md` — build a new feature without risking `main`.
