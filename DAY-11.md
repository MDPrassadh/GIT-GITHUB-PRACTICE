PR ----------------------

A Git pull request (PR) proposes merging changes from one branch (e.g., your bugfix) into another (e.g., main) on platforms like GitHub,

enabling code review before integration. Unlike git pull (fetch+merge), PRs facilitate collaboration through discussion, approvals, and CI checks.

GitHub Workflow

From your /d/GIT-PRACTICE setup with prassadh remote:


git checkout -b feature-login       # Make changes, commit: git commit -m "Add login form"

git push prassadh feature-login

Go to GitHub > MDPrassadh/GIT-GITHUB-PRACTICE > "Compare & pull request" > Select main as base.

PR Stages

Draft: Mark as "Draft" for WIP feedback.

Review: Teammates comment, suggest changes, approve.

Merge: Use ORT (default), squash, or rebase options.

Delete branch: Auto-cleanup after merge.
​

Best Practice

Small, focused PRs (1-3 commits) with clear titles/descriptions. Link issues: "Fixes #5". Require 1-2 approvals in team settings. 

Perfect for your cherry-pick/ORT merge practice before production pushes.

<img width="564" height="1600" alt="image" src="https://github.com/user-attachments/assets/9d1f789c-8092-44be-a680-edf3285eef53" />  
after got from approval higher officails proceed to merge pull request and confirm merge---

now main branch also refelected...

this process is not only for prarent branch every branches will do like this industry best approach.

README.md ---------------------------------

Readme file is all about total summary of the repo or project each and every step inckudes and expalantion in briefly this is cretaed while creation of repo select readme.md file 

option also and create repo in remote

total end of GITHUB




