# Stage and Snapshots

Git does not track files automatically we have to explicitly specify files to be tracked by Git.\
Even when a new repository is initialized with `git init`, in project that already as several files, Git will only track them, when we add them explicitly..

The `git status` command can be run to see the status of the **Working Directory** and **Staging Area**.

![](./images/Screenshot2.png)

- The above command shows untracked folders containing untracked files, that needs to be staged explicitly.

## Staging files

- Git does not automatically start tracking changes in file. The file needs to be staged explicitly.

| Command                         | Description                                                        |
|---------------------------------|--------------------------------------------------------------------|
| `git add <file>`                | To add a file to staging area                                      |
| `git add <file1, file2>`        | To add multiple files to staging area                              |
| `git add <directory>`           | To add a directory to staging area                                 |
| ` git add *.txt`                | To add files with certain patterns to the staging area (like .txt) |
| ` git add -A` </br> or <br/> `git add .` | To add all files and directories to the staging area      |

