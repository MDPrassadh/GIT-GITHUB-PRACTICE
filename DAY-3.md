
# Git Revert vs Reset: File Behavior Deep Analysis

**Scenario Analysis**: How `git revert` and `git reset` affect **existing modified files** vs **new files** in local working directory.

---

## Deep Analysis: `git revert` vs `git reset` File Behavior

### What Happens to Files?

| Scenario | `git reset --hard HEAD~1` | `git revert HEAD` |
|----------|---------------------------|-------------------|
| **Existing file** (tracked, modified locally) | **Changes lost** - resets to previous commit state | **Changes lost** - applies inverse patch (reverts commit changes) |
| **New file** (untracked, created locally) | **File remains** (untracked files unaffected) | **File remains** (untracked files unaffected) |
| **New file** (staged but uncommitted) | **File deleted** from staging + working dir | **File remains staged** |

### Key Difference
- **Both discard local working directory modifications** to tracked files
- **Neither affects truly untracked files**
- **reset rewrites history**; **revert adds new commit**

---

## Scenario 1: Existing Tracked File (Modified Locally)

### Definition & Behavior
**Existing file** = tracked by Git (in previous commits). Local modifications exist in working directory.

**`git reset --hard HEAD~1`**:
- Moves HEAD to previous commit
- **Resets working directory + staging area** to match previous commit
- **Local changes are LOST forever**

**`git revert HEAD`**:
- Creates new commit with inverse changes of last commit
- **Applies inverse patch** to working directory
- **Local changes are LOST** (overwritten by revert patch)

### Example
```bash
# File: app.js (tracked, previously committed)
echo "v1.0 code" > app.js    # commit 1
git add app.js; git commit -m "v1"

echo "v2.0 code + local edit" > app.js  # modify locally

# CASE 1: reset (local only)
git reset --hard HEAD~1      # app.js → "v1.0 code", local edit LOST

# CASE 2: revert (safe for pushed)
git revert HEAD              # app.js → "v1.0 code", local edit LOST
```
[web:5][web:14]

### Use Cases
- **reset**: Quick local cleanup before new commit
- **revert**: Undo pushed commit safely

### Interview Q&A
**Q1. Modified tracked file locally, run `git reset --hard HEAD~1`. What happens?**  
**A1.** Working directory resets to previous commit state; **all local modifications are permanently lost**.[web:14]

**Q2. Same scenario but `git revert HEAD`. Result?**  
**A2.** Creates new commit reverting last commit's changes; **local modifications overwritten** by revert patch.[web:5]

---

## Scenario 2: New File (Untracked)

### Definition & Behavior
**New untracked file** = created locally, never `git add` or committed.

**Both commands**:
- **File remains untouched** (untracked files ignored)
- Neither `reset` nor `revert` affects untracked files

### Example
```bash
# Create new untracked file
echo "new feature" > newfile.txt  # NEVER git add

git reset --hard HEAD~1    # newfile.txt still exists
git revert HEAD            # newfile.txt still exists
```
[web:14][web:33]

### Use Cases
- Safe: new experimental files survive both operations
- Clean with `git clean -f` afterward if needed

### Interview Q&A
**Q1. New untracked file exists. Does `git reset --hard` delete it?**  
**A1.** **No** - untracked files are never affected by reset/revert/checkout.[web:14]

**Q2. Safest way to discard new untracked files?**  
**A2.** `git clean -n` (preview) then `git clean -f` (delete).[web:41]

---

## Scenario 3: New File (Staged but Uncommitted)

### Definition & Behavior
**Staged new file** = `git add newfile.txt` but not yet committed.

**`git reset --hard HEAD~1`**:
- Removes from staging area
- **Deletes from working directory**

**`git revert HEAD`**:
- File was never committed, so **remains staged**
- No effect on uncommitted staged files

### Example
```bash
echo "new feature" > newfile.txt
git add newfile.txt        # staged but uncommitted

git reset --hard HEAD~1    # newfile.txt GONE from staging + working dir
git revert HEAD            # newfile.txt still staged (no change)
```
[web:33][web:35]

### Use Cases
- **reset**: Completely discard staged mistakes
- **revert**: Only affects committed history

### Interview Q&A
**Q1. New file staged (`git add`) but uncommitted. `git reset --hard` effect?**  
**A1.** **Removes from staging AND deletes from working directory**.[web:33]

**Q2. Same file with `git revert HEAD`?**  
**A2.** **No effect** - revert only touches committed history.[web:35]

---

## Complete Workflow Examples

### Example 1: Local Mistake (Use Reset)
```bash
# BAD: committed wrong code locally
echo "wrong code" > app.js
git add app.js; git commit -m "oops"

# FIX: reset locally
git reset --soft HEAD~1     # keep changes staged to fix
# OR
git reset --hard HEAD~1     # discard completely
```

### Example 2: Pushed Mistake (Use Revert)
```bash
# BAD: pushed broken code
git push origin main

# FIX: safe for team
git revert HEAD             # new commit undoes damage
git push origin main        # share fix
```

### Recovery: Lost Changes?
```bash
git reflog                   # see all HEAD movements
git reset --hard HEAD@{1}    # recover from reflog
```
[web:50]

---

## Summary Table: File Fate

| File Type | `git reset --hard` | `git revert HEAD` | Recovery Possible? |
|-----------|-------------------|-------------------|-------------------|
| Tracked + Modified | **Lost** | **Lost** | reflog (reset only) |
| New Untracked | **Remains** | **Remains** | N/A |
| New Staged | **Deleted** | **Remains** | reflog (reset only) |

---

## Interview Questions & Answers

**Q1. Team pushed bad commit to main. Modified file locally. Best fix?**  
**A1.** `git revert HEAD` then `git push` - safe, preserves history, overwrites local mods.[web:8]

**Q2. Local commit with secrets, not pushed yet?**  
**A2.** `git reset --hard HEAD~1` + regenerate secrets + `git clean -fd` for untracked files.[web:43]

**Q3. `git reset --hard` lost my changes. Recover?**  
**A3.** `git reflog` shows history → `git reset --hard HEAD@{N}` (N from reflog).[web:50]

**Q4. Why does `git revert` affect tracked files but not untracked?**  
**A4.** Revert applies patch to working directory (tracked files only); untracked files outside Git's scope.[web:5]

---
