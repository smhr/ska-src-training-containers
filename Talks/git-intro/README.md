## Introduction to git

In this section you will learn the basics of Git. We will cover all the 
necessary terminology and commands, so that you become a profficient Git user.
**It is important that you follow this introduction if you have not used Git
before!** The following sections will either expand on the concepts first 
introduced here or will make use of them on multiple occasions.

### In this section you will learn

- [**What version control is and where Git gits**](#1-version-control-and-git)
- [**Basic git terminology**](#2-basic-git-terminology-and-operations)
- [**How to download the code**](#3-basic-git-repositories)
- [**How to change the code**](#4-changing-git-repository)
- [**How to track the changes to the code**](#5-tracking-git-repository-changes)

## 1. Version control and Git

First of all we need to explain what version control is. It is a way of keeping 
track of changes to your files. Modern version control systems also provide 
tools that enable code sharing, making working in a collaboration much easier
**and safer**. 

For example, **this is not version control** (extreme example):
![Not a version control](media/not_version_control.png)

- false sense of security - easy to delete important things
- easy to make changes in a wrong directory
- not suitable for collaborations
- impossible to find that right version of algorithm you wrote 3 months ago
- there are tools that make it easy

Git is one of many version control systems available. It is arguably one of the
most popular solutions and is used in a range of projects from academia to
industry. Even though we are here for Git today, you should be aware of other
version control systems that are still in use today (some more popular than 
the others):

| VCS | Quick description |
|---|---|
| CVS | One of the first version control systems. <br>Pretty much dead, but some projects still insist on using it. |
| Mercurial | Fairly similar to Git, but can be considered a bit more limited |
| SVN | _De facto_ VCS in the past. Less popular these days, but some big projects still use it |
| + many more | Visit: https://en.wikipedia.org/wiki/Comparison_of_version-control_software <br> for an exhaustive list of the version control software from the past and the present

**Why Git?**
- works on Linux, Windows and macOS
- easy to install: all major Linux distributions have relatively new version available (you can always build form the source code if the newest version is required), .exe installer for Windows and an installer for macOS
- uses command line interface (CLI) but GUIs are available
- **you need only a few commands to start**
- very difficult to permanently erase the data by mistake
- works both locally and remotely

## 2. Basic Git terminology and operations

We will not be running any commands in this part just yet. Before we do that, there are a few concepts specific to Git that you have to be familiar with: 

- **[git] repository/repo**
- **3 stages of your repository:**
  - ***modified*** - you made changes to some of your files, you saved them with your editor of choice (e.g. vim), but Git is not yet aware of them. It detects that something changed, but has not yet stored it in its long-term memory (a database)
  - ***staged*** - you tell Git which changes should be stored in the database next (you stage these files)
  - ***commited*** - Git takes all the staged files you ordered it to keep track of and stores their snapshots (how they look at that point in time) into the database
  
  Your workflow with Git should generally look something like this:
  ![Git workflow](media/git_stages.png)
- **branch**
- **main/master branch**

## 3. Creating and getting a Git repository
So you have a new codebase or a ducment that you have just started working on and decided to start using Git to keep tract of all the changes you make. As we have already mentioned, it is eas yto start using Git and you need only a single command to initialise it for your project (yes, it's really that easy). If can go to your project's directory and run the following command:

`git init`

If you now check all the files, including the hidden ones (using `ls -a` command on Linux and macOS), you will see a new `.git` directory appear. **This is the place where all of the necessary information for your repository is kept.** You know how we said it is difficult to remove the data by mistake? Make sure that mistake is not removing `.git` directory, especially with the `rm` command, as that will delete all of your repository history if you do not store is securely somewhere else.

If you store you repository in a single place, you get all the advanteges of version control, such as tracking the changes to your codebase over the time. However, you are still susceptible to losing all your data if for example your laptop gets damaged or stolen. That is why it is important to store your repository on a remote server, be it privately hosted or an existing solution such as GitHub or GitLab (these will be covered in details in the next couple of sections).

How do you get this repository though? That is what a `clone` command is used for. If you have a link to the GitHub repository, for example your coworker shared a link with you to some amazing plotting library and wants you to have a look at the source code, you can download the contents of this repository with a single command:

`git clone <repository link>`.

For example, to clone an official Git repository (using Git of course and hosted on GitHub), you should run

`git clone https://github.com/git/git.git` (that's a lot of git's)

This commands downloads the repository and automatically places it inside a `git` folder (don't confuse it with a `.git` folder, which contains all the information relevant to the version control). 

By default Git will always create a folder with a name that is the same as the repository name (in this case `git`). it is possible that you already have a folder named git, maybe with some training materials, but you still want to `clone` the official Git repository. Do you have to move your existing folder somewhere else? Rename it? These sure are viable options, but (arguably) the most convenient method is to force Git to use a different directory name:

`git clone https://github.com/git/git.git mygit`

With this command we again get all the data from the official Git repository, but this time this data is placed inside the `mygit` directory, making any moving or renaming of existing directories unnecessary.

When you `clone` a git repository, you do not have to run the `git init` again - the `.git` directory and all the required files are downloaded automatically.

## 4. Changing a Git repository

## 5. Tracking Git repository changes

## Further reading