# Module 03 · Staging & Commits

⏱️ ~20 minutes · The heart of Git. You'll create the profile page and learn working directory → staging area → commit by *doing* it.

---

## Step 1 — Create the HTML skeleton

In your `cloud-profile` folder, create a file called **`index.html`** in your text editor and paste this starter:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cloud Engineer Profile</title>
</head>
<body>
  <h1>My Profile</h1>
</body>
</html>
```

Save the file. You can open it in a browser (double-click `index.html`) to see a page that just says **My Profile**.

> 📝 You just edited your **working directory** — the live files on disk. Git has *noticed* but is not yet tracking this file.

---

## Step 2 — See the untracked file

```bash
git status
```

**Expected output:**

```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        index.html

nothing added to commit but untracked files present (use "git add" to track)
```

🔴 `index.html` is shown in red as **Untracked** — Git sees it exists but isn't recording its history yet.

---

## Step 3 — Stage the file (`git add`)

Move the change from the **working directory** into the **staging area**:

```bash
git add index.html
```

(No output means success — Git is quiet when things go well.)

Check status again:

```bash
git status
```

**Expected output:**

```
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   index.html
```

🟢 Now `index.html` is green and listed under **Changes to be committed** — it's **staged** and ready.

> 🗂️ **Analogy:** You put the page in the "to be filed" box. It's not in the cabinet yet — but it's selected.

---

## Step 4 — Make your first commit (`git commit`)

Save the staged snapshot into the repository, with a message describing it:

```bash
git commit -m "Add HTML skeleton for profile page"
```

**Expected output:**

```
[main (root-commit) a1b2c3d] Add HTML skeleton for profile page
 1 file changed, 11 insertions(+)
 create mode 100644 index.html
```

🎉 **Your first commit!** `a1b2c3d` is the short **commit hash** — a unique ID for this snapshot. Git can return to exactly this state forever.

> ✍️ **Commit message rules of thumb:**
> - Write in the **imperative**: "Add header", not "Added header" or "Adding header".
> - Describe **what the change does**, not "update" or "stuff".
> - Keep the first line under ~50 characters.

---

## Step 5 — Add real content, then see the *difference*

Open `index.html` and replace the `<body>` with a proper header and an About section:

```html
<body>
  <header class="profile-header">
    <h1>Asha Verma</h1>
    <p class="role">Cloud Engineer · AWS &amp; Azure Certified</p>
  </header>

  <main>
    <section class="about">
      <h2>About Me</h2>
      <p>I design and automate scalable cloud infrastructure, with a focus on
         reliability, cost optimization, and infrastructure-as-code.</p>
    </section>
  </main>
</body>
```

> 🔁 Personalize the name, role, and text if you like — it's *your* profile.

Now ask Git **what changed** since the last commit:

```bash
git status
```

**Expected output:**

```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html

no changes added to commit (use "git add" to track)
```

`index.html` is now **modified**. To see the exact lines that changed:

```bash
git diff
```

`git diff` shows removed lines with `-` and added lines with `+`. This is how engineers review *exactly* what they're about to save. Press `q` to exit the diff view.

---

## Step 6 — Stage and commit the new section

```bash
git add index.html
git commit -m "Add header and About Me section"
```

**Expected output:**

```
[main e4f5g6h] Add header and About Me section
 1 file changed, 12 insertions(+), 1 deletion(-)
```

You now have **two commits**.

---

## Step 7 — The power of the staging area (selective commits)

Here's *why* the staging area exists. Sometimes you make **two unrelated changes** but want to save them as **separate, clean commits**.

Make **two** edits to `index.html`:

1. Add a contact email inside `<main>`, after the About section:

   ```html
   <section class="contact">
     <h2>Contact</h2>
     <p>Email: asha.verma@example.com</p>
   </section>
   ```

2. Also change the page `<title>` in the `<head>` to:

   ```html
   <title>Asha Verma — Cloud Engineer</title>
   ```

These are two different ideas (a new section vs. a metadata tweak). With staging, you *could* commit them separately. Since they're in the same file here, the lesson is the **mindset**: stage deliberately, commit logically.

```bash
git add index.html
git commit -m "Add Contact section and update page title"
```

> 🧠 **On real teams** you'll often edit several *files* at once and run `git add file-a.html` then commit, then `git add file-b.css` then commit — keeping each commit focused on one idea. Clean history makes debugging and code review far easier.

> 💡 **Shortcut you'll see later:** `git commit -am "message"` stages **all already-tracked** modified files and commits in one step. It skips the separate `git add` — but it does **not** include brand-new untracked files, and it removes your chance to stage selectively. Use it once you understand what staging does.

---

## Step 8 — View your history (`git log`)

```bash
git log --oneline
```

**Expected output** (your hashes will differ):

```
f7g8h9i Add Contact section and update page title
e4f5g6h Add header and About Me section
a1b2c3d Add HTML skeleton for profile page
```

Read it bottom-to-top — that's the story of your project so far. For full detail (author, date, full message), run plain `git log` (press `q` to exit).

---

## ✅ Checkpoint

- [x] `index.html` exists with a header, About, and Contact section
- [x] `git status` shows `nothing to commit, working tree clean`
- [x] `git log --oneline` shows **three** commits

If `git status` is clean and you have three commits, you've mastered the core Git loop:

> **edit → `git add` → `git commit`** — repeat forever.

---

## 🧠 Try it / Discuss

1. Run `git diff` *after* a clean commit. Why is the output empty?
2. What's the difference between `git status` (which lists files) and `git diff` (which shows lines)?
3. Why would a team prefer ten small, focused commits over one giant "did a bunch of stuff" commit?

---

➡️ **Next:** Open `04-GitHub-and-Push.md` — put your profile page online.
