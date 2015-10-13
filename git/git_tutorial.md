# Git tutorial

## Summary 

* [Introducion](#introduction)
* [Basics and most useful commands](#basics-and-most-useful-commands)
* [Add and Commit files](#add-and-commit-files)
* [Logs and status](#logs-and-status)
* [Configuration](#configuration)
* [Branch Tag and Merging](#branch-tag-and-merging)
* [Diff](#diff)
* [reset and change commit](#reset-and-change-commit)
* [Remote repository](#remote-repository)
* [Useful aliases](#useful-aliases)
* [Useful links](#useful-links )

## Introduction 

### Basics of git 

Git is a version control system allowing you to collaborate on a project.

Git works similar to a classic version control system but inserts another layer, the index, between the working directory and the repository to stage. 

When you manage your code with Git, you edit in your working directory, accumulate changes in your index, and commit whatever has amassed in the index as a single changeset.

You can think of Git’s index as a set of intended or prospective modifications. You add, remove, move, or repeatedly edit files right up to the culminating commit, which actualizes the accumulated changes in the repository. Most of the critical work actually precedes the commit step.

Remember, a commit is a two-step process: stage your changes and commit the changes. An alteration found in the working directory but not in the index isn’t staged and thus can’t be committed.

With Git, sharing work between repositories happens via operations called “push” and “pull”: you pull changes from a remote repository and push changes to it. 

To work on a project, you “clone” it from an existing repository, possibly over a network via protocols such as HTTP and SSH. Your clone is a full copy of the original, including all project history, completely functional on its own.Your new repository does retain a reference to the original one, called a “remote.” 

### Quick git Dictionnary

* *index* : the staged area, it is the place where you acumulate your change before commiting 
* A commit is used to record changes to a repository.
* *staged* : Files are ready to be committed.
* *unstaged* : Files with changes that have not been prepared to be commited.
* *untracked* : Files aren't tracked by Git yet. This usually indicates a newly created file.
* *deleted* :  File has been deleted and is waiting to be removed from Git.
* *HEAD* : your last commit 
* *remote* : the remote repository is the cloud repo (on github) where you are going to push and pull code. 


## Basics and most useful commands

Set up you local repo 

	$ git : To see all the command type
	$ git init : to initiate a git project ( located with all github  files in a. .git/ folder ) 

A commit is a two step process, you have to stage the file and after commit 

	$ git add file
	$ git add .: add all the files 
	$ git commmit file -m "your message"

Info and logs 

	$ git status : monitor the state between the repository and the working directory
	$ git log : look at the history of all the commits

Add a remote repository  

	$ git remote add remote <name> <url of the remote> : add a remote repository to your project 
	$ git remote -v : check the list of your remote 

Push an pull to the repo 

	 $ git push <repo_name> <local branch> : this will updarte the local branch in the repo or create it if necessary
	 $ git pull <repo_name> <remote branch> : pull fetch the data and do a fast-forward merging 


### Add and Commit files 
A commit is a two step process, you have to stage the file and after commit 

	$ git add <filename>
	$ git commmit <filename> -m "your message"

More detaillded command 

	$ git add -A : add all file from the working directory to the index 
	$ git commit –m or git commit  --message : standard hyphens abbreviation 
	$ git commit –m “first commit” : do your first commit 
	$ git commit –all: staged all unstaged files 
	$ git commit <filename> –m “message” : one step process to add a file and commit it 
	$ git ls-files –stage : more detailed than git commit 
	$ git blame –L 100 –n 35 : look at who modified each line of code and when –L to sepecify starting line n for the number of lines 
	$ git bisect start : start a binary research to find a bug 

the user specify if the commit is good or bad by typing git bisect good or git bisect bad.

	$ git reset file : unstaged a file 
	$ git rm file : remove from working directory and index 


## Logs and status

	$ git status 

You can pass multiple options for logs, type `$ git log` to see all options

	$ git log --summary 
	$ git log --pretty=oneline
	$ git log --pretty=oneline --max-count=2
	$ git log --pretty=oneline --since='5 minutes ago'
	$ git log --pretty=oneline --author=<your name>
	$ git log --pretty=oneline --all

Nice format 

	$ git log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short


## Configuration 

###  Global configuration 

	$ git config --global user.name "Eric Fourrier"
	$ git config --global  user.email efourrier@lendingclub.com
	$ git config --global credential.helper cache (store password in cache)

### Per project configuration 

	$ git config  user.name "your name"
	$ git config user.email "your email"
	$ git config –l : look at your configuration 

### Show commits and file in the tree 
	$ git log : show the history of commits

## Branch Tag and Merging 

### Branch and Tag 

* Each branch have a name, you should choose explicit name. 
* The default branch is called master.

Basics of branching

	$ git branch : list all the branch on local 
	$ git branch --all : list all the branch on local and remote
	$ git branch -d : deleting a branch 
	$ git show-branch : more detailed output 
	$ git checkout <branch_name> : go to branch_name
	$ git branch <branch_name> : create branch_name
	$ git checkout -b <branch_name> : create and go to branch_name
	$ git checkout v1.3.0 : you want to checkout to a tag or a commit


A tag serves to distinguish a particular commit by giving it a human-readable name

	$ git tag v1

### Merge and conflict 

Go to the branch that is going to another branch with `$ git checkout yourbranch`

	$ git merge <other_branch>

In case of a conflict, you have to fix yourself the conflict

	$ git add <conflict_file>
	$ git commit -m "Merged fixed conflict"


## Diff


### Designed with unix command diff 

	$ diff –u file1 file2 

the diff command is designed to look at the difference between two files in term of addition,deletion,insertion.

### Git commands 

	$ git diff : look at difference between working directory and index 
	$ git diff –cached : look at difference between index and Head 
	$ git diff HEAD look at difference between working directory and head 
	$ git commit1 commit2 : look at difference between commit1 and commit2 

## Reset and change commit


You have to be careful with all the different area of a file in the git work

	$ git checkout <filename> : undo local changes (berfore staging)
	$ git reset HEAD <filename> : undoing staged changes (before committing)
	$ git revert HEAD : undoing after commiting

Git reset is used when you did a mistake in a commit and you want go back. Be careful 
with the different type of reset in git.

	$ git reset HEAD^ : undo last commit ( default mixed type change HEAD and index _
	$ git reset --soft HEAD^ : only change HEAD not index 
	$ git reset –_hard : change working directory, index and HEAD (be careful)

Amend the Previous Commit, you want change the commit message

	$ git commit --amend -m "new message"



## Remote repository

	$ git remote add <short_name> <url>: add the remote with the alias short_name

Push and pull in a subdirectory

	$ git subtree push --prefix=path/to/file <remote_alias> <remote_branch>
	$ git subtree pull --prefix=path/to/file <remote_alias> <remote_branch>



## Useful aliases 

### Git aliases to put in .gitconfig
	[alias]
		co = checkout
		ci = commit
		st = status
		br = branch
		hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
		setup = ! "git init; git add .; git commit"
		type = cat-file -t
		dump = cat-file -p


### Shell aliases 
To be faster you can use the following saliases (bash_profile on mac, bashrc on VM linux):

	alias gs="git status "
	alias ga="git add "
	alias gb="git branch "
	alias gc="git commit"
	alias gd="git diff"
	alias go="git checkout "


## Useful links 

### Good Introduction 
- [try git](https://try.github.io/levels/1/challenges/1)
- [git the simple guide](http://rogerdudler.github.io/git-guide/)
- [cheatsheet](https://training.github.com/kit/downloads/github-git-cheat-sheet.pdf)

### Going Further 
- [git immersion](http://gitimmersion.com/lab_01.html)
- [pro git](http://git-scm.com/book/en/v2)


