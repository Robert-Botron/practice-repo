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
     Switching to other branches to make changes or additions outside of your current active branch is common. **Note:** It's a nice idea to stage and commit your current work to your active branch before switching branches.  You can do this even if you don't commit your current work, but you will want to be very specific when commiting the new document, as not to commit other work to the master branch as well.  
