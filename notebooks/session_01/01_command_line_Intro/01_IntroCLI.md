# Command Line Interface (CLI) Tutorial
### (Adapted from [Software Carpentry Shell Lesson](https://swcarpentry.github.io/shell-novice/))


To clone the repository containing the class materials (including this 
tutorial), type the following into a Terminal:
```
git clone https://gitlab.adrf.info/project_class2/project-repository.git
```
You will be asked to enter your username and password. You will see your 
username as you type; however, for security, you will *not* see your password,
or even asterisks or placeholder characters. Don't worry, just type your 
password in and hit enter.

## Introduction

You are most likely comfortable interacting with a computer using point-and-click
interfaces, also known as **GUIs**, or *Graphical User Interfaces*. But there is
another way that came before and will always be: the **CLI**, or *Command Line Interface*.

The command line interface allows you to communicate with your computer more
directly than you can through a GUI, in a **REPL**, or *read-evaluate-print loop*
format: The user (you!) types a command, then presses the return key. The computer
reads the command, evaluates it, and *prints out* the output. This term comes from
the days when we had to use physical printers called "teleprinters" to interact with
computers.

The software you use to communicate with your computer is known as a **shell**,
because it acts as a "shell" from the underlying complexity of the operating system.
The most popular shell is known as [BASH, the Bourne Again Shell](https://www.gnu.org/software/bash/).
Bash is the default shell for most UNIX systems and Macs.

So, why use the command line instead of a GUI? There are several reasons:

1. In the shell you can easily handle data by chaining programs into a cohesive pipeline
to handle large amounts of data.

2. You can automate your workflow through scripting to save time and be more productive. A good
rule of thumb is if you do something twice -- script it!

3. Your work will be much more reproducible because there will be a
digital record of the steps you took to produce your results compared to
point and clicking in a program like Excel.

4. If you're working with remote machines, like supercomputers or
machines in the cloud, the CLI is often the only interface available.

5. The CLI is usually much faster -- once you get the hang of it.

The learning objectives of this mini-tutorial are the following:

* Learn how to navigate a UNIX file system.
* Learn some basic shell commands.


## Unix File System

### Terminal
Let's get started. On Linux systems or Macs, open up your Terminal application.
If you are using Windows, you may need to download a separate application;
one suggestion is [PuTTY](http://www.putty.org/).

In the ADRF environment, right-click on the desktop and select open terminal.

### Command Line Prompt
Every line in your terminal will start with a **prompt**. Commands that you type
will be prefaced by a prompt; output that is returned by the computer will not be.
For the rest of the examples below, we'll assume the prompt is `$`, so only type in
the commands that start with a `$`, and don't type the `$`.

Sometimes the default prompt will be your user name, or just a character, like `$`.
If you want to *change* your prompt so it matches what you'll see here, then type
`PS1='$ '` and hit Enter.
```
$
```

Next, type `whoami` and hit Enter:
```
$ whoami

ckent
```
The output should be your user name. This may seem like a silly
command - obviously you know who you are! The `whoami` command will come in
handy if you have multiple terminal windows open that are connected to different
machines, or if you discover an abandoned terminal session where the previous
user has not logged off.

## Unix File System

Now we'll learn how to navigate though a UNIX file system and how to **create**,
**edit**, **rename** and **copy** files and directories within the system.

First, a little background: UNIX has a hierarchical (tree-structure)
directory organization known as the **file system**. In the file system our
data is organized into **files**, which are organized in **directories**.
The base of the directory is called the *root directory* and denoted by a `/`.
All user-available disk space is combined into a single directory under '/'.

Here is an example of the directory tree of a typical Linux system.

![Image source](FS-layout.png)

From this figure, we can see all directories are under the root directory (`/`).
The folders under the root directory contain information for the configuration and operation
of the operating system, so you shouldn't change these (unless you really know
what you are doing). The special folder `home` contains the files for all users. In this
example, we have the directories `rick`, `anna`, `emmy`, `bob`, which contain files
created by users rick, anna, emmy, and bob, respectively.

When you first open a Terminal window, you will automatically start from your 
home directory. The shorthand for your home directory is `~`, so a file path
beginning at your home directory will begin with `~`, for example: 
`~/Documents/my_file.txt`. 

To navigate through the file system, or **change directories**, we use the `cd`
command. If you just type `cd` (without any extra words or arguments), it will
take you to your home directory. To see where you are within the file system, 
use the `pwd`, or **print working directory** command:
```
$ cd
$ pwd

/home/ckent
```
In my case, my home directory is located at `/home/ckent`, because as we saw above
using the `whoami` command, my username is `ckent`. Yours will be something different.

**In the case of ADRF all home directories are listed under `/nsfhome`/.**

`/home/ckent/` is a **path**; in this case, the path leads to my home directory.
A path can also be a path to a file name, for example
`/home/ckent/Documents/justice_league_meetings_notes.txt`. Paths that start with `/`
are called **absolute paths**, because they begin at the root directory.
They're *absolute* because they start at the root (the beginning of the filesystem),
so they will always be the same *regardless of your current location*.

**Relative paths** start at your current location. So the relative path to the file
above *from my home directory* (`/home/ckent`) would be
`Documents/justice_leage_meetings_notes.txt`.  Note that `/` has two meanings:
To signify an absolute path (originating in the root directory), and to separate
directories and files in the path.

Let's assume that I (user `ckent`) have the following directory structure:
```
.
├── home
│   └── ckent
│       ├── data
│       │   └── confidential_lexcorp.dat
│       └── Documents
│           └── DailyPlanet_Articles
│               └── superman_saves_the_day.txt

```
There are two directories in `ckent`'s home directory: `data` and `Documents`.
In the `data` directory there is one file: `confidential_lexcorp.dat`. In the `Documents`
directory is a **subdirectory** `DailyPlant_Articles`, which contains the file
`superman_saves_the_day.txt`.

To **list** all the files and subdirectories in a given directory, we can
type `ls`:
```

$ ls

data
Documents
```
Try the command in your terminal.

We see that the contents of `ckent`'s home directory are two directories called
`data` and `Documents`, as we'd expect. If we want to see the contents of one
of these directories, we can use the same `ls` command, but specify the 
directory whose contents we'd like to see as an argument to the `ls` command:
```
$ ls Documents/DailyPlanet_Articles

superman_saves_the_day.txt
```

Note that this would have the same output as running:
```
$ cd Documents/DailyPlanet_Articles
$ ls

superman_saves_the_day.txt
```
where we moved into the `DailyPlanet_Articles` directory and ran the `ls`
command from within the directory.

Say we've navigated to the `DailyPlanet_Articles` directory, and now we want
to navigate to the `data` directory. There are multiple ways to do this:
We could use the absolute path: ` cd /home/ckent/data/` (remember, that will
work from anywhere in the filesystem), or we could use a relative path.
But how do we use a relative path when `data` is not in our current directory,
and we have to go up the tree to reach our destination? We can use the
shorthand `.`. One `.` means our current directory, and `..` means **move up one directory**
from our current location.

First, we would navigate to the `DailyPlant_Articles` directory:
```
cd /home/ckent/Documents/DailyPlant_Articles
```
Now let's move up two directories into the data directory.

```
cd ../../data

```
This command moved us up one directory from `DailyPlanet_Articles` to `Documents`, then up
one more directory to `/home/ckent`, then down one directory to `data`.

> Note: When you start typing in the path the data directory, you can use `TAB` to
> **auto-complete**. The TAB button is your friend on the command-line.
> If TAB is not displaying anything, there are probably  multiple options 
> that match what you've typed so far. Try hitting `TAB` twice to see a list 
> of all the possible completions, then use the **up arrow** to bring back
> what you typed last.
 
If you ever get lost in the file system, remember that the command `cd` (without
specifying another directory) will always drop you into your home directory.
```
$ cd
$ pwd

/home/ckent
```

## Creating, Editing, Moving, Copying, and Deleting Files

Now that we know how to move around the file system, let's put it to work for
us by manipulating the files and directories. Let's get started in our home directory:
```
$ cd
```
Say we're starting a new project called "welfare_project", and we want an
organized directory structure to keep our files together. Every good project
deserves an organized directory structure! First things first, let's **make a
directory** for the project using the `mkdir` command:
```
$ mkdir welfare_project

```
You might have noticed that we named the directory `welfare_project` instead of
`Welfare Project`. *Do not include spaces in your directory and file names* 
-- when using the shell, the shell interpreter interprets a space as a
separation between file names.

For example, if you type:
```
$ mkdir Welfare Project
```
`mkdir` will create two directories, `Welfare` and `Project`.
Sometimes people also prefer not to capitalize file names, or to
only capitalize certain types of names. Those are more personal preferences,
and you should just decide on some conventions that work for you and whomever 
you're collaborating with.

Now let's make a few subdirectories  (we'll be able to change these later 
if we like):
```
$ cd welfare_project
$ mkdir raw_data
$ mkdir clean_data
$ mkdir analysis
$ mkdir paper
$ mkdir notes
$ mkdir model
$ ls

analysis clean_data model notes paper raw_data

```

Great! Now we have a project directory called `welfare_project`, and a way 
to organize the materials for our projects - all done from the command line!

But we've just started to scratch the surface with these very simple examples.
We could have done the same thing (create directories `welfare_project/raw_data`,
`welfare_project/clean_data`, and `welfare_project/analysis`, etc) using the 
following command:
```
$ cd
$ mkdir -v -p welfare_project/{raw_data,clean_data,analysis,paper,notes,model}

```
Let's break down this command. `mkdir` is our old friend who makes directories.
`welfare_project/{raw_data,clean_data,analysis,paper,notes,model}` is a **brace expansion**,
which is shorthand for 
`welfare_project/raw_data 
welfare_project/clean_data 
welfare_project/analysis` etc.

`-v` and `-p` are **flags**, which switch on options for the `mkdir` command.
`-v` is for *verbose*, which means that you want your computer to print out
as much information about the process as possible. In this particular case, it
will output the name of the directory after it is named. `-p` is
for *parent*, so `mkdir` will make parent directories if necessary. In this 
case, since `welfare_project` is the *parent directory* to `raw_data`, 
`clean_data`, and `analysis`, etc. and because `welfare_project` didn't 
previously exist, we need to create the parent before we can create the children.

Let's give this a try! This also gives up an opportunity to learn how to remove
directories. 

> BE VERY CAREFUL with the `rm -rf` command. Make sure you absolutely know
> what you are removing before you remove it! 

```
$ rm -rf welfare_project #this will remove the directory and subdirectories, more on this later

$ mkdir -v -p welfare_project/{raw_data,clean_data,analysis,paper,notes,model}

mkdir: created directory 'welfare_project/raw_data'
mkdir: created directory 'welfare_project/clean_data'
mkdir: created directory 'welfare_project/analysis'
mkdir: created directory 'welfare_project/paper'
mkdir: created directory 'welfare_project/notes'
mkdir: created directory 'welfare_project/model'
```

Now let's `cd` into our `notes` directory and create a TODO list.
```
$ cd /home/ckent/welfare_project/notes
```

You're probably used to editing text files using Microsoft Word or Google Docs;
maybe you have used an application such as Notepad to edit **plaintext files**.
To edit text files from the command line we need a text editor; here we'll use
`komodo-edit`. To start `komodo-edit`, all you have to do is type `komodo-edit` at the
command line:
```
$ komodo-edit
```
A text editor should then appear.
Type in the following, or something similar:
```
1. Create descriptive stats on idhs data in analysis
2. Write up a paper
```
Next, click the "save" button, which looks like a floppy disk. Use the mouse
to find the directory you want to save the file in, change the name of your 
file to `TODO`, and save it. Then **close the Komodo text editor**. 
Back in the Terminal, invoke the `ls` command to double check that your `TODO` 
file saved:
```
$ ls

TODO
```
Sometimes you'll want to **copy** a file, whether to back it up, or to make edits
to it without changing the original version. To copy a file, use the `cp` command,
with where you're copying the file *from* (source) and where you're copying it *to*
(destination):
```
$ cp TODO TODO.backup_dont_delete
$ ls

TODO
TODO.backup_dont_delete
```
Another common task you'll want to do is *move* or **rename** files. Since the file path (or
name) is how you tell your computer (and yourself) *where to look* for that file,
changing its name is equivalent to changing its location, or **moving** it.
So we use the `mv` command. Similarly to `cp`, we pass to the `mv` command where the file you
are moving  *from* (source) and where you're moving it *to* (destination):
```
$ mv TODO TODO.txt
$ ls

TODO.txt
```
Note that the difference between `cp` and `mv` is that `cp` will leave the
original version of the file and create a copy of the file in the filesystem, 
whereas `mv` will change the name of the file and its location in the 
filesystem (so, in the example above, there will no longer be a file
called `TODO`).

You might also notice that we added a `.txt` *file extension* to the end of `TODO`.
Some applications use the file extension to know what kind of file they're
dealing with, so the can only open files with certain extensions. For example,
Microsoft Word documents usually end in `.doc` or `.docx`, and Excel
spreadsheets usually end in `.xls` or `.xlsx`.

We can **remove** a file using the `rm` command:
```
$ rm TODO.txt

```
>Warning: There is no Recycle Bin or Trash Can in UNIX. When
>you delete something, it is gone **forever** -- so be careful!!
> The `rm` command can be a weapon of mass destruction!

Uh oh! We didnt' mean to delete our TODO list!! Luckily, we had the foresight
to create a backup of our to-do list. We can use `cp` to restore the file
from the backup:
```
$ cp TODO.backup_dont_delete TODO.txt
$ ls

TODO.backup_dont_delete TODO.txt
```
That is the basics of the Command Line. Next up: how to use Git.
