---
published: true
---
<!-- HTML generated using hilite.me --><div style="background: #202020; overflow:auto;width:auto;border:solid gray;border-width:.1em .1em .1em .8em;padding:.2em .6em;"><pre style="margin: 0; line-height: 125%"><span style="color: #cccccc">* Installing git</span>
<span style="color: #cccccc">$ sudo apt install git-all // Use this command if you’re on a Debian-based distribution, such as Ubuntu. For other operating system follow https://git-scm.com/book/en/v2/Getting-Started-Installing-Git</span>
<span style="color: #cccccc">$ git --version // check version</span>

<span style="color: #cccccc">* Set your username</span>
<span style="color: #cccccc">$ git config --global user.name &quot;Firstname Lastname&quot;</span>

<span style="color: #cccccc">* Set your email address</span>
<span style="color: #cccccc">$ git config --global user.email &quot;name@example.com&quot; </span>

<span style="color: #cccccc">* Initialize a local git repository </span>
<span style="color: #cccccc">$ git init  </span>

<span style="color: #cccccc">* Check status</span>
<span style="color: #cccccc">$ git status</span>

<span style="color: #cccccc">* Add a file to staging area</span>
<span style="color: #cccccc">$ git add [filename]</span>

<span style="color: #cccccc">* Add all files to staging area. Use any of the following two commands</span>
<span style="color: #cccccc">$ git add -A </span>
<span style="color: #cccccc">$ git add .</span>

<span style="color: #cccccc">* Add commit message</span>
<span style="color: #cccccc">$ git commit -m &quot;message&quot;</span>

<span style="color: #cccccc">* Add a remote repository</span>
<span style="color: #cccccc">$ git remote add origin git@github.com:USERNAME/REPOSITORY.git </span>

<span style="color: #cccccc">* Push changes to remote repository</span>
<span style="color: #cccccc">$ git push -u origin [branch name] </span>

<span style="color: #cccccc">* Pull changes from remote repository </span>
<span style="color: #cccccc">$ git pull origin [branch name] </span>

<span style="color: #cccccc">* List existing remotes    </span>
<span style="color: #cccccc">$ git remote -v</span>

<span style="color: #cccccc">* Change remote repository</span>
<span style="color: #cccccc">$ git remote set-url origin git@github.com:USERNAME/NEW_REPOSITORY.git </span>

<span style="color: #cccccc">* List branches    </span>
<span style="color: #cccccc">$ git branch </span>
<span style="color: #cccccc">$ git branch -a	// list all branches (local and remote)</span>

<span style="color: #cccccc">* Create new branch </span>
<span style="color: #cccccc">$ git branch [branch name]	</span>

<span style="color: #cccccc">* Delete a branch from local repository</span>
<span style="color: #cccccc">$ git branch -d [branch name]</span>

<span style="color: #cccccc">* Delete remote branch</span>
<span style="color: #cccccc">$ git push origin --delete [branch name]</span>

<span style="color: #cccccc">* Create new branch and switch to it</span>
<span style="color: #cccccc">$ git checkout -b [branch name]	</span>

<span style="color: #cccccc">* Rename branch</span>
<span style="color: #cccccc">$ git branch -m [old branch name] [new branch name] </span>

<span style="color: #cccccc">* Switch to a branch</span>
<span style="color: #cccccc">$ git checkout [branch name]</span>

<span style="color: #cccccc">* Discard changes to a file</span>
<span style="color: #cccccc">$ git checkout -- [filename]</span>

<span style="color: #cccccc">* Change last commit message </span>
<span style="color: #cccccc">$ git commit --amend -m &quot;New commit message.&quot;</span>

<span style="color: #cccccc">* Change last commit message if already pushed to remote</span>
<span style="color: #cccccc">$ git commit --amend -m &quot;New commit message.&quot;</span>
<span style="color: #cccccc">$ git push --force [branch-name] </span>

<span style="color: #cccccc">* Merge a branch into current branch</span>
<span style="color: #cccccc">$ git merge [branch-name]</span>

<span style="color: #cccccc">*  When a conflict occurs, this option can be used to finish the merge after resolving the conflicts</span>
<span style="color: #cccccc">$ git merge --continue</span>

<span style="color: #cccccc">* When a conflict occurs, this option can be used to abort the merge and restore the project&#39;s state</span>
<span style="color: #cccccc">$ git merge --abort </span>

<span style="color: #cccccc">* Delete last commit from remote repository</span>
<span style="color: #cccccc">$ git reset --hard HEAD^ </span>
<span style="color: #cccccc">$ git push origin -f</span>

<span style="color: #cccccc">* Delete last commit from local repository</span>
<span style="color: #cccccc">$ git reset --hard HEAD^ </span>

<span style="color: #cccccc">* Delete last n commits.</span>
<span style="color: #cccccc">$ git reset --hard HEAD~n // n= 1,2,3 etc</span>

<span style="color: #cccccc">* Uncommit the last commit, but keeps the changes</span>
<span style="color: #cccccc">$ git reset HEAD^ </span>

<span style="color: #cccccc">* Stash </span>
<span style="color: #cccccc">$ git stash // git stash temporarily shelves (or stashes) changes you&#39;ve made to your working copy so you can work on something else, and then come back and re-apply them later on.</span>
<span style="color: #cccccc">$ git stash pop //  throws away the (topmost, by default) stash after applying it</span>
<span style="color: #cccccc">$ git stash clear // deletes all stash</span>

<span style="color: #cccccc">* Inspecting changes</span>
<span style="color: #cccccc">$ git diff</span>

<span style="color: #cccccc">* Viewing commit history</span>
<span style="color: #cccccc">$ git log</span>

<span style="color: #cccccc">* Rebase</span>
<span style="color: #cccccc">$ git rebase [branch name] // rebase a branch </span>
<span style="color: #cccccc">$ git rebase --continue // to finish a rebase after resolving conflicts</span>
<span style="color: #cccccc">$ git rebase --abort // to completely undo the rebase</span>

<span style="color: #cccccc">* Example Workflow to rebase master and feature/1 branch</span>
<span style="color: #cccccc">$ git checkout master</span>
<span style="color: #cccccc">$ git pull</span>
<span style="color: #cccccc">$ git checkout feature/1</span>
<span style="color: #cccccc">$ git rebase master</span>
<span style="color: #cccccc">$ git checkout master</span>
<span style="color: #cccccc">$ git rebase feature/1</span>
<span style="color: #cccccc">$ git push</span>
</pre></div>
