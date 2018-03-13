# Applied Analytics Git CheatSheet

The git command always is used by first calling git, then telling it what action you want to perform, then passing it additional arguments to tell it how you want it to carry out the requested action:

    git <action> <parameters>
    
Example with action "add", adding "`my_file.txt`":

    git add my_file.txt

## Git quickstart - add-commit-pull-push

To check in using git at the command line:

- First, go into the directory of the git repository in which you are working.
- run git status to see what changes have been made:

        git status
        
- Add any files or directories that are new or have been changed:

        git add <file_name>
        
        git add <directory_name>

        git add README.md
        
        git add *.py   # you can use wild cards
        
- Once you've added all the files, commit.

        git commit
        
- As part of commit, it will ask you to enter a commit message.  On Unix and Mac, this will open up your default shell text editor.

- After commit, you sync with the github remote repository.

        # first pull, to receive changes that are on the server, not on your computer.
        git pull
        
        # then, push your changes to github
        git push
        
When you are collaborating with a team of developers, pulls sometimes force you to manually reconcile changes made to the same bits of code.  If it is just you working alone in a repository, however, chances are your pull won't result in any changes or merges.  It will just tell you there aren't any changes.

When you push, depending on how you cloned your repository, you will likely have to log in to gitlab.

## Git Concepts

**remote** - a remote is an external repository that the local repository syncs with.  A given repository can have more than one remote.  Standard remotes:

- origin -- default remote repository (i.e, the GitLab repo if you clone a repository from gitlab)

**branch** - a branch is a set of code changes that are kept separate from the main code base (or trunk) in a git repository.  A branch can be worked on in isolation until one wants to merge the changes back into the trunk.  Git makes it easy to create branches both in your local repository and in a remote.  Standard branches:

- master -- default development branch
- HEAD   -- current branch
- HEAD^  -- parent of head
- HEAD~4 -- the great-grandfather of head


## Set up a Git Configuration
```
# Adding some customization
git config --global user.name "Clark Kent"
git config --global user.email "clark.kent@dailyplanet.com"
git config --global color.ui "auto"
git config --global core.editor 'nano' #or vim, emacs sublime
git config --global push.default current
```

## Create a Git Repo

### From an existing repo
```
git clone git://host.org/myproject.git # an external GitHub Repo though HTTPS
git clone ssh://you@somehost.org/project.git # through SSH
git clone ~/some/repo.git ~/new/repo.git # #through the filesystem
```

### From a new project
```
cd ~/myproject
git init # intialize the repo
git add . # add the folder
```

## Stashing - Moving changes to the side

The `git stash` command lets you put aside a set of changes so that you can pull updated code from a remote.  You can then either re-apply your stash of changes to the updated code files or discard them.

```
git stash -- save modified and staged changes and them remove them from current branch.
git stash list -- list stack-order of stashed file changes
git stash pop -- worte working from top of stash stack
git stash drop -- discard the changes from top of stash stack
```

## Other Useful Commands

```
git <command> --help #pull up documentation for a <command>

git status -- check which files have been changed in the working directory

git log -- get a history of changes

git checkout <somefile> HEAD --revert to a the state of a file at the last commit

git reset --hard Revert back to the last state WARNING THIS CANNOT BE UNDONE
```

## GitHub Flow

So far we have been doing the "solo" workflow, which looks something
like the following:
```
 > mkdir my_working_directory
 > cd my_working_directory
 > git init
 > touch some_file.py
  # hack, do some work, hack
  # hack
 > git add some_file.py
 > git commit -m "Working with some awesome idea"
 > git push origin master
  # hack
  # more hacking
```

As you might have guessed, this workflow is just fine when you are
working by yourself. When you're working in a team, it's useful to
have a more structured workflow. Here we'll talk about the Github flow.

In the GitHub flow, *we never code anything unless there is a need to.*
When something needs to be done, we create an **issue** on the GitHub repository
for it. *Good* issues:
- Are clear
- Have a defined output
- Are actionable (written in the imperative voice)
- Can be completed in a few days (at most)

Here are some examples:
- *Good*: /Fix the bug in .../
- *Good*: /Add a method that does .../
- *Bad*:  /Solve the project/
- *Bad*:  /Some error happen/

[Here is how to create a GitLab issue.](https://docs.gitlab.com/ee/gitlab-basics/create-issue.html)

Once an issue exists, we'll pull from the repo and create a *branch*.
A *branch* is a copy of the code base separate from the main master branch
where we can work on our issue (e.g, fixing a bug, adding a feature) without
affecting the master branch during our work and then ultimately merge our
change into the master branch.

The flow goes something like this:
```
##Pull from the repo
> git pull
##Decide what you want to do and create an issue
> git checkout -b a-meaningful-name
```
The command `git checkout -b` creates a new branch (in this case
called "a-meaningful-name") and switches to that branch. We can see what
branch we are on by using the command `git branch`, which displays all
the branches in the local repository with a `*` next to the branch we are
currently on.
```
##
##hack, hack, hack, make some changes, add/rm files, commit
##
##Push to the repo and create a remote branch
> git push
##Create a pull request and describe your work (Suggest/add a reviewer)
##Someone then reviews your code
##The pull-request is closed and the remote branch is destroyed
##Switch to master locally
> git checkout master
##Pull the most recent changes (including yours)
> git pull
##Delete your local branch
> git branch -d a-meaningful-name
```
[Here is how to create a GitLab pull request.](https://docs.gitlab.com/ee/gitlab-basics/add-merge-request.html)

# Common Scenarios
### When you first start working ...
```
git pull
```
### After you have made some changes to a file, or whenever you finish working...
```
git add <filename>
git commit 
git pull
git push
```
### If you try `git pull` and get an error message saying "Your local changes
to the follow files will be overwritten...Please stash or commit your changes"...
```
git stash
git pull
```
