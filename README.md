# practice-repo

## Introduction

This practice repo allows us to play with git and learn how things work without destroying a live production project.  

To Clone use the CLI or a GUI tool

CLI

```bash
$ git clone https://github.com/Robert-Botron/practice-repo.git
```

GUI

```bash
https://github.com/Robert-Botron/practice-repo.git
```

## Examples

## Workflows

* Centralized Workflow
* Feature Branching Workflow
* Gitflow Workflow
* Forking Workflow
  
## Q&A

* **Q:** I want to add a document, but I don't want to add it to my current development branch.  How should I add it.

     **A:** Sure, you can always switch to the master branch, add and commit the document, and switch back to your active branch.

   ```bash
     $ git checkout master
     $ touch document <add the document>
     $ git add document
     $ git commit -m 'comment on document'
     $ git checkout my-active-branch
   ```

     or in Git 2.23 or later of git.  Both checkout and switch will work.

   ```bash
     $ git switch master
     $ touch document <add the document>
     $ git add document
     $ git commit -m 'comment on document'
     $ git switch my-active-branch
   ```

     Switching to other branches to make changes or additions outside of your current active branch is common. 
     **Note:** It's a nice idea to stage and commit your current work to your active branch before switching branches.  You can do this even if you don't commit your current work, but you will want to be very specific when committing the new document, as not to commit other work to the master branch as well.  
---

* **Q:** How do I push an existing local repo into a new Github repo
  
     **A:** This only requires that you add a remote origin and push to the new remote origin. When a local git repo is initialized it will not have an orgin so the process easy.  If you cloned a repo, your local repo will have and origin from which it was cloned from. I'll illustrate both situations.

     *Below is a configuration of an empty local repo*

     ```bash

     PS C:\Users\Robert\Projects> cd test

     PS C:\Users\Robert\Projects\test> git init
     Initialized empty Git repository in C:/Users/Robert/Projects/test/.git/

     PS C:\Users\Robert\Projects\test> git config --local -l
     core.repositoryformatversion=0
     core.filemode=false
     core.bare=false
     core.logallrefupdates=true
     core.symlinks=false
     core.ignorecase=true
     ```

     Now we see what the config looks like after adding the remote origin to our empty repo.

     ```bash

     PS C:\Users\Robert\Projects\test> git remote add origin https://github.com/Robert-Botron/practice-repo.git

     PS C:\Users\Robert\Projects\test> git config --local -l
     core.repositoryformatversion=0
     core.filemode=false
     core.bare=false
     core.logallrefupdates=true
     core.symlinks=false
     core.ignorecase=true
     remote.origin.url=https://github.com/Robert-Botron/practice-repo.git
     remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
     ```

     Below we see what a cloned repo's config looks like    **Note:** the remote.origin already exists.

     ```bash
     PS C:\Users\Robert\Projects\practice-repo> git config --local -l

     core.repositoryformatversion=0
     core.filemode=false
     core.bare=false
     core.logallrefupdates=true
     core.symlinks=false
     core.ignorecase=true
     remote.origin.url=https://github.com/Robert-Botron/practice-repo.git
     remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
     branch.main.remote=origin
     branch.main.merge=refs/heads/main
     PS C:\Users\Robert\Projects\practice-repo>
     ```

     Because an existing "origin" remote repo exists, there two ways we can handle this.  We can remove the original origin or we can rename it and add a new origin.  The name "origin" is just a name given to the URL and can be anything.  The name "origin" seems to be apropos to where the repo came from, but does not need to be so named.  In this example I'll rename the original origin to "old-origin" and add a new one named "origin".

     ```bash
     PS C:\Users\Robert\Projects\practice-repo> git remote rename origin old-origin

     PS C:\Users\Robert\Projects\practice-repo> git remote add origin https://gitlab.localdomain:5000/rchapman/practice-repo.git

     PS C:\Users\Robert\Projects\practice-repo> git config --local -l
     core.repositoryformatversion=0
     core.filemode=false
     core.bare=false
     core.logallrefupdates=true
     core.symlinks=false
     core.ignorecase=true
     remote.old-origin.url=https://github.com/Robert-Botron/practice-repo.git
     remote.old-origin.fetch=+refs/heads/*:refs/remotes/old-origin/*
     branch.main.remote=old-origin
     branch.main.merge=refs/heads/main
     remote.origin.url=https://gitlab.localdomain:5000/rchapman/practice-repo.git
     remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*

     ```

Now you can push the repo to the new origin using `git push origin --all --tags`.  This will push your local repo to the new remote origin repo. Handling remote repositories in this way preserves the original repo where the source came from.

* **Q:** how do you see the history of a repo?
  
  **A:** You use ```git log``` to view the history of the repository.  There are various parameters that can be used to format the view of the commit log.

  ```bash
  PS C:\Users\Robert\Projects\practice-repo> git log
  commit 624c62569023b6793ef90fe18c098342201972a7 (HEAD -> main, origin/main, origin/HEAD)
  Author: Robert F. Chapman <rchapman@botron.com>
  Date:   Mon Oct 11 12:41:41 2021 -0700

    Add swap and backup files

    Addition of *.swp and *.*~

  commit c1283a72474f5080454e80b9d5dbed49a5f3b9b2
  Author: Robert F. Chapman <rchapman@botron.com>
  Date:   Mon Oct 11 12:28:49 2021 -0700

    Add Q&A question, how to move a repo

    Illustrates how to move a repo from one account to another by changing
    the remote origin.

  ...

  commit 1809fc9278effcca2207b94e5c7af9670c467b66
  Author: Robert F. Chapman <90871532+Robert-Botron@users.noreply.github.com>
  Date:   Thu Sep 23 12:44:12 2021 -0700

    Initial commit
  PS C:\Users\Robert\Projects\practice-repo>
  ```

  With formating parameters you can make it easier to read.

  ```git
  PS C:\Users\Robert\Projects\practice-repo> git log --oneline
  d9cc035 (HEAD -> main, origin/main, origin/HEAD) Addition and formatting
  624c625 Add swap and backup files
  c1283a7 Add Q&A question, how to move a repo
  f14c9ca Spelling and formatting corrections
  c91ff43 Changed "add and commit" to "stage and commit",  the word "add" is a little confusion when talking about adding a document
  99a0c67 Addition of Q&A section along with an example.
  110bb6a Added introduction and CLI example to README
  1809fc9 Initial commit
  
  PS C:\Users\Robert\Projects\practice-repo> git log --oneline --decorate
  d9cc035 (HEAD -> main, origin/main, origin/HEAD) Addition and formatting
  624c625 Add swap and backup files
  c1283a7 Add Q&A question, how to move a repo
  f14c9ca Spelling and formatting corrections
  c91ff43 Changed "add and commit" to "stage and commit",  the word "add" is a little confusion when talking about adding a document
  99a0c67 Addition of Q&A section along with an example.
  110bb6a Added introduction and CLI example to README
  1809fc9 Initial commit
  PS C:\Users\Robert\Projects\practice-repo>

  PS C:\Users\Robert\Projects\practice-repo> git log --oneline --decorate --graph
  * d9cc035 (HEAD -> main, origin/main, origin/HEAD) Addition and formatting
  * 624c625 Add swap and backup files
  * c1283a7 Add Q&A question, how to move a repo
  * f14c9ca Spelling and formatting corrections
  * c91ff43 Changed "add and commit" to "stage and commit",  the word "add" is a little confusion when talking about adding a document
  * 99a0c67 Addition of Q&A section along with an example.
  * 110bb6a Added introduction and CLI example to README
  * 1809fc9 Initial commit
  PS C:\Users\Robert\Projects\practice-repo>
  ```

## Links

* [Publish Aritifacts in Github Actions](https://www.youtube.com/watch?v=Zcsk_Nzv-aU)