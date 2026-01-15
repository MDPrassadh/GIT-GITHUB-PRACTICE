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

COMMANDS:

1 git stash list    listing all stash files

2 git stash save    it gives you like stash@{0} stash@{1} stash@{2}

3 git stash apply stash@{0}  unstash position now you can edite or something....

4 stash@{0} this is very recent stash ID

5 git stash drop stash@{0}   delete this stash immedialtely but best apporoach is unstash and drop that otherwise your changes will be missed

6 if you want to delete all stashes immeadiately in single syntax is 
 git stash clear 

7 If you use only single command for unstash and delete back to back in single way is command is
git stash pop stash@{0} :---apply and deletion in back to back

8 If you update one file in anywhere if you forgot what changes you made then its hard to get in manual but there is command is there..
git restore fn  prevuious file will be displayed

9 clear evry stash in single syntax is 
git stash clear :------------all stashes will be clear immediately.

summary:-----------
git stash list      # See stash@{0}, stash@{1}, etc.
git stash save      # save stash with id 
git stash pop       # Apply & delete top stash
git stash apply     # Apply without deleting
git stash drop      # Delete without applying
git stash clear     # Delete ALL stashes

Delete multiple remote tags------------

git push origin --delete ord-mgt-1.0.1 order-mgt-1.2.2

For specific branches Deletion----------

git push origin --delete feature/old1 feature/old2 feature/old3
