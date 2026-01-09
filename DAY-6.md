------------ADVANCED COMMANDS-------------------


If you have branches in your local repo those repos are pushed to remote repo
how will you do that syntax

<--> git push main
              hotfix
              bugfix  or

     git push origin main
                     hotfix
                     bugfix    or
     git push origin --all

   `git push origin --all` pushes **all your local branches** to the remote repository named `origin` (typically GitHub).

## Usage
Use when syncing multiple local branches (features, hotfixes, experiments) to remote after local development. Common in GitFlow after creating branches locally.[1][9]

**Syntax**: `git push origin --all`

## When to Use
- After `git clone`, local-only branches created (`feature-x`, `hotfix-y`)
- Backup all branches to GitHub before cleanup
- Team onboarding: share all WIP branches
- **Not** for production: avoid pushing unfinished/unreviewed branches to `main`/`develop`

## Example
```
Local branches: main, feature-login, hotfix-bug123, experiment-ui
$ git push origin --all
  Enumerating objects: ..., done.
  ... (pushes all 4 branches to origin)
```

**Result**: All local branches appear on GitHub under `origin/`

## Interview Q&A
**Q: What's the difference between `git push` and `git push origin --all`?**  
A: `git push` pushes only current branch's upstream. `--all` pushes every local branch regardless of upstream config.[1]

**Caution**: Creates remote-tracking branches for unfinished work – use PRs for collaboration, not direct pushes to shared branches.[9]

Use **`git push origin --all`** when you have **multiple remotes** configured or want **explicit control** over which remote receives all branches.

## Key Differences

| Command | Pushes to | When to Use |
|---------|-----------|-------------|
| `git push --all` | **Default remote** (usually `origin`) | **Single remote** setup [conversation_history] |
| `git push origin --all` | **Specific remote** `origin` | **Multiple remotes** or **explicit targeting** |

## Use `git push origin --all` When:
- **Multiple remotes exist**: `upstream`, `origin`, `backup`
- **Remote renamed**: Default ≠ `origin`
- **Script/automation**: Explicit remote name prevents errors
- **Team confusion**: Clarifies exact target

## Use `git push --all` When:
```
$ git remote -v
origin  https://github.com/user/repo (fetch)
origin  https://github.com/user/repo (push)
```
**Only one remote** → both commands identical.

## Example Scenario 
```
$ git remote -v
origin    https://github.com/team/project (main remote)
upstream  https://github.com/org/project (fork parent)
```
**✅ `git push origin --all`** → pushes to your fork  
**❌ `git push --all`** → pushes to `upstream` (might lack permissions)

## DevOps Best Practice
Always prefer **explicit** `git push origin --all` in CI/CD pipelines and shared repos for predictable behavior.[conversation_history]

Local repo branches listing-------
 git branch
 git branch -r [remote branches listing]
 git branch -a [Both Local and Remote branches listing]


 If you dont know the repo name are mapping repo ------

 git remote -v [ then you will git here ]


 LOCAL BRANCHES DELETION------------

 git branch -d hotfix [ delete in local branch]
 git push origin :bugfix [ deletion branches in remote through cli and also UI also possible got for branches clicke branches select in active branches what you want and delete figure if you get restore it is possible only before refesh of the paga itself once refresh not available restore until and unless back up available ]
