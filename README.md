# Practical Guidance To Git
In this quick introduction we will be going over the basics of GIT and using it with the help of IntelliJ.
## Preparation
Make sure you have installed:
- GIT
  - You can check this in the terminal by entering git --version
  - Windows users should have GIT bash
- (Optional) IntelliJ (Community Edition is fine for this workshop, but Ultimate is more comfortable if you have a license)
## Creating a project from a remote repository 
- Copy the URL for "Clone with HTTPS"
  - If you have set up an SSH key for github then feel free to use the "Clone with SSH" option
- To clone the repository via command line
  -  Open your terminal (Windows users can use GIT bash for example)
  -  Navigate to a suitable folder (IdeaProjects for example)
  -  Enter: `git clone the_url_you_copied`
  -  If you're cloning via HTTPS then you will be prompted for a username and password. Use the same login data that you used to access Gitlab/Github.
  -  Navigate to the project's root folder: `cd git-workshop-2023`
- To clone the repository via IntelliJ IDE:
  - Choose "New project" and "Project from Version Control" and follow the steps in IntelliJ.
## Checkout branches
- Check your current branch with command: `git branch`.
  - In IntelliJ you can check your current branch in the right bottom corner of the screen.
## Create a branch
* First switch to the branch ```develop```
* Let's create and switch to a new branch called ```feature/your-name```
  * Command line
    ```
    CHEATSHEET
    
    # Create new branch and switch to it  
    git checkout -b branch-name
    
    # Switch to an existing branch
    git checkout -b branch-name 
    ```
  * IntelliJ
    * Click on the name of the branch in the bottom right corner
    * Choose "New branch" and enter the name you wish
    * You can tick the box "Checkout branch" or if you do not, then find the branch under "Local branches", click it and choose "Checkout".
## Add, commit, push, pull changes
* Create new file in directory ```files/file_1.txt``` following the instructions there.
* When adding a new file IntelliJ will ask if you wish to add it to git - uncheck this option for now.
* When the file is created we will add it to git, commit the changes and push them to the repository.
* Notice differences between "tracked" and "untracked" files.
    ```
    CHEATSHEET
    
    # To add a file/directory to git 
    git add filename
    git add dirname
  
    # To commit changes
    git commit -m "A nice and clear message about what I changed"
  
    # To push commits
    # NB! Try to never use -force option
    git push
    ```
* All this can be done via IntelliJ as well.
  * Right click on file or directory, choose "Git" -> "Add"
  * Find "Git" in top menu, and "Commit" to open commit window or "Push" to send all committed changes to repository.
## Remove or amend commits
* Create a new file in directory ```files/file_2.txt```
* Commit this file
* Make a change to the file
* Amend the previous commit
  * ```git commit --amend```
  * Open commit window in IntelliJ and tick the "Amend commit" box
* Remove previous commit
  * ```git reset HEAD~```
  * ```git reset HEAD~2```
## Stash changes
You can stash changes for later if you wish to discard them at the moment, but easy access and reuse them again later
* Command line
    ```
    CHEATSHEET
    
    # To stash uncommited changes
    git stash   
   
    # To stash uncommited changes with a meaningful message
    git stash save "my message"
  
    # To view stashes
    git stash list
  
   # To re-apply changes from stash and remove them in your stash (by default will apply latest stash)
   git stash pop
   git stash pop stash@{2}
  
   # To re-apply changes from stash and keep them in your stash (by default will apply latest stash)
   git stash apply
   git stash apply stash@{2}
   
    # To view changes in stash
    git stash show
    git stash show -p
    git stash show stash@{2}
    ```
* IntelliJ
  * Top menu "Git" -> "Uncommitted changes" -> "Stash Changes"/"Unstash Changes"
  * Opens a windows for creating stashes or viewing existing stashes and applying them.
## Changelists
If there are files you do not wish to accidentally commit at the moment, but at the same time wish to keep unstashed in your local project
(for examples changes made in configuration files, that are needed locally, but you do not wish to commit at this point)
then you can add them to a different changelist.
* Open "Git" tab from your bottom menu
* Open "Local Changes"
* Right-click the area where you see a list of your changed files and choose "New Changelist"
* Give your changelist a name and drag and drop to move files between
* You can specify which changelist is the active one by right-clicking on it and choosing "Set active changelist"
* The active changelist is the one chosen by default while committing
* You can choose which changelist to commit, at the top of the commit window
## Ignore files
- Create a new file in directory ```files/file_3.txt```
- Open file .gitignore
  - Add a rule to ignore the newly created file
  - You need to find a suitable regex pattern to match the file(s) you want
https://git-scm.com/docs/gitignore
- Check your changelist
## Manage tags
Tags are references that point to specific commit in Git history. Tagging is generally used to capture a point in history that is used for a version release (i.e. v1.0.1).
* Create and push a new tag with your name
  * Command line
  ```
  git tag tagname
  git push --tags
  ```
  * IntelliJ
    * From bottom menu "Git" -> "Logs" -> right-click on the commit you wish to tag (your last commit) -> "New tag" -> enter name
    * Open git push window and tick "Push tags" at the bottom before pushing
* You can add additional information to tags when creating them. Read more here: https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-tag
## Merge branches
* Checkout ```develop```
* Merge your feature branch
  * Command line
  ```
   git merge your-branch
  ```
   * If there are no conflicts the default text editor will open for you to edit the commit message
   * If there are conflicts, you will need to resolve them before you can commit
   * You can resolve commits manually in your files (which can be slightly tedious) or use IntelliJ GUI (see below)
   * IntelliJ
     * Find your branch from "Local branches" -> "Merge your-branch into develop"
     * In case of conflicts you will see a message and/or IntelliJ will open a window to resolve merge conflicts
     * If the window isn't automatically opened, you can find it from the top menu "Git" -> "Resolve merge conflicts"
     * Sometimes it takes a few seconds before the option appears in the dropdown while IntelliJ processes the changes
* Your merge should not cause any conflicts so far, if you wish to try resolving a conflict, refer to task #13
* When conflicts are resolved push the merge commit
## History & blame
* Git history
  * You can view commit history by finding the "Git" tab in IntelliJ bottom menu and opening "Logs"
  * You can view changes and commits in a specific file or directory by right-clicking on file/dir -> "Git" -> "Show history"
* Local history
  * IntelliJ also records automatically snapshots of your local history, even if the changes are not committed, so you can return to a previous state that existed on your local machine
  * By default, local history is kept for 5 days
  * You can view local history for a specific file or directory by right-clicking on file/dir -> "Git" -> "Show history"
* Git blame
  * If you want to check who authored a specific file or change
  * In a file, right-click the area next to the file where you see line numbers and choose ["Annotate with git blame"](!https://pbs.twimg.com/media/E7KHDddXoAMVtPI.jpg)
  * By clicking the name on the line, you can open a window that shows the commit and changes that were made with it
## If we have time left then we can discuss:
* Rebasing https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase
* Remotes 
#
Thanks to Krõõt Grete Mänd for the workshop materials.
