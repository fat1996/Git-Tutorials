Based on the video tutorials by Corey Schafer & stuff I learned at work!
Git is a distributed vcs, unlike centralized ones like svn or perforce.
central is located at 1 place. if this gets corrupted or damaged, you better pray there's a backup somewhere.
distributed: everyone has a local repo. your local repo has all the info the remote repo has.
its like every developer has a copy of the same repo.
2 scenarios we can start out with:
1. there's a local project you have on your computer that you want to start tracking
2. there's a remote repo you want to start tracking(eg if you're collabing with friends or work)

scenario 1:
1. navigate into the folder you want to start tracking.
2. so for eg, create a folder on your desktop. open git bash. navigate into it.
3. type "git init". this will initialize a git repo within this folder.
4. if you want to create some personal files with sensitive data that you don't want shared with other people, create a .gitignore file.
5. simply type "touch .gitignore". this is a simple textfile.
6. open this file now, and add the file names you want ignored. these files should start with "." for eg .ignorethisfile
7. add .ignorethisfile to the .gitignore file.
8. once you add files to the .gitignore file, you will no longer see them once you run "git status"

so there's 3 stages in git:
1. the working dir - this is where you start working. so any files you create, make changes to start off in this area. if you run git status, you'll see files in the working dir in red.
2. the staging area - files that have been added using the "git add" command will show up in green.
3. the .git dir (final stage)

once files are in the staging area, they can be committed.
to remove a file from the staging area, type "git reset filename"
if you run git status now, this file should show up in red instead of green.

to commit your changes from the staging area to the .git repo:
type "git commit -m commitmsg"
now, if you type git status, it'll say that the working tree is clean, which basically means that everything that was in the working dir has been committed.

"git log" command: get a list of commits you've made.

now, we want to create a remote repo of this folder meaning you want to see this repo is the list of repo's in your github profile.
1. create a new repo in your github profile. it'll ask you for a repo name, description etc.
2. type "git remote add origin URL-of-the-remote-repo"
3. git push -u origin master
^you don't need to memorize these instructions. these will be displayed as soon as you create the remote repo from your github profile.
4. refresh, and you should be able to see the files you committed!

If you haven't created any branches, and you've made changes to your files, do
1. run "git status" to check what files have been changed.
2. git add filename
3. git commit -m commitmsg
4. git push origin HEAD
5. your changes should be reflected in the remote git repo!
if you want to stop tracking this with git, type "rm rf .git"
run "git status" to see the status of your files i.e which have been committed etc.


2nd scenario: cloning a remote(i.e existing) repo. most likely, this is what you'll do if you're at work.
1. clone the repo. git clone URL-of-the-remote-repo destination (git clone url-of-remote-repo destinationURL)
alternatively, you could simply navigate to the dir where you want to clone this repo, and then type "git clone URL-of-remoterepo"
2. since this most likely is a scenario where you're collaborating with a bunch of people, you'll need to create a branch to work on.
3. to see the existing list of branches, type "git branch -a". you'll see all the local and remote(that other people have created) branches.
4. to create a branch "git checkout -b branchname"
5. you'll switch over to this new branch.
6. make any changes. "git add filename" followed by "git commit -m commitmsg"
TODO: MIGHT NEED TO ADD SOME INSTRUCTIONS HERE(LIKE A GIT PULL TO PULL IN ANY NEW CHANGES. Will confirm from work).
7. git push origin branchname
8. open your remote repo in your browser. you should see the branch you created a light color. open a new pull request. add desc. add reviewer, if required. done!


once you've started contributing daily, you'll also need to bring in other people's changes before you add your own. here's what you do:
1. do a "git pull". this will pull in other people's changes from the remote.
2. follow the normal process to add and commit changes.
3. git push origin branchname
4. if it rejects your changes, do a force push i.e "git push origin branchname --force"
5. to make sure the correct files were added, always go see 5these commits reflected in your remote repo, under the branch you created.

how to merge branches:
1. switch from your branch to master. git checkout master
2. git pull origin master i.e you pull in all the changes others made before you add your changes.
3. git branch --merged ->allows you to view all the branches that have been merged with master so far.
4. git merge branchname
5. git push origin master
6. rerun "git branch --merged" to check the list of branches that've been merged so far. your recently merged branch should show up here.

deleting a branch:
1. git branch -d branchname ->this only deletes the branch from the local repo.
2. to delete the branch from the remote repo as well, run "git push origin --delete branchname"

how to discard local changes you've made and revert to the original condition of the repo:
1. run git status to make sure we've looking at the correct files
2. git checkout filename -> here the filename is the file you made changes to, but now want reverted.
3. run git status again, and you'll see that your working dir is clean
4. open file too and you'll see the original, uncorrupted file.

how to change the commit msg:
1. git commit --amend -m type-new-msg ->this saves you from having to create a new commit.

how to add a file to the previous commit instead of creating a new commit:
1. git commit --amend -> this will open an interactive mode. you'll be able to see your previous commit msg. you can change it, if you want. just do a :wq and you're set!
the new file you wanted to add is now part of your previous commit.

committing to the wrong branch for eg committed to master instead of your local branch:
how to move the commit you made on master branch to your local branch. we also want to restore the original state of our master branch.
1. this is called cherry-pick
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

to get rid of any untracked files(those that show up in red when you run git status):
run "git clean -df"
run "git status" and it should say that your working dir is clean.

stash command i.e you have some changes you don't wanna commit yet, or you want to revert back to where you started from , but don't wanna discard your changes cause you aern't sure if you'll need them in the future
1. you make some changes. but now you wanna check how the file looked before you made any changes to it.
2. run "git stash save msg-to-remind-you-what-you-did(in inverted commas)"
3. run git status and those changed files won't show up. if you check those files, you won't be able to see the changes you made.
4. to restore these changes, run "git stash list" -> this will show you the msgs you saved your stashes with.
there are 2 ways to doing this i.e restoring the changes:
a. git stash apply stash-name -> you get the stashname from running "git stash list". this will bring back your changes, but you'll still see the stash if you run "git stash list"
b. git stash pop -> changes brough back, and you won't see the stash now if you run "git stash list"

how to discard a stash from your stash list:
git stash drop stash-name

