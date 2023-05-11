# Rewording Commit Messages

To reword commits messages we  use the [Git interactive reabase](./07-Git%20Interactive%20Rebase.md), and in the rebase script choose the `reword` option.

For each commit we want to reword, Git will open the default editor and give us a chance to rewrite the commit message.

```shell
~/BadHistory (master)
$ git log --oneline
7ddb97b (HEAD -> master) Render cafes on map
c84706b Update terms of service and Google Map SDK version.
2a0c4c1 Add a reference to Google Map SDK.
15bf387 Change the color of restaurant icons.
fdf3781 Fix a typo.
7b90516 Render restaurants the map.
de1b321 Initial commit

```

Let's consider rewording the `7b90516 Render restaurants the map.` and `c84706b Update terms of service and Google Map SDK version.` commit

```shell
~/BadHistory (master)
$ git rebase -i de1b321    #Start the interactive rebase operation
hint: Waiting for your editor to close the file...
```
Git will then prompt in default editor to select the operation for commit `7b90516` and the commits that come after it.
```shell
pick 7b90516 Render restaurants the map.
pick fdf3781 Fix a typo.
pick 15bf387 Change the color of restaurant icons.
pick 2a0c4c1 Add a reference to Google Map SDK.
pick c84706b Update terms of service and Google Map SDK version.
pick 7ddb97b Render cafes on map

# Rebase de1b321..7ddb97b onto de1b321 (6 commands)
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
Out of these our desired commit for rewording are `7b90516` and `2a0c4c1` , so we will change their instruction from **pick** to **reword**.
```shell
reword 7b90516 Render restaurants the map.
pick fdf3781 Fix a typo.
pick 15bf387 Change the color of restaurant icons.
reword 2a0c4c1 Add a reference to Google Map SDK.
pick c84706b Update terms of service and Google Map SDK version.
pick 7ddb97b Render cafes on map

# Rebase de1b321..7ddb97b onto de1b321 (6 commands)
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
Upon closing the default editor window the rebase operation will start.

Since we instructed Git to **reword** two commits, the rebasing operation halted while applying these commit to allow us to edit the commit message in default editor.

```shell
~/BadHistory (master)
$ git log --oneline
9342dc0 (HEAD -> master) Render cafes on map
648f08a Update terms of service and Google Map SDK version.
383a49c Add a reference to Google Map SDK v1.0.
bfe589f Change the color of restaurant icons.
d5420b1 Fix a typo.
515c77d Render restaurants on the map.
de1b321 Initial commit

```