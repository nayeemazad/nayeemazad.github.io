---
published: true
---
## Set your username
	$ git config --global user.name "Firstname Lastname"

## Set your email address
    $ git config --global user.email "name@example.com" 

## Initialize a local git repository 
    $ git init  

## Check status
	$ git status

## Add a file to staging area
	$ git add [filename]

## Add all files to staging area. Use any of the following two commands
	$ git add -A 
    $ git add .

## Add commit message
	$ git commit -m "message"

## Add a remote repository
    $ git remote add origin git@github.com:USERNAME/REPOSITORY.git 

## Push changes to remote repository
	$ git push -u origin [branch name] 

## Pull changes from remote repository 
	$ git pull origin [branch name] 

## List existing remotes    
	$ git remote -v

## Change remote repository
    $ git remote set-url origin git@github.com:USERNAME/NEW_REPOSITORY.git 

## List branches    
	$ git branch 
    $ git branch -a	// list all branches (local and remote)

## Create new branch 
	$ git branch [branch name]	

## Delete a branch from local repository
	$ git branch -d [branch name]

## Delete remote branch
    $ git push origin --delete [branch name]

## Create new branch and switch to it
    $ git checkout -b [branch name]	

## Rename branch
    $ git branch -m [old branch name] [new branch name] 

## Switch to a branch
	$ git checkout [branch name]

## Discard changes to a file
    $ git checkout -- [filename]

## Change last commit message 
    $ git commit --amend -m "New commit message."

## Change last commit message if already pushed to remote
    $ git commit --amend -m "New commit message."
    $ git push --force [branch-name] 

## Merge a branch into current branch
    $ git merge [branch-name]

##  When a conflict occurs, this option can be used to finish the merge after resolving the conflicts
    $ git merge --continue

## When a conflict occurs, this option can be used to abort the merge and restore the project's state
    $ git merge --abort 

## Delete last commit from remote repository
    $ git reset --hard HEAD^ 
    $ git push origin -f

## Delete last commit from local repository
	$ git reset --hard HEAD^ 

## Delete last n commits.
    $ git reset --hard HEAD~n // n= 1,2,3 etc

## Uncommit the last commit, but keeps the changes
    $ git reset HEAD^ 

## Stash 
	$ git stash // git stash temporarily shelves (or stashes) changes you've made to your working copy so you can work on something else, and then come back and re-apply them later on.
    $ git stash pop //  throws away the (topmost, by default) stash after applying it
    $ git stash clear // deletes all stash

## Inspecting changes
	$ git diff

## Viewing commit history
	$ git log

## Rebase
	$ git rebase [branch name] // rebase a branch 
    $ git rebase -- continue // to finish a rebase after resolving conflicts
    $ git rebase -- abort // to completely undo the rebase
    
## Example Workflow to rebase master and feature/1 branch
	$ git checkout master
    $ git pull
    $ git checkout feature/1
    $ git rebase master
    $ git checkout master
    $ git rebase feature/1
    $ git push