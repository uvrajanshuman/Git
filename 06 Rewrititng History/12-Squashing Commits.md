# Squashing Commits

## Squash rebase

To squash commits together we use the [Git interactive reabase](./07-Git%20Interactive%20Rebase.md).<br> In the rebase script we select the `squash` option only for the child commits, the parent commit keeps the `pick` option. A commit can only be squashed into its parent commit. All commits that need to be squashed have to be in sequence, so if needed we can reorder them first.


```shell
~/BadHistory (master)
$ git log --oneline
a731545 (HEAD -> master) Render cafes on map
d428719 Update terms of service and Google Map SDK version.
e233339 Change the color of restaurant icons.
db97ae8 Fix a typo.
1d2cd98 Render restaurants on the map.
95532e9 Add a reference to Google Map SDK v1.0.
de1b321 Initial commit
```

Let's consider squashing `e233339 Change the color of restaurant icons.`,
`db97ae8 Fix a typo.` and `1d2cd98 Render restaurants on the map.` into a single commit.

All these changes are logically part of same unit of work, so, should be encapsulated into a single snapshot.

```shell
~/BadHistory (master)
$ git rebase -i 95532e9    #Start the interactive rebase operation
hint: Waiting for your editor to close the file...
```
Git will then prompt in default editor to select the operation for commit `1d2cd98` and the commits that come after it.
```shell
pick 1d2cd98 Render restaurants on the map.
pick db97ae8 Fix a typo.
pick e233339 Change the color of restaurant icons.
pick d428719 Update terms of service and Google Map SDK version.
pick a731545 Render cafes on map

# Rebase 95532e9..a731545 onto 95532e9 (5 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified); use -c <commit> to reword the commit message
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#

```
In this script we have all the affected commits listed from the oldest to the newest. <br>

change the command for `db97ae8 Fix a typo.` from **pick** to **squash**. Now, it will be combined with its parent commit.<br>
Similarly, change the command for `e233339 Change the color of restaurant icons.` from **pick** to **squash**. This will get combined with its parent commit which the combination of `1d2cd98` and `db97ae8` commits.

For commits which are not directly next to each other, we can reorder them first then squash
```shell
pick 1d2cd98 Render restaurants on the map.
squash db97ae8 Fix a typo.
squash e233339 Change the color of restaurant icons.
pick d428719 Update terms of service and Google Map SDK version.
pick a731545 Render cafes on map

# Rebase 95532e9..a731545 onto 95532e9 (5 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified); use -c <commit> to reword the commit message
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#

```

Git suggest commit message which is the combination of all the three squashed commit we can discard and provide our custom message as well.
```shell
# This is a combination of 3 commits.
# This is the 1st commit message:

Render restaurants on the map.

# This is the commit message #2:

Fix a typo.

# This is the commit message #3:

Change the color of restaurant icons.

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Mon May 8 11:57:49 2023 +0530
#
# interactive rebase in progress; onto 95532e9
# Last commands done (3 commands done):
#    squash db97ae8 Fix a typo.
#    squash e233339 Change the color of restaurant icons.
# Next commands to do (2 remaining commands):
#    pick d428719 Update terms of service and Google Map SDK version.
#    pick a731545 Render cafes on map
# You are currently rebasing branch 'master' on '95532e9'.
#
# Changes to be committed:
#	new file:   map.txt
#
# Untracked files:
#	terms.txt.orig
#

```
we will edit this and provide only **Render restaurants on the map.** as the commit message.

Squashing complete
```shell
~/BadHistory (master)
$ git rebase -i 95532e9    #Start the interactive rebase operation
[detached HEAD 5663806] Render restaurants on the map.
 Date: Mon May 8 11:57:49 2023 +0530
 1 file changed, 1 insertion(+)
 create mode 100644 map.txt
Successfully rebased and updated refs/heads/master.

~/BadHistory (master)
$ git log --oneline
ab649be (HEAD -> master) Render cafes on map
358ed7a Update terms of service and Google Map SDK version.
5663806 Render restaurants on the map.
95532e9 Add a reference to Google Map SDK v1.0.
de1b321 Initial commit

```

## Fixup rebase

The `fixup` rebase option works like `squash` option, but instead of allowing us to edit the commit message, it will use the message form the parent squashed commit.