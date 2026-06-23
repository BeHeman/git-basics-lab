# Module 05 · Branching & Merging

⏱️ ~20 minutes · You'll add a **Skills section** on a separate branch, then merge it into `main` — the safe way real teams build features.

---

## Concept — why branches?

Your `main` branch is the **official, working version** of the project. You don't want to make risky, half-finished edits directly on it.

A **branch** is an independent line of work. You "branch off" `main`, build your feature in isolation, and only **merge** it back when it's ready. If the experiment fails, you just throw the branch away — `main` was never touched.

```
                ┌──● add CSS ──● style skills ──┐
                │   (feature/skills-section)    │  merge
main ──●──●──●──┴───────────────────────────────┴──●──▶
       (stable, untouched while you work)        (feature now in main)
```

> 🌿 **Analogy:** `main` is the published edition of a book. A branch is a private draft where you rewrite a chapter. Readers only see your changes once you merge them back in.

---

## Step 1 — Confirm you're on `main` and clean

```bash
git status
```

You want to see `On branch main` and `working tree clean`. If you have uncommitted changes, commit or stash them first.

---

## Step 2 — Create and switch to a feature branch

```bash
git switch -c feature/skills-section
```

**Expected output:**

```
Switched to a new branch 'feature/skills-section'
```

- `git switch -c <name>` creates a new branch **and** moves you onto it.
- Branch names often describe the work: `feature/...`, `fix/...`, etc.

> 🧓 **You may also see** the older command `git checkout -b feature/skills-section` — it does the exact same thing. `git switch` is the newer, clearer version. Both are fine.

**Confirm which branch you're on:**

```bash
git branch
```

**Expected output** (the `*` marks your current branch):

```
* feature/skills-section
  main
```

---

## Step 3 — Build the feature: add a Skills section

You'll also introduce the **CSS file** now, so the page actually looks good.

**3a.** In `index.html`, add a Skills section inside `<main>` (after About, before Contact):

```html
    <section class="skills">
      <h2>Skills</h2>
      <ul>
        <li>Terraform &amp; Infrastructure as Code</li>
        <li>Kubernetes &amp; Docker</li>
        <li>CI/CD Pipelines</li>
        <li>AWS · Azure · GCP</li>
        <li>Python &amp; Bash automation</li>
      </ul>
    </section>
```

**3b.** Link a stylesheet by adding this line inside `<head>` (under the `<title>`):

```html
  <link rel="stylesheet" href="style.css">
```

**3c.** Create a **new file** `style.css` in the same folder:

```css
body {
  font-family: system-ui, Arial, sans-serif;
  max-width: 720px;
  margin: 40px auto;
  padding: 0 20px;
  color: #1a1a2e;
  line-height: 1.6;
}

.profile-header h1 {
  margin-bottom: 4px;
}

.role {
  color: #0066cc;
  font-weight: 600;
}

.skills ul {
  list-style: none;
  padding: 0;
}

.skills li {
  background: #eef4ff;
  display: inline-block;
  margin: 4px;
  padding: 6px 12px;
  border-radius: 6px;
}

footer {
  margin-top: 40px;
  border-top: 1px solid #ddd;
  padding-top: 10px;
  font-size: 0.9em;
  color: #777;
}
```

Open `index.html` in your browser — it now has styled skill "chips" and a clean layout.

---

## Step 4 — Commit the feature on the branch

```bash
git status
```

You'll see `index.html` modified **and** `style.css` untracked. Stage both and commit:

```bash
git add index.html style.css
git commit -m "Add Skills section and stylesheet"
```

> `git add index.html style.css` stages both files at once. You could also run `git add .` to stage **everything** changed in the folder — handy, but always run `git status` first so you know exactly what `.` will include.

**All of this happened on `feature/skills-section`.** Prove `main` is untouched:

```bash
git switch main
```

Open `index.html` now — the Skills section and styling are **gone**! That's the branch doing its job: `main` still holds the old version. Switch back:

```bash
git switch feature/skills-section
```

…and the Skills section reappears. 🪄 *(This is the "aha" moment for most students — let it sink in.)*

---

## Step 5 — Merge the feature into `main`

When the feature is ready, bring it into `main`. **You merge INTO the branch you're currently on**, so first switch to `main`:

```bash
git switch main
git merge feature/skills-section
```

**Expected output:**

```
Updating f7g8h9i..k1l2m3n
Fast-forward
 index.html | 9 +++++++++
 style.css  | 38 ++++++++++++++++++++++++++++++++++++++
 2 files changed, 47 insertions(+)
 create mode 100644 style.css
```

🎉 `main` now contains the Skills section and the stylesheet. Open `index.html` from `main` — the styled page is there.

> ℹ️ **"Fast-forward"** means `main` hadn't changed since you branched, so Git simply moved `main`'s pointer forward. If `main` *had* received other commits in the meantime, Git would create a **merge commit** instead — both are normal.

---

## Step 6 — Push the merged `main` to GitHub

```bash
git push
```

Refresh GitHub — `style.css` and the Skills commit now appear on `main`.

---

## Step 7 — Clean up the merged branch (optional but tidy)

Once merged, you usually delete the feature branch:

```bash
git branch -d feature/skills-section
```

**Expected output:**

```
Deleted branch feature/skills-section (was k1l2m3n).
```

> `-d` only deletes branches that are already merged — a safety net. (`-D` force-deletes; avoid it unless you mean to discard unmerged work.)

---

## A note on merge conflicts (preview)

If two branches change the **same lines** of the same file differently, Git can't decide which to keep — that's a **merge conflict**. Git pauses and marks the spot in the file like this:

```
<<<<<<< HEAD
<p class="role">Cloud Engineer</p>
=======
<p class="role">Senior Cloud Engineer</p>
>>>>>>> feature/skills-section
```

You **edit the file** to keep what you want, remove the `<<<<`/`====`/`>>>>` markers, then `git add` the file and `git commit` to finish the merge. You likely won't hit one in this lab — but now you'll recognize it.

---

## ✅ Checkpoint

- [x] You created `feature/skills-section`, committed work there, and `main` was untouched until merge
- [x] `git merge` brought the Skills section + `style.css` into `main`
- [x] GitHub shows `style.css` on `main`
- [x] You understand what a merge conflict looks like

---

## 🧠 Try it / Discuss

1. Why work on a branch instead of editing `main` directly?
2. When you ran `git switch main` mid-feature, the Skills section vanished. Where did it go?
3. What's the difference between a **fast-forward** merge and a **merge commit**?

---

➡️ **Next:** Open `06-Pull-Requests.md` — the professional, reviewed way to merge.
