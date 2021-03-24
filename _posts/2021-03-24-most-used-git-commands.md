---
published: true
---
<div style="background: #000000; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #888888">* Installing git</span>
<span style="color: #888888">$ sudo apt install git-all // Use this command if you’re on a Debian-based distribution, such as Ubuntu. For other operating system follow https://git-scm.com/book/en/v2/Getting-Started-Installing-Git</span>
<span style="color: #888888">$ git --version // check version</span>

<span style="color: #888888">* Set your username</span>
<span style="color: #888888">$ git config --global user.name &quot;Firstname Lastname&quot;</span>

<span style="color: #888888">* Set your email address</span>
<span style="color: #888888">$ git config --global user.email &quot;name@example.com&quot; </span>

<span style="color: #888888">* Initialize a local git repository </span>
<span style="color: #888888">$ git init  </span>

<span style="color: #888888">* Check status</span>
<span style="color: #888888">$ git status</span>

<span style="color: #888888">* Add a file to staging area</span>
<span style="color: #888888">$ git add [filename]</span>

<span style="color: #888888">* Add all files to staging area. Use any of the following two commands</span>
<span style="color: #888888">$ git add -A </span>
<span style="color: #888888">$ git add .</span>

<span style="color: #888888">* Add commit message</span>
<span style="color: #888888">$ git commit -m &quot;message&quot;</span>

<span style="color: #888888">* Add a remote repository</span>
<span style="color: #888888">$ git remote add origin git@github.com:USERNAME/REPOSITORY.git </span>

<span style="color: #888888">* Push changes to remote repository</span>
<span style="color: #888888">$ git push -u origin [branch name] </span>

<span style="color: #888888">* Pull changes from remote repository </span>
<span style="color: #888888">$ git pull origin [branch name] </span>

<span style="color: #888888">* List existing remotes    </span>
<span style="color: #888888">$ git remote -v</span>

<span style="color: #888888">* Change remote repository</span>
<span style="color: #888888">$ git remote set-url origin git@github.com:USERNAME/NEW_REPOSITORY.git </span>

<span style="color: #888888">* List branches    </span>
<span style="color: #888888">$ git branch </span>
<span style="color: #888888">$ git branch -a	// list all branches (local and remote)</span>

<span style="color: #888888">* Create new branch </span>
<span style="color: #888888">$ git branch [branch name]	</span>

<span style="color: #888888">* Delete a branch from local repository</span>
<span style="color: #888888">$ git branch -d [branch name]</span>

<span style="color: #888888">* Delete remote branch</span>
<span style="color: #888888">$ git push origin --delete [branch name]</span>

<span style="color: #888888">* Create new branch and switch to it</span>
<span style="color: #888888">$ git checkout -b [branch name]	</span>

<span style="color: #888888">* Rename branch</span>
<span style="color: #888888">$ git branch -m [old branch name] [new branch name] </span>

<span style="color: #888888">* Switch to a branch</span>
<span style="color: #888888">$ git checkout [branch name]</span>

<span style="color: #888888">* Discard changes to a file</span>
<span style="color: #888888">$ git checkout -- [filename]</span>

<span style="color: #888888">* Change last commit message </span>
<span style="color: #888888">$ git commit --amend -m &quot;New commit message.&quot;</span>

<span style="color: #888888">* Change last commit message if already pushed to remote</span>
<span style="color: #888888">$ git commit --amend -m &quot;New commit message.&quot;</span>
<span style="color: #888888">$ git push --force [branch-name] </span>

<span style="color: #888888">* Merge a branch into current branch</span>
<span style="color: #888888">$ git merge [branch-name]</span>

<span style="color: #888888">*  When a conflict occurs, this option can be used to finish the merge after resolving the conflicts</span>
<span style="color: #888888">$ git merge --continue</span>

<span style="color: #888888">* When a conflict occurs, this option can be used to abort the merge and restore the project&#39;s state</span>
<span style="color: #888888">$ git merge --abort </span>

<span style="color: #888888">* Delete last commit from remote repository</span>
<span style="color: #888888">$ git reset --hard HEAD^ </span>
<span style="color: #888888">$ git push origin -f</span>

<span style="color: #888888">* Delete last commit from local repository</span>
<span style="color: #888888">$ git reset --hard HEAD^ </span>

<span style="color: #888888">* Delete last n commits.</span>
<span style="color: #888888">$ git reset --hard HEAD~n // n= 1,2,3 etc</span>

<span style="color: #888888">* Uncommit the last commit, but keeps the changes</span>
<span style="color: #888888">$ git reset HEAD^ </span>

<span style="color: #888888">* Stash </span>
<span style="color: #888888">$ git stash // git stash temporarily shelves (or stashes) changes you&#39;ve made to your working copy so you can work on something else, and then come back and re-apply them later on.</span>
<span style="color: #888888">$ git stash pop //  throws away the (topmost, by default) stash after applying it</span>
<span style="color: #888888">$ git stash clear // deletes all stash</span>

<span style="color: #888888">* Inspecting changes</span>
<span style="color: #888888">$ git diff</span>

<span style="color: #888888">* Viewing commit history</span>
<span style="color: #888888">$ git log</span>

<span style="color: #888888">* Rebase</span>
<span style="color: #888888">$ git rebase [branch name] // rebase a branch </span>
<span style="color: #888888">$ git rebase --continue // to finish a rebase after resolving conflicts</span>
<span style="color: #888888">$ git rebase --abort // to completely undo the rebase</span>

<span style="color: #888888">* Example Workflow to rebase master and feature/1 branch</span>
<span style="color: #888888">$ git checkout master</span>
<span style="color: #888888">$ git pull</span>
<span style="color: #888888">$ git checkout feature/1</span>
<span style="color: #888888">$ git rebase master</span>
<span style="color: #888888">$ git checkout master</span>
<span style="color: #888888">$ git rebase feature/1</span>
<span style="color: #888888">$ git push</span>
</pre></div>
