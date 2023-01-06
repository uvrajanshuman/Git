# Finding Bugs Using Bisect

- Git provides a great tool **Bisect** to find bugs quickly.
- Using the bisect command we can easily find the commit that introduced the issue/bug.
- Instead of manually checking each commit for bug, we can use bisect command to instantly find the commit that introduced the bug.
- We just need to provide bad state (bug) and good state

Imagine there is a bug in an application, but we do not know the specific commit where the bug was introduced. Using the **Bisect** to we can narrow our search.

With `git bisect` we can keep on splitting our history in half, then by process of ellimination and find the commit that introduced a problem.

## Sample Example: 
First we have to tell it that the current state, being the last commit, is a bad commit. And them we have to give it a good commit, as the good state.

### Display all commit history
**`git log --oneline --all`**  
```shell
~/Git&GitHub (master)
$ git log --oneline    #Git log
d154a98 (HEAD -> master) Checking out a Commit Complete
38f4fad Viewing a Commit Complete
15c88a1 Aliases Complete
b512ad1 Formatting the Log Output Complete
bd86ebd Filtering the History Complete
c039340 Viewing the History Complete
80b6694 Module 02 - Creating Snapshots
9ca624a Restore '11-Restoring Files.md'
25c146e Remove '11-Restoring Files.md'
2bc671a Restoring Files Complete
10fca0f Add 'Restoring Files.md'
[...]
```

### Initialize the bisect operation
**`git bisect start`** : This will initialize the bisect operation
```shell
~/Git&GitHub (master)
$ git bisect start    #Initialize bisect operation
```

### Specify a bad commit
**`git bisect bad`** : To Specify current commit as bad commit

```
~/Git&GitHub (master|BISECTING)
$ git bisect bad    #Specify the current commit as bad commit
```

### Specify a good commit
**`git bisect good 10fca0f`** : To Specify a good commit using commitId.

```
~/Git&GitHub (master|BISECTING)
$ git bisect good 10fca0f    #Specify the good commit using the commitId
Bisecting: 4 revisions left to test after this (roughly 2 steps)
[c0393409c98ef1a2bb329ee6d265edb3702c649c] Viewing the History Complete
```

### Display all commit history
**`git log --oneline --all`** </br> 
We can see that the `HEAD` is in detached state. So, Git made a checkout to the middle of the history, between the bad and good commit. 

The Working Directory gets restored to that point in time where we can test the application and conclude whether the commit is good or bad.

```shell
~/Git&GitHub ((c039340...)|BISECTING)
$ git log --oneline --all
d154a98 (master, refs/bisect/bad) Checking out a Commit Complete
38f4fad Viewing a Commit Complete
15c88a1 Aliases Complete
b512ad1 Formatting the Log Output Complete
bd86ebd Filtering the History Complete
c039340 (HEAD) Viewing the History Complete
80b6694 Module 02 - Creating Snapshots
9ca624a Restore '11-Restoring Files.md'
25c146e Remove '11-Restoring Files.md'
2bc671a Restoring Files Complete
10fca0f (refs/bisect/good-10fca0ff1423e452766310cff1e1d39fbbc73994) Add 'Restoring Files.md'
[...]
```

- At this point we can run our application and automated tests to see if the problem is still there. 
- If the bug persists it means it was introduced somewhere between commit `80b6694` and commit `10fca0f` (i.e: lower half/prior half). 
- If the bug is gone it means it was introduced somehere between `d154a98` and `bd86ebd` (i.e: upper half/later half).

### Consider current commit to be good
**git bisect good** : Specify current commit as good

Suppose we test the application at this stage and conclude the commit is bad.

This means the bug was introduced somehere between the commit `d154a98` and `bd86ebd` (i.e: upper half/later half).

```shell
~/Git&GitHub ((c039340...)|BISECTING)
$ git bisect good    #Specify the current commit as good commit
Bisecting: 2 revisions left to test after this (roughly 1 step)
[b512ad1de89708f81b961389567a432c502022e7] Formatting the Log Output Complete
```

### Display all commit history
**`git log --oneline --all`** </br> 
Git as moved the `HEAD` to the commit `b512ad1` (middle of upper half)

```shell
~/Git&GitHub ((b512ad1...)|BISECTING)
$ git log --oneline --all
d154a98 (master, refs/bisect/bad) Checking out a Commit Complete
38f4fad Viewing a Commit Complete
15c88a1 Aliases Complete
b512ad1 (HEAD) Formatting the Log Output Complete
bd86ebd Filtering the History Complete
c039340 (refs/bisect/good-c0393409c98ef1a2bb329ee6d265edb3702c649c) Viewing the History Complete
80b6694 Module 02 - Creating Snapshots
9ca624a Restore '11-Restoring Files.md'
25c146e Remove '11-Restoring Files.md'
2bc671a Restoring Files Complete
10fca0f (refs/bisect/good-10fca0ff1423e452766310cff1e1d39fbbc73994) Add 'Restoring Files.md'
[...]
```
- At this point we can run our application and automated tests to see if the problem is still there. 
- If the bug persists it means it was introduced in the commit `bd86ebd`. 
- If the bug is gone it means it was introduced somehere between `15c88a1` and `d154a98` (i.e: upper half)`.

### Consider current commit to be bad
**git bisect bad** : Specify current commit as bad

Now `HEAD` points the `b512ad1` commit, suppose we test the application at this stage and conclude the commit is bad.

This means the bug must have been introduced in commit `bd86ebd`.

```shell
~/Git&GitHub ((b512ad1...)|BISECTING)
$ git bisect bad    #Specify current commit as bad commit
Bisecting: 0 revisions left to test after this (roughly 0 steps)
[bd86ebdbea43cdb0648e9a8b7533bba055b2384a] Filtering the History Complete
```
## Display all logs of the repo
**`git log --oneline --all`** </br> 
Git as moved the `HEAD` to the `bd86ebd` commit.

At this stage the previous commit `c039340` is marked good and next commit `b512ad1` is marked as bad; So, this must be the commit that introduced the bug.

```shell
~/Git&GitHub ((bd86ebd...)|BISECTING)
$ git log --oneline --all
d154a98 (master) Checking out a Commit Complete
38f4fad Viewing a Commit Complete
15c88a1 Aliases Complete
b512ad1 (refs/bisect/bad) Formatting the Log Output Complete
bd86ebd (HEAD) Filtering the History Complete
c039340 (refs/bisect/good-c0393409c98ef1a2bb329ee6d265edb3702c649c) Viewing the History Complete
80b6694 Module 02 - Creating Snapshots
9ca624a Restore '11-Restoring Files.md'
25c146e Remove '11-Restoring Files.md'
2bc671a Restoring Files Complete
10fca0f (refs/bisect/good-10fca0ff1423e452766310cff1e1d39fbbc73994) Add 'Restoring Files.md'
[...]
```

### Specifying current commit as bad commit

After verfifying let's suppose we found out the bug is still there, meaning the bug was introduced in commit `bd86ebd`. 

So we run `git bisect bad`. Git will output the info about that commit like the following example:

```shell
~/Git&GitHub ((bd86ebd...)|BISECTING)
$ git bisect bad
bd86ebdbea43cdb0648e9a8b7533bba055b2384a is the first bad commit
commit bd86ebdbea43cdb0648e9a8b7533bba055b2384a
Author: Anshuman Yuvraj <uvrajanshuman@gmail.com>
Date:   Thu Jan 5 00:58:00 2023 +0530

    Filtering the History Complete

 03 Browsing History/02-Filtering the History.md |  88 ++++++++++++++++++++++++
 03 Browsing History/images/Screenshot10.png     | Bin 0 -> 52503 bytes
 03 Browsing History/images/Screenshot11.png     | Bin 0 -> 76453 bytes
 03 Browsing History/images/Screenshot12.png     | Bin 0 -> 74587 bytes
 03 Browsing History/images/Screenshot13.png     | Bin 0 -> 71462 bytes
 03 Browsing History/images/Screenshot7.png      | Bin 0 -> 58769 bytes
 03 Browsing History/images/Screenshot8.png      | Bin 0 -> 107640 bytes
 03 Browsing History/images/Screenshot9.png      | Bin 0 -> 103369 bytes
 8 files changed, 88 insertions(+)
 create mode 100644 03 Browsing History/02-Filtering the History.md
 create mode 100644 03 Browsing History/images/Screenshot10.png
 create mode 100644 03 Browsing History/images/Screenshot11.png
 create mode 100644 03 Browsing History/images/Screenshot12.png
 create mode 100644 03 Browsing History/images/Screenshot13.png
 create mode 100644 03 Browsing History/images/Screenshot7.png
 create mode 100644 03 Browsing History/images/Screenshot8.png
 create mode 100644 03 Browsing History/images/Screenshot9.png

```

### Switching back to master
After we are done we have to attach the `HEAD` pointer to the branch with the command `git bisect reset`.
```shell
~/Git&GitHub ((bd86ebd...)|BISECTING)
$ git bisect reset    #Reset the bisect operation
Previous HEAD position was bd86ebd Filtering the History Complete
Switched to branch 'master'

```

## Summary:

```shell
$ git bisect start    #Start the bisect operation

$ git log --oneline   #Display the gitlog history with prefix git commit id

$ git bisect good commitId/HEADpointer    #Specify good commit

$ git bisect bad    #Specify bad commit

# Continue bisecting until the first bad commit is found

$ git bisect reset    #Reset the bisect operation.

$ git revert BAD_COMMIT_ID    #Revert the bad commit and provide commit message
```
