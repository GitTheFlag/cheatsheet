# 🚩 Git The Flag — Command Cheatsheet

> Every git command taught across all cases, in one place.
> Use this as a reference while playing or after completing the cases.

---

## Case 01 — Welcome to the Team

### See all branches
```bash
git branch -a
# lists all local and remote branches, including remote ones
```

### Switch to a branch
```bash
git checkout <branch-name>
# switches your working directory to that branch
```

### Read commit history
```bash
git log --oneline
# compact view of all commits on the current branch — hash + message
```

### Compare branches
```bash
git diff main..<branch-name>
# shows everything that exists on <branch-name> but not on main
```

---

## Case 02 — The Vanishing Feature

### Read history of a specific branch
```bash
git log --oneline <branch-name>
# shows commits on that branch — read every message carefully
```

### Inspect a commit
```bash
git show <hash>
# shows the full commit: message, author, date, and all file changes
```

### Find deleted files
```bash
git log --diff-filter=D --name-only <branch-name>
# lists commits where files were deleted, and which files were removed
git show <hash>
# shows the full diff of that commit — deleted file contents appear as removed lines
```

### Read annotated tags
```bash
git tag -l
# lists all tags in the repo
git show <tagname>
# shows the tag message, tagger, date, and the commit it points to
```

### Find hidden refs
```bash
git ls-remote origin
# lists every ref on the remote — branches, tags, and anything non-standard
git fetch origin <ref>
# fetch a specific ref by its full path, e.g. refs/blobs/flag4
git cat-file -p FETCH_HEAD
# read the raw content of whatever was just fetched
```

---

## Case 03 — The Rewritten Past

### Save and restore work in progress
```bash
git stash list                          # list all stashes
git stash show -p                       # show what is inside the latest stash
git stash apply                         # restore stash to working directory
git fetch origin refs/stash:refs/stash  # fetch a stash pushed to a remote
```

### Rebase — rewrite history
```bash
git rebase main                    # replay current branch commits on top of main
git log --oneline --graph --all    # visualize all branches and their history
```

### Cherry-pick — copy a commit
```bash
git cherry-pick <hash>        # apply that commit to the current branch
git diff main..<branch>       # compare branches to spot what changed
```

### Reflog — recover lost commits
```bash
git reflog                    # all local HEAD movements — nothing is hidden
git reflog show <branch>      # history of a specific branch pointer
git show <hash>               # read a commit recovered from reflog
```

---

## Case 04 — The Inside Job

### Find the bad commit — git bisect
```bash
git bisect start
git bisect bad                  # current commit is broken
git bisect good <hash-or-tag>   # this old commit was working
# test the checked-out commit, then:
git bisect good                 # test passes
git bisect bad                  # test fails
# repeat — git narrows it down in O(log n) steps
git bisect reset                # return to HEAD when done
```

### Trace a line to its author — git blame
```bash
git blame <file>              # shows commit hash · author · date for every line
git blame -L 10,20 <file>    # blame only lines 10–20
git show <hash>               # read the full commit that owns a line
```

### Understand merge conflicts
```bash
git merge <branch>            # triggers conflict when both branches changed the same line
# conflict markers in the file:
# <<<<<<< HEAD        ← your version
# =======
# >>>>>>> branch      ← their version
git merge --abort             # cancel the merge and go back
```

### Git notes — read commit annotations
```bash
git fetch origin refs/notes/commits:refs/notes/commits   # fetch remote notes
git log --notes --oneline     # show commits with attached notes
git notes show <hash>         # read the note on a specific commit
git notes add -m "..." <hash> # attach a note to a commit
```

---

## Universal commands (used everywhere)

```bash
git clone <url>          # download a repo to your machine
git status               # show what's changed in your working directory
git checkout <branch>    # switch to a branch
git checkout -b <name>   # create and switch to a new branch
git add <file>           # stage a file for commit
git commit -m "message"  # save staged changes as a commit
git push origin <branch> # upload a branch to GitHub
git pull                 # download latest changes from GitHub
git merge <branch>       # merge a branch into the current one
```

---

## How flags work

Flags look like: `GTF{something_here}`

When you find one:
1. Go to the case repo on GitHub
2. Open a new **Issue**
3. Use the flag as the **title**
4. Submit — a bot validates it instantly

---

*Part of [Git The Flag](https://github.com/GitTheFlag) — Investigate the repo. Find the truth.*
