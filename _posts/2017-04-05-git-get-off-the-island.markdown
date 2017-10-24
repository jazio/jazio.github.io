---
layout: post
title:  "Git, the director uncut film of staging"
date:   2017-10-24 08:08:26 +0100
categories: tools
---

# Git, the director uncut film of staging
# Things you need to know.



## Starting a project on github.com

Initialize this repository with a README
This will allow you to git clone the repository immediately. Skip this step if you have already run git init locally.

Then locally:

```
$ git init
```

```
$ git remote add origin https://github.com/jazio/silexbasic.git
fatal: remote origin already exists.
$ git remote -v
origin	ssh://lorette@lorette.ro:15554/home/lorette/public_html/.git (fetch)
origin	ssh://lorette@lorette.ro:15554/home/lorette/public_html/.git (push)
$ git remote add origin https://github.com/jazio/silexbasic.git
fatal: remote origin already exists.
$ git remote rm origin
$ git remote add origin https://github.com/jazio/silexbasic.git
```

```
git add .
git status
git commit -m 'First commit'
git push
```


## Interactive mode

```
git add -i
```

## Ignore folders

A .gitignore file should be committed into your repository, in order to share the ignore rules with any other users that clone the repository.
GitHub maintains an official list of recommended .gitignore files for many popular operating systems, environments, and languages in the github/gitignore public repository.
If you already have a file checked in, and you want to ignore it, Git will not ignore the file if you add a rule later. In those cases, you must untrack the file first, by running the following command in your terminal:


### Remove untracked files from the working tree
```
git-clean -
Dangerous!
git clean -n -d <path>
will do a ‘dry run’ of the command and show you just what files and folders are going to be removed
git -f -d .
```

## CRLF
#### Convert files
unix2dos, dos2unix -D filename


### Remove files from repository
```
$ git rm -r .
```

### Remove from index only
```
$ git rm -r --cached .
```


## Revert some changes to latest commit
```
$ git status, see what's changed
$ git checkout filename
```


## When you forgot to add something to latest commit
```
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```
After these three commands, you end up with a single commit — the second commit replaces the results of the first.

http://git-scm.com/book/en/Git-Basics-Undoing-Things


In Git, there are two main ways to integrate changes from one branch into another: the merge and the rebase git


You can get a branch e.g.
git checkout -b my-urgent-fix origin/hotfix/my-urgent-fix

if you just type

git checkout origin/hotfix/my-urgent-fix

you run into a dettached state.


### You can create a GitHub repo via the command line using the GitHub API. Check out the repository API.

```
curl -u 'USER' https://api.github.com/user/repos -d '{"name":"REPO"}'
```




### Accidentaly remove head

$ git push
fatal: You are not currently on a branch.
To push the history leading to the current (detached HEAD)
state now, use

    git push origin HEAD:<name-of-remote-branch>

$ git branch
* (detached from 75bc0b7)
  master
$ git status
HEAD detached from 75bc0b7
nothing to commit, working directory clean


$ git branch
* (detached from 75bc0b7)
  master

HEAD is the symbolic name for the currently checked out commit
 HEAD actually points to a branch’s “ref” and the branch points to the commit. HEAD is thus “attached” to a branch.

 We have HEAD → refs/heads/master → 17a02998078923f2d62811326d130de991d1a95a

 When HEAD is detached, it points directly to a commit—instead of indirectly pointing to one through a branch. You can think of a detached HEAD as being on an unnamed branch.
 git branch temporary
git checkout temporary

(these two commands can be abbreviated as git checkout -b temp)
This will reattach your HEAD to the new temp branch.




Next, you should compare the current commit (and its history) with the normal branch on which you expected to be working:


$ git log --graph --decorate --pretty=oneline --abbrev-commit master origin/master temporary
* ef6a942 (HEAD, temporary) Validation
* 75bc0b7 (origin/master, master) form
* 96c5f9d personalized description in templates
* e9405d3 form improved, local css, js in template, url generator in contact
* f1690fd Initial contact form
* 60f9021 yml parser
* 1ce6170 layout fix, new templates, active states
* 52db402 minor changes
* 11bb548 blog pages
* 13fcf4f generic layout
* a593e3c Add sample blog controllers
* 83875d5 layout and homepage template
* 3dfe548 removed vendor
*   0c03004 Merge branch 'master' of https://github.com/jazio/silexbasic
|\
| * b15301a Initial commit
* 722b121 First commit
$




NowIf your new temp branch looks good, you may want to update (e.g.) master to point to it:

```
$ git branch -f master temporary
$ git branch
  master
* temporary
$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
$ git log
commit ef6a942e79443e2c3ffb444ae3bd62b6b470cf5f
Author: Ovi Farcas <farcaso@gmail.com>
Date:   Fri Apr 25 16:09:31 2014 +0200

    Validation

commit 75bc0b7205119ed2b78edbe0c4365b95b64fd6c8
Author: Ovi Farcas <farcaso@gmail.com>
Date:   Tue Apr 22 17:32:55 2014 +0200

    form

commit 96c5f9db0a81893b17c6fdad1057d98476e9ec0f
Author: Ovi Farcas <farcaso@gmail.com>
Date:   Sat Apr 12 17:33:33 2014 +0200

    personalized description in templates

commit e9405d3788c17321b60302e98517c73e90bfe733
$ git push
```

Display all branches
```
git branch -a
```

$ git branch -a
* master
  temporary
  remotes/origin/master


git branch -d temporary


git

Initialize this repository with a README
This will allow you to git clone the repository immediately. Skip this step if you have already run git init locally.

Then locally:
```
git init

$ git remote add origin https://github.com/jazio/silexbasic.git
fatal: remote origin already exists.
$ git remote -v
origin	ssh://lorette@lorette.ro:15554/home/lorette/public_html/.git (fetch)
origin	ssh://lorette@lorette.ro:15554/home/lorette/public_html/.git (push)
$ git remote add origin https://github.com/jazio/silexbasic.git
fatal: remote origin already exists.
$ git remote rm origin
$ git remote add origin https://github.com/jazio/silexbasic.git

git add .
git status
git commit -m 'First commit'
git push
```

## Ignore folders


A .gitignore file should be committed into your repository, in order to share the ignore rules with any other users that clone the repository.

GitHub maintains an official list of recommended .gitignore files for many popular operating systems, environments, and languages in the github/gitignore public repository.

If you already have a file checked in, and you want to ignore it, Git will not ignore the file if you add a rule later. In those cases, you must untrack the file first, by running the following command in your terminal:

git rm -r --cached
--cached means will only be removed from index.


"Reset the working tree to the last commit"
```
git reset --hard HEAD
```
"Clean unknown files from the working tree"
```
git clean
```

### What's the difference between git pull and git fetch?
In the simplest terms, "git pull" does a "git fetch" followed by a "git merge".
You can do a "git fetch" at any time to update your local copy of a remote branch.
This operation never changes any of your own branches and is safe to do without changing your working copy.

A "git pull" is what you would do to bring your repository up to date with a remote repository.
Good Article: It explain branches
git: fetch and merge, don’t pull

http://longair.net/blog/2009/04/16/git-fetch-and-merge/


#Inspect a deleted file

This won't work
```
git log deletedFile.txt
fatal: ambiguous argument 'deletedFile.txt': unknown revision or path not in the working tree.
```

So you need to indicate -- there are no options
```
git log -- deletedFile.txt
```