# Tagging

Tags are use to mark a certain point in the project. Most of the times they are used to mark release version, like v1.0.

There are two type of tags lightweight tags, and annotated tags. The lightweight tag has only the tag name, while a annotated tag has more properties, like tagger name, email and message. 


Because a annotated tag has more info so, they are preffered over lightweight tags.

## Tagging the last commit

`git tag <tag name>` : To tag the last commit

```shell
~/Git&GitHub (master)
$ git tag v1.0    #Tagging the last commit
```

## Tagging an earlier commit

`git tag <tag name> <reference of the commit>` : To tag an earlier commit using its reference.

```shell
~/Git&GitHub (master)
$ git tag "M-01" 729fcdd    #Tagging an earlier commit
```

## Annotated tag `-a`

`git tag -a <tag name> -m <tag message>` : To tag the last commit using annotated tag.

`git tag -a <tag name> <reference to the commit> -m <tag message>` : To tag an earlier commit using annotated tag. 

To create a annotated tag we use the option `-a`, followed by the tag name, reference to commit (in case of tagging an earlier commit) and then `-m` to specify the message.

```zsh
~/Git&GitHub (master)
$ git tag -a "M-02" 80b6694 -m "Module 02 - Creating Snapshots"    #Tagging an earlier commit using annotated tag
```
## Viewing the commit history

With `git log --oneline` we can see the tags.

```shell
~/Git&GitHub (master)
$ git log --oneline    #View commit log
d028a00 (HEAD -> master, tag: v1.0) Finding the Author of Line using Blame Complete
32d1ae4 Refactor 'Restoring a Deleted File'
2aeabfe Restoring a Deleted File Complete
b30df15 Restore 'Finding Contributors using Shortlog.md'
7e60bd9 Remove 'Finding Contributors using Shortlog.md'
[...]
80b6694 (tag: M-02) Module 02 - Creating Snapshots
9ca624a Restore '11-Restoring Files.md'
25c146e Remove '11-Restoring Files.md'
2bc671a Restoring Files Complete
10fca0f Add 'Restoring Files.md'
[...]
729fcdd (tag: M-01) Module 01 - Introduction
```

## Reference a commit using a tag

`git checkout <tag name>` : To reference a commit using its tag name.

A commit can also be referenced using it's tag; just like it's commitId.

```shell
~/Git&GitHub (master)
$ git checkout M-02    #Checkout a tag
Note: switching to 'M-02'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 80b6694 Module 02 - Creating Snapshots

~/Git&GitHub ((M-02))
$
```

## View all the tags

`git tag` : To view all the tags of the project.

```shell
~/Git&GitHub (master)
$ git tag    #View all tags
M-01
M-02
v1.0
```

## Tags messages `-n`

`git tag -n` : To view the tags along with the messages.

```shell
~/Git&GitHub (master)
$ git tag -n    #View all tags along with their messages
M-01            Module 01 - Introduction
M-02            Module 02 - Creating Snapshots
v1.0            Finding the Author of Line using Blame Complete
```

The lightweight tag gets associated with the commit message of the commit that it points to. And the annotated tag has a custom message that was provided at the time of its creation.

## Show Tag

`git show <tag name>`: To view all the infos of the specified tag. 

Similar to `git show <commit>`. If the command is run on an annotated tag besides the commit info we also have the tag info.

```shell
~/Git&GitHub (master)
$ git show M-02    #View all infos of a tag
tag M-02
Tagger: Anshuman Yuvraj <uvrajanshuman@gmail.com>
Date:   Mon Jan 9 01:50:18 2023 +0530

Module 02 - Creating Snapshots

commit 80b669448401b72de0741d2fdf1d6b314c6ad5d2 (tag: M-02)
Author: Anshuman Yuvraj <uvrajanshuman@gmail.com>
Date:   Fri Dec 30 05:59:55 2022 +0530

    Module 02 - Creating Snapshots

diff --git a/02 Creating Snapshots/12-Restoring a File to an Earlier Version.md b/02 Creating Snapshots/12-Restoring a File to an Earlier Version.md
new file mode 100644
index 0000000..f5ff922
--- /dev/null
+++ b/02 Creating Snapshots/12-Restoring a File to an Earlier Version.md
@@ -0,0 +1,22 @@
+# Restoring a File to an Earlier Version
+
+Once git tracks a file it stores every version of that file in the 
[...]
```

## Delete a tag `-d`

`git tag -d <tag name>` : To delete a tag.

```shell
~/Git&GitHub (master)
$ git tag -d v1.0    #Delete the specified tag
Deleted tag 'v1.0' (was d028a00)
```

| Command                                                                                                          | Description                                 |
|------------------------------------------------------------------------------------------------------------------|---------------------------------------------|
| `git tag <tag name>` <br> `git tag <tag name> <reference of the commit>`                                         | Lightweight tag                             |
| `git tag -a <tag name> -m <tag message>` <br> `git tag -a <tag name> <reference to the commit> -m <tag message>` | Annotated tag                               |
| `git checkout <tag name>`                                                                                        | To reference a commit using its tag name.   |
| `git tag`                                                                                                        | To view all the tags of the project.        |
| `git tag -n`                                                                                                     | To view the tags along with the messages.   |
| `git show <tag name>`                                                                                            | To view all the infos of the specified tag. |
| `git tag -d <tag name>`                                                                                          | To delete a tag                             |
