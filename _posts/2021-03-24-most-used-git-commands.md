---
published: true
---
## Most used git commands

<div style="background: #000000; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #888888">    $ git config --global user.name &quot;Firstname Lastname&quot; // set your username</span>
<span style="color: #888888">    $ git config --global user.email &quot;name@example.com&quot; // set your email address</span>
<span style="color: #888888">    $ git init // Initialize a local git repository  </span>
<span style="color: #888888">    $ git status // check status</span>
<span style="color: #888888">    $ git add [filename] // add a file to staging area</span>
<span style="color: #888888">    $ git add -A // add all files to staging area </span>
<span style="color: #888888">    $ git add . // add all files to staging area </span>
<span style="color: #888888">    $ git commit -m &quot;message&quot; // add commit message</span>
<span style="color: #888888">    $ git remote add origin git@github.com:USERNAME/REPOSITORY.git // add a remote repository</span>
<span style="color: #888888">    $ git push -u origin [branch name] // push changes to remote repository</span>
<span style="color: #888888">    $ git pull origin [branch name] // pull changes from remote repository</span>
<span style="color: #888888">    $ git remote -v // list existing remotes</span>
<span style="color: #888888">    $ git remote set-url origin git@github.com:USERNAME/NEW_REPOSITORY.git // change remote repository</span>
<span style="color: #888888">    $ git branch // list branches </span>
<span style="color: #888888">    $ git branch -a	// list all branches (local and remote)</span>
<span style="color: #888888">    $ git branch [branch name]	// create new branch</span>
<span style="color: #888888">    $ git branch -d [branch name]	// delete branch</span>
<span style="color: #888888">    $ git push origin --delete [branch name]	// delete remote branch</span>
<span style="color: #888888">    $ git checkout -b [branch name]	// create new branch and switch to it</span>
<span style="color: #888888">    $ git branch -m [old branch name] [new branch name] // rename branch</span>
<span style="color: #888888">    $ git checkout [branch name] // switch to a branch</span>
<span style="color: #888888">    $ git checkout -- [filename] // discard changes to a file</span>
<span style="color: #888888">    $ git commit --amend -m &quot;New commit message.&quot; // changing last commit message. if the commit was already pushed to remote repository then you have to force push to update the remote repository. </span>
<span style="color: #888888">    $ git push --force [branch-name] // force push to update remote repository</span>
<span style="color: #888888">    $ git merge [branch-name] // merge a branch into current branch</span>
<span style="color: #888888">    $ git merge --continue // When a conflict occurs, this option can be used to finish the merge after resolving the conflicts and commiting changes</span>
<span style="color: #888888">    $ git merge --abort // When a conflict occurs, this option can be used to abort the merge and restore the project&#39;s state</span>
<span style="color: #888888">    $ git reset --hard HEAD^ // delete last commit from local repository. if the commit was already pushed in remote then you have to force push after this command.  use $ git push origin -f to force push to remote  </span>
<span style="color: #888888">    $ git reset --hard HEAD~2 // deletes last two commits.</span>
<span style="color: #888888">    $ git reset HEAD^ // uncommit the last commit, but keeps the changes</span>
</pre></div>