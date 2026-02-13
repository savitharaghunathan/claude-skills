---
name: new-branch
description: Creates a new branch after syncing upstream/main to origin/main via rebase. Use when starting new work, creating feature branches, or when the user says "new branch" or "create branch".
---

Create a new Git branch from a freshly synced main. Follow these steps exactly:

## 1. Get the branch name

If the user did not provide a branch name as an argument (`$ARGUMENTS`), ask them what to name the branch using AskUserQuestion.

## 2. Sync upstream/main to origin/main

Run these commands sequentially:

```
git fetch upstream
git fetch origin
git checkout main
git rebase upstream/main
git push origin main
```

If any step fails, stop and report the error. Common issues:
- No `upstream` remote configured — tell the user to add it with `git remote add upstream <url>`
- Rebase conflicts — report them and do not continue

## 3. Create and switch to the new branch

```
git checkout -b <branch-name>
```

## 4. Confirm

Report that the branch was created and is tracking the latest upstream/main.
