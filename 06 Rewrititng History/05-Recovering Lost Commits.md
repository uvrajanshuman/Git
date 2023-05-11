# Recovering Lost Commits

Sometimes we might end up screwing while reseting the HEAD.
```shell
~/BadHistory (master)
$ git log --oneline
efb7762 (HEAD -> master) Revert bad code
92ade19 WIP
357f15f Update terms of service and Google Map SDK version.
42f2f93 WIP
de106c9 Add a reference to Google Map SDK.
15bf387 Change the color of restaurant icons.
fdf3781 Fix a typo.
7b90516 Render restaurants the map.
de1b321 Initial commit

~/BadHistory (master)
$ git reset --hard HEAD~6    #Reseting HEAD,consider accidental
HEAD is now at fdf3781 Fix a typo.

~/BadHistory (master)
$ git log --oneline    #The commits are gone
fdf3781 (HEAD -> master) Fix a typo.
7b90516 Render restaurants the map.
de1b321 Initial commit

```

Later on you realise this was a mistake and you want to undo the `git reset` operation.

This commit that just got discarded through the `git reset` operation won't be visible in normal `git log`<br> 
But Git keeps a log of all reference updates and can be viewed using `git reflog`. It is the log of how a reference has moved in the history.<br>
If nothing is passed, Git will show the reference log of **HEAD** (how has **HEAD** pointer moved across the history)

```shell
~/BadHistory (master)
$ git reflog
fdf3781 (HEAD -> master) HEAD@{0}: reset: moving to HEAD~6
efb7762 HEAD@{1}: commit: Revert bad code
92ade19 HEAD@{2}: reset: moving to HEAD~3
4d983c5 HEAD@{3}: revert: Revert "WIP"
8a11c0d HEAD@{4}: revert: Revert "Update terms of service and Google Map SDK version."
45ec33d HEAD@{5}: revert: Revert "WIP"
92ade19 HEAD@{6}: reset: moving to HEAD
92ade19 HEAD@{7}: reset: moving to HEAD
92ade19 HEAD@{8}: reset: moving to HEAD~1
b305d5a HEAD@{9}: commit: .
92ade19 HEAD@{10}: commit: WIP
357f15f HEAD@{11}: commit: Update terms of service and Google Map SDK version.
42f2f93 HEAD@{12}: commit: WIP
de106c9 HEAD@{13}: commit: Add a reference to Google Map SDK.
15bf387 HEAD@{14}: commit: Change the color of restaurant icons.
fdf3781 (HEAD -> master) HEAD@{15}: commit: Fix a typo.
7b90516 HEAD@{16}: commit: Render restaurants the map.
de1b321 HEAD@{17}: commit (initial): Initial commit

```

Every entry of the `reflog` command starts with a commit the `HEAD` is pointing to after the operation, then a unique identifier like `HEAD@{n}`. The output is sorted in order latest to oldest. 

| Commit ID | Identifier | Operation/Message                 |
| :-------: | :--------: | :---------------------- |
|  efb7762  |  HEAD@{1}  | commit: Revert bad code |

So we can revert any of theses operations to recover lost commits. 

In this example the operation `HEAD@{0}` is resetting `HEAD~6`. We can recover the lost commit with the `reset` command by passing the unique identifier or the commit ID

History before revert:

```shell
~/BadHistory (master)
$ git log --oneline    #Log before the revert of accidental reset of HEAD
fdf3781 (HEAD -> master) Fix a typo.
7b90516 Render restaurants the map.
de1b321 Initial commit
```

```zsh
~/BadHistory (master)
$ git reset --hard HEAD@{1}    #Reverting the accidental reset of HEAD
HEAD is now at efb7762 Revert bad code
```

History after revert:

```zsh
~/BadHistory (master)
$ git log --oneline    #Log after the revert of accidental reset of HEAD
efb7762 (HEAD -> master) Revert bad code
92ade19 WIP
357f15f Update terms of service and Google Map SDK version.
42f2f93 WIP
de106c9 Add a reference to Google Map SDK.
15bf387 Change the color of restaurant icons.
fdf3781 Fix a typo.
7b90516 Render restaurants the map.
de1b321 Initial commit
```

## Garbage collection
All commits can be considered safe so, even though a commit is reset it remains safe and can be viewed in the reflog. However, there is a limitation:

The Git garbage collector will remove all unreachable commits automatically after a certain time (30 days by default).

[Git bash Screenshot](./images/Screenshot16.jpg)
