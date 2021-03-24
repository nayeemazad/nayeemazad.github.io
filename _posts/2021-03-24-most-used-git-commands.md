---
published: true
---
## Most used git commands
![git.jpeg]({{site.baseurl}}/_posts/git.jpeg)

    $ git config --global user.name "Firstname Lastname" // set your username
    $ git config --global user.email "name@example.com" // set your email address
    $ git init // Initialize a local git repository  
    $ git status // check status
    $ git add [filename] // add a file to staging area
    $ git add -A // add all files to staging area 
    $ git add . // add all files to staging area 
    $ git commit -m "message" // add commit message
    $ git remote add origin git@github.com:USERNAME/REPOSITORY.git // add a remote repository
    $ git push -u origin [branch name] // push changes to remote repository
    $ git pull origin [branch name] // pull changes from remote repository
    $ git remote -v // list existing remotes
    $ git remote set-url origin git@github.com:USERNAME/NEW_REPOSITORY.git // change remote repository
    $ git branch // list branches 
    $ git branch -a	// list all branches (local and remote)
    $ git branch [branch name]	// create new branch
    $ git branch -d [branch name]	// delete branch
    $ git push origin --delete [branch name]	// delete remote branch
    $ git checkout -b [branch name]	// create new branch and switch to it
    $ git branch -m [old branch name] [new branch name] // rename branch
    $ git checkout [branch name] // switch to a branch
    $ git checkout -- [filename] // discard changes to a file
    $ git commit --amend -m "New commit message." // changing last commit message. if the commit was already pushed to remote repository then you have to force push to update the remote repository. 
    $ git push --force [branch-name] // force push to update remote repository
    $ git merge [branch-name] // merge a branch into current branch
    $ git merge --continue // When a conflict occurs, this option can be used to finish the merge after resolving the conflicts and commiting changes
    $ git merge --abort // When a conflict occurs, this option can be used to abort the merge and restore the project's state
    $ git reset --hard HEAD^ // delete last commit from local repository. if the commit was already pushed in remote then you have to force push after this command.  use $ git push origin -f to force push to remote  
    $ git reset --hard HEAD~2 // deletes last two commits.
    $ git reset HEAD^ // uncommit the last commit, but keeps the changes
