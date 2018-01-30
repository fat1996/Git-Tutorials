Based on the video tutorials by Corey Schafer & stuff I learned at work!

Some useful terms
1.	Checksum:
A checksum is basically the result of an algorithm called the cryptographic hash function that is used to determine if your file is genuine or not. 
Say you’re downloading a file. Once its downloaded, you want to make sure if you downloaded it successfully or whether some parts of it were left behind or whether it has been maliciously tampered with. If the source that you downloaded your file from provides you with a checksum of the data on the website, you can use a checksum calculator (available online) to determine the checksum for the data you downloaded and compare the 2 values. If they’re the same, your download was successful in the sense that nothing was tampered with or modified. If not, something went wrong (these reasons don’t necessarily have to be malicious. It could be something as trivial as losing your internet connection while you were downloading).

2.	Version Control:
The major difference between git and other version control systems is how they keep track of any changes made in a certain directory/project. Other systems such as subversion (SVN) or perforce think of the changes made per file. They basically track the changes made to files over a certain period. On the contrary, git thinks of its files as ‘screenshots’. Every time you commit some changes, it takes a ‘screenshot’ of all the files in your directory. 
Git has ‘integrity’ in the sense that it stores everything using its checksum and then that piece of data is referred to using that checksum. This ensures that git is aware of every minuscule change you make. Git stores everything using its hash value, so if you happen to see a long sequence of seemingly random strings and numbers, don’t be surprised. 
Git is a distributed VCS, unlike centralized ones like SVN or perforce.
Centralized means data is located at one place. If this gets corrupted or damaged, you better pray there's a backup somewhere.
Distributed: everyone has a local repository. Your local repo has all the data the remote repo has. It's like every developer has a copy of the same repo.

3 main sections of a git project:

	1. Git directory 
	2. Working tree
	3. Staging area

<b>Basic git workflow:</b>

	You make a change in your working directory. The files are then staged, so snapshots of them are created and stored in the staging area. Once you do a commit, these snapshots are taken and stored in your git directory. 

<b>Using git:</b>

	While there are GUI’s that you could use to avoid using the terminal, I would strongly advise against them. Not that there’s anything wrong with them, just that using the terminal is an incredibly powerful tool to have, and it’ll help you gain a better and deeper understanding of how things work in git. 

<b>Squashing Commits:</b>

	Multiple commits, do you want to either squash them together or delete some of them. Type ‘git rebase -i HEAD~x’ where x is the number of commits you wish to view. This will open a file where you’ll be presented with multiple options (where you can pick which commits to squash together, which to delete, if you want to change the commit message etc). Once this is successfully done, type ‘git push –force origin HEAD’.

<b>Removing Files:</b>

	Simply removing the file from your working directory: ‘git rm filename’
 
<b>Moving Files:</b>

	If you want to rename a file, simply type ‘git mv older-version newer-version’

<b>Viewing the commit history:</b>

	Type ‘git log’. You’ll see a list of commits in reverse chronological order(recent most commit first). Each commit is accompanied by its checksum, author name, email, date and the commit message.

2 scenarios we can start out with:

	1. There's a local project you have on your computer that you want to start tracking.
	2. There's a remote repo you want to start tracking (e.g. if you're collaborating with friends or for work)

<b>Scenario 1:</b>

	1. navigate into the folder you want to start tracking.
	2. so for e.g., create a folder on your desktop. open git bash. navigate into it.
	3. type "git init". this will initialize a git repo within this folder.
	4. if you want to create some personal files with sensitive data that you don't want shared with other people, create a .gitignore file.
	5. simply type "touch .gitignore". this is a simple textfile.
	6. open this file now, and add the file names you want ignored. these files should start with "." for eg .ignorethisfile
	7. add .ignorethisfile to the .gitignore file.
	8. once you add files to the .gitignore file, you will no longer see them once you run "git status"

<b>So there's 3 stages in git:</b>

	1. The working dir - this is where you start working. so any files you create, make changes to start off in this area. if you run git status, you'll see files in the working dir in red.
	2. The staging area - files that have been added using the "git add" command will show up in green.
	once files are in the staging area, they can be committed.
	to remove a file from the staging area, type "git reset filename"
	if you run git status now, this file should show up in red instead of green.
	3. The .git dir (final stage)

<b>To commit your changes from the staging area to the .git repo:</b>
type "git commit -m commitmsg"
now, if you type git status, it'll say that the working tree is clean, which basically means that everything that was in the working dir has been committed.

<b>Now, we want to create a remote repo of this folder meaning you want to see this repo is the list of repo's in your github profile.</b>

	1. create a new repo in your github profile. it'll ask you for a repo name, description etc.
	2. type "git remote add origin URL-of-the-remote-repo"
	3. git push -u origin master
	^you don't need to memorize these instructions. these will be displayed as soon as you create the remote repo from your github profile.
	4. refresh, and you should be able to see the files you committed!

<b>If you haven't created any branches, and you've made changes to your files, do</b>

	1. run "git status" to check what files have been changed.
	2. git add filename
	3. git commit -m commitmsg
	4. git push origin HEAD
	5. your changes should be reflected in the remote git repo!
	if you want to stop tracking this with git, type "rm rf .git"

<b>2nd scenario: cloning a remote (i.e existing) repo. most likely, this is what you'll do if you're at work.</b>

	1. clone the repo. git clone URL-of-the-remote-repo destination (git clone url-of-remote-repo destinationURL)
	alternatively, you could simply navigate to the dir where you want to clone this repo, and then type "git clone URL-of-remoterepo"
	2. since this most likely is a scenario where you're collaborating with a bunch of people, you'll need to create a branch to work on.
	3. to see the existing list of branches, type "git branch -a". you'll see all the local and remote(that other people have created) branches.
	4. to create a branch "git checkout -b branchname"
	5. you'll switch over to this new branch.
	6. make any changes. "git add filename" followed by "git commit -m commitmsg"
	7. git push origin branchname
	8. open your remote repo in your browser. you should see the branch you created a light color. open a new pull request. add desc. add reviewer, if required. done!

<b>once you've started contributing daily, you'll also need to bring in other people's changes before you add your own. here's what you do(one's recommended, the other isn't):</b>

Recommended:

	1. git checkout master 
	2. git fetch upstream          
	3. git rebase upstream/master  
	4. git push origin master      

Not recommended:

	1. do a "git pull". this will pull in other people's changes from the remote.
	2. follow the normal process to add and commit changes.
	3. git push origin branchname
	4. if it rejects your changes, do a force push i.e "git push origin branchname --force"
	5. to make sure the correct files were added, always go see these commits reflected in your remote repo, under the branch you created.

<b>how to merge branches:</b>

	1. switch from your branch to master. git checkout master
	2. git pull origin master i.e you pull in all the changes others made before you add your changes.
	3. git branch --merged ->allows you to view all the branches that have been merged with master so far.
	4. git merge branchname
	5. git push origin master
	6. rerun "git branch --merged" to check the list of branches that've been merged so far. your recently merged branch should show up here.

<b>deleting a branch:</b>

	1. git branch -d branchname ->this only deletes the branch from the local repo.
	2. to delete the branch from the remote repo as well, run "git push origin --delete branchname"

<b>how to discard local changes you've made and revert to the original condition of the repo:</b>

	1. run git status to make sure we've looking at the correct files
	2. git checkout filename -> here the filename is the file you made changes to, but now want reverted.
	3. run git status again, and you'll see that your working dir is clean
	4. open file too and you'll see the original, uncorrupted file.

<b>how to change the commit msg:</b>

	1. git commit --amend -m type-new-msg ->this saves you from having to create a new commit.

<b>how to add a file to the previous commit instead of creating a new commit:</b>

	1. git commit --amend -> this will open an interactive mode. you'll be able to see your previous commit msg. you can change it, if you want. just do a :wq and you're set!
	the new file you wanted to add is now part of your previous commit.

<b>committing to the wrong branch for eg committed to master instead of your local branch:</b>

	how to move the commit you made on master branch to your local branch. we also want to restore the original state of our master branch.
	1. this is called cherry-pick (to abort a cherrypick, type "git cherry-pick --abort")
	2. while remaining on the branch where you accidentally committed, run a git log. this will show you the list of commits you made, including the one you want to move. copy the hash(you don't need the entire thing. a couple of chars will do)
	3. switch to the branch you want to add the commit to. git checkout -b branchname
	4. on this branch, run "git cherry-pick hash-value-you-copied"
	5. run git log to ensure the commit has been transferred.
	6. now, we want to delete this commit from where we accidentally committed it in the beginning. switch to that branch now.
	there are 3 kinds of reset: soft, mixed, hard
	say you want to get rid of the last 2 commits you made.
	run a git log.
	ignore the last 2 commits you made.
	copy the hash of the 3rd last commit you made. you want to restore the state of your files to how it was when you made the 3rd last commit i.e get rid of the last 2 commits.
	a. git reset --hard hash-you-copied ->this will discard all the changes you made in your previous 2 commits that you want discarded. you'll never be able to see those changes again.
	b. git reset --soft hash-you-copied ->this will set you back to the commit you specified, but it won't get rid of your changes. those changed files will still be in the staging area.(if you run a git status, you'll see them in green)
	c. git reset hash-you-copied ->this is the default setting(mixed). same as above, but the changes will be in the working dir, instead of the staging dir.(will show up in red if you run git status)
	

<b>to get rid of any untracked files(those that show up in red when you run git status):</b>

	run "git clean -df"
	run "git status" and it should say that your working dir is clean.

<b>stash command</b> 

	i.e you have some changes you don't wanna commit yet, or you want to revert back to where you started from , but don't wanna discard your changes cause you aern't sure if you'll need them in the future
	1. you make some changes. but now you wanna check how the file looked before you made any changes to it.
	2. run "git stash save msg-to-remind-you-what-you-did(in inverted commas)"
	3. run git status and those changed files won't show up. if you check those files, you won't be able to see the changes you made.
	4. to restore these changes, run "git stash list" -> this will show you the msgs you saved your stashes with.
	there are 2 ways to doing this i.e restoring the changes:
	a. git stash apply stash-name -> you get the stashname from running "git stash list". this will bring back your changes, but you'll still see the stash if you run "git stash list"
	b. git stash pop -> changes brough back, and you won't see the stash now if you run "git stash list"

<b>how to discard a stash from your stash list:</b>

	git stash drop stash-name
	
<b>Deleting a specific commit</b>

2 possible scenarios:

	1. you've made the commit but you haven't pushed it yet.
	git rebase -p --onto SHA^ SHA
	where SHA is substituted with the hash ID from the git log. 
	2. you've pushed the commit to remote.
	git rebase -p --onto SHA^ SHA
	same as above, only this time you need to push this deletion of commit to your remote. Type
	git push origin +master
	The + is necessary.

<b>Setting up your email address(useful if you have multiple github profiles e.g work vs personal and you want to contribute to both simultaneously)</b>

open git bash in the dir you're making your changes in. Type
git config user.email "email-address"

reverting a single file that hasn't been committed yet:
https://www.norbauer.com/rails-consulting/notes/git-revert-reset-a-single-file
git checkout filename
if you made changes to a file that you <b>haven't committed</b> yet, type the above mentioned command and it will revert back to its original state.


<b>SVN:</b>
For working on every new jira issue, create a new branch.
But 1st, always update your local repo.
If you see red ! marks, delet those files, and then do an svn update.
Proceed when everything has green ticks.
To create a new branch, right click and click on branch/tag.
Done!
But now we need to get that branch in our local repo. Do this with a git checkout. Your branch will be created (the entire folder). Make any changes you need in that folder and nowhere else.
Once you make changes in your branch, you want to be able to view them everywhere. Commit everytime you’re done making changes through ‘svn commit’. This will update your branch on the local server and you’ll be able to view any changes you made everywhere.

