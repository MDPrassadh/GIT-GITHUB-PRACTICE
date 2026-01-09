============GIT MERGING========================
Git merge integrates changes from one branch into the current branch by combining commit histories, preserving both lineages. It supports DevOps workflows like GitFlow for feature integration or hotfixes. Use it after completing branches to unify code without overwriting history.[1][3]

## Command Usage
Run `git merge <branch-name>` from the target branch (e.g., `git checkout main; git merge feature-xyz`) to incorporate changes. Git auto-detects merge type and handles conflicts by marking files for manual resolution. Options include `--no-ff` for always creating a merge commit, `--abort` to cancel, or `-s ours` to ignore incoming changes.[2][4][5][1]

## Merge Types
- **Fast-forward**: Moves branch pointer when no divergent commits exist; linear history (e.g., `main` unchanged since `feature` branched).[3][1]
- **Three-way (recursive)**: Creates merge commit with two parents when branches diverge; compares common ancestor, source, target.[6][1]
- **Octopus**: Merges multiple branches at once (e.g., `git merge branch1 branch2`).[2]

| Type | Condition | Result |
|------|-----------|--------|
| Fast-forward | Linear path | No new commit[1] |
| Three-way | Diverged branches | Merge commit[3] |
| Octopus | Multiple branches | Single commit[2] |

## Examples
**Fast-forward**: From `main`, `git checkout main; git merge hotfix`—updates `main` to `hotfix` tip if unchanged.[4]
```
Before: A---B (main)
             \
              C---D (hotfix)
After:  A---B---C---D (main)
```
**Three-way with conflict**: `git merge feature` after both branches advance; edit conflicts, `git add .; git commit`.[1]
```
Before: A---B---E (main)
         \     \
          C---D (feature)
After:   A---B---E---M (main)
         \     /   /
          C---D---/

For Instance We have one main branch now there is bug in main branch code so main branch modification is not best approach then

go for new branch creation from main branch new branch is hotfix branch now all code copied to hotfix bracnh from main branch itself what have it

now in thoses code files all are tracked and added and committed and pushed to remote earlier so all are trcking files right if any changes happend

they are modified files only not new things so at that scenario some changes will be done and now ready to commit now like using command is

<---> git commit -am "code updated"        [ -am all messages ]  when you commit like this it will save in local repo..

this is the best approch if not done like that merge  will be happend. in this scenario git checkout to other branch and merge will work properly if not like that ...

AUTO/BLIND MERGE------------------

before git checkout you didn't commit and checkout to otehr branch automatically merge will be done through git checkout ..this is not recommended

this will prove not proper merge updataion in both branches and then check

<--> git diff command ----------------
git diff hotfix   ----------when you are in main branch

git diff main     ----------when you are in hotfix branch  notice changes to be required

hotfix branch changes made then go for PR pull request ..raise for desitination branch will like it and authorise that otherwise cancel

================Merging IMP points to be noted before merging=====================================

1 Code updatetion completed then certainly go for git commit -am "" before git checkout to required branch and then go  for merge this is the best approach

Merge Conflict:-------------------

more than two developers are code updataing in different changes and commit individually and checkout out destination branch merge will try to do reaming deveopers are commited after updation of code now main branch ready to do merge now rejected to merge due to conflict from rest of branches are mis matched code then it will called merge conflict and inform to both developers and will understand the scenario and right one will keep the code and remaing developer will edit the code then only merge conflict will sort out..
