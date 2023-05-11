# Amending an earlier commit
To amend an earlier commit we use the [Git interactive reabase](./07-Git%20Interactive%20Rebase.md)

```shell
~/BadHistory (master)
$ git log --oneline
c3dddb1 (HEAD -> master) Render cafes on map
efb7762 Revert bad code
92ade19 WIP
357f15f Update terms of service and Google Map SDK version.
42f2f93 WIP
de106c9 Add a reference to Google Map SDK.
15bf387 Change the color of restaurant icons.
fdf3781 Fix a typo.
7b90516 Render restaurants the map.
de1b321 Initial commit

```

Consider the commit `de106c9 Add a reference to Google Map SDK.`
```shell
~/BadHistory (master)
$ git show de106c9    #View contents of specified commit
commit de106c992ef432968090b93d32e601b5f89deaa2
Author: Anshuman Yuvraj <uvrajanshuman@gmail.com>
Date:   Mon May 8 12:28:56 2023 +0530

    Add a reference to Google Map SDK.

diff --git a/package.txt b/package.txt
new file mode 100644
index 0000000..7324ece
--- /dev/null
+++ b/package.txt
@@ -0,0 +1 @@
+Google Map 1.0.0

```

Let's consider we forgot to add license for Google Map, so we need to go back in history and amend this commit.

To do so we will be using the interactive rebase. With rebasing we can replay a bunch of commit on top of another commit.
So, here we are going to replay this commit (`de106c9 Add a reference to Google Map SDK.`) and the commits that come after it on top of parent of this commit (i.e: `15bf387 Change the color of restaurant icons.`)
```shell
~/BadHistory (master)
$ git rebase -i 15bf387    #Interactive rebase
```
Git will then prompt in default editor to select the operation for commit `de106c9` and the commits that come after it. 
```shell
pick de106c9 Add a reference to Google Map SDK.
pick 42f2f93 WIP
pick 357f15f Update terms of service and Google Map SDK version.
pick 92ade19 WIP
pick efb7762 Revert bad code
pick c3dddb1 Render cafes on map

# Rebase 15bf387..c3dddb1 onto 15bf387 (6 commands)
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
Out of these first one is our desired commit for amending, so we will change the first instruction from **pick** to **edit**.
```shell
edit de106c9 Add a reference to Google Map SDK.
pick 42f2f93 WIP
pick 357f15f Update terms of service and Google Map SDK version.
pick 92ade19 WIP
pick efb7762 Revert bad code
pick c3dddb1 Render cafes on map

# Rebase 15bf387..c3dddb1 onto 15bf387 (6 commands)
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

Since we instructed Git to **edit** this commit, the rebasing operation stopped at this point/commit to allow us to edit it.
```shell
~/BadHistory (master)
$ git rebase -i 15bf387    #Interactive rebase
Stopped at de106c9...  Add a reference to Google Map SDK.
You can amend the commit now, with

  git commit --amend

Once you are satisfied with your changes, run

  git rebase --continue

```
we will do the required change, amend the current commit (at which the rebase operation has halted for edit) and then continue with the rebase operation.
```shell
~/BadHistory (master|REBASE 1/6)
$ echo "Google license" > license.txt

~/BadHistory (master|REBASE 1/6)
$ git add .
warning: LF will be replaced by CRLF in license.txt.
The file will have its original line endings in your working directory

~/BadHistory (master|REBASE 1/6)
$ git commit --amend --no-edit
[detached HEAD 2a0c4c1] Add a reference to Google Map SDK.
 Date: Mon May 8 12:28:56 2023 +0530
 2 files changed, 2 insertions(+)
 create mode 100644 license.txt
 create mode 100644 package.txt

```
Once we continue the rebase operation all the subsequent commit will be replayed on top this amended commit (a new commit will be created replicating each one of these and the previous ones will be discarded).

```shell
~/BadHistory (master|REBASE 1/6)
$ git rebase --continue    #Continue with the rebase operation
Successfully rebased and updated refs/heads/master.
```

```shell
~/BadHistory (master)
$ git log --oneline
d9b57c5 (HEAD -> master) Render cafes on map
58074cf Revert bad code
02ae978 WIP
6ec7c1b Update terms of service and Google Map SDK version.
08b1815 WIP
2a0c4c1 Add a reference to Google Map SDK.
15bf387 Change the color of restaurant icons.
fdf3781 Fix a typo.
7b90516 Render restaurants the map.
de1b321 Initial commit
```
we can verify that the commit id of the affected commits changed.

**Interesting Fact**:<br>
Even though we added license.txt in `2a0c4c1 Add a reference to Google Map SDK.`, it will be present in all the commits that comes after it (although it was not present in their previous versions).<br>
So, the change we introduce in one of teh earlier commits carries on through out the rest of history.


**Instead of continuing with the rebase (`git rebase --continue`) after making the changes, the rebase operation can also be aborted using `git rebase --abort`.**


## Git bash Screenshots
[Git bash Screenshot : 1](./images/Screenshot19.png)

[Default Editor Screenshot : 2](./images/Screenshot20.png)

[Default Editor Screenshot : 3](./images/Screenshot21.png)

[Git bash Screenshot : 4](./images/Screenshot22.jpg)