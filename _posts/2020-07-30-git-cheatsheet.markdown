---
layout: post
title:  "Git Cheatsheet"
date:   2020-07-30 12:20:00 -0400
categories: IT reference
---

# Download  
[https://git-scm.com/download](https://git-scm.com/download)  

# Common Commands  
`git init` Create a repository  
`git status` compare working directory, staging area, and current branch  
`git add` add changes to the staging area  
`git commit` commit changes from staging area to current branch  
`git log` show history of project commits  

# Commit messages  
Default editor is vim  
`git commit -m "message"` will add a comment explaining the commit  
Commit messages should be clear, accurate, and concise  
[https://chris.beams.io/posts/git-commit/](https://chris.beams.io/posts/git-commit/)  

# Branches  
A branch is a reference to a commit. When you commit on a given branch, that branch gets updated.  
'HEAD' means current branch  
`git branch -c branch_name` Creates a new branch  
`git checkout branch_name` Switches to that branch  
`git branch` Lists branches and marks the current one  
`git checkout -b branch_name` create a branch, then checkout  
`git stash` stash changes from a working directory  
`git stash list` list stashes  
`git stash pop` apply stashed changes to a working directory  

# Log, Show, and Diff  
`git log --author <string>` Shows commits with matching author  
`git log --since <date>` Shows commits since a given date  
`git log --until <date>` Shows commits prior to a given date  
`git log --oneline` Shows one commit per line  
`git log --graph` Show graph view of commits  
`git show <commit ID>` Shows the contents of a commit  
`git diff --cached` Difference between staging area and HEAD  
`git diff --cached <commit>` Difference between staging area and commit  
`git diff <commit1>..commit2>` Difference between commits.  
Show and Diff are powerful commands with many options  

# Git Remotes  
A remote repo is one hosted somewhere other than our local machine. We can add remotes with `git remote add`, and set up *tracking branches* to track differences between our local and remote repositories.

We push to remotes with `git push`, and fetch from them with `git fetch`. We can also fetch and merge in one set with `git pull`.

# Git Merge  
Merging means to bring changes from one branch into another.  
`git merge` Merge changes from different branches  
fast-forward - type of merge when the target branch was branched from the current one, and there are no new changes to the current branch since then.  
automatic merge - type of merge when the two histories have diverged, but git is able to reconcile them into one set of changes. This creates a new commit on the current branch.  

# Merge Conflicts  
`git log --oneline --all --graph`  

To resolve:
1. Edit the files to resolve the conflict.
2. Add changes to the staging area with `git add`
3. Commit changes with `git commit`

# Storing Credentials
```
$ git config credential.helper store

$ git push https://github.com/owner/repo.git

Username for 'https://github.com': <USERNAME>

Password for 'https://USERNAME@github.com': <PASSWORD>
```
