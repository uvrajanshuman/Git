# Picking a File from Another Branch

we learnt cherrypick but what if we are intreseted in a single file not an entire commit.

Sometimes we may need a single file from one branch in another branch. <br>Unlike cherry picking that merges a commit, we can bring only one file.

For this operation we use the `restore` command.<br>
In the branch that needs the files we run `git restore --source=<name-of-branch> -- <file-name>`, git will update the **_Working Directory_** with the latest version of that file from the target branch

Let's suppose we need a file named `file1.txt` from an unmerged branch called **feature** in **_`master`_**, so we run:

```shell
>git restore --source=feature -- file1.txt
```
