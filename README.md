# git-merge-conflict-demo

A minimal, hands-on demonstration of **Git branching and merge-conflict resolution**, created for the Complex Engineering Problem (CEP) in *Open Source Technologies (01CE0526)*, Marwadi University.

## 📌 Overview

This repository shows the complete lifecycle of a merge conflict:

1. A `main` branch and a `feature` branch independently modify the **same line** of the **same file**.
2. Merging `feature` into `main` triggers a real Git conflict (not a simulated one).
3. The conflict is resolved manually, committed, and verified.

## 📂 Project Structure

```
git-merge-conflict-demo/
├── app.txt      # the single tracked file used to create and resolve the conflict
└── README.md    # this file
```

## ⚙️ Prerequisites

- [Git](https://git-scm.com/downloads) installed (`git --version` to check)
- A terminal / Git Bash
- (Optional) A GitHub account, if you want to push this repo remotely

## 🚀 Workflow Reproduced in This Repo

| Step | Command(s) | Result |
|---|---|---|
| Initialize repo | `git init` / `git branch -M main` | Empty repo on `main` |
| Initial commit | `git add . && git commit -m "Initial commit"` | `app.txt` with baseline content committed |
| Create feature branch | `git checkout -b feature` | Isolated branch for independent changes |
| Conflicting edits | Edited the same line of `app.txt` differently on `main` and `feature` | Two diverging commits |
| Merge | `git checkout main && git merge feature` | Git reports `CONFLICT (content): Merge conflict in app.txt` |
| Resolve | Manually edited `app.txt`, removed `<<<<<<<`, `=======`, `>>>>>>>` markers | Single agreed final line |
| Finalize | `git add app.txt && git commit -m "Resolve merge conflict"` | Merge commit completed |
| Verify | `git status` / `git log --oneline --graph --all` | Clean working tree, full traceable history |

## 🔍 Understanding the Conflict Markers

When Git can't auto-merge a line, it wraps both versions like this inside the file:

```
<<<<<<< HEAD
(content currently on main)
=======
(incoming content from feature)
>>>>>>> feature
```

- `<<<<<<< HEAD` → start of **your current branch's** version
- `=======` → divider between the two versions
- `>>>>>>> feature` → end of the **incoming branch's** version

Resolving a conflict means deleting these markers and leaving only the correct final content.

## ▶️ Reproduce It Yourself

```bash
git --version
mkdir git-merge-conflict-demo && cd git-merge-conflict-demo
git init
git branch -M main

echo "Application Mode: Basic" > app.txt
git add .
git commit -m "Initial commit"

git checkout -b feature
# edit app.txt -> Application Mode: Development
git add app.txt
git commit -m "Update mode to Development on feature branch"

git checkout main
# edit app.txt -> Application Mode: Production
git add app.txt
git commit -m "Update mode to Production on main branch"

git merge feature
# -> CONFLICT (content): Merge conflict in app.txt

# resolve manually in app.txt, then:
git add app.txt
git commit -m "Resolve merge conflict"

git status
git log --oneline --graph --all
```

## 🎯 Learning Outcomes

- Understanding branch isolation and why conflicts occur only when the **same line** changes differently.
- Reading and correctly interpreting Git's conflict-marker syntax.
- Making a deliberate, documented decision when resolving a conflict (not just picking one side blindly).
- Verifying repository integrity after a merge using `git status` and `git log`.

## 📄 License

This is an educational demo project created for coursework purposes.
