# Working in a Repository

Let's work with our project repositories.

In this tutorial, all shell commands that you should type in the terminal will be prefixed with `>`
not the $ we used in Introduction to CLI.

## Clone a git repository

To get a copy of an existing repository, you use the command
`git clone`. Cloning a repository will pull down a full copy of all the
data the server has -- every version of every file for the history of
the project. *You only need to do this once for every project*.

```
git clone https://gitlab.adrf.info/project_jan5/project-repository.git
```
This creates a directory named `project-repository`, initializes a `.git`
directory inside it, pulls down all the data for that repository, and
checks out a copy of the latest version. 

To confirm that this worked, we can *list* all the files in this directory 
using the `ls` command. We include the `-a` flag to tell the command to 
display *hidden* files, or those that begin with a `.`, in the list.
```
> cd project-repository
> ls -a
.  ..  .git/
```

We see that there is now a `.git` directory in the `project-repository` directory.
*Unless you really know what you are doing* **DO NOT EVER** *modify anything in this
directory. If you delete this directory, the entire history of your project will be gone.*

## Make our first commit!!
All good projects deserve to have a "README" describing the purpose and 
organization of the project, so let's start with that.

**Pick ONE person on your team to do the following:**

Fire up your text editor (`komodo-edit` will work here) and create a file
called `README.md`.  The `.md` means this file will be read as `markdown`, which
allows us to format the text programmatically. Here's a basic example of a 
`README.md`:
```
# Welfare Project

## Description

This repo is for <team_name>'s group project using python2.7.
```
When you're first starting a project, there's a good chance you won't have much more to add,
and that's OK. Notice that we *do* have a title, a short description of the project, and a
list of the software the project required, also known as the *dependencies*. It's a good idea
to keep updating both the description and dependencies as your project grows and evolves.

The `#` here don't signify hashtags or comments - they are part of
[`markdown` syntax](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet), and
they designate headings.

Now let's look at the *status* of our repo using `git status`:
```
> git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

          README.md

          nothing added to commit but untracked files present (use "git add" to track)
```
`git status` tells us which *branch* we are on, which files are being tracked, and which
files are present that *aren't* being tracked. We see our new file `README.md` listed
under `Untracked files` - `git` sees that we've added something, but doesn't know whether
it should be logged as part of our project. When we create a new file, we need to *tell*
`git` to start tracking it. Like the command suggests, let's use `git add` to track
`README.md`.
```
> git add README.md
```
Now let's invoke the command `git status` again.

```
> git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

          new file:   README.md
```
Now that we have added the file, it has been "staged" to be committed. We can now make
our first commit! A **commit** is a snapshot in time of the work that you've 
done. The commit groups together the changes that you have made with a message
where you *explain* those changes. The message is for your collaborators, and
for your future self, to understand what changes you made and why you made
those changes. 

It's a good rule of thumb to make a commit at least at the end of every working 
session, but it's common to make commits more often than that if you are 
making multiple changes in one session.

To make a commit, type:

```
> git commit
```
When you invoke the `git commit` command, an editor should pop up. This is for you to
write your **commit message**, a message that provides the context of
*what you did* and *why you did it*. Anyone can look at a commit and examine
what was changed; you might look at a commit message to find where you changed a
certain file, or your collaborator might read it before incorporating your changes
into the shared version of the project.

Give some thought to what you write here - good commit messages lead to a usable `git` log,
and separate novice `git` users from competent practitioners. Generally, you should follow
these guidelines in a commit message:

1. **First line** is a one-line summary (fewer than 80 characters) of the commit. It should
be in [title case](https://en.wikipedia.org/wiki/Letter_case#Title_case) and written in
the [imperative voice](https://en.wikipedia.org/wiki/Imperative_mood). A good rule of thumb:
*If applied this commit will, <insert title of git message here>*.

2. **Second line** should be blank.

3. **Third (and subsequent) lines** should include more details of the commit.

My commit message is the following:
```
Check in README file

* Added short description of the project
* Added python2.7 as a dependency
```
Now that we have made our first commit we can examine our log using `git log`!
```
> git log

* commit aaf89fd77e9b43d99fe32823843a7519b2108c90
  Author: Clark Kent <clark.kent@dailyplanet.com>
  Date:   Sat Nov 05 13:45:11 2016 -0600

          Check in README file

          * Added short description of the project
          * Added python2 as a dependency
```
The long string of characters in the first line is a unique identifier for your commit.
You can use this identifier to switch back to this specific version of your project in
the future. The second line is who made the commit. The third line gives the date
and time. Everthing that follows is the commit message.

To see only the *titles* of commit messages, you can use `git log` with the
`--oneline` option:
```
> git log --oneline
```
There are many other options to the `git log` command; explore the documentation to find
which ones suit your needs. Here's one combination we recommend (check it out!):
```
> git log --oneline --graph --all --decorate
```
For very short, simple commits, you can just enter one-line commits using the following syntax:
```
git commit -m "This is a short commit message"
```
# Pushing and Pulling

The remote version on the GitLab server does not automatically sync with your local version
(or vice-versa). To sync up the *remote*  and local (the version on your computer), you have to
**push** your local changes *to* the remote repository, or *pull* any changes *from* the
remote repository into your local repository. To push changes, we use the `git push` command:

```
> git push #The person who wrote the README should do this
```
To *pull* in changes from the remote repository to your copy of the repository, you can use the
following commands.

```
git pull origin master #The people who did not write the README should do this. 
```

So far we have been doing the "solo" workflow, which looks something
like the following:
```

 > cd my_working_directory
 > git pull # do this whenever you start working
 > touch some_file.py
  # hack, do some work, hack
  # hack
 > git add some_file.py
 > git commit -m "Working with some awesome idea"
 > git push origin master
  # hack
  # more hacking
```


# Useful git commands

## Getting rid of changes when you don't need them (Git Stash)
When your local changes do not conflict with the the changes in the upstream, a simple
`git pull` will let you move forward.

However, there are cases in which your local changes do conflict with the remote, and
`git pull` refuses to overwrite your changes. In such a case you can *stash* your changes
away, perform a pull, and then unstash later, like this:
```
> git pull
...
file foobar not up to date, cannot merge.
> git stash
> git pull
> git stash pop
```

## Moving and removing files
Now you know how to *add* a file to your project using `git`. What if you want to get
rid of something? You can **remove** files from your repo using `git rm`:
```
> git rm FILENAME
> git rm -r DIRECTORY
```
Note that when you remove a file using `git`, you can still go back to a *previous* commit
before you removed the file and **recover** that file. This is different than simply using
the command `rm`, which permanently erases the file.

You'll also have to tell `git` if you want to *rename* a file using the `git mv` command,
because *renaming* a file is basically *moving* it to a new location. For
example, to change the name of a file from `OLD` to `NEW`:
```
> git mv OLD NEW
```
`git rm` and `git mv` will stage the changes, so after invoking one of these commands, you can
just `commit` your changes without using `git add` again.


