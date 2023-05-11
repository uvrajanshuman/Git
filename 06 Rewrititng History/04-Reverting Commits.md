# Reverting Commits

In case we have pushed our commits to the **Remote Repository** we should not use the `reset` command. We should use the `revert` command instead, it will create a new commit base on our target commit reverting all the changes of the base commit.

## Revert a single commit

To revert a single commit we pass that commit to the revert command either by the commit ID or by the `HEAD~n` syntax. This will create new revert commit that will undo all the changes of that commit.<br>
Example: 
```shell
 git revert <commit-sha/HEAD~n>
```

## Revert a range of commits

We can revert a range of commits using the `..` notation

History before revert:
```shell
~/BadHistory (master)
$ git log --oneline --graph
* 92ade19 (HEAD -> master) WIP
* 357f15f Update terms of service and Google Map SDK version.
* 42f2f93 WIP
* de106c9 Add a reference to Google Map SDK.
* 15bf387 Change the color of restaurant icons.
* fdf3781 Fix a typo.
* 7b90516 Render restaurants the map.
* de1b321 Initial commit
```
Reverting last three commits
```zsh
~/BadHistory (master)
$ git revert HEAD~3..HEAD    #Revert specified range of commit
[master 45ec33d] Revert "WIP"
 1 file changed, 1 deletion(-)
[master 8a11c0d] Revert "Update terms of service and Google Map SDK version."
 2 files changed, 2 insertions(+), 2 deletions(-)
[master 4d983c5] Revert "WIP"
 1 file changed, 1 deletion(-)
 delete mode 100644 terms.txt

```
Note that the commit pointed by `HEAD~3` or `de106c9 Add a reference to Google Map SDK`, will not be included. so, the start commit is not included in revert.

This operation will create a new commit for each commit reverted and will open the default editor with default commit messege for each of the revert commits (we can accept the default messages or provide custom one).

History after revert:

```shell
~/BadHistory (master)
$ git log --oneline --graph
* 4d983c5 (HEAD -> master) Revert "WIP"
* 8a11c0d Revert "Update terms of service and Google Map SDK version."
* 45ec33d Revert "WIP"
* 92ade19 WIP
* 357f15f Update terms of service and Google Map SDK version.
* 42f2f93 WIP
* de106c9 Add a reference to Google Map SDK.
* 15bf387 Change the color of restaurant icons.
* fdf3781 Fix a typo.
* 7b90516 Render restaurants the map.
* de1b321 Initial commit
```

This has added so much noise in the history (a revert commit for each revert). It may be better if we could revert all the three desired commits into a single revert commit.

To do so, first we need to reset the **HEAD** to the position it was before the revert operation started. (as if this revert never happened)

```shell
~/BadHistory (master)
$ git reset --hard HEAD~3    #Undoing the previous revert
HEAD is now at 92ade19 WIP

~/BadHistory (master)
$ git log --oneline --graph
* 92ade19 (HEAD -> master) WIP
* 357f15f Update terms of service and Google Map SDK version.
* 42f2f93 WIP
* de106c9 Add a reference to Google Map SDK.
* 15bf387 Change the color of restaurant icons.
* fdf3781 Fix a typo.
* 7b90516 Render restaurants the map.
* de1b321 Initial commit
```

### Revert a range of commits into a single commit `--no-commit`

Instead of creating one new commit for each reverted commit (which might pollute the history) we can use the option `--no-commit`, that will create only one commit, for all the reverted commits.

With this option git will simply add the required changes for each revert in the **staging area** which will need to be comitted manually. So, for every commit we want to revert git will figure out the changes that needs to be undone then it will apply those changes in the staging area.

History before revert:
```shell
~/BadHistory (master)
$ git log --oneline --graph
* 92ade19 (HEAD -> master) WIP
* 357f15f Update terms of service and Google Map SDK version.
* 42f2f93 WIP
* de106c9 Add a reference to Google Map SDK.
* 15bf387 Change the color of restaurant icons.
* fdf3781 Fix a typo.
* 7b90516 Render restaurants the map.
* de1b321 Initial commit
```
Reverting last three commits
```shell
~/BadHistory (master)
$ git revert --no-commit HEAD~3..HEAD    #Revert specified range of commit using a single revert commit
```
If we run `git status`, we can see the changes of the reverse of the last 3 commits has been added to the staging area.

```shell
~/BadHistory (master|REVERTING)
$ git status -s    #Short Git status
M  map.txt
M  package.txt
D  terms.txt

```

If we want to abort the revert operation we can use the `--abort` option.
```shell
git revert --abort
```

or, If we are happy with the changes we use the `--continue` option.
```shell
~/BadHistory (master|REVERTING)
$ git revert --continue    #Continue the revert operation
[master efb7762] Revert bad code
 3 files changed, 1 insertion(+), 3 deletions(-)
 delete mode 100644 terms.txt

```
This will open the default editor with a default commit message. we can either accept it or provide a custom message like 'Revert bad code'.

History after revert:

```zsh
~/BadHistory (master)
$ git log --oneline --graph
* efb7762 (HEAD -> master) Revert bad code
* 92ade19 WIP
* 357f15f Update terms of service and Google Map SDK version.
* 42f2f93 WIP
* de106c9 Add a reference to Google Map SDK.
* 15bf387 Change the color of restaurant icons.
* fdf3781 Fix a typo.
* 7b90516 Render restaurants the map.
* de1b321 Initial commit

```

[Git bash Screenshot](./images/Screenshot15.jpg)
