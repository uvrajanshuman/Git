# Viewing Merged and Unmerged Branches

When we are finished working in a branch, we should merge it into ***`master`*** branch, and afterwards delete it.

## List merged branches `--merged`

`git branch --merged` : To list all the merged branches.

```shell
~/Git&GitHub (master)
$ git branch --merged    #List merged branches
  3-way-merge
  fast-forward-merge
* master
  no-fast-forward-merge
```

## List unmerged branches `--no-merged`

`git branch --no-merged` : To list all the unmerged branches.

```shell
~/Git&GitHub (master)
$ git branch --no-merged    #List unmerged branches
```
