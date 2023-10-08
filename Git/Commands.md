**Git**

- [https://www.gitignore.io/](https://www.gitignore.io/)
	- git add
	
	- git add -A stages all changes
	- git add . stages new files and modifications, without deletions
	- git add -u stages modifications and deletions, without new files
	
	- git squash existing pushed branch -  below example of 4 commits
	
	- git checkout my_branch
	- git reset --soft HEAD~4
	- git commit
	- git push --force origin my_branch

- Find the most recent common ancestor of two branches

	- $ git merge-base branch2 branch3
	- 050dc022f3a65bdc78d97e2b1ac9b595a924c3f2

- how to properly configure github ssh keys on mac  
    [https://medium.com/@aklson_DS/how-to-properly-setup-your-github-repository-mac-version-3a8047b899e5](https://medium.com/@aklson_DS/how-to-properly-setup-your-github-repository-mac-version-3a8047b899e5)
- How to merge a branch

# Start a new feature

- git checkout -b new-feature master

# Edit some files

- git add <file>
- git commit -m "Start a feature"

## Edit some files

- git add <file>
- git commit -m "Finish a feature"

## Merge in the new-feature branch

- git checkout master
- git merge new-feature
- git branch -d new-feature

## How to delete commits from repository

- # First, check out the commit you wish to go back to (get sha-1 from git log)

- git reset --hard 9d3c3a0caa7f7b35ef15adb96fc80fcbb59ac72a

## Then do a forced update.

- git push origin +9d3c3a0caa7f7b35ef15adb96fc80fcbb59ac72a^:develop

## Push specific commit

- git push origin 9d3c3a0caa7f7b35ef15adb96fc80fcbb59ac72a:develop

# How to rebase  
    [https://stackoverflow.com/questions/7929369/how-to-rebase-local-branch-onto-remote-master/18442755#18442755](https://stackoverflow.com/questions/7929369/how-to-rebase-local-branch-onto-remote-master/18442755#18442755)
- After committing changes to your branch, checkout master and pull it to get its latest changes from the repo:

- git checkout master
- git pull origin master

- Then checkout your branch and rebase your changes on master:

- git checkout RB
- git rebase master

- ...or last two commands in one line:

- git rebase master RB
- When trying to push back to origin/RB, you'll probably get an error; if you're the only one working on RB, you can force push:

- git push --force origin RB_
- ...or as follows if you have git configured appropriately:

- git push -f
- Create a branch with current changes  
    git checkout -b <branch_name>
- git add -u
- git commit -m "jira-id message"
- git push --set-upstream origin <branch_name>
- Create a branch from another commit  
    git branch <branch name> <commit hash>
- Cherry-pick from one repo to another  
    --> Below example is for cherry picking from "flexcore" to "ssoms"
- git fetch [git@git.flextrade.com](mailto:git@git.flextrade.com):flexcore/flexcore.git master && git cherry-pick af31a16e2d4a4b40bdc6fd88d98579fce29e20a1
- Once cherry pick is done, "git add" is run automatically so you won't see changes in "git status".