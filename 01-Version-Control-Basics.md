# Module 01 · Version Control Basics

⏱️ ~10 minutes · **Concept-only module** (no commands yet — just understanding)

---

## The problem version control solves

Imagine you're building the profile page and you save copies as you go:

```
index.html
index-v2.html
index-final.html
index-final-REALLY.html
index-final-use-this-one.html
```

Sound familiar? This is **manual version control**, and it's painful:

- ❌ Which file is actually the latest?
- ❌ What changed between `v2` and `final`?
- ❌ A teammate emails *their* `index-final.html` — now whose is correct?
- ❌ You broke something. Which version worked?

**Version control** solves all of this. It's a system that records **every change** to your files over time, so you can:

- ✅ See exactly **what changed, when, and who changed it**
- ✅ Go **back** to any previous version instantly
- ✅ Work on **new features safely** without breaking the working version
- ✅ **Collaborate** — multiple people edit the same project without overwriting each other

---

## What is Git?

**Git** is the world's most popular version control system. It was created in 2005 by Linus Torvalds (the creator of Linux) and is used by virtually every software company on earth.

Git is a **distributed** version control system. That means:

- Every developer has the **full project history** on their own machine.
- You can work **offline** — commit, branch, view history — with no server.
- There's no single point of failure.

> 🗝️ **Key idea:** Git takes *snapshots* of your project. Each time you save a checkpoint (a **commit**), Git remembers the entire state of your files at that moment, like a save point in a video game.

---

## How Git thinks: the three areas

This is the **single most important concept** in this lab. Git moves your changes through **three areas**:

```
┌──────────────────┐   git add    ┌──────────────────┐   git commit   ┌──────────────────┐
│ Working Directory│  ─────────▶  │   Staging Area   │  ───────────▶  │   Repository     │
│  (your edits)    │              │  (ready to save) │                │ (saved history)  │
└──────────────────┘              └──────────────────┘                └──────────────────┘
```

| Area | What it is | Real-world analogy |
|------|------------|--------------------|
| **Working Directory** | The actual files you see and edit in your folder | Your desk — papers you're actively writing on |
| **Staging Area** | A "holding zone" for changes you've chosen to include in your next commit | A box where you place the pages you want to file |
| **Repository (.git)** | The permanent, saved history of commits | The filing cabinet — sealed records you can always retrieve |

**Why three areas instead of two?** The staging area lets you **choose exactly what goes into each commit**. You might edit five files but only want to save two of them together as one logical change. Staging gives you that control.

You'll *feel* why this matters in Module 03.

---

## The core vocabulary

You'll use these words all day. Learn them now:

| Term | Meaning |
|------|---------|
| **Repository (repo)** | A project tracked by Git — your folder + its hidden `.git` history |
| **Commit** | A saved snapshot of your project at a point in time, with a message |
| **Staging** | Marking changes (`git add`) to be included in the next commit |
| **Branch** | An independent line of work — lets you build features without touching `main` |
| **`main`** | The default primary branch (the "official" version) |
| **Remote** | A copy of the repo hosted elsewhere (e.g., on GitHub) |
| **`origin`** | The default name Git gives to your main remote |
| **Push** | Upload your local commits to the remote |
| **Pull** | Download commits from the remote to your local repo |
| **Clone** | Make a local copy of a remote repository |
| **Merge** | Combine the changes from one branch into another |

> Don't memorize these in isolation — you'll use each one in context shortly, and that's when they'll stick.

---

## ✅ Checkpoint

Before moving on, you should be able to answer:

1. Why is saving `index-final-v3.html` a bad version-control strategy?
2. What are the **three areas** Git moves changes through, in order?
3. What's the difference between **Git** and **GitHub**?

---

## 🧠 Discuss

- The staging area is unique to Git — many older tools went straight from "edit" to "save." Why might "choosing what to commit" be valuable on a real team?
- Git is *distributed* — everyone has the full history. How is that safer than storing the only copy on one central server?

---

➡️ **Next:** Open `02-Setup-and-Init.md` — time to install Git and create your first repository.
