# Example of Bad History

To demonstrate various history rewriting techniques, let's create [a repo with bad commit history](./images/Screenshot9.jpg)

**Initial Commit**
```shell
~/BadHistory
$ git init    #Initialize empty git repo
Initialized empty Git repository in C:/Users/anshu/BadHistory/.git/

~/BadHistory (master)
$ echo "# Bad History" > README.md    #Create a new file README.md with specified content

~/BadHistory (master)
$ git add README.md    #Stage the changes
warning: LF will be replaced by CRLF in README.md.
The file will have its original line endings in your working directory

~/BadHistory (master)
$ git commit -m "Initial commit"    #Commit the changes
[master (root-commit) de1b321] Initial commit
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```

**Render restaurants the map** : wording issue in commit message and typo in content of map.txt
```shell
~/BadHistory (master)
$ echo "Restrnts" > map.txt    #Create a new file map.txt with specified content (typo in content)

~/BadHistory (master)
$ git add map.txt    #Stage the changes
warning: LF will be replaced by CRLF in map.txt.
The file will have its original line endings in your working directory

~/BadHistory (master)
$ git commit -m "Render restaurants the map."    #Commit the changes (typo in commit message)
[master 7b90516] Render restaurants the map.
 1 file changed, 1 insertion(+)
 create mode 100644 map.txt
```

**Fix a typo** : Fixed the typo in map.txt (that was introduced in previous commit)
```shell
~/BadHistory (master)
$ echo "restaurants" > map.txt    #Fixing the typo in map.txt

~/BadHistory (master)
$ git diff    #Verify the fix
warning: LF will be replaced by CRLF in map.txt.
The file will have its original line endings in your working directory
diff --git a/map.txt b/map.txt
index be8e8b0..8bbcbe1 100644
--- a/map.txt
+++ b/map.txt
@@ -1 +1 @@
-Restrnts
+restaurants

~/BadHistory (master)
$ git add map.txt    #Stage the changes
warning: LF will be replaced by CRLF in map.txt.
The file will have its original line endings in your working directory

~/BadHistory (master)
$ git commit -m "Fix a typo."    #Commit the changes
[master fdf3781] Fix a typo.
 1 file changed, 1 insertion(+), 1 deletion(-)

```

**Change the color of restaurant icons.** : Changed the content of map.txt
```shell
~/BadHistory (master)
$ echo "red restaurants" > map.txt    #Change the content of map.txt

~/BadHistory (master)
$ git diff    #Verify the change
warning: LF will be replaced by CRLF in map.txt.
The file will have its original line endings in your working directory
diff --git a/map.txt b/map.txt
index 8bbcbe1..ec02c61 100644
--- a/map.txt
+++ b/map.txt
@@ -1 +1 @@
-restaurants
+red restaurants

~/BadHistory (master)
$ git add map.txt    #Stage the changes
warning: LF will be replaced by CRLF in map.txt.
The file will have its original line endings in your working directory

~/BadHistory (master)
$ git commit -m "Change the color of restaurant icons."    #Commit the changes
[master 15bf387] Change the color of restaurant icons.
 1 file changed, 1 insertion(+), 1 deletion(-)
```

**Add a reference to Google Map SDK.** : Consider added the dependency of Google Map.
```shell
~/BadHistory (master)
$ echo "Google Map 1.0.0" > package.txt    #Create a new file package.txt with specified content

~/BadHistory (master)
$ git add package.txt    #Stage the changes
warning: LF will be replaced by CRLF in package.txt.
The file will have its original line endings in your working directory

~/BadHistory (master)
$ git commit -m "Add a reference to Google Map SDK."    #Commit the changes
[master de106c9] Add a reference to Google Map SDK.
 1 file changed, 1 insertion(+)
 create mode 100644 package.txt
```

**WIP** : Work in Progress, added temproary change in terms of service
```shell
~/BadHistory (master)
$ echo "draft" > terms.txt    #Create a new file terms.txt with specified content

~/BadHistory (master)
$ git add terms.txt    #Stage the changes
warning: LF will be replaced by CRLF in terms.txt.
The file will have its original line endings in your working directory

~/BadHistory (master)
$ git commit -m "WIP"    #Commit the changes
[master 42f2f93] WIP
 1 file changed, 1 insertion(+)
 create mode 100644 terms.txt
```

**Update terms of service and Google Map SDK version.**: Consider updated the Google map dependency version and terms of service.
```shell
~/BadHistory (master)
$ echo "Google Map 2.0.0" > package.txt    #Change the content of package.txt

~/BadHistory (master)
$ echo "completed" > terms.txt    #Change the content of terms.txt

~/BadHistory (master)
$ git diff    #Verify the changes
warning: LF will be replaced by CRLF in package.txt.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in terms.txt.
The file will have its original line endings in your working directory
diff --git a/package.txt b/package.txt
index 7324ece..5111c93 100644
--- a/package.txt
+++ b/package.txt
@@ -1 +1 @@
-Google Map 1.0.0
+Google Map 2.0.0
diff --git a/terms.txt b/terms.txt
index f3d4377..6ab9fed 100644
--- a/terms.txt
+++ b/terms.txt
@@ -1 +1 @@
-draft
+completed

~/BadHistory (master)
$ git add package.txt terms.txt    #Stage the changes
warning: LF will be replaced by CRLF in package.txt.
The file will have its original line endings in your working directory
warning: LF will be replaced by CRLF in terms.txt.
The file will have its original line endings in your working directory

~/BadHistory (master)
$ git commit -m "Update terms of service and Google Map SDK version."    #Commit the changes
[master 357f15f] Update terms of service and Google Map SDK version.
 2 files changed, 2 insertions(+), 2 deletions(-)
```

**WIP** : Work in progress
```shell
~/BadHistory (master)
$ echo "TEST" >> map.txt    #Append specified content to map.txt

~/BadHistory (master)
$ git add map.txt    #Stage the changes
warning: LF will be replaced by CRLF in map.txt.
The file will have its original line endings in your working directory

~/BadHistory (master)
$ git commit -m "WIP"    #Commit the changes
[master 92ade19] WIP
 1 file changed, 1 insertion(+)
```

**.** : ambiguious commit message
```shell
~/BadHistory (master)
$ echo "TEST" >> terms.txt    #Append specified content to terms.txt

~/BadHistory (master)
$ git add terms.txt    #Stage the changes
warning: LF will be replaced by CRLF in terms.txt.
The file will have its original line endings in your working directory

~/BadHistory (master)
$ git commit -m "."    #Commit the changes (ambiguious commit message)
[master b305d5a] .
 1 file changed, 1 insertion(+)
```

**git log --oneline**
```shell
~/BadHistory (master)
$ git log --oneline
b305d5a (HEAD -> master) .
92ade19 WIP
357f15f Update terms of service and Google Map SDK version.
42f2f93 WIP
de106c9 Add a reference to Google Map SDK.
15bf387 Change the color of restaurant icons.
fdf3781 Fix a typo.
7b90516 Render restaurants the map.
de1b321 Initial commit
```

- `7b90516 Render restaurants the map.` : Rewording issue in the commit message. should be Render resturants on the map.
- `fdf3781 Fix a typo.` : We shouldn't have a typo in the first place. Such commits are noise in the history. It should be combined with `7b90516 Render restaurants the map.` commit.
- `15bf387 Change the color of restaurant icons.` : This is the part of same line of work as Render Resturants on the map. <br>
    Actually `15bf387 Change the color of restaurant icons.`, `fdf3781 Fix a typo.`and `7b90516 Render restaurants the map.` should be combined into a single commit 
- `de106c9 Add a reference to Google Map SDK.` : The problem here is the postion of this commit in the commit history. If we checkout `7b90516 Render restaurants the map` commit our app is not going to work at that instant as Google Map SDK reference/dependency comes afterwards.<br>
    So either this should commit should come before the commit `7b90516 Render restaurants the map.` or we should combine it with `7b90516 Render restaurants the map.`.
- `42f2f93 WIP` : A work in progress commit. It is just noise in history. we should either drop it, change the message or combine it with other commits.
- `357f15f Update terms of service and Google Map SDK version.` : Ideally this commit should be seperated into two commits because updating the terms of service has nothing to do with updating the Google Map SDK.
- `92ade19 WIP` : A work in progress commit. It is just noise in history. we should either drop it, change the message or combine it with other commits.
- `b305d5a (HEAD -> master) .` : A mysterious commit we should either drop it or change the commit message.