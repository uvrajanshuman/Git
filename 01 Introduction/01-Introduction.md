# Git

- Git is a version control system for tracking changes in computer files and co-ordinating work on those files among multiple people.
- A version control system records the changes made to a file over time, in a special database called repository.
- Git is a distributed version control system. So, Git does not necessarily rely on central server to store all the versions of a project files.
  Instead, every user clones a copy of a repository and has full history of the project on their own machine.
- The clone has all the metadata of the original while the original itself is stored on a self-hosted server or third party hosting service like GitHub.
- Git being a distributed version control system helps to:
    1. Track changes among the files.
    2. Easily recover files.
    3. Check who introduced issues and when.
    4. Rollback to previous working states.

## History of Version Control Systems
1. **Local VCS**
  - Databases are used to track files (Local Storage).
  - Pros: Can track changes, facility of Rollback.
  - Cons: Limited to local drive/disk. If one looses Local drive, everything is lost. No Collaboration.
2. **Centralized VCS**
  - Storage done in centralized servers.
  - Pros: Can track changes, Facility of Rollback, Allows collaboration
    (Multiple user can collaborate, each user pulls the data admits the changes and then pushes back to server. The version present at server is treated as master version).
  - Cons: There is single point of failure. In case of Server damage/failure all the data will be lost.
3. **Distributed VCS**
  - Data is stored in centralized servers as well as local machines of each user.
  - Since each user has complete history of the project, so in case of server damage all the data will still be present in each user's machine.
    And in case of local machine damage, the data remains stored in centralized server. So, there is no issue of data loss.
  - In Distributed VCS each collaborator has complete version of project along with the changes. So, every contributor has complete backup of the project.

>Note:
><br> `.git` is a hidden folder where the complete project history is saved in form of snapshots; And the working directory ca be moved to any of these snapshots
><br> Git has integrity. i.e: Git generates SHA-1 checksums of all the changes. So, if anyone tries to manually change files in `.git` folder, it would not reflect into the project.
><br> So, unauthorized changes can't be done.



