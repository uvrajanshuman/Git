# Sharing Branches

Similar to Tags branches are private for the **Local Repository** by default.

## Push a branch to **Remote Repository**

When we create a new branch it will only be available in our **Local Repository**. If we want to share our branches with other collaborators we have to manually `push` them to the **Remote Repository**.

If we try to `push` a branch, that it is not in the **Remote Repository**, with `git push`, we will get an error.

For example, Let's say we have a branch named `bugfix` and on `git push` Git will throw an error:

```shell
>git push
fatal: The current branch bugfix has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin bugfix
```

The error message **_`The current branch bugfix has no upstream branch.`_** means that this branch is not linked to a remote tracking branch in origin, if we run `git branch -vv`, we can see this (info about local and remote tracking branches).

```shell
>git branch -vv
* bugfix 9edbb2f Sample commit
  main   9edbb2f [origin/main] Sharing Tags
```
>Here **_`master`/`main`_** (local branch) is linked to **_`origin/master` / `origin/main`_** (remote tracking branch); But **_`bugfix`_** is not linked to any remote tracking branch

To see all the remote tracking branches
```shell
git branch -r
origin/HEAD -> origin/master
origin/master
```
### Setting a upstream branch

To set the remote tracking branch we run the command Git suggested `git push --set-upstream origin <name-of-branch>`, we only have to pass `--set-upstream` option the first time.

We can abbreviate the option `--set-upstream` to `-u`.

```shell
>git push -u origin bugfix
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 1.56 KiB | 1.56 MiB/s, done.
Total 4 (delta 2), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
[...]
Branch 'bugfix' set up to track remote branch 'bugfix' from 'origin'.
```

And then again `git branch -vv` to see the result.

```zsh
❯ gb -vv
* bugfix 9edbb2f [origin/bugfix] Sample commit
  main   9edbb2f [origin/main] Sharing Tags
```

View all remote branches
```shell
git branch -r  
origin/HEAD -> origin/master
origin/bugfix    # A new remote tracking branch
origin/master
```
we can start working with this branch the same way we work with master, make few commits and then push them to remote using their remote tracking branch.

## Delete a branch from **Remote Repository**

To delete a branch from the **Remote Repository** we run `git push -d <remote> <name-of-branch>`. This will only detete the branch in the **Remote Repository**, it will still be available in the **Local Repository**.

```shell
git push -d origin bugfix
```
This branch is now deleted from the origin.

We can check with `git branch -vv`.

```shell
>git branch -vv
* bugfix 133c99c [origin/bugfix: gone] add details to lesson
  main   9edbb2f [origin/main] lesson complete
```
Here **gone** represents removed from remote.

view all remote tracking branches.

```shell
>git branch -r   #Remote tracking branch is now gone.
origin/HEAD -> origin/master
origin/master
```
>Even though we have removed the remote tracking branch the local branch is still there. which if needed must be deleted manually (`git branch -d bugfix`)
