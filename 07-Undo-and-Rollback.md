# Module 07 · Undo & Rollback

⏱️ ~20 minutes · The safety-net module. You'll learn to undo uncommitted edits, fix a bad commit, and roll back a mistake that's already on GitHub — **safely**.

---

## The golden rule first

There are two very different situations, and they call for different tools:

| Situation | Safe tool | Why |
|-----------|-----------|-----|
| The mistake is **only on your laptop** (not pushed) | `reset` or `restore` or `--amend` | You can freely rewrite local history |
| The mistake is **already pushed/shared** | `revert` | It creates a *new* commit that undoes the old one — it doesn't rewrite shared history |

> ⚠️ **Never rewrite history that others may have pulled.** Rewriting *shared* history (`reset`/`--amend` then force-push) breaks your teammates' repos. For anything already on GitHub, prefer **`git revert`**.

You'll practice each tool below.

---

## Scenario A — Undo edits you haven't committed yet

You're experimenting and make a change to `index.html` you don't want to keep.

**Set it up:** open `index.html` and change your role line to something silly, e.g.:

```html
<p class="role">Professional Nap Taker</p>
```

Save. Now you regret it. Check status:

```bash
git status
```

```
Changes not staged for commit:
        modified:   index.html
```

**Throw away the un-staged change** and restore the last committed version:

```bash
git restore index.html
```

Open `index.html` — your real role is back. ✅ The bad edit is gone, no commit was ever made.

> 🧯 `git restore <file>` discards **uncommitted** changes in your working directory. It only affects edits you have *not* committed — it can't hurt your saved history.
>
> If you had already **staged** it (`git add`), first un-stage with `git restore --staged index.html`, then `git restore index.html`.

---

## Scenario B — Fix the *message* of your most recent commit

You just committed but made a typo **in the commit message** (and haven't pushed yet).

**Set it up** — make a small real change and commit it with a typo:

```bash
# add a tagline to index.html (e.g., inside the header), then:
git add index.html
git commit -m "Add taglien"        # oops, typo
```

**Fix the message** with `--amend`:

```bash
git commit --amend -m "Add tagline to header"
```

`git log --oneline` now shows the corrected message. `--amend` **replaces** the last commit.

> ⚠️ `--amend` rewrites the last commit, which changes its hash. Only amend commits you **haven't pushed**. If you already pushed, use Scenario D instead.

You can also use `--amend` to add a **forgotten file** to the last commit:

```bash
git add forgotten-file.css
git commit --amend --no-edit       # keep the same message
```

---

## Scenario C — Undo a local commit but keep the work

You committed too early — the code's fine but you want to **un-commit** and keep editing.

**Set it up** — make a change and commit it:

```bash
# edit style.css, then:
git add style.css
git commit -m "WIP: experimenting with colors"
```

Now "un-commit" it — move the commit's changes **back to your working directory**:

```bash
git reset --soft HEAD~1     # undo commit, keep changes STAGED
# — or —
git reset HEAD~1            # (a.k.a. --mixed) undo commit, keep changes UNSTAGED
```

`HEAD~1` means "one commit before the current tip." Your files are untouched on disk — only the **commit** was removed. Keep editing, then re-commit when ready.

| Reset mode | Removes the commit? | Your file changes | Staged? |
|------------|--------------------|-------------------|---------|
| `--soft`  | Yes | **Kept** | Yes (staged) |
| `--mixed` (default) | Yes | **Kept** | No (unstaged) |
| `--hard`  | Yes | **DISCARDED** ❌ | — |

> ☢️ **`git reset --hard` deletes your changes permanently.** Use it only when you truly want to throw work away. When in doubt, use `--soft` or `--mixed` — they keep your edits.

---

## Scenario D — Roll back a commit that's already pushed (the safe way)

This is the most important real-world skill. A bad change is **already on GitHub**, possibly pulled by teammates. You must undo it **without rewriting shared history**.

**Set it up** — make a genuinely bad change, commit, and push:

```bash
# In style.css, wreck the body color, e.g.:  color: #ff00ff;  background: #00ff00;
git add style.css
git commit -m "Update color scheme"
git push
```

Yikes — the page is now neon and unreadable, and it's live on GitHub.

**Roll it back with `git revert`:**

```bash
git revert HEAD
```

Git opens an editor with a prepared message like `Revert "Update color scheme"`. Save and close it (in the default `vim`, type `:wq` then Enter; in nano, `Ctrl+O`, Enter, `Ctrl+X`).

**Expected output:**

```
[main t7u8v9w] Revert "Update color scheme"
 1 file changed, 2 insertions(+), 2 deletions(-)
```

Then publish the fix:

```bash
git push
```

**What happened:** `revert` created a **brand-new commit** that is the *opposite* of the bad one — it puts the good colors back. Your history now reads:

```bash
git log --oneline
```

```
t7u8v9w Revert "Update color scheme"
s6t7u8v Update color scheme          ← the bad commit is still here, but undone
p4q5r6s Add 'Open to work' availability badge
...
```

> ✅ **Why this is the safe choice:** the original commit is **preserved** in history, and the undo is just another normal commit on top. Anyone who pulls simply gets the fix. Nobody's repo breaks. This is how you fix mistakes on shared branches.

> 🔁 **revert vs reset — the one-line summary:**
> - **`revert`** = undo by adding a new "opposite" commit. **Safe for pushed/shared code.**
> - **`reset`** = undo by removing commits / moving the branch pointer back. **Local-only.**

---

## Scenario E — Go *look at* an old version (without changing anything)

Sometimes you just want to **see** how the project looked at an earlier commit.

```bash
git log --oneline                 # find the commit hash you want
git checkout a1b2c3d              # jump to that snapshot (read-only "detached HEAD")
```

Open the files — they're exactly as they were back then. To return to the present:

```bash
git switch main
```

> 👀 This is **time travel for reading**, not editing. Great for "when did this break?" investigations. You looked; nothing changed.

---

## Quick decision guide

```
Did I already push / share the change?
├─ NO  → Want to discard uncommitted edits?     → git restore <file>
│        Want to fix the last commit/message?   → git commit --amend
│        Want to un-commit but keep my work?    → git reset --soft HEAD~1
│        Want to nuke local commits & changes?  → git reset --hard  (☢️ careful)
│
└─ YES → Undo a pushed commit safely            → git revert <commit>  ✅
```

---

## ✅ Checkpoint

- [x] You discarded an uncommitted edit with `git restore`
- [x] You fixed a commit message with `git commit --amend`
- [x] You un-committed with `git reset --soft` and kept your work
- [x] You safely rolled back a **pushed** commit with `git revert` and pushed the fix
- [x] You can explain **revert vs. reset** in one sentence

---

## 🧠 Try it / Discuss

1. Your teammate already pulled your bad commit. Why is `git revert` safer than `git reset` here?
2. What's the practical difference between `reset --soft`, `--mixed`, and `--hard`?
3. `git restore` vs `git revert` vs `git reset` — which touches *uncommitted* changes, which adds a *new* commit, which *removes* commits?

---

➡️ **Next:** Open `08-Cheat-Sheet.md` — your one-page command reference. And `09-Instructor-Guide.md` if you're teaching this.
