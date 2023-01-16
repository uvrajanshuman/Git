# Cloning a Repository

`git clone` is a Git command used to target an existing repository and create a clone, or copy of the target repository. 

- Every collaborator should clone the repository. They sholfd be able to locally work with the repository and when they are done with with the changes they will push to the remote repository.

- To clone a repository we need the repository url.<br> 
For example: [https://github.com/uvrajanshuman/Git-GitHub.git](https://github.com/uvrajanshuman/Git-GitHub.git)

- Then on local machine run the command command `git clone <url>`, this will create a local copy of the repository. 

```shell
>git clone https://github.com/uvrajanshuman/Git-GitHub.git
```

## Changing the name of default directory while cloning

- When using the `clone` command Git locally creates a directory with the same name as the repository. 
- But, we can change it by passing a new name after the url `git clone <url> <new-folder-name>`

```shell
>git clone https://github.com/uvrajanshuman/Git-GitHub.git Git&GitHub
```
The above command will copy the repository to a new folder called `Git&GitHub`.

## Does Git Clone Get All Branches?

Yes, Git clone does download all branches. 

- Every downloaded branch is designated as a remote tracking branch. However, only the master branch is checked out locally, which tracks a remote tracking branch called **_`origin/master`_**. Any of the other remote tracking branches can be checked out locally as needed.

- `git branch` : To view all the local branches.<br>
Ex:
    ```shell
    > git branch    #List all the local branches
    * master
    ```
    - As you can see, we're only shown the master branch available locally. As previously stated, that's because master is checked out by default during the cloning process and therefore the local branch itself is created.
    - But there are other branches hiding in the repository which can be viewed using the `-a` or `--all` flag:

- `git branch --all` : To view all the local branches as well as remote branches.<br>
Ex:
    ```shell
    $ git branch -a    #List all branches (local & remote)
    * master
    remotes/origin/HEAD
    remotes/origin/master
    remotes/origin/v1.0-stable
    [...]
    ```

    - Git doesn't create a local branch for each remote tracking branch, but it does give us the ability to view them all and check one out if needed. Although there are ways to clone a repo and make a local branch for each remote branch, it's usually not recommended aside from a few specific scenarios.

## Remote Repository

```shell
>git log --oneline --graph
* 0065a18 (HEAD -> master, origin/main, origin/HEAD) start new lesson
* 488cbba ......
[...]
```

- **_`master`_** is the name of a default branch of local repo.
- When we clone a **Remote Repository**, in this case from GitHub, Git names this source repository **_`origin`_**.<br>
Technically this is called a remote tracking branch, we can not switch to it or commit to it.<br>
So, **_`origin`** is the reference to the remote repository.
- Because now we have multiple repositories (local, remote) and history of each of these repositories can evolve independently.
- **_`origin/main`_** tells us where is the master/main branch in that origin repository. Technically this is called a remote tracking branch. <br>
It is a branch on which we can not directly commit to, switch or checkout.
- **_`origin/HEAD`_** tell us where is the HEAD pointer in origin repository.

### Reference `origin/main`

The **_`origin/main`_** pointer, tell us where is the **_`main`_**/**_`master`_** branch in the **Remote Repository**.<br>
If we start to work and commit to the **Local Repository**, **_`master`_** will move forward, but **_`origin/main`_**, will stay where it was until we push our work.

### List remote repositories

We can have more than one **Remote Repositories**, with the command `git remote` we can list all the **Remote Repositories** connected to our **Local Repository**.

`git remote`: Shows the list of remote repositories.

`git remote -v` Shows details about the remote repositories.

```shell
>git remote -v
origin  https://github.com/uvrajanshuman/Git-GitHub.git (fetch)
origin  https://github.com/uvrajanshuman/Git-GitHub.git (push)
```
This is the url git is going to use when we talk to this remote repository.
Using the `-v` option we get a more verbose output, showing more details. <br>In this example we only hev one **Remote Repository**


## Summary:

| Command                                                             | Description                                                                  |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------|
| `git clone <url>`                                | To clone a remote git repository.                                                               | 
| `git clone <url> <new-folder-name>`              | To clone a remote git repository and change the default directory to specied `new-folder-name`. | 
| `git branch`                                     | To list all the local branches.                                                                 | 
| `git branch --all`                               | To list all branches (local and hideen remote branches).                                        | 
| `git branch --all`                               | To list all branches (local and hideen remote branches).                                        | 
| `git remote`                                     | To list all remote repositories.                                                                | 
| `git remote -v`                                  | To list all remote repositories along with details like git url for fetch and push.             | 