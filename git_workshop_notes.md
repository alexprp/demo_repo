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
- Here we have created 
