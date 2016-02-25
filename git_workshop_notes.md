---
author: Alex Phillips
title: Title
date: \today
fontsize: 10pt
linestretch: 1.5
geometry: margin=2.5cm
csl: /home/alex/Documents/.csl/cell.csl
dpi: 200
format: latex

...


Git is about version control. Changes made to files are called commits. 

1. To set git account locally

```bash
$ git config --global user.email "user.email@email.com"
```

1. To initialize folder as git repository.

```bash
$ git init
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .git_workshop_notes.md.swp
        git_workshop_notes.md
        git_workshop_notes.pdf
        git_workshop_notes.tex
        git_workshop_notestex
        git_workshop_notestex.aux
        git_workshop_notestex.log
        git_workshop_notestex.out
        git_workshop_notestex.pdf

nothing added to commit but untracked files present (use "git add" to track)


```
- By default, first commit goes to Master.
- Here I have created files, and they are UNTRACKED!!
- As soon as you make git aware of them, git will begin tracking their changes. 
- git add stages the changes. 
- Some people add each file separately, then commit in bulk. 

```bash
$ git add *
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

        new file:   git_workshop_notes.md
        new file:   git_workshop_notes.pdf
        new file:   git_workshop_notes.tex
        new file:   git_workshop_notestex
        new file:   git_workshop_notestex.aux
        new file:   git_workshop_notestex.log
        new file:   git_workshop_notestex.out
        new file:   git_workshop_notestex.pdf

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .git_workshop_notes.md.swp
```
- Now it's tracking them, but they have not been committed yet. 
- git commit 
```bash
$ git commit
[opens vi editor and wants message with the stuff]
[master (root-commit) 0e0d499] Start notes on this tutorial folder
 8 files changed, 1280 insertions(+)
 create mode 100644 git_workshop_notes.md
 create mode 100644 git_workshop_notes.pdf
 create mode 100644 git_workshop_notes.tex
 create mode 100644 git_workshop_notestex
 create mode 100644 git_workshop_notestex.aux
 create mode 100644 git_workshop_notestex.log
 create mode 100644 git_workshop_notestex.out
 create mode 100644 git_workshop_notestex.pdf
```

- vi editor is default, but I prefer vim:
```bash
$  git config --global user.editor "vim"
```
- git log tells use the history of changes that we have made. 
```bash
$ git log
commit 0e0d499b750312cf8fe371799803dfdb5637d321
Author: alexprp <alexprphillips@gmail.com>
Date:   Thu Feb 25 13:32:33 2016 -0600

    Start notes on this tutorial folder

$ git log --oneline
0e0d499 Start notes on this tutorial folder
```

- This is why it's super important to leave good commit messages. Otherwise, the
  message in the log is meaningless. 
- I have made more changes to this notes file and its derivatives since we last
  committed. Let's see what that does
```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   git_workshop_notes.md
	modified:   git_workshop_notes.pdf
	modified:   git_workshop_notes.tex

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.git_workshop_notes.md.swp

no changes added to commit (use "git add" and/or "git commit -a")
```
- git diff tells us the changes specifically that have been made. 
- I don't put that here because it's the same text and pandoc/latex/markdown get
  confused. 
```bash
$ rm *notestex*
$ git add *
$ git commit -m 'deleted accidental files and added more notes'
[master 904dcea] deleted accidental files and added more notes
 3 files changed, 203 insertions(+), 3 deletions(-)
 rewrite git_workshop_notes.pdf (62%)
$ git log 

commit 904dceaff5ee685c3a52d11e673068e9c22baed0
Author: alexprp <alexprphillips@gmail.com>
Date:   Thu Feb 25 13:58:12 2016 -0600

    deleted accidental files and added more notes

commit 0e0d499b750312cf8fe371799803dfdb5637d321
Author: alexprp <alexprphillips@gmail.com>
Date:   Thu Feb 25 13:32:33 2016 -0600

    Start notes on this tutorial folder
$ git log --oneline

904dcea deleted accidental files and added more notes
0e0d499 Start notes on this tutorial folder
```
- 'git --staged' only shows staged chages

Branches
--------

- Master always points to latest commit; it's a pointer
- HEAD is a special pointer that points to Master, not directly to the latest
  commit. HEAD points to the **parent of the nest commit**. 
- If chages are made off of another instance of the previous commit, a new
  master is created. If there is a dangling Master, it will be deleted
periodically, automatically by git if it has not been committed. 

Folders
-------------

```bash
$ mkdir folder1

$ git add folder1

[nothing happens]

```
- git does not track empty folders

```bash
$ echo 'qwer' > folder1/asdf.txt
$ git add folder1

```
- nested git repositories are dangerous. don't do it. 
- To make git forget about a directory, simply:
```bash
$ rm -rf .git
```
.git
----

```bash
$ ls .git

branches
COMMIT_EDITMSG
config
description
HEAD
hooks
index
info
logs
objects
refs
```
- contains many files, including a local instance of ~/.config

```bash
$ cat COMMIT_EDITMSG


# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Changes to be committed:
#	modified:   git_workshop_notes.md
#	modified:   git_workshop_notes.pdf
#	modified:   git_workshop_notes.tex
#
# Changes not staged for commit:
#	deleted:    git_workshop_notestex
#	deleted:    git_workshop_notestex.aux
#	deleted:    git_workshop_notestex.log
#	deleted:    git_workshop_notestex.out
#	deleted:    git_workshop_notestex.pdf
#
# Untracked files:
#	.git_workshop_notes.md.swo
#	.git_workshop_notes.md.swp
#

```
- This is what will be shown upon commit; contains stuff from last stage. 

```bash
$ cat .git/HEAD

ref: refs/heads/master

```

- To commit quickly:
```bash
$ git commit -am 'quickly commit more notes without multiple commands or staging'

[master 1064b17] quickly commit more notes without multiple commands or staging
 9 files changed, 249 insertions(+), 1086 deletions(-)
 create mode 100644 folder1/asdf.txt
 rewrite git_workshop_notes.pdf (64%)
 delete mode 100644 git_workshop_notestex
 delete mode 100644 git_workshop_notestex.aux
 delete mode 100644 git_workshop_notestex.log
 delete mode 100644 git_workshop_notestex.out
 delete mode 100644 git_workshop_notestex.pdf
```

If you committed a mistake and want to amend
```bash
$ git commit --amend
# opens vi editor and allows editing of commit message, uses same hash and everything
$ git log --oneline

daa3b30 quickly commit more notes without multiple commands or staging with slight changes
904dcea deleted accidental files and added more notes
0e0d499 Start notes on this tutorial folder
```

Demo
----

```bash
$ mkdir git_workshop_2
$ cd git_workshop_2
$ vim file1.txt
$ cat file1.txt

asdfl;kjasdfl
asdfl;kasdfl

$ git init

Initialized empty Git repository in /home/alex/git_workshop_2/.git/

$ ls

file1.txt

$ git add file1.txt
$ git commit -m 'new'

[master (root-commit) 6aaa158] new
 1 file changed, 3 insertions(+)
 create mode 100644 file1.txt

$ vim file1.txt
$ cat file1.txt

sdfl;kjasdfl
asdfl;kasdfl
fjdkfjdkfdk

and now for something completely different

$ git diff

diff --git a/file1.txt b/file1.txt
index 9dea9ee..ab8d3ea 100644
--- a/file1.txt
+++ b/file1.txt
@@ -1,3 +1,5 @@
 asdfl;kjasdfl
 asdfl;kasdfl
 fjdkfjdkfdk
+
+and now for something completely different


```
