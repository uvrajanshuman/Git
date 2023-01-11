# Fast-forward Merges

Renaming the **bugfix** branch to **fast-forward-merge**.
```shell
~/Git&GitHub (bugfix)
$ git branch -m bugfix fast-forward-merge    #Rename 'bugfix' branch to 'fast-forward-merge'
```

## Git log for branches `--graph`

To have a better visualizations of branches with `git log`, it is better to include the `--graph` option. 

It will produce an output where we are abe to better view the branch path.

```shell
~/Git&GitHub (fast-forward-merge)
$ git log --oneline --graph --all
* 536d022 (HEAD -> fast-forward-merge) Merging Introduction
* bfba2b9 Stashing Complete
* 096c972 Comparing Branches Complete
* 17501ba working with branches Complete
* e3e348f Working with branches
* 537ee9d (master) Branching Introduction
* 907f0e1 (tag: M-03) Module 03 - Browsing History
* d028a00 Finding the Author of Line using Blame Complete
[...]
```

From this we can verify that the branch ***`fast-forward-merge`*** is few commits ahead of ***`master`***, and there is a linear path between them. So they could be merged using the fast-forward method.

## Merge branch fast-forward

`git merge <branch-name>` : To fast-forward merge a branch.

To merge the ***`fast-forward-merge`*** branch into ***`mastr`***, we first should have committed all of our work in that branch and then we switch to ***`master`***(branch in which the merge will happen). 

```shell
~/Git&GitHub (fast-forward-merge)
$ git switch master
Switched to branch 'master'
```

In the ***`master`*** branch we perform the merge operation:

```shell
~/Git&GitHub (master)
$ git merge fast-forward-merge
Updating 537ee9d..536d022
Fast-forward
 04 Branching/02-Comparing Branches.md |  47 ++++++++++
 04 Branching/03-Stashing.md           | 167 ++++++++++++++++++++++++++++++++++
 04 Branching/04-Merging.md            |  43 +++++++++
 04 Branching/Branching.md             | 146 +++++++++++++++++++++++++++++
 04 Branching/images/Screenshot3.png   | Bin 0 -> 87385 bytes
[...]
```

After the merge operation both **master** and **fast-forward-merge** branch will be pointing to the same commit, which can be verified using `git log`.

```shell
~/Git&GitHub (master)
$ git log --oneline --graph
* 536d022 (HEAD -> master, fast-forward-merge) Merging Introduction
* bfba2b9 Stashing Complete
* 096c972 Comparing Branches Complete
* 17501ba working with branches Complete
* e3e348f Working with branches
* 537ee9d Branching Introduction
* 907f0e1 (tag: M-03) Module 03 - Browsing History
* d028a00 Finding the Author of Line using Blame Complete
[...]
```
