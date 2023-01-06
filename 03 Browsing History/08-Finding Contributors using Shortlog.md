# Finding contributors using shortlog

| Command                                             | Description                                                                                    |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------|
| `git shortlog`                                      | Displays name, no of commits and a summary of commit messages made by contributors.            |
| `git shortlog -n` or,<br> `git shortlog --numbered` | Sort the `git shortlog` output based on number of commits per author.                          |
| `git shortlog -s`                                   | To supress commit descriptions in `git shortlog` output. Only show no. of commits per author.  |
| `git shortlog -s`                                   | To show email addresses of authors as well in `git shortlog` output.                           |

- We can also filter using `--before=` and `--after=`, to view the contributor in a date range.


```shell
~/Git&GitHub (master)
$ git shortlog
Anshuman Yuvraj (32):
      Module 01 - Introduction
      Committing changes
      Best Practices for committing the code
      Skipping the Staging area while committing the changes
      Add file1.txt and file2.txt (to be removed later)
      Remove file1.txt
      Remove file2.txt
      Removing Files Complete
      Add newFile.md
      Rename 'newFile.md' to '05-Renaming or Moving Files.md'
      [...]

[...]
```

```shell
~/Git&GitHub (master)
$ git shortlog -s
    32  Anshuman Yuvraj
[...]
```

