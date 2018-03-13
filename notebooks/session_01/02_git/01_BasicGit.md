# Git Overview

The tutorial will give a quick overview of what git is, how to use it, and how to work
as a team using the GitHub workflow.

For this tutorial you will need to have access to [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git), a [Terminal](http://swcarpentry.github.io/shell-novice/), and a [text editor](http://swcarpentry.github.io/git-novice/02-setup/) - you can use a terminal-based text editor like [vim](http://www.vim.org/) or [emacs](https://www.gnu.org/software/emacs/), or you can use one with a more complex interface like [Sublime](https://www.sublimetext.com/).

> For this tutorial, all commands that you should type in your terminal will be
> prefaced with `$`.

## Git in a nutshell

![git](git.png)

[Image source](https://xkcd.com/1597/)

Git is a *version control system* which helps you keep track of changes you make to files during the development
of your project. You can think of it as an undo button, a lab notebook, and a tool to safely and efficiently collaborate with others on a shared project, all rolled into one.
All serious software projects use version control.

While git is mostly used in software development, it can be used for anything you like
([writing books](https://www.gitbook.com/), for example), as long as your files are plain text
(e.g., source code, $\LaTeX$  files).

Simply speaking, git saves snapshots of your work called `commits`; after a `commit` is created, you can go back
and forth through different commits in your project -- maybe you were experimenting with some new function and
realized the old function was better, no problem, you can bring back anything! The collections of commits together with their associated
metadata (like who made the changes, and when) form the `repository` of your project.

![git 2](git_commit.png)

[Image source](https://xkcd.com/1296/)

The entire development of your project, the `repository`, is stored on your computer.  but we know that's
dangerous, so you can also host a remote copy on a hosting service like GitHub, Bitbucket, or GitLab.
Hosting a project's `repository` on GitHub also allows for the distribution of your work and collaboration
with others. This prevents endless emailing of source code and the following situation:



![final](phd101212s.gif)


## git sounds awesome! How do I get it?

Chances are, git is already installed on your computer. To check, open up a terminal and type `git`.
If not, you can get it [here](https://git-scm.com/).

OS X users can use `homebrew` to install git.

## Can I get buttons and stuff?

`git` is a command line tool, which means it doesn't have a native graphical user interface. Using the
`git` CLI is the most flexible way of working with `git`, and if you are working on a remote server you will
unlikely be able to use a GUI.

However, if you *really* want a point-and-click interface on your computer, here are some options:

*   [Options for Mac](https://git-scm.com/download/gui/mac)
*   [GitKraken](https://www.gitkraken.com/) (Windows and Mac)

*Keep in mind that if you are logging into a remote machine, such as AWS, a GUI may not be an option.*

## Configure your Git Profile

First things first: you need to configure your `git` client, so that your commits are correctly attributed to you,
and so you get pretty output. Do the following:

Open up a terminal: Go to your desktop on ADRF, left-click and
select Open Terminal.

```
# How my git configuration currently looks
$ git config --list
```

 My workspace #switch the names to your information

```
# Adding some customization
$ git config --global user.name "Clark Kent"
$ git config --global user.email "clark.kent@dailyplanet.com"
$ git config --global color.ui "auto"
$ git config --global core.editor 'komodo-edit' #or vim, emacs sublime
```
For a list of text editors, see Software Carpentry's [list](http://swcarpentry.github.io/git-novice/02-setup/)

Also do the following (important):
```
$ git config --global push.default current
```
