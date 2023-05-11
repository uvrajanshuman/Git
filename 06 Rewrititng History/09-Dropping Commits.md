# Dropping Commits

To drop commits we use the [Git interactive reabase](./07-Git%20Interactive%20Rebase.md).


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

Let's say we want to drop the `08b1815 WIP` commit. But first lets look at it's content
```shell
~/BadHistory (master)
$ git show 08b1815    #View content of specified commit
commit 08b18150c9339db4b09574fe42e1b004b0c1295f
Author: Anshuman Yuvraj <uvrajanshuman@gmail.com>
Date:   Mon May 8 12:31:45 2023 +0530

    WIP

diff --git a/terms.txt b/terms.txt
new file mode 100644
index 0000000..f3d4377
--- /dev/null
+++ b/terms.txt
@@ -0,0 +1 @@
+draft

```
In this commit we added a file **terms.txt**. Now, lets view the next commit `6ec7c1b Update terms of service and Google Map SDK version.`

```shell
~/BadHistory (master)
$ git show 6ec7c1b    #View content of specified commit
commit 6ec7c1bde44038cd320a84d940ba38edb73c6877
Author: Anshuman Yuvraj <uvrajanshuman@gmail.com>
Date:   Mon May 8 12:37:34 2023 +0530

    Update terms of service and Google Map SDK version.

diff --git a/package.txt b/package.txt
index 7324ece..5111c93 100644
--- a/package.txt
+++ b/package.txt
@@ -1 +1 @@
-Google Map 1.0.0
+Google Map 2.0.0
diff --git a/terms.txt b/terms.txt
index f3d4377..6ab9fed 100644
--- a/terms.txt
+++ b/terms.txt
@@ -1 +1 @@
-draft
+completed

```
In this commit we have two changes one in package.txt and another in **terms.txt**.

So what will happen if we drop the commit `08b1815 WIP`.<br>
we will end up with a conflict. Dropping this commit will mean the file **terms.txt** was never introduced/added.<br>
In contrast the next commit `6ec7c1b Update terms of service and Google Map SDK version.` has updated the **terms.txt** file. This results in an ambiguity that would need a manual interventaion to resolve the conflict.

Start the ineractive rebase
```shell
~/BadHistory (master)
$ git rebase -i 08b1815~1    #Start the interactive rebase operation
hint: Waiting for your editor to close the file...
```
Git will then prompt in default editor to select the operation for commit `08b1815 WIP` and the commits that come after it. 
```shell
pick 08b1815 WIP
pick 6ec7c1b Update terms of service and Google Map SDK version.
pick 02ae978 WIP
pick 58074cf Revert bad code
pick d9b57c5 Render cafes on map

# Rebase 2a0c4c1..d9b57c5 onto 2a0c4c1 (5 commands)
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
Out of these first one is our desired commit for amending, so we will change the first instruction from **pick** to **drop**, or simply remove the entire first line.
```shell
drop 08b1815 WIP
pick 6ec7c1b Update terms of service and Google Map SDK version.
pick 02ae978 WIP
pick 58074cf Revert bad code
pick d9b57c5 Render cafes on map

# Rebase 2a0c4c1..d9b57c5 onto 2a0c4c1 (5 commands)
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
Upon closing the default editor window the rebase operation will start.<br>
we get merge conflict.
```shell
~/BadHistory (master)
$ git rebase -i 08b1815~1    #Start the rebase operation
CONFLICT (modify/delete): terms.txt deleted in HEAD and modified in 6ec7c1b (Update terms of service and Google Map SDK version.).  Version 6ec7c1b (Update terms of service and Google Map SDK version.) of terms.txt left in tree.
error: could not apply 6ec7c1b... Update terms of service and Google Map SDK version.
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply 6ec7c1b... Update terms of service and Google Map SDK version.

~/BadHistory (master|REBASE 2/5)
$ git status -s    #Short Git status
M  package.txt
DU terms.txt

```
The git status shows the conflict. On one hand we are deleting the file while on another trying to update it

```shell
~/BadHistory (master|REBASE 2/5)
$ git log --oneline --graph --all
* d9b57c5 (master) Render cafes on map
* 58074cf Revert bad code
* 02ae978 WIP
* 6ec7c1b Update terms of service and Google Map SDK version.
* 08b1815 WIP
* 2a0c4c1 (HEAD) Add a reference to Google Map SDK.
* 15bf387 Change the color of restaurant icons.
* fdf3781 Fix a typo.
* 7b90516 Render restaurants the map.
* de1b321 Initial commit

```
**HEAD** in detached mode asmwe told git to undo the commit `WIP`. So, it trying to undo the its changes (addition of new file terms.txt). 
The changes we have in staging area are going to go when replaying the future commits.

To resolve the conflict manually 
```shell
~/BadHistory (master|REBASE 2/5)
$ git mergetool    #Resolving the conflict manually

This message is displayed because 'merge.tool' is not configured.
See 'git mergetool --tool-help' or 'git help config' for more details.
'git mergetool' will now attempt to use one of the following tools:
opendiff kdiff3 tkdiff xxdiff meld tortoisemerge gvimdiff diffuse diffmerge ecmerge p4merge araxis bc codecompare smerge emerge vimdiff nvimdiff
Merging:
terms.txt

Deleted merge conflict for 'terms.txt':
  {local}: deleted
  {remote}: modified file
Use (m)odified or (d)eleted file, or (a)bort? m

```
we have two type of changes deletion and modification. Since, we want to keep the file **terms.txt** we will go ahead with modification `m`.

```shell
~/BadHistory (master|REBASE 2/5)
$ git status -s    #Short Git status
M  package.txt
A  terms.txt
?? terms.txt.orig
```
we have two changes in the staging and they will go with the next commit.

```shell
git rebase --continue
```
Git will open default editor with a default commit message. we will accept the default one.
<br><br>

As another example we are going to remove two commits `a107f64 Revert bad code` and `051dbdd WIP`.
```shell
~/BadHistory (master)
$ git log --oneline
e14dc4b (HEAD -> master) Render cafes on map
a107f64 Revert bad code
051dbdd WIP
c84706b Update terms of service and Google Map SDK version.
2a0c4c1 Add a reference to Google Map SDK.
15bf387 Change the color of restaurant icons.
fdf3781 Fix a typo.
7b90516 Render restaurants the map.
de1b321 Initial commit
```

```shell
git rebase -i HEAD~3
```

```shell
drop 051dbdd WIP
drop a107f64 Revert bad code
pick e14dc4b Render cafes on map

# Rebase c84706b..e14dc4b onto c84706b (3 commands)
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
```

In this case we didn't had conflicts
```shell
~/BadHistory (master)
$ git rebase -i HEAD~3    #Start the interactive rebase
Successfully rebased and updated refs/heads/master.

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