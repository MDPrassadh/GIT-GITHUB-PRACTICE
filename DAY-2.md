
# Git Advanced Commands Documentation

**Continuation of Git Core Documentation** - Additional commands following the same **Definition → Explanation → Use Cases → Examples → Interview Q&A** pattern.

---

## 10. `git remote -v`

### Definition
`git remote -v` (verbose) displays all remote repositories linked to your local repository with their URLs.

### Explanation
- Git remotes are bookmarks to remote repositories (like GitHub repos).
- `-v` shows both **fetch** (pull from) and **push** (push to) URLs; you can have different URLs for each.
- Without `-v`, just `git remote` lists remote names only.

### Use Cases
- Check which GitHub repos your local project is connected to.
- Verify push/pull URLs before `git push` or `git pull`.
- Debug remote connection issues or multiple remotes.

### Examples
```bash
git remote -v                          # show all remotes with URLs
git remote add origin https://github.com/user/repo.git  # add remote
git remote rename origin upstream      # rename remote
git remote remove origin               # remove remote
```
[web:30][web:29]

### Interview Q&A
**Q1. What does `git remote -v` show and why use `-v`?**  
**A1.** It shows all remotes with their fetch and push URLs; `-v` (verbose) is used because `git remote` alone only shows remote names without URLs.[web:30]

**Q2. How do you add a new remote repository?**  
**A2.** Use `git remote add <name> <url>` (e.g., `git remote add origin https://github.com/user/repo.git`), then verify with `git remote -v`.[web:30]

**Q3. What if `git push` fails with "no upstream branch"?**  
**A3.** Run `git push -u origin main` first to set upstream tracking, then future `git push` works without specifying remote/branch.[web:29]

---

## 11. `git log` (including `-1`, `-2`, `--oneline`)

### Definition
`git log` displays the commit history of the current branch, from newest to oldest.

### Explanation
- Shows commit hash, author, date, and message for each commit.
- `-1` or `-n 1` = last 1 commit; `-2` = last 2 commits.
- `--oneline` condenses to single line: hash + first line of message (very useful for overview).
- Other flags: `--graph` (branch visualization), `--author=<name>`, `--since=<date>`.

### Use Cases
- Review recent commits before merging or pushing.
- Find specific commits by author/date/message.
- Visualize branch history with `--graph --oneline`.

### Examples
```bash
git log                          # full history
git log -1                       # last commit only
git log -2                       # last 2 commits
git log --oneline                # compact one-line view
git log --oneline --graph        # branches + compact
git log --author="John"          # commits by specific author
```
[web:40][web:42]

### Interview Q&A
**Q1. Difference between `git log`, `git log -1`, and `git log --oneline`?**  
**A1.** `git log` shows full details of all commits; `git log -1` shows only the latest commit; `git log --oneline` condenses entire history to single lines (hash + message).[web:42]

**Q2. How do you see commit history for a specific file?**  
**A2.** Use `git log -- <filename>` or `git log -p -- <filename>` to see commits that modified that file (with `-p` for diffs).[web:40]

**Q3. How do you visualize branches in git log?**  
**A3.** Run `git log --graph --oneline --all` to see ASCII branch graph for all branches in compact format.[web:42]

---

## 12. `git clean -n` and `git clean -f`

### Definition
`git clean` removes **untracked files** from your working directory; `-n` (dry-run) shows what would be deleted; `-f` (force) actually deletes them.

### Explanation
- **Untracked files** = files not in Git index and not ignored by `.gitignore`.
- `-n` (dry-run): preview what will be removed (safe to test).
- `-f` (force): permanently delete untracked files.
- Combine with `-d` for untracked directories: `git clean -fd`.

### Use Cases
- Clean up build artifacts, temp files, IDE caches after switching branches.
- Remove downloaded dependencies or generated files before committing.
- Always use `-n` first to preview!

### Examples
```bash
git clean -n                # DRY RUN: preview untracked files to delete
git clean -f                # FORCE: delete untracked files
git clean -fd               # delete untracked files AND directories
git clean -fx               # ignore .gitignore (dangerous!)
```
[web:41]

### Interview Q&A
**Q1. What does `git clean` remove and what's the difference between `-n` and `-f`?**  
**A1.** Removes untracked files (not staged/committed); `-n` previews (dry-run), `-f` actually deletes them.[web:41]

**Q2. What are "untracked files" in Git?**  
**A2.** Files in working directory that are neither staged (`git add`) nor committed, and not ignored by `.gitignore`.[web:41]

**Q3. Safe way to use `git clean`?**  
**A3.** Always run `git clean -n` first to preview, then `git clean -f` or `git clean -fd` to delete files/directories.[web:41]

---

## 13. What is a "Bad Commit" + How to Fix with `git reset` vs `git revert`

### Definition
A **bad commit** is one with wrong code, incomplete features, poor messages, accidental secrets, or files that shouldn't have been committed.

### Explanation
- **Local bad commit** (not pushed): Use `git reset` to rewrite history.
- **Pushed bad commit** (shared): Use `git revert` to safely undo without breaking others' history.
- `git reset` rewrites history (dangerous for shared repos); `git revert` adds new commit undoing the bad one.

### Use Cases
- **reset** (local only): Fix message (`--soft`), change files (`--mixed`), discard completely (`--hard`).
- **revert** (pushed/shared): Undo bug/security issue while keeping audit trail.

### Examples
```bash
# BAD COMMIT (local) - fix with reset
git reset --soft HEAD~1     # keep changes staged, redo commit
git reset --hard HEAD~1     # discard commit + changes

# BAD COMMIT (pushed) - fix with revert
git revert HEAD             # create new commit undoing last one
git push origin main
```
[web:43][web:11]

### Interview Q&A
**Q1. What is a "bad commit" and how do you fix it locally vs remotely?**  
**A1.** Bad commit = wrong code/secrets/poor message; locally use `git reset --soft HEAD~1` to fix; remotely use `git revert HEAD` to safely undo.[web:43]

**Q2. When do you use `git reset` vs `git revert` for bad commits?**  
**A2.** `git reset` for unpushed/local commits (rewrites history); `git revert` for pushed/shared commits (adds safe undo commit).[web:43][web:11]

**Q3. Accidentally committed a secret (API key)? What do you do?**  
**A3.** `git reset --hard HEAD~1` locally + never push; if pushed, `git revert HEAD`, regenerate key, and use BFG Repo-Cleaner for history rewrite (extreme cases).[web:43]

---

