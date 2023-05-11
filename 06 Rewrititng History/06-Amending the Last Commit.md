# Amending the Last Commit

In situations where we made a mistake in the last commit, like a typo in the message, or adding a file that shouldn't be there,or any change that shouldn't be there, we can amend the commit. 

```shell
git commit --amend
```

It provides a convenient way to modify the most recent commit. It lets you to combine staged changes with the previous commit instead of creating an entirely new commit. (It moves to the stage we were just before committing the most recent commit, the changes are there in staging area. This allows to make the desired changes and re-commit discarding the previous one). It can also be used to simply edit the previous commit message without changing the actual snapshot.

But, amending does not alters the most recent commit, instead replaces it entirely with a new commit containing the desired changes.


## Changing the most recent commit message

```shell
git commit --amend
```
It will prompt to edit the last commit message in the default editor

or, we can specify the new message directly using `-m` flag

```shell
git commit --amend -m "new commit message"
```
The `-m` flag allows to directly pass the message, else git prompts for commit message in the default editor.

## Changing the most recent commit

Consider the following commit renders cafes on the map
```shell
~/BadHistory (master)
$ echo cafes >> map.txt    #Appending specified content in map.txt

~/BadHistory (master)
$ git commit -am "Render cafes on map"    #Staging and Commiting the change
warning: LF will be replaced by CRLF in map.txt.
The file will have its original line endings in your working directory
[master 8ff8312] Render cafes on map
 1 file changed, 1 insertion(+)

~/BadHistory (master)
$ git show HEAD:map.txt    #Viewing the contents of map.txt in current commit
red restaurants
cafes

```

Lets say we made a mistake we should had rendered blue cafes on the map. <br>
In such cases, we can make the desired change, stage it and amend our last commit to include those changes.

```shell
~/BadHistory (master)
$ code map.txt    #Replace 'cafes' with 'blue cafes'

~/BadHistory (master)
$ git status    #Git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   map.txt

no changes added to commit (use "git add" and/or "git commit -a")

~/BadHistory (master)
$ git add map.txt    #Staging the change
warning: LF will be replaced by CRLF in map.txt.
The file will have its original line endings in your working directory

~/BadHistory (master)
$ git commit --amend --no-edit    #Amending the last commit
[master c3dddb1] Render cafes on map
 Date: Wed May 10 17:14:15 2023 +0530
 1 file changed, 1 insertion(+)

~/BadHistory (master)
$ git show HEAD:map.txt    #Viewing the contents of map.txt in current commit
red restaurants
blue cafes

```

The `--no-edit` flag allows to amend the commit without changing its message. If ommitted git prompts with a default commit message in the default editor, we can either accept it or change it.

### Avoid amending public history :
Amended commits are actually entirely new commits and the previous commit will no longer be on your current branch. This has the same consequences as resetting a public snapshot. Avoid amending a commit that other developers have based their work on. This is a confusing situation for developers to be in and it’s complicated to recover from.

But sometime we may need to ammend a recently pushed commit.

### Amending a pushed commit
```shell
git push --force repository-name branch-name
```
Although, the `--force` option is not recomended unless you are absolutely sure that no one else has cloned your repository after the latest commit.

A safer alternative :

```shell
git push --force-with-lease repository-name branch-name
```
Unlike `--force`, which will destroy any changes someone else has pushed to the branch, `--force-with-lease` will abort if there was an upstream change to the repository.

[Git bash Screenshot](./images/Screenshot17.jpg)
