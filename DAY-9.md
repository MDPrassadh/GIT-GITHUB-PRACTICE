GIT FETCH & GIT PULL :-------------
1 Git fetch downloads commits and updates from a remote repository into local remote-tracking branches

2 (like origin/main) without altering your working directory or current branch. 

3 Git pull combines git fetch with git merge (or rebase), automatically integrating those remote changes into your current local branch.

| Command   | Action                            | Merges Changes? | Risk of Conflicts                     |
| --------- | --------------------------------- | --------------- | ------------------------------------- |
| git fetch | Updates remote-tracking refs only | No              | None during fetch                     |
| git pull  | Fetch + merge/rebase              | Yes             | Possible during merge about.gitlab+1​  |



![WhatsApp Image 2026-01-16 at 12 46 54](https://github.com/user-attachments/assets/45d8a2fa-83f1-4b2e-8150-32aca70082a8)

git fetch + merge = git pull --------------

If you need working area use git pull otherwise git fetch
when you use git fetch remote repo files into local repo only if you want to working area use merge coammand or 

directly code need to aorking area use git pull command 


    git fetch origin          # Safe preview: git log origin/main
    git merge origin/main     # Then merge manually
             # Or one-shot:
    git pull origin main      # Fetch + merge (may conflict like your ORT merge)

