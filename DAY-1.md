
# Git & GitHub Core Documentation

Git works in stages: you edit files in the **working directory**, select what to save in the **staging area**, then permanently store snapshots in the **repository**, and finally sync them to GitHub with `git push`.

Complete documentation with **Definition → Explanation → Use Cases → Examples → Interview Q&A** for each core concept and command.

---

## Table of Contents

1. [.git Directory](#1-git-directory)
2. [git init](#2-git-init)
3. [git add](#3-git-add)
4. [git commit](#4-git-commit)
5. [git push](#5-git-push)
6. [git reset](#6-git-reset)
7. [git revert](#7-git-revert)
8. [git restore](#8-git-revert)
9. [git show](#9-git-show)

---

## 1. .git Directory

### Definition
The `.git` directory is a hidden folder that turns a normal project folder into a **Git repository**, storing all commits, branches, tags, and configuration.

### Explanation
- When you run `git init` or `git clone`, Git creates `.git` and puts all history and metadata there.
- Your working files are just a checkout of one commit; the real "database" of Git (objects, refs, `HEAD`, config) lives inside `.git`.

### Use Cases
- Enable version control on a project; without `.git`, Git treats it as a normal folder.
- Back up or move full history by copying the project including `.git` (or at least `.git`).

### Example
```bash
mkdir myapp
cd myapp
git init        # creates .git
ls -a           # shows .git directory
```

### Interview Q&A
**Q1. What is the `.git` directory and why is it important?**  
**A1.** The `.git` directory is the internal database of a Git repository; it stores objects (blobs, trees, commits), refs (branches, tags), and configuration, and without it Git cannot track history for that folder.

**Q2. What happens if you delete the `.git` folder from a project?**  
**A2.** All version history, branches, and Git configuration are lost, and the folder becomes a normal untracked directory, although the files themselves remain.

**Q3. How is `.git` different from `.gitignore`?**  
**A3.** `.git` stores repository data, while `.gitignore` is a text file listing patterns of files that Git should ignore when staging and committing.

---

## 2. `git init`

### Definition
`git init` creates a new, empty Git repository in the current directory by initializing the `.git` folder.

### Explanation
- After `git init`, Git starts tracking changes in that directory; before that, `git status` will say "not a git repository".
- It does not create any commits or connect to GitHub automatically; you still need `git add`, `git commit`, and `git remote add` plus `git push`.

### Use Cases
- Start version control for an existing local project folder.
- Re-initialize a repository after moving files into a new folder (taking care not to break an existing `.git`).

### Example
```bash
cd myapp
git init
git status       # now shows an empty repository
```

### Interview Q&A
**Q1. When do you use `git init` vs `git clone`?**  
**A1.** Use `git init` to start a brand-new local repository from existing files; use `git clone` when you want to copy an existing remote repository, which creates `.git`, downloads history, and checks out files.

**Q2. After running `git init`, what are the next steps to push code to GitHub?**  
**A2.** 1) Stage files with `git add`, 2) create a commit with `git commit`, 3) add remote `origin` with `git remote add origin <url>`, 4) `git push -u origin <branch>`.

**Q3. What happens if you run `git init` inside an existing repo?**  
**A3.** Usually it re-initializes the same `.git`, which is mostly harmless but can confuse structure; running it inside a subfolder can create nested repos and is generally discouraged.

---

## 3. `git add`

### Definition
`git add` takes changes from the working directory and adds them to the **staging area** (index) so they are ready to be committed.

### Explanation
- Git has three areas: working directory → staging area → repository; `git add` is the step from working directory to staging area.
- You can stage whole files, directories, or selected hunks (`git add -p`) to create clean, focused commits.

### Use Cases
- Stage only related changes for a meaningful commit (e.g., stage just "login feature", not all random edits).
- Interactively stage parts of a file when you mixed two tasks in the same file.

### Examples
```bash
git add file1.py           # stage one file
git add src/               # stage folder
git add .                  # stage all new/modified files
git add -p                 # interactive staging
```

### Interview Q&A
**Q1. What does `git add` actually do?**  
**A1.** It records the current version of selected files into the staging area, telling Git "these changes should go into the next commit," without creating a commit yet.

**Q2. Difference between `git add file.txt` and `git add .`?**  
**A2.** `git add file.txt` stages only that file; `git add .` stages all modified and untracked files under the current directory, which can accidentally include temporary or unrelated files.

**Q3. How do you stage only part of a file? Why is it useful?**  
**A3.** Use `git add -p file.txt`, which lets you accept or reject individual hunks; this is useful to separate unrelated changes into separate commits for better history and code review.

---

## 4. `git commit`

### Definition
`git commit` takes everything in the staging area and creates a new snapshot (commit) in the local repository with a message.

### Explanation
- A commit stores a tree of files, metadata (author, date), and a pointer to parent commit(s).
- Git identifies commits by SHA-1 hash, which you use in commands like `git show`, `git revert`, etc.

### Use Cases
- Save a logical unit of work (feature, bug fix, refactor) with a clear message.
- Create history checkpoints so you can revert, compare, or bisect later.

### Examples
```bash
git commit -m "Implement user login"
git commit               # opens editor for detailed message
```

### Interview Q&A
**Q1. What information is stored in a Git commit object?**  
**A1.** A commit stores a tree (snapshot of files), parent commit hash(es), author/committer info, timestamp, and commit message.

**Q2. What is a good commit message and why does it matter?**  
**A2.** A good message briefly describes the "what" and sometimes the "why" (e.g., "Fix NPE in OrderService when cart is empty"); it improves history readability, code review, and debugging.

**Q3. Difference between `git commit` and `git commit --amend`?**  
**A3.** `git commit` creates a new commit; `git commit --amend` replaces the last commit with a new one (updated message and/or content), rewriting history and should be used only before sharing that commit.

---

## 5. `git push`

### Definition
`git push` uploads local commits from your branch to a remote repository (like GitHub).

### Explanation
- By default, `git push origin main` sends your local `main` branch commits to `origin/main` on the remote.
- `git push -u origin main` sets tracking so later `git push` knows which remote branch to update.

### Use Cases
- Share work with team members or open source community via GitHub.
- Back up your local history on a remote server.

### Examples
```bash
git remote add origin https://github.com/user/repo.git
git push -u origin main       # first time
git push                      # subsequent pushes
```

### Interview Q&A
**Q1. Difference between `git push`, `git pull`, and `git fetch`?**  
**A1.** `git push` sends local commits to remote; `git fetch` downloads remote commits but doesn't merge; `git pull` = `git fetch` + `git merge` into current branch.

**Q2. What does `-u` do in `git push -u origin main`?**  
**A2.** It sets `origin/main` as the upstream branch for `main`, allowing simple `git push`/`git pull` without specifying remote and branch each time.

**Q3. What happens if your local branch is behind the remote when you push?**  
**A3.** Git normally rejects the push with a non-fast-forward error; you must first `git pull` (or fetch + rebase/merge) and resolve conflicts before pushing again.

---

## 6. `git reset`

### Definition
`git reset` moves the current branch (HEAD) to another commit and optionally updates the staging area and working directory.

### Explanation
- `--soft`: move HEAD only, keep index and working dir unchanged.
- `--mixed` (default): move HEAD and reset index, keep working dir.
- `--hard`: move HEAD, reset index and working dir, discarding local changes.
- Used mainly for **local** history rewriting or un-staging.

### Use Cases
- Remove or modify recent commits before they are pushed (cleanup before sharing).
- Unstage files accidentally added with `git add .`.

### Examples
```bash
git reset --soft HEAD~1      # undo last commit, keep changes staged
git reset HEAD file.txt      # unstage file, keep changes in working dir
git reset --hard HEAD~1      # remove last commit & discard changes
```

### Interview Q&A
**Q1. Explain `git reset --soft`, `--mixed`, and `--hard`.**  
**A1.** 
- `--soft`: moves HEAD to another commit but leaves staging and working directory as-is.
- `--mixed`: moves HEAD and resets staging to match new commit, leaving working directory unchanged.
- `--hard`: moves HEAD and resets both staging and working directory to match target commit, discarding local changes.

**Q2. Why is `git reset --hard` dangerous on a shared branch?**  
**A2.** It rewrites history and discards files; if commits were already pushed, others may have them locally, causing divergence and potential loss of changes when they pull.

**Q3. How do you unstage a file you accidentally added?**  
**A3.** Run `git reset HEAD file.txt` (classic way) or `git restore --staged file.txt` (newer way) to move it back to "modified but not staged".

---

## 7. `git revert`

### Definition
`git revert` creates a new commit that reverses the changes introduced by a specific commit.

### Explanation
- It does not remove the old commit; instead, it adds an "inverse" commit on top, preserving history.
- This is the recommended way to undo changes on **public** branches that are already pushed.

### Use Cases
- Undo a buggy commit on `main` after it has been pushed to GitHub.
- Safely revert a specific change without rewriting history.

### Examples
```bash
git revert HEAD             # revert latest commit
git revert abc1234          # revert specific commit
git push origin main        # publish the revert
```

### Interview Q&A
**Q1. Difference between `git reset` and `git revert`?**  
**A1.** `git reset` moves branch pointers and can drop commits (rewriting history), usually used locally; `git revert` adds a new commit that undoes changes while keeping the original commits in history, safe for shared branches.

**Q2. How do you revert a commit that has already been pushed?**  
**A2.** Use `git revert <commit>` to create a new commit that inverts the original, then `git push origin <branch>`; this keeps other developers' history intact.

**Q3. What if you reverted the wrong commit?**  
**A3.** Run `git revert <revert-commit-hash>` (revert the revert) or create a new commit manually fixing the change; both keep history consistent.

---

## 8. `git restore`

### Definition
`git restore` restores file content either from the index or from a commit to the working directory, and can also unstage files.

### Explanation
- Introduced in Git 2.23 to separate "restore files" from "move HEAD", which `git reset` combines.
- Does **not** move HEAD; it only manipulates working directory and index.

### Use Cases
- Discard local changes in a file and go back to last committed version.
- Unstage a file without touching its content using `git restore --staged`.

### Examples
```bash
git restore file.txt                 # discard local changes in file.txt
git restore --staged file.txt        # unstage, keep changes in working dir
git restore --source=HEAD~1 file.txt # restore from older commit
```

### Interview Q&A
**Q1. How is `git restore` different from `git reset`?**  
**A1.** `git restore` only affects files in working directory and index, never moves HEAD; `git reset` can move HEAD and optionally index/working tree, rewriting commit history.

**Q2. How do you discard local changes to a single file?**  
**A2.** Use `git restore file.txt` (or older `git checkout -- file.txt`), which replaces file contents with the version from HEAD.

**Q3. How do you unstage a file using `git restore`?**  
**A3.** Run `git restore --staged file.txt`; this removes it from the staging area while keeping modifications in the working directory.

---

## 9. `git show` (and pretty)

### Definition
`git show` shows details about Git objects; by default, it displays the latest commit's metadata and diff.

### Explanation
- You can pass a commit hash, tag, or reference to inspect that object.
- Options like `--stat`, `--name-only`, and `--pretty=format:` customize the output for scripts or logs.

### Use Cases
- Inspect what exactly changed in a specific commit before reverting or cherry-picking.
- Generate machine-friendly commit logs for tooling.

### Examples
```bash
git show                        # last commit
git show abc1234                # specific commit
git show --stat                 # summary of changes
git show --pretty=oneline       # short hash + message
git show --pretty=format:"%h %an %s"
```

### Interview Q&A
**Q1. What does `git show` display by default, and how is it different from `git log`?**  
**A1.** `git show` with no args shows one commit (usually HEAD) with metadata and diff; `git log` shows a list of commits (history) and typically no full diff unless asked.

**Q2. How can you show only the files changed in a commit?**  
**A2.** Use `git show --name-only <commit>` or `git show --stat <commit>` to see just file names and summary stats instead of full diff.

**Q3. How do you customize `git show` output to show only hash, author, and subject?**  
**A3.** Use `git show --pretty=format:"%h %an %s" --no-patch`, which prints the formatted header without the diff.

---

## Quick Reference Table

| Command | Purpose |
|---------|---------|
| `git init` | Initialize repository |
| `git add` | Stage changes |
| `git commit` | Save snapshot |
| `git push` | Upload to remote |
| `git reset` | Move HEAD / unstage / discard |
| `git revert` | Create commit that undoes another |
| `git restore` | Restore/unstage file changes |
| `git show` | Show commit details |

