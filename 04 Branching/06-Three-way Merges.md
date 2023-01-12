# Three-way Merges

The 3-way-merge is implicit when the branches to be merged diverge. This happens when changes are made to the original branches after the creation of the new branch.

### Creating a new branch ***`3-way-merge`*** from ***`master`***

```shell
~/Git&GitHub (master)
$ git switch -C "3-way-merge"    #Create branch '3-way-merge' and switch to it
Switched to a new branch '3-way-merge'
```

At this moment of creation both branches are pointing to the same commit.

```shell
~/Git&GitHub (3-way-merge)
$ git log --oneline --graph --all    #Git log before the branches diverge (i.e: before committing to '3-way-merge' and 'master')
* 154fe29 (HEAD -> 3-way-merge, master) Three-way Merges Introduction
* 73a7141 Fast-forward Merges Complete
[...]
```
### Committing changes to ***`3-way-merge`*** branch

```shell
~/Git&GitHub (3-way-merge)
$ git commit -am "Three-way Merges Introduction Contd."    #Staging and committing changes.
[3-way-merge 18d71f2] Three-way Merges Introduction Contd.
 1 file changed, 22 insertions(+), 1 deletion(-)
```

After committing to the ***`3-way-merge`*** branch, it will move forward, but will have a linear path to ***`master`***. <br>
This can be verified using `git log`.

```shell
~/Git&GitHub (3-way-merge)
$ git log --oneline --graph --all    #Git log after committing to '3-way-merge'.
* 18d71f2 (HEAD -> 3-way-merge) Three-way Merges Introduction Contd.
* 154fe29 (master) Three-way Merges Introduction
* 73a7141 Fast-forward Merges Complete
[...]
```

### Switching back to ***`master`*** and making a commit

```shell
~/Git&GitHub (3-way-merge)
$ git switch master    #Switch to master
Switched to branch 'master'

~/Git&GitHub (master)
$ git commit -am "Add Summary to 'Fast-forward Merges.md'"    #Staging and committing changes.
[master f544e36] Add Summary to 'Fast-forward Merges.md'
 1 file changed, 7 insertions(+)

```

This linear path is broken after changes are committed to ***`master`*** as well. <br>
This can also be verified using `git log`.

```shell
~/Git&GitHub (master)
$ git log --oneline --graph --all
* f544e36 (HEAD -> master) Add Summary to 'Fast-forward Merges.md'
| * 18d71f2 (3-way-merge) Three-way Merges Introduction Contd.
|/
* 154fe29 Three-way Merges Introduction
* 73a7141 Fast-forward Merges Complete
[...]
```

### Merging ***`3-way-merge`*** branch into ***`master`*** branch
Now when we run a `git merge` Git will perform a 3-way-merge. It will open the default editor with a commit message, we can modify the commit message if needed.

```shell
~/Git&GitHub (master)
$ git merge 3-way-merge    #Merge '3-way-merge' branch into master
Merge made by the 'ort' strategy.
 04 Branching/06-Three-way Merges.md | 23 ++++++++++++++++++++++-
 1 file changed, 22 insertions(+), 1 deletion(-)
```

In the log we can see the merge commit. 

```shell
~/Git&GitHub (master)
$ git log --oneline --graph --all
*   6370191 (HEAD -> master) Merge branch '3-way-merge'
|\
| * 18d71f2 (3-way-merge) Three-way Merges Introduction Contd.
* | f544e36 Add Summary to 'Fast-forward Merges.md'
|/
* 154fe29 Three-way Merges Introduction
* 73a7141 Fast-forward Merges Complete
[...]
```

## Summary:

| Command                                                             | Description                                                              |
|---------------------------------------------------------------------|--------------------------------------------------------------------------|
| `git merge <branch-name>`                                           | To perform a 3-way merge. (in case branches have diverged)               | 