# Version Control Guide for Writers

> **Intended audience:** Writers with an IT background. Basic familiarity with the command line and Git concepts is assumed.

This is a guide, not a requirement. Writers are welcome to work in whatever way they feel most comfortable. That said, following this workflow is strongly encouraged - AI tools like Claude only retain the latest version of a file on their servers, meaning that if you need to revert an erroneous edit, doing so quickly and cleanly may not be possible without version control. Git ensures that every stage of your work is preserved and that any change can be undone at any point.

## Overview

1. Generate report from Claude, insert screenshots, and initialise the Git repository.
2. Create a `humanization` branch, humanize the entire document, and merge it into the `main` branch.
3. Submit for AI detection and similarity scoring. Proceed to next step only after passing those tests.
4. Create a `footnote` branch, add footnotes to the sentences, and rebase `footnote` onto `main`.
5. Push the repository to GitHub.

---

## Steps in Git

### 1. Initialise the Repository

Generate your report, insert all required screenshots, then initialise a Git repository and create the first commit.

```bash
git init
git add .
git commit -m "Initial commit: report with screenshots"
```

> **Tip:** Commit after every meaningful change throughout this workflow, not just at the end of each phase. The more granular your commits, the more precisely you can revert if something goes wrong - committing everything at once defeats the purpose.

---

### 2. Create and Work on the Humanization Branch

Create and switch to the `humanization` branch. Apply all humanization edits to the document, then stage and commit your changes.

```bash
git checkout -b humanization
# Apply humanization edits to the document
git add .
git commit -m "Humanization: revised tone and readability"
```

---

### 3. Merge Humanization Branch into Main

Switch back to `main` and merge the `humanization` branch to incorporate all changes.

```bash
git checkout main
git merge humanization
```

---

### 4. Create and Work on the Footnote Branch

From `main`, create and switch to the `footnote` branch. Add footnotes to all relevant sentences, then stage and commit your changes.

```bash
git checkout -b footnote
# Add footnotes to sentences
git add .
git commit -m "Footnotes: added references and annotations"
```

---

### 5. Rebase Footnote Branch onto Main

Rebase the `footnote` branch onto `main`. This replays the footnote commits on top of the current main history, producing a clean, linear commit log.

```bash
git checkout footnote
git rebase main
```

---

### 6. Promote Footnote Branch to Main

Rebasing moves the commits of `footnote` on top of `main` but does not update `main` itself - `main` still points to its old position. This step fast-forwards `main` to match `footnote`, making the annotated version the authoritative main branch.

```bash
git checkout main
git reset --hard footnote
```

---

### 7. Push to GitHub

Push the completed repository to GitHub.

```bash
git remote add origin https://github.com/<org>/<repo>.git
git push -u origin main
```

---

## What to Do If Something Goes Wrong

**Check your commit history** to find where things went sideways:

```bash
git log --oneline
```

**Undo the last commit** while keeping your file changes intact:

```bash
git revert HEAD
```

**Undo the last commit and discard all changes** (destructive - use with caution):

```bash
git reset --hard HEAD~1
```

**Conflict resolution:** If conflicts arise during a merge or rebase, Git will pause and prompt you to resolve them. After resolving each file, stage it and continue:

```bash
git add <resolved-file>
git rebase --continue   # or: git merge --continue
```

---

## After Publishing

Any follow-up from the team will be dealt with promptly, but the repository will not be updated after the initial push. All changes must be incorporated and verified before running the push in Step 7.

---

## Notes

- **After rebasing:** The `footnote` branch will have the same history as `main`, with its commits applied on top.
- **Force-updating main:** The `git reset --hard footnote` command is irreversible. Verify the rebase is complete and correct before running it.

---

# Command Reference

A quick explanation of every command used in this guide.

| Command                       | What it does                                                                                                      |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| `git init`                    | Creates a new Git repository in the current folder - sets up the hidden `.git` directory that tracks all changes. |
| `git add .`                   | Stages all changed files, marking them as ready to be included in the next commit.                                |
| `git commit -m "..."`         | Saves a snapshot of all staged files with a short description of what changed.                                    |
| `git checkout -b <branch>`    | Creates a new branch and switches to it in one step.                                                              |
| `git checkout <branch>`       | Switches to an existing branch.                                                                                   |
| `git merge <branch>`          | Brings the changes from the specified branch into the current branch.                                             |
| `git rebase <branch>`         | Replays the current branch's commits on top of the specified branch, producing a cleaner, linear history.         |
| `git reset --hard <branch>`   | Moves the current branch pointer to match another branch exactly, discarding any differences.                     |
| `git remote add origin <url>` | Links the local repository to a remote GitHub repository.                                                         |
| `git push -u origin main`     | Uploads the `main` branch to GitHub and sets it as the default tracking branch for future pushes.                 |
| `git log --oneline`           | Shows the commit history in a compact one-line-per-commit format.                                                 |
| `git revert HEAD`             | Creates a new commit that undoes the last commit, leaving history intact.                                         |
| `git reset --hard HEAD~1`     | Moves the branch back one commit and discards all changes - this cannot be undone.                                |
| `git rebase --continue`       | Resumes a rebase after you have resolved a conflict.                                                              |
