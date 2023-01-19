# 10- Sharing Tags

## Push tag

By default the `push` command does not transfer tags to the **Remote Repository**. We have to explicitly `push` them, with the command `git push origin <tag-name>`.

Ex:
```shell
>git push origin v1.0
```

GitHub automatically generates assets and assosiates it with a tag.
So, we can download out entire source code at this point in time.

## Deleted pushed tag

To delete an already pushed tag from the **Remote Repository**, we use the command `git push origin --delete <tag-name>`.

Ex:
```shell
>git push origin --delete v1.0
```

This only deletes the tag from the **Remote Repository**, it will still be present in the **Local Repository**.


To delete it from local repository explicity
```shell
>git tag -d <tag-name>
```


<!-- ## Release Management
The github feature that goes hand-in-hand with tags is release management.
We can create a release to package our software along with the source code binary files and relese notes.
Homepage of rep>tags>releases --create a new release> create a new tag or existing tag and select branch. --add release title and release note and optionally attach binary files and publish it. -->