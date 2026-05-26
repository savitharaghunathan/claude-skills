---
name: commit-push
description: Selectively stages files, commits with sign-off, and pushes to the current branch. Use when the user wants to commit and push their work, or says "commit", "push", or "ship it".
---

Commit and push changes to the current branch. Follow these steps exactly:

## 1. Show current state

Run `git status` and `git diff --stat` in parallel to show the user what has changed.

## 2. Select files to stage

Ask the user which files to stage using AskUserQuestion. Present the changed/untracked files as options (use multiSelect). If the user provided file paths in `$ARGUMENTS`, use those directly without asking.

Do NOT use `git add .` or `git add -A` — only stage the files the user selected.

## 3. Get commit message

Show `git diff --cached --stat` so the user can see what will be committed. Then ask the user for a commit message using AskUserQuestion, or use a message from `$ARGUMENTS` if one was provided.

Draft a suggested commit message based on the staged changes and present it as the first option. The message should be concise, in imperative mood, and describe the "why" not just the "what".

## 4. Credit Claude Code

Ask the user how to credit Claude Code using AskUserQuestion. Options:

- **Assisted-By (Recommended)** — `Assisted-By: Claude Code <noreply@anthropic.com>`
- **Co-Authored-By** — `Co-Authored-By: Claude Code <noreply@anthropic.com>`
- **No credit** — omit any Claude trailer

## 5. Commit with sign-off

Commit using sign-off. Always use a HEREDOC to pass the message:

```
git commit -s -m "$(cat <<'EOF'
<message>

Assisted-By: Claude Code <noreply@anthropic.com>
EOF
)"
```

If the user chose Co-Authored-By, use that trailer instead. If the user chose no credit, omit the trailer:

```
git commit -s -m "<message>"
```

## 6. Push to current branch

Determine the current branch name and push:

```
git push origin <current-branch>
```

If the branch has no upstream tracking, use:

```
git push -u origin <current-branch>
```

## 7. Confirm

Report the commit hash and that the push succeeded.
