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

