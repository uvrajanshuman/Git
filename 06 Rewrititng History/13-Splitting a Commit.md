# Splitting a Commit

To split a commit we use the [Git interactive reabase](./07-Git%20Interactive%20Rebase.md).<br> We pass to the rebase operation the parent of the commit we need to split. In the script we select the `edit` option for the commit we need to split.

Then in the `rebase` operation we unstage the changes of the commit with `git reset --mixed HEAD^`. Now the changes applied in this commit are in our **Working Directory**.

With the unstaged changes we slipt the commit to our needs with normal `git add <file>` and `git commit -m <message>`. This will create new commits. Then continue the `rebase` operation to finish `git rebase --continue`.

```shell
~/BadHistory (master)
$ git log --oneline
ab649be (HEAD -> master) Render cafes on map
358ed7a Update terms of service and Google Map SDK version.
5663806 Render restaurants on the map.
95532e9 Add a reference to Google Map SDK v1.0.
de1b321 Initial commit
```
`Update terms of service and Google Map SDK version.` needs to be split into two differnt commits.

```shell
~/BadHistory (master)
$ git rebase -i 5663806    #Start the rebase operation
hint: Waiting for your editor to close the file...
```
Git will then prompt in default editor to select the operation for commit `358ed7a` and the commits that come after it.
```shell
pick 358ed7a Update terms of service and Google Map SDK version.
pick ab649be Render cafes on map

# Rebase 5663806..ab649be onto 5663806 (2 commands)
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
edit 358ed7a Update terms of service and Google Map SDK version.
pick ab649be Render cafes on map

# Rebase 5663806..ab649be onto 5663806 (2 commands)
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
$ git rebase -i 5663806    #Start the rebase operation
Stopped at 358ed7a...  Update terms of service and Google Map SDK version.
You can amend the commit now, with

  git commit --amend

Once you are satisfied with your changes, run

  git rebase --continue

~/BadHistory (master|REBASE 1/2)
$ git log --oneline
358ed7a (HEAD) Update terms of service and Google Map SDK version.
5663806 Render restaurants on the map.
95532e9 Add a reference to Google Map SDK v1.0.
de1b321 Initial commit

```
we can use the **reset** command with **mixed** option to go back to state before we made this commit. i.e: parent of this commit.

With this we go one step back before we made this commit but our changes will be there in the wording area.
we can stage and commit them individually
```shell
~/BadHistory (master|REBASE 1/2)
$ git reset --mixed HEAD~1    #Reseting the head to its parent commit
Unstaged changes after reset:
M       package.txt
```

```shell
~/BadHistory (master|REBASE 1/2)
$ git status -s    #Short Git status
 M package.txt
?? terms.txt
?? terms.txt.orig

~/BadHistory (master|REBASE 1/2)
$ git add package.txt    #Staging the changes of package.txt

~/BadHistory (master|REBASE 1/2)
$ git commit -m "Update google map sdk version 1.0 -> 2.0"    #Commit the staged changes of package.txt
[detached HEAD 9603c59] Update google map sdk version 1.0 -> 2.0
 1 file changed, 1 insertion(+), 1 deletion(-)

~/BadHistory (master|REBASE 1/2)
$ git add terms.txt    #Staging the changes of terms.txt

~/BadHistory (master|REBASE 1/2)
$ git commit -m "Update terms of service"    #Commit the staged changes of terms.txt
[detached HEAD 0a75e2b] Update terms of service
 1 file changed, 1 insertion(+)
 create mode 100644 terms.txt

```
After committing individually, we can continue with the rebase operation.
```shell
~/BadHistory (master|REBASE 1/2)
$ git rebase --continue
Successfully rebased and updated refs/heads/master.

~/BadHistory (master)
$ git log --oneline
5c8003c (HEAD -> master) Render cafes on map
0a75e2b Update terms of service
9603c59 Update google map sdk version 1.0 -> 2.0
5663806 Render restaurants on the map.
95532e9 Add a reference to Google Map SDK v1.0.
de1b321 Initial commit

```