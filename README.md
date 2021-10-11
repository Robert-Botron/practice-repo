# practice-repo

## Introduction
This practice repo allows us to play with git and learn how things work without destroying a live production project.  

To Clone use the CLI or a GUI tool

CLI
```
$ git clone https://github.com/Robert-Botron/practice-repo.git
```

GUI
```
https://github.com/Robert-Botron/practice-repo.git
```

## Examples

## Workflows
 
* Centeralized Workflow
* Feature Branching Workflow
* Gitflow Wrokflow
* Forking Workflow
  
## Q&A
* **Q:** I want to add a document, but I don't want to add it to my current development branch.  How should I add it.
**A:** Sure, you can always switch to the master branch, add and commit the document, and switch back to your active branch.
     ```
     $ git checkout master
     $ touch document <add the document>
     $ git add document
     $ git commit -m 'comment on document'
     $ git checkout my-active-branch
     ``` 
     or in Git 2.23 or later of git.  Both checkout and switch will work.
     ```
     $ git switch master
     $ touch document <add the document>
     $ git add document
     $ git commit -m 'comment on document'
     $ git switch my-active-branch
     ```
     Switching to other branches to make changes or additions outside of your current active branch is common. 
     **Note:** It's a nice idea to stage and commit your current work to your active branch before switching branches.  You can do this even if you don't commit your current work, but you will want to be very specific when committing the new document, as not to commit other work to the master branch as well.  

     * **Q:** How do I push an existing local repo into a new Github repo
     **A:** This only requires that you add a remote origin and push to the new remote origin. When a local git repo is initialized it will not have an orgin so the process easy.  If you cloned a repo, your local repo will have and origin from which it was cloned from. I'll illustrate both situations.
     
     Below is a configuration of an empty local repo

     ```
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
     ```
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

     ```
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
```
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

