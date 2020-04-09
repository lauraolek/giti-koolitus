# gitgut

## Useful links / theory

Understand the lingo of the stages:

<img src="https://www.jrebel.com/sites/rebel/files/blog-images/2016/02/GitHub-cheat-sheet-graphic-v1.jpg"/>

Cheat sheet: https://www.jrebel.com/blog/git-cheat-sheet

For practicing: https://learngitbranching.js.org/?demo

How to write a commit message: https://chris.beams.io/posts/git-commit/
 
#### Tools
The basic & (almost) all you really need: git bash

Decent GUI: tortoisegit

### Working on your code
#### Starting up 

Create the repository (following gitlab or github commands should be easy enough) or clone an existing one
    `git clone repository_address 
    ` 

If you're creating a repository with lots of external libraries (eg node_modules) 
or you're working with IDEs,
add a .gitignore file to keep big or user-specific files off the repository! 
Google for available .gitignore samples,  you'll need something like https://gist.github.com/chhh/4961200 for Java

You can also look into using code style settings to have consistent whitespaces for example. 

#### The basic commands

See files with local changes in the branch you're in:
    `git status`

Get changes from remote repository:
    `git pull` OR `git pull origin master`

Stage your changes (add what you want to commit):
    `git add .` OR `git add folder_or_file_name`
    
Commit your changes and add a meaningful message:
        `git commit -m "issue_0001 reasons for these changes"`
        
Push your changes to remote:
         `git push origin your_branch_name`     
         
#### Stuff you learn a bit later on
1. you don't ALWAYS need to use the longer command on command line
1. `git commit -am message` combines `git add .` + `git commit -m`, one-word message doesn't require `""`
1. commit messages matter! https://chris.beams.io/posts/git-commit/
1. git commit --amend 
1. using git with ssh
1. `git tag` to remember your releases by
1. `git stash`
1. git history is not necessarily the truth
#### Branches

(Especially useful when using the master branch + feature branches approach)

1. Move to master (or any other branch)

    `
    git switch master
    ` OR     `
             git checkout master
             `

1. Create new branch (based on the branch you're in). You will be switched to it automatically.

    `
    git checkout -b 0001_new_feature
    `

1. Add, commit, push*, etc as you would normally. NB! Switching between branches with uncommitted changes is bothersome 
if not straight up impossible. If you really don't want to commit, look into GIT STASH to keep the changes or GIT RESET
to discard them https://docs.gitlab.com/ee/topics/git/numerous_undo_possibilities_in_git/#undo-local-changes.  

    `
    git checkout -b 0001_new_feature
    `
    
    * If you're pushing your branch for the first time, you will see the simple `git push origin 0001_new_feature` (or `git push`) 
    won't work. Copy-paste (ctrl+insert, shift+insert) the command printed out in command line after you tried
    one of those, or use `git push -u origin 0001_new_feature`
    
##### Merging the feature branch into master
If you want to merge your changes to master, the easiest way is to first merge master back into 
your feature branch and solving any conflicts locally before making a pull/merge request into master!

1. Make sure you have the latest version of master (git fetch/pull master)

1. On your feature branch, use `git merge master` to merge updates from master into your feature branch.
    If this results in conflicts, resolve them in your code and stage the changes (git add).
    When done, commit the merge with `git commit` and use the generated message (if it opens in VIM, learn how to quit VIM).
    
1. Push the updated feature branch and go online to create the pull request (merge request).
    1. If you've had several commits in this branch, update the title of your request to reflect what you've been trying to achieve.  
    1. Use the "squash commits" option to keep your master history easier to read.
    1. If it's a generic feature branch, use the "delete after merging" option. You don't need clutter in your life

1. Review the code differences before merging! Also, if the merge request cannot be merged due to conflicts, 
resolve them locally and push again. Attempting to resolve these changes online can have unforeseen consequences :))))
    1. If  you care about code quality, make a checklist for code review
    1. Have another developer do the merging

    
## Tasks
 1. Unstage local changes (undo “git add”)
 1. Undo commits:
    1. Make a local commit (don’t push) and undo it.
    1. Redo the commit and push it to remote.
    1. Undo the remote commit.
     
     Soft hint: 
     > there are two ways to go about it, one to preserve history, another to overwrite
 
     Hint 2: 
     > one is git revert, another git reset
     
 1. Stash changes: Let’s suppose you need to switch from an incomplete task to a more urgent one. Make some local changes and stash them for an indefinite amount of time (add a good stash message). Then look at your stash list and unstash.
     
 1. Learn conflicts
     1. Create a merge conflict.     Hint:
     
    > create a new branch based on master, change same parts of the new branch and the master branch, push both changes to remote, then try to merge into master

    1. Solve the merge conflict (LOCALLY)
