# Three-way Merges

The 3-way-merge is implicit when the branches to merge diverge. This happens when changes are made to the original branches after the creation of the new branch.

Creating a new branch ***`3-way-merge`*** from ***`master`***
```shell
~/Git&GitHub (master)
$ git switch -C "3-way-merge"    #Create branch '3-way-merge' and switch to it
Switched to a new branch '3-way-merge'
```

At this moment of creation both branches are pointing to the same commit.

```zsh
~/Git&GitHub (3-way-merge)
$ git log --oneline --graph --all
* 154fe29 (HEAD -> 3-way-merge, master) Three-way Merges Introduction
* 73a7141 Fast-forward Merges Complete
*   edafa2e Merge branch 'no-fast-forward-merge'
[...]
```
When we commit to ***`3-way-merge`***, this branch will move forward, but will have a linear path to ***`main`***. 

This linear path is broken when changes are committed to ***`master`*** as well.