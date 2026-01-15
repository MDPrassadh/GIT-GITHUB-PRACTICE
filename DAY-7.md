GIT STASH meaning and definition:--------------

git stash temporarily saves your uncommitted changes (working directory + staging area) into a stack and reverts your working tree to match the last commit.
​

Definition

Git stash creates a local snapshot of your modified files without committing them, giving you a clean working directory to switch branches or pull changes.

Stashes live in .git/refs/stash and are private to your local repo

Key use cases:------------------------

Emergency branch switch: Working on feature-X but need to fix a bug on main immediately


git stash    # Save feature-X work

git checkout main

# Fix bug, commit, push

git checkout feature-X

git stash pop  # Resume work
![WhatsApp Image 2026-01-16 at 00 09 33](https://github.com/user-attachments/assets/5923a6d1-970e-44c3-9f23-2f8e04938302)

