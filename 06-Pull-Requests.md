# Module 06 · Pull Requests (PRs)

⏱️ ~15 minutes · In Module 05 you merged on your own machine. On real teams, changes go through a **Pull Request** — a proposal to merge, with review and discussion. You'll do a full PR round-trip now.

---

## Concept — what is a Pull Request?

A **Pull Request (PR)** is you saying:

> "I built something on my branch. Please **review** it and, if it looks good, **merge** it into `main`."

PRs add a human checkpoint before code reaches the official branch:

- 👀 Teammates **review** your changes line by line
- 💬 They can **comment**, request changes, or approve
- ✅ Automated checks (tests, linters) can run
- 📜 The discussion is **recorded forever** alongside the code

```
  your branch         Pull Request          main
 ┌───────────┐   "please review & merge"  ┌────────┐
 │  feature  │  ───────────────────────▶  │  main  │
 └───────────┘     review → approve →      └────────┘
                        merge
```

> On GitHub it's a **Pull Request**. On GitLab/Azure DevOps the same idea is called a **Merge Request** — same concept, different name.

---

## Step 1 — Create a new feature branch

You'll add an **"Open to Work" badge** to the profile via a PR.

Make sure you're on an up-to-date `main`:

```bash
git switch main
git pull
```

Create the feature branch:

```bash
git switch -c feature/open-to-work
```

---

## Step 2 — Make the change

In `index.html`, add this line inside the `<header class="profile-header">`, right after the `.role` paragraph:

```html
    <p class="badge">🟢 Open to new opportunities</p>
```

And add a style for it to `style.css`:

```css
.badge {
  display: inline-block;
  background: #e6f9ec;
  color: #1a7f37;
  padding: 4px 10px;
  border-radius: 12px;
  font-size: 0.85em;
  margin-top: 8px;
}
```

---

## Step 3 — Commit and push the **branch**

```bash
git add index.html style.css
git commit -m "Add 'Open to work' availability badge"
git push -u origin feature/open-to-work
```

**Expected output** ends with something like:

```
remote: Create a pull request for 'feature/open-to-work' on GitHub by visiting:
remote:      https://github.com/YOUR-USERNAME/cloud-profile/pull/new/feature/open-to-work
 * [new branch]      feature/open-to-work -> feature/open-to-work
```

> 💡 Notice you pushed the **branch**, not `main`. The branch now exists on GitHub, ready to become a PR. Nothing has touched `main` yet.

---

## Step 4 — Open the Pull Request on GitHub

1. Go to your repo on GitHub. You'll see a yellow banner:
   **"feature/open-to-work had recent pushes — Compare & pull request."** Click it.
   *(Or: **Pull requests** tab → **New pull request** → set base = `main`, compare = `feature/open-to-work`.)*
2. Confirm the merge direction at the top:
   **base: `main`  ←  compare: `feature/open-to-work`**
3. Fill in:
   - **Title:** `Add "Open to work" availability badge`
   - **Description:** e.g., *"Adds a green availability badge under the role. Styled with a rounded pill in `style.css`."*
4. Scroll down — GitHub shows the **diff**: every line you added/changed, in green/red.
5. Click **Create pull request**.

---

## Step 5 — Review the PR

On a team, a *colleague* reviews here. Since this is your lab, play both roles:

1. Open the **Files changed** tab — read your own diff as a reviewer would.
2. Hover a line → click the blue **+** → leave a comment (e.g., *"Nice, the emoji adds personality"*) → **Add single comment**.
3. *(Optional)* Use the **Review changes** button → **Approve**.

> This is exactly how code review feels day-to-day: read the diff, leave comments, approve or request changes.

---

## Step 6 — Merge the PR

1. Go back to the **Conversation** tab.
2. Click the green **Merge pull request** → **Confirm merge**.
3. GitHub confirms: *"Pull request successfully merged and closed."*
4. Click **Delete branch** (the cloud copy of the branch is no longer needed).

🎉 Your badge is now part of `main` **on GitHub** — reviewed and recorded.

---

## Step 7 — Sync your local `main`

The merge happened **on GitHub**, so your **local** `main` doesn't have it yet. Pull it down:

```bash
git switch main
git pull
```

**Expected output:**

```
Updating k1l2m3n..p4q5r6s
Fast-forward
 index.html | 1 +
 style.css  | 9 +++++++++
 2 files changed, 10 insertions(+)
```

Your local and remote `main` now match. Clean up the local feature branch:

```bash
git branch -d feature/open-to-work
```

---

## The complete PR workflow (memorize this loop)

```bash
git switch main && git pull            # 1. start from fresh main
git switch -c feature/my-change        # 2. branch
#    ... edit files ...                # 3. build
git add . && git commit -m "..."       # 4. commit
git push -u origin feature/my-change   # 5. push the branch
#    ... open PR on GitHub, review ...  # 6. propose + review
#    ... merge PR on GitHub ...         # 7. merge
git switch main && git pull            # 8. sync local main
```

This **branch → push → PR → review → merge → pull** cycle is the daily rhythm of professional software teams.

---

## ✅ Checkpoint

- [x] You pushed a **branch** (not `main`) to GitHub
- [x] You opened a PR, reviewed the diff, and merged it on GitHub
- [x] `git pull` brought the merged change into your local `main`
- [x] You can recite the 8-step PR loop

---

## 🧠 Try it / Discuss

1. Why merge through a PR instead of `git merge` on your laptop?
2. After merging on GitHub, why did you need to `git pull` locally?
3. What's the difference between a **branch**, a **commit**, and a **pull request**?

---

➡️ **Next:** Open `07-Undo-and-Rollback.md` — everyone makes mistakes; learn to fix them safely.
