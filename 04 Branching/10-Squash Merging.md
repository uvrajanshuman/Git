# Squash Merging

Let us consider we have a bugfix branch with two commits b1 and b2.<br>
Normally when we are done making changes in bugfix branch we merge them into master
This will lead to a merge-commit in master which will have two parents **_master_** and **_bugfix_**.<br>
After merge the commits b1 and b2 will become part of the history of the **_master_** branch.

![](./images/Screenshot21.png)

But what if these commits b1 and b2 are not good quality commits. And we don't care about the history of the **_bugfix_** branch. 

In such cases **Squash Merging** should be used. 

## Squash Merge

In Sqush Merge all the changes/commits of a branch (that is to be merged) get combined into a single commit, and this combined commit get applied on top of the branch in which merge is going to happen.

So, here a new commit will combine all the changes of the bugfix branch (i.e: b1+b2). we will be having a single logical changeset representing all the changes for bugfix.<br>
Then this combined commit will be applied on top of the master branch. 

![](./images/Screenshot22.png)

- This is useful in situations where the commits in the branch are not good quality commits, or simply we do not need the history from the coming branch.

This new commit is not a merge commit, because it does not have two parents. It is lacking the reference to **B2**, the last commit from the **bugfix** branch. <br>
It is just a regular commit added on top of ***`main`*** that combines the commits from the other branch.

when we are done with squash merging and delete the **bugfix** branch, we are left with a clean linear history. This is the benefit fo Squash merging. 

![](./images/Screenshot23.png)

> But usually we should only use squash merging for short lived branches with bad history.

 `git merge --squash <name-of-branch>` : To perform a squash merge.
 
Git will create a new commit, called a ***`Squash commit`***, that combines the changes made in the merged branch, and it will apply these changes to the ***Staging Area***. Then these staged changes can be committed normally.
