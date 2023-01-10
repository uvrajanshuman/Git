# Stashing

When we switch branches Git restores our **Working Directory** to the last snapshot of the target branch. In case we have local changes (staged/unstaged) in the **Working Directory** that have not yet been committed, they could be lost. <br>
Git does not allows to switch branches in such case.

```shell
~/Git&GitHub (bugfix)
$ git switch master    #Switch to master branch
error: Your local changes to the following files would be overwritten by checkout:
        04 Branching/02-Comparing Branches.md
Please commit your changes or stash them before you switch branches.
Aborting

```

Let's imagine these changes are still work in progress, and we do not want to commit them yet. 

In this situation we should stash our changes. Stashing changes means saving them in a Git safe place, but they will be not part of the history.

## Creating a stash
`git stash push -m <stashing-message>` : To stash the local changes.

```shell
~/Git&GitHub (bugfix)
$ git stash push -m "02-Comparing Branches.md changes"    #Stashing changes
Saved working directory and index state On bugfix: 02-Comparing Branches.md changes
```

- This command will stash (save) our changes, but these changes will be removed from the **Working Directory**, to allow switching to other branches. <br>
At this point we can switch branches and the changes will be safe.

```shell
~/Git&GitHub (bugfix)
$ git switch master    #Switch to 'master' branch
Switched to branch 'master'
A       04 Branching/03-Stashing.md

~/Git&GitHub (master)
$ git switch bugfix    #Switch back to 'bugfix' branch
Switched to branch 'bugfix'
A       04 Branching/03-Stashing.md
```

## Stashing untracked files

`git stash push  -a -m <stashing-message>` or `git stash push  -am <stashing-message>` : To stash the untracked file changes as well.

If we have new untracked files, by default, they are not included in the stash, to include them we have to use the `--all` or `-a` option.

```shell
~/Git&GitHub (bugfix)
$ git status -s    #Short Git Status
?? "04 Branching/03-Stashing.md"

~/Git&GitHub (bugfix)
$ git stash push -a -m "03-Stashing.md changes"    #Stashing the untracked file changes.
warning: LF will be replaced by CRLF in bin/app.bin.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in logs/dev.log.
The file will have its original line endings in your working directory
Saved working directory and index state On bugfix: 03-Stashing.md changes
```

## List stashes

`git stash list` : To list all the stashes.

Each stash as a unique identifier, `stash@{indexNo}`.

```shell
~/Git&GitHub (bugfix)
$ git stash list
stash@{0}: On bugfix: 03-Stashing.md changes
stash@{1}: On bugfix: 02-Comparing Branches.md changes
```

## Show stash changes
`git stash show stash@{i}` or `git stash show i` : To view the stashed changes.

Before applying the changes to the **Working Directory** we can view them with the command `git stash show stash@{i}`, where `i` is the stash index.

```shell
~/Git&GitHub (bugfix)
$ git stash show 1
 04 Branching/02-Comparing Branches.md | 7 +++++++
 1 file changed, 7 insertions(+)
```

## Apply stash changes to Working Direcotry

`git stash apply i` : To apply the stashed changes to working directory

**List all stashes:**
```shell
~/Git&GitHub (bugfix)
$ git stash list
stash@{0}: On bugfix: 03-Stashing.md changes
stash@{1}: On bugfix: 02-Comparing Branches.md changes
```
**Apply stash with index 0:**
```zsh
~/Git&GitHub (bugfix)
$ git stash apply 0
Already up to date.
On branch bugfix
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        04 Branching/03-Stashing.md

nothing added to commit but untracked files present (use "git add" to track)
```
**Apply stash with index 1:**
```shell
~/Git&GitHub (bugfix)
$ git stash apply 1
On branch bugfix
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   04 Branching/02-Comparing Branches.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        04 Branching/03-Stashing.md

no changes added to commit (use "git add" and/or "git commit -a")
```
## Delete a stash

`git stash drop i`: To drop/delete a stash with index i.

After applying the stash we can delete it running. Or, we may not need to apply the changes from the stash, so we can delete it without applying.

**List all stashes:**

```shell
~/Git&GitHub (bugfix)
$ git stash list
stash@{0}: On bugfix: 03-Stashing.md changes
stash@{1}: On bugfix: 02-Comparing Branches.md changes
```
**Dropping a stash:**

```shell
~/Git&GitHub (bugfix)
$ git stash drop 0
Dropped refs/stash@{0} (7f276e69fd39a6ca373641fd3b74db41989c11c5)
```

Alternately we can delete all stash using `git stash clear`.

```shell
~/Git&GitHub (bugfix)
$ git stash clear
```

## Summary:

| Command                                                                                | Description                                       |
|----------------------------------------------------------------------------------------|---------------------------------------------------|
| `git stash push -m <stashing-message>`                                                 | To stash the local changes.                       |
| `git stash push  -a -m <stashing-message>`<br>`git stash push  -am <stashing-message>` | To stash the untracked file changes as well.      |
| `git stash list`                                                                       | To list all the stashes.                          |
| `git stash show stash@{i}` <br> `git stash show i`                                     | To view the stashed changes.                      |
| `git stash apply i`                                                                    | To apply the stashed changes to working directory | 
| `git stash drop i`                                                                     | To drop/delete a stash with index i.              | 
| `git stash clear`                                                                      | To drop/delete all stash                          |