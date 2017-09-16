
#GIT


## A Short History of Git

Linus Torvalds and Linux development community together developed GIT. Some of the goals of git are as follows

- Speed
- Simple design
- Strong support for non-linear development (thousands of parallel branches)
- Fully distributed
- Able to handle large projects like the Linux kernel efficiently (speed and data size)

## Git Basics

- Other VCS stores data as changes to base version of each file
- Git stores data like a set of snapshots of a miniature filesystem
- Near every operation is local
- Everything in git is checksummed before its stored
- Git generally adds data


## Three states of Git

Git has three main states that your files can reside in: committed, modified, and staged.

- Committed means that the data is safely stored in your local database.
- Modified means that you have changed the file but have not committed it to your database yet.
- Staged means that you have marked a modified file in its current version to go into your next commit snapshot.

This leads us to the three main sections of a Git project: the Git directory, the working directory, and the staging area

- The Git directory is where Git stores the metadata and object database for your project. This is the most important part of Git, and it is what is copied when you clone a repository from another computer.
- The working directory is a single checkout of one version of the project.These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify.
- The staging area is a file, generally contained in your Git directory, that stores information about what will go into your next commit. It’s sometimes referred to as the “index”, but it’s also common to refer to it as the staging area.

The basic Git workflow goes something like this:
1. You modify files in your working directory.
2. You stage the files, adding snapshots of them to your staging area.
3. You do a commit, which takes the files as they are in the staging

## Git Commands - config

git config --system -l

git config --global -l

git config --list

git config user.name

git config core.editor

git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -nosession"

git help

git help config


## Git Basics Commands

cd proj-dir

git init

git add *

git add file_name

git clone https://github.com/kalyansmiles/datastructures

git clone https://github.com/kalyansmiles/datastructures target-dir

git status

git status -s

git status --short

cat .gitignore

git diff => what is changed but not staged

git diff --staged

git diff --cached

git commit

git commit -m 'Initial Project Version'

git commit -a -m 'Initial Project Version'

git commit --amend

git rm PROJECTS.md

git rm --cached PROJECTS.md

git rm log/\*.log

git rm \*~

git log

git log -p

git log -p -2

git log --stat

git log --pretty=oneline

git log --pretty=format:"%h - %an, %ar : %s"

git log --since=2.weeks

git reset HEAD CONTRIBUTING.md

git checkout -- CONTRIBUTING.md

git remote

git remote -v

git remote show origin

git remote add shortname url

git remote rename pb paul

git remote rm paul

git fetch shortname

git fetch origin

git push remote_name branch_name

git push origin master

git tag

git tag -l "v1.8.5*"

git tag -a v1.0.0 -m "my first tag v1.0.0"

git tag v1.0.1-lw

git show v1.0.0

git push origin v1.0.0

git push origin --tags

git checkout -b [branchname] [tagname]:

git checkout -b version2 v2.0.0

git config --global alias.co checkout

git config --global alias.br branch

git config --global alias.ci commit

git config --global alias.st status

git config --global alias.unstage 'reset HEAD --'

git config --global alias.last 'log -1 HEAD'



##Git Samples from Github

https://github.com/github/gitignore
