# Reordering Commits

To reorder commits we use [Git interactive reabase](./07-Git%20Interactive%20Rebase.md), all we have to do is change the commits order in the rebase script.

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

Let's consider the commit `383a49c Add a reference to Google Map SDK v1.0.`. The problem with this commit is it's position in history. It should be before the `515c77d Render restaurants on the map.` as the dependency needs to be added first before using it.

```shell
~/BadHistory (master)
$ git rebase -i de1b321    #Start the interactive rebase
hint: Waiting for your editor to close the file...

```
Git will then prompt in default editor to select the operation for commit `515c77d` and the commits that come after it.
```shell
pick 515c77d Render restaurants on the map.
pick d5420b1 Fix a typo.
pick bfe589f Change the color of restaurant icons.
pick 383a49c Add a reference to Google Map SDK v1.0.
pick 648f08a Update terms of service and Google Map SDK version.
pick 9342dc0 Render cafes on map

# Rebase de1b321..9342dc0 onto de1b321 (6 commands)
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
we simply need to reorder the commit to its correct positon in the script.
```shell
pick 383a49c Add a reference to Google Map SDK v1.0.
pick 515c77d Render restaurants on the map.
pick d5420b1 Fix a typo.
pick bfe589f Change the color of restaurant icons.
pick 648f08a Update terms of service and Google Map SDK version.
pick 9342dc0 Render cafes on map

# Rebase de1b321..9342dc0 onto de1b321 (6 commands)
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
The reordering is complete
```shell
~/BadHistory (master)
$ git rebase -i de1b321    #Start the interactive rebase
Successfully rebased and updated refs/heads/master.

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