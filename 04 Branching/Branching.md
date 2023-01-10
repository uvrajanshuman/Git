# Branching

![](./images/Screenshot1.png)
- Branching allows us to diverge from main line of work and work on something else in isolation.
It can also be thought of as a separate isolated workspace.

- Branching allows to work on different work items (workspaces) without messing the main line of work. The main line is kept stable.
<br> And when the work in the new branch is completed, it can be merged into the main branch.

- Branching in git is quite fast and efficient unlike other version control systems like subversion.
Like in subversion whe we create a new branch, subversion takes a copy of working directory and makes in a new branch. This can take some time as each files need to be copied.<br>
while, in git a branch is represented by just a pointer to a commit.


![](./images/Screenshot2.png)
- In git a branch is just a pointer to the commit. 
- The **Master** pointer points to the last commit in the main line of work and with each new commit git automatically moves it forward to
point to the latest commit.
- When we create new branch, git simply creates a new pointer pointing to the commit pointed by **Master** (last commit).
<br>And with each new commit in the new branch, the new branch pointer moves forward to point to the latest commit done in the new branch. But **Master** keeps on pointing to the last commit done in the main branch.<br>
In this way git knows the latest commit in both of the branches.
- When we switch back to master ,git matches our working directory to the commit that master points to. </br>
Thus, we always have a single working directory with multiple pointers.
- Git uses special pointer **HEAD** to know which branch we are currently working on.
- When we move to the new branch, **HEAD** starts pointing to the new branch pointer, else it keeps pointing the **Master**.<br>
So, moving into branches is done by just moving the **HEAD** pointer.


## Working with Branches

### Create new branch

`git branch <name-of-branch>` : To create a new branch.

```shell
~/Git&GitHub (master)
$ git branch demo-branch    #Create a new branch 'demo-branch'
```

### View Branches

`git branch` : To view all the available branches.

```shell
$ git branch    #View all branches
  demo-branch
* master
```

The `*` in front of the **_master_** means that at the moment we are in that branch. 
It is also possible to view the current branch with `git status`.

```shell
$ git status
On branch master
nothing to commit, working tree clean
```

### Switch branches

`git switch <name-of-branch>` : To switch to specified branch. <br>
It can also be done using `git checkout <name-of-branch>` (old command)

```shell
~/Git&GitHub (master)
$ git switch demo-branch    #Switch to 'demo-branch'
Switched to branch 'demo-branch'
```

### Rename a branch `-m`

`git branch -m <old-name> <new-name>` : To rename a branch.

```shell
~/Git&GitHub (demo-branch)
$ git branch -m demo-branch bugfix    #Rename 'demo-branch' to 'bugfix'
```

> we may have used dummy names for branches. But the branche name should be meaningful and should represent the work that is being performed on it.
