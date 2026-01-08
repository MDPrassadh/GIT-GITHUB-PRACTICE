
# Git & GitHub Documentation

A practical guide to core Git concepts and commands with definitions, deep explanations, use cases, examples, and interview questions & answers.

---

## Table of Contents

- [Overview](#overview)
- [Git Architecture & Stages](#git-architecture--stages)
- [.git Directory](#git-directory)
- [git init](#git-init)
- [git add](#git-add)
- [git commit](#git-commit)
- [git push](#git-push)
- [git reset](#git-reset)
- [git revert](#git-revert)
- [git restore](#git-restore)
- [git show](#git-show)
- [Local-to-Remote Workflow](#local-to-remote-workflow)
- [Quick Reference](#quick-reference)

---

## Overview

This repository contains detailed documentation of essential Git commands and concepts:

- Clear **definitions**  
- Deep **explanations**  
- Real‑world **use cases**  
- Terminal **examples**  
- **Interview questions and answers** for each topic  

You can use this as:
- Personal revision notes  
- Interview preparation material  
- A portfolio repo to showcase Git knowledge  

---

## Git Architecture & Stages

### Definition

Short paragraph about:
- Working Directory  
- Staging Area (Index)  
- Local Repository (.git)  

### Explanation

Explain how a file flows through Git:

1. Edit in **working directory**  
2. Stage with `git add` into **staging area**  
3. Save snapshot with `git commit` into **repository**  
4. Publish to GitHub with `git push`  

### Example Diagram (optional)

Describe or include an ASCII diagram of the three stages.

### Interview Q&A

**Q1. Explain working directory, staging area, and repository.**  
**A1.** Your answer here.

**Q2. Why does Git have a staging area?**  
**A2.** Your answer here.

---

## .git Directory

### Definition

Explain what the `.git` folder is and why it matters.

### Explanation

- What is stored inside (`objects`, `refs`, `HEAD`, `config`, etc.)  
- Difference between project files and Git metadata  

### Use Cases

- Enabling version control  
- Copy/move full history  

### Example

```bash
mkdir my-project
cd my-project
git init
ls -a      # shows .git
```

### Interview Questions & Answers

**Q1. What is the .git directory?**  
**A1.** Your answer here.

**Q2. What happens if you delete .git from a project?**  
**A2.** Your answer here.

---

## git init

### Definition

Short definition of `git init`.

### Explanation

- When to use it  
- Difference between `git init` and `git clone`  

### Use Cases

- Start Git tracking on an existing folder  
- Initialize a new project  

### Examples

```bash
cd myapp
git init
git status
```

### Interview Questions & Answers

**Q1. When would you use git init vs git clone?**  
**A1.** Your answer here.

**Q2. Steps after git init to push to GitHub?**  
**A2.** Your answer here.

---

## git add

### Definition

Short definition of `git add`.

### Explanation

- Relationship to staging area  
- Staging full files vs partial hunks  

### Use Cases

- Create clean commits  
- Stage partial changes (`git add -p`)  

### Examples

```bash
git add file1.py
git add src/
git add .
git add -p app.py
```

### Interview Questions & Answers

**Q1. What does git add do internally?**  
**A1.** Your answer here.

**Q2. Difference between git add file.txt and git add . ?**  
**A2.** Your answer here.

---

## git commit

### Definition

Short definition of `git commit`.

### Explanation

- What a commit contains (snapshot, metadata, parents)  
- Importance of good commit messages  

### Use Cases

- Saving logical units of work  
- Creating history for debugging  

### Examples

```bash
git commit -m "Add user login feature"
git commit          # opens editor
```

### Interview Questions & Answers

**Q1. What information is stored in a commit?**  
**A1.** Your answer here.

**Q2. What is the difference between git commit and git commit --amend?**  
**A2.** Your answer here.

---

## git push

### Definition

Short definition of `git push`.

### Explanation

- Relationship between local branch and remote branch  
- Meaning of upstream tracking (`-u`)  

### Use Cases

- Share code to GitHub  
- Sync local changes with remote  

### Examples

```bash
git remote add origin https://github.com/<user>/<repo>.git
git branch -M main
git push -u origin main
git push
```

### Interview Questions & Answers

**Q1. Difference between git push, git pull, and git fetch?**  
**A1.** Your answer here.

**Q2. What does -u do in git push -u origin main?**  
**A2.** Your answer here.

---

## git reset

### Definition

Short definition of `git reset`.

### Explanation

Explain the three modes:

- `git reset --soft`  
- `git reset --mixed` (default)  
- `git reset --hard`  

### Use Cases

- Clean up local history before push  
- Unstage files  
- Discard local work (carefully)  

### Examples

```bash
git reset --soft HEAD~1
git reset HEAD file.txt
git reset --hard HEAD~1
```

### Interview Questions & Answers

**Q1. Explain soft, mixed, and hard reset.**  
**A1.** Your answer here.

**Q2. Why is git reset --hard dangerous on a shared branch?**  
**A2.** Your answer here.

---

## git revert

### Definition

Short definition of `git revert`.

### Explanation

- How revert creates a new commit  
- Why it is safer for public branches  

### Use Cases

- Undo a bad commit after it has been pushed  
- Keep history intact  

### Examples

```bash
git revert HEAD
git revert <commit-hash>
git push origin main
```

### Interview Questions & Answers

**Q1. Difference between git reset and git revert?**  
**A1.** Your answer here.

**Q2. How do you revert a commit that is already pushed to main?**  
**A2.** Your answer here.

---

## git restore

### Definition

Short definition of `git restore`.

### Explanation

- How it affects working directory and staging area  
- Difference from `git reset`  

### Use Cases

- Discard local changes to a file  
- Unstage a file using `--staged`  

### Examples

```bash
git restore file.txt
git restore --staged file.txt
git restore --source=HEAD~1 file.txt
```

### Interview Questions & Answers

**Q1. How is git restore different from git reset?**  
**A1.** Your answer here.

**Q2. How do you discard local changes to a single file?**  
**A2.** Your answer here.

---

## git show

### Definition

Short definition of `git show`.

### Explanation

- Default behavior (last commit details)  
- Custom formats using `--pretty`  

### Use Cases

- Inspect a commit before revert/cherry‑pick  
- Generate custom logs  

### Examples

```bash
git show
git show <commit-hash>
git show --stat
git show --pretty=oneline
git show --pretty=format:"%h %an %s" --no-patch
```

### Interview Questions & Answers

**Q1. Difference between git show and git log?**  
**A1.** Your answer here.

**Q2. How do you show only files changed in a commit?**  
**A2.** Your answer here.

---

## Local-to-Remote Workflow

### Typical Flow

```bash
# 1) Initialize repository
git init

# 2) Check status
git status

# 3) Stage changes
git add .

# 4) Commit changes
git commit -m "Meaningful message"

# 5) Connect to GitHub
git remote add origin https://github.com/<user>/<repo>.git

# 6) Push to remote
git push -u origin main
```

### Interview Scenario

Describe step‑by‑step how you would:

- Create a new repo locally  
- Push it to GitHub  
- Fix a bad commit using `git revert`  

---

## Quick Reference

| Command        | Purpose                          |
|----------------|----------------------------------|
| `git init`     | Initialize repository            |
| `git add`      | Stage changes                    |
| `git commit`   | Save snapshot                    |
| `git push`     | Upload to remote                 |
| `git reset`    | Move HEAD / unstage / discard    |
| `git revert`   | Create commit that undoes another|
| `git restore`  | Restore/unstage file changes     |
| `git show`     | Show commit details              |
```
