# Git

- ==**Commits**==: the user-created checkpoints --> each commit represents a version of the content at one point in time

  - Git requires the user to **supply commit message** each time a commit is created

  - Git uses the commit IDs to refer to different versions of the files

  - `git commit -m "Commit message"`

    - <u>Message Structure</u>

      A commit messages consists of three distinct parts <u>separated by a blank line</u>: the title, an optional body and an optional footer. The layout looks like this:

      ```
      type: Subject  
      
      body
      
      footer
      ```

      - Title: The title consists of the type of the message and subject. Subjects should be no greater than 50 characters, should <font color=red>**begin with a capital letter and do not end with a period**</font>. Use an **imperative tone** to describe what a commit does, rather than what it did. For example, use **change**; not changed or changes.
      - Body: Not all commits are complex enough to warrant a body, therefore it is optional and only used when a commit requires a bit of explanation and context. Use the body to explain the <u>**what** and **why** of a commit</u>, <u>not the how</u>. When writing a body, the blank line between the title and the body is required and you should limit the length of each line to no more than 72 characters.
      - Fooster: The footer is optional and is used to <u>reference issue tracker IDs</u>.

    - <u>The Type</u>

      The type is contained within the title and can be one of these types:

      - **feat:** A new feature
      - **fix:** A bug fix
      - **docs:** Changes to documentation
      - **style:** Formatting, missing semi colons, etc; no code change
      - **refactor:** Refactoring production code
      - **test:** Adding tests, refactoring test; no production code change
      - **chore:** Updating build tasks, package manager configs, etc; no production code change

  - `git log`: see all change commits history (from the recent commit)

    `git log -n <number/k>`: show the first k commits

    `git log -p`: has a flag that can be used to display the actual changes made to a file (combination of `git log` and `git diff`)

    `git log --stat`: give statistics about which files have changed in each commit

    press `q` to stop viewing the git log output

    <img src="/Users/xinyuzhang/Library/Application Support/typora-user-images/image-20220601224228681.png" alt="image-20220601224228681" style="zoom: 50%;" />

    (green plus: insertions; red minus: deletions)

  - `git diff`: can compare different versions of a file within git `git diff <commit ID-A> <commit ID-B>` --> operate on commits

    <img src="/Users/xinyuzhang/Library/Application Support/typora-user-images/image-20220601181012728.png" alt="image-20220601181012728" style="zoom:33%;" />

    (red: removed; green: added; blue: not changed, remain the same)

  - `git show <commit ID>`: show the changes of that commit without expressing its parents

  - `git checkout <commit ID>`: reset all files back to how they were at the time when that commit was made

  - `git clone <URL of a repository>`: instead of only downloading files from the recent commit, want to dowload the entire history

    If you make changes to the cloned repository, <font color=red>**the original will not change**</font>.

  - <font color=blue>**make *one commit per logical change (single change)***</font> --> each commit has one purpose that can be easily understood + <font color=blue>**never do too much work without committing**</font>

  - **Eg.** **You found three typos in your README. You fix and commit the first.**

    This commit seems too small. It would be better to fix all three typos, then commit. That way, your history won't get too cluttered with typo fixes. Plus, you don’t need to worry about introducing bugs to a README, so bundling changes together is more likely to be a good idea.

    **You commit all the changes required to add a new feature, which you’ve been working on for an hour.**

    This is probably a good size for a commit. All the work is on a single feature, so the commit will have a clear logical purpose. After an hour, the diff will probably have a fair amount of content in it, but not too much to understand.

    On the other hand, sometimes after working for an hour you’ll have run into more than one natural committing point, in which case you would want to break the feature up into smaller commits. Because of this, “too big” could also be a reasonable answer here.

    **You fix two small bugs in different functions and commit them both at once.**

    This commit is probably too big. It would have been better to commit after the first bug fix, since the two bug fixes aren't related to each other.

  - **Track across Inter-related Files** --> multiple-file commits (save multiple files in one commit)

    - **Repository**: a collection of related files
    - Each time a commit is made, all files in the repository will be tracked

- **==Git Errors and Warnings==**

  - **Should not be doing an octopus**
    Octopus is a strategy Git uses to <font color=blue>**combine many different versions of code together**</font>. This message can appear if you try to use this strategy in an inappropriate situation.

  - **You are in 'detached HEAD' state**
    <font color=blue>**HEAD is what Git calls the commit you are currently on.**</font> You can “detach” the HEAD by switching to a previous commit. Despite what it sounds like, it’s actually not a bad thing to detach the HEAD. Git just warns you so that you’ll realize you’re doing it.

- **==Repository==**

  - ` .git` is a hidden file that the user doesn't need to directly interact with --> can use `ls -a` to see all file (hidden and not hidden)

  - `git init`: to initialize a repository

  - `git status`: see the stages of commits and tracked files

  - Staging area:

    <img src="/Users/xinyuzhang/Library/Application Support/typora-user-images/image-20220605221546304.png" alt="image-20220605221546304" style="zoom: 67%;" />

    --> <font color=blue>**used to control exactly what changes go into each commit**</font>

    - `git add`: add files to the staging area

      (If you accidentally add a file to the staging area, you can remove it using `git reset <file name>`)

  - Compare changes between working directory, staging area and repository

    <img src="/Users/xinyuzhang/Library/Application Support/typora-user-images/image-20220611001824674.png" alt="image-20220611001824674" style="zoom:50%;" />

    - `git diff`: get the changes between working directory and staging area (can be used for commits and branches)
    - `git diff --stages`: get the changes between staging area and repository (the most recent commit)
    - `git reset --hard`: discard any changes in either the working directory or the staging area

- **==Branches==**

  - <u>**Uses:**</u>

    - <u>Solo project</u>: want to keep another experimental version of the project or the project in another language or work on a new feature --> **maintain parallel versions** of the code --> <font color=blue>**Context Switching**</font>

      <img src="/Users/xinyuzhang/Library/Application Support/typora-user-images/image-20220611004539803.png" alt="image-20220611004539803" style="zoom:50%;" />

      - <u>Collaboration</u>
        - Make a new branch for every feature / bug-fix --> after the process completes, the author can either update master branch to point to the tip of the new branch (combine with the current master using `git merge`)

  --> Git allows to create labels for commits --> these labels are called ***Branches***

  - <u>Master</u>: the main branch in most Git repositories

  - If checkout to a branch and make a commit, the branch label automatically updates to the new commit

  - <u>Tip of the branch:</u> the most recent commit in the branch

  - `git branch`: show the current branches (the * means the branch that is currently checked out)

    `git branch -a`: list all remote branches (including `master`, `origin/master`...)

  - `git branch <name>`: create a new branch with a new name <font color=blue>--> **该branch里会copy master branch的所有代码文件**</font>

  - `git checkout <branch name>`: switch from the current branch to another branch

  - `git log --graph --oneline <branch 1> <branch 2>`: see the visual representation of the overall commit history of selected branches 

  - `git checkout -b <branch name>`: implement `git branch` and `git checkout <branch>` simultaneously --> 这样这个时候的commit就会自动归属于这个新的branch里

  - **Merging**

    - <u>Combing simple files:</u>

      Same lines in multiple versions: on the final file

      Different lines in multiple versions: unknown (need to decide which is deleted from the original version <u>(not wanted)</u> or which is added to the original version <u>(keep)</u>)

    - <u>Merge two branches together</u>:

      - The merged version is also a commit --> store information about both of its parents

        Eg. Merge the coin branch into the master branch --> the merged commit is the tip of the master branch --> have all changes merged as well --> can delete the coin branch (delete the label, not the commits in coin branch) 

      - After merging, the commits will show with the timestamp (might be interleaved)

        <img src="/Users/xinyuzhang/Library/Application Support/typora-user-images/image-20220711032633870.png" alt="image-20220711032633870" style="zoom: 25%;" />

      - If a branch is deleted and leaves some commits unreachable from existing branches, those commits will continue to be accessible by commit id, until Git’s garbage collection runs. This will happen automatically from time to time, unless you actively turn it off. You can also run this process manually with `git gc`.

      - `git merge <brach-into> <branch-from>` --> merge `branch-from` into `branch-into`

      - `git branch -d <branch name>`: delete a branch (only label, not commits) --> commits are now available from `branch-info`

        <font color=blue>**Note.**</font> After deleting a branch, the whole commit history can be view by `git log --graph --oneline`

    - <u>Merge conflict</u>

      --> when git doesn't know which line should be merged into the new file (cause: different lines in multiple versions)

      --> ask the user whenver there's any ambiguity

      - Example

        ![image-20220711032928555](/Users/xinyuzhang/Library/Application Support/typora-user-images/image-20220711032928555.png)

        --> `master` and `easy-mode` branches both change the same general area in `game.js` 

        --> Solution: find the conflit in the file and solve it

        <img src="/Users/xinyuzhang/Library/Application Support/typora-user-images/image-20220711033705353.png" alt="image-20220711033705353" style="zoom:50%;" />

        - First section (marked `head`): my current code in `easy-mode` branch

          Second section: the original version

          Bottom section (marked `master`): the code in `master` branch right now

        - Solution

          - S1: Look at the code and understand what others want to change in the code

          - S2: Discuss with them to determine the change

          - S3: Resolve the conflict

            <img src="/Users/xinyuzhang/Library/Application Support/typora-user-images/image-20220711183423618.png" alt="image-20220711183423618" style="zoom: 67%;" />

          - S4: Commit the solution to let git know

  - **Update Local Copies of Remote Branches**

    Using `git clone` gets a local branch same as the remote one on GitHub and also *<u>gets a copy of the last known position</u>* of that branch on the remote

    `git fetch`: 用于从远程获取代码库，该命令执行完后需要执行 git merge 远程分支到你所在的分支。(used when you have different changes on each repository, with one changed locally and another remote) --> update the local copy of the remote branch to see changes from GitHub --> update `origin/master` branch, which needs merging to `master` branch

    `git fetch <branch>`: update all local copies of every branch for the origin remote

    <img src="/Users/xinyuzhang/Library/Application Support/typora-user-images/image-20220814222340235.png" alt="image-20220814222340235" style="zoom: 33%;" />

    <img src="/Users/xinyuzhang/Library/Application Support/typora-user-images/image-20220814223242447.png" alt="image-20220814223242447" style="zoom:40%;" />

    

- ==**GitHub**==

  --> share an entire git repository with others (interact with git)

  <img src="/Users/xinyuzhang/Library/Application Support/typora-user-images/image-20220712001142476.png" alt="image-20220712001142476" style="zoom: 25%;" />

  - <u>Syncing Repositories</u>

    - Information sent and received is in the form of git commits, so changes must **<u>be staged and commited</u>** before they can be sent

    - **Remote repository** (by git): store the location of a repository that the user wants to send and receive new commits to and from (a <u>reference</u>)

    - Syncing doesn't happen automatically. How to sync between the local copy of a repository and the one hosted on GitHub?

      - S1: Create an empty repository on GitHub
      - S2: Add the repository as a remote to the local repository
      - S3: `push` and `pull` data for interaction --> `push` a branch will automatically send all commits on that branch to GitHub

      ![image-20220711224805021](/Users/xinyuzhang/Library/Application Support/typora-user-images/image-20220711224805021.png)

    - `git remote`: view current remotes

      `git remote add <name> <URL of the GitHub repository> `: the name is within the local repository to refer to the repository on GitHub (If there is only one remote, it's standard to name it `origin`)

      `git remote -v`: `v` is for `verbose` --> output more information insternt remote names

      `git push <remote name to send change> <local branch name to push>`: send local changes to the remote --> copy all commits reachable from the local branch to the remote

      `git pull <remote name to receive change> <local branch name to pull>`: receive changes made from GitHub
      
      <font color=red>**git pull = git fetch + git merge !!**</font>

  - <u>Forking a Repository</u>

    --> get a copy of others' GitHub repositories directly on the GitHub servers without pulling down the code to the local machine first (like `git clone`) and <u>git automatically sets up a remote (origin)</u>

    - `git clone`:

      <img src="/Users/xinyuzhang/Library/Application Support/typora-user-images/image-20220808223432581.png" alt="image-20220808223432581" style="zoom: 33%;" />

      `fork`:

      <img src="/Users/xinyuzhang/Library/Application Support/typora-user-images/image-20220808223605417.png" alt="image-20220808223605417" style="zoom:50%;" />

      --> count the number of people forking the repository; easier to suggest changes back to the original repository
