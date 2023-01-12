# Merge Conflicts

Very often when we are merging branches we run into conflicts. <br>
Conflicts happen when:

1. The same line of code is changed in two different ways, in the two branches.
2. A given file is modified in one branch, but deleted in the other branch.
3. The same file is added in two different branches with different content.

When conflict happens Git cannot automatically determine what is correct, and thus can not merge the branches automatically
Git will mark the file as being conflicted and halt the merging process. It is then the developers responsibility to resolve the conflict.
