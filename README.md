# Introduction to Git

Welcome to the session "Version Control for your network". This guide will provide you an introduction on how you can execute basic operations in Git and how you can start using Git to version control your network configuration files.

## Version Control of Your Network
Before explaining the concept of Git, we will briefly discuss why and when its useful to start version control your network configuration files. 

Until now, we configured networks manually and on a box-by-box basis, e.g. one switch at a time. This sequential process is slow and highly error prone. To work more effectively, we can leverage programmability in our network to configure and apply changes automatically and rapidly. Similar as in software development, we can adapt the DevOps CICD pipeline into our network infrastructure, a process which is called NetDevOps. This means, we treat the network configuration files as code and store it in a version control system like Git. When adding a configuration file or when changes are applied, we spin up a new branch in Git. It allows us to write changes separately from the configuration which is in production. After successfully testing the changes in a separate test environment, the new branch can be merged with the production branch, deployed, and built for production. 

To read more about NetDevOps and get hands-on experience, we recommend you to check out this [GitHub repository](https://github.com/juliogomez/netdevops).

## Git

Git is one of the most popular version control systems. It is free and open source and can efficiently manage large volumes of files. Git allows you to keep track of your files, which can be of any type, including network configuration files. In Git, files can be added quickly, changes can be applied, or features can be added easily by multiple participants in parallel. Since it keeps a record of all changes made in the past, you can always go back and retrieve an older version of your files. It provides a distributed version control system, which means that not only are the files stored on a remote server, but each participant also has a copy of the files stored on their local machine. 


<!-- TABLE OF CONTENTS -->
## Overview
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#git-installation-guide">Git Installation Guide</a>
      <ul>
        <li><a href="#installing-git-on-mac-os">Installing Git on Mac OS</a></li>
        <li><a href="#installing-git-on-mac-windows">Installing Git on Windows</a></li>
      </ul>
    </li>
    <li>
      <a href="#start-with-git">Start with Git</a>
      <ul>
        <li><a href="#set-up-your-remote-github-repository">Set up your Remote GitHub Repository</a></li>
        <li><a href="#set-up-your-local-github-repository">Set up your Local GitHub Repository</a></li>
      </ul>
    </li>
    <li>
      <a href="#basic-git-operations">Basic Git Operations</a>
      <ul>
        <li><a href="#add">Add</a></li>
        <li><a href="#commit">Commit</a></li>
        <li><a href="#pull">Pull</a></li>
        <li><a href="#push">Push</a></li>
        <li><a href="#branch">Branching</a></li>
        <li><a href="#merge">Merge</a></li>
      </ul>
    </li>
  </ol>
</details>


## Git Installation Guide
Before you start, you need to install Git on your local machine. 
### Installing GIT on Mac OS
There are several ways how you can install Git on your Mac OS. If you have Xcode installed, it might already have a pre-installed Git version on your computer.
To verify that Git is installed you can run:
```bash 
git --version
```
If this is not the case or if you want to install a more current version of Git, you can simply use homebrew 
```bash 
brew install git
```
to get it installed on your Mac OS. For more information you can visit [Git-smc](https://git-scm.com/download/mac).

### Installing GIT on Windows 
The easiest way to install Git on a Windows machine is to download the Git installer from [Git-smc](https://git-scm.com/download/win).

## Start with Git

### Set up your Remote GitHub Repository 
1. First, you need to create an account on [GitHub](www.github.com). Pick a username and password and log in to your new account.
2. In your newly created account, on the top right click on the "+"-sign and select "New Repository". Define a repository name and create the new repository. For more detailed instructions you can refer to [GitHub Docs](https://docs.github.com/en/github/getting-started-with-github/create-a-repo).
3. Once the repository is created you can copy the URL of your repository `https://github.com/<user>/<repo>` as you will need it later for the setup on your local machine.

### Set up your Local Git Repository 
1. Open your terminal emulator application and navigate to the folder that you want to use or create a new project folder.
```bash 
mkdir my-project
cd my-project
``` 

2. Initialize a new, empty Git repository on your machine
```bash 
git init
``` 

3. Set up your username and email address. If you add `--global` you only need to run these commands once as the configuration will be stored globally on your system.
```bash
git config --global user.name "John Doe"
git config --global user.email john.doe@example.com
```
4. After having written some files you can add all changes to your first commit
```bash 
git add .
``` 

5. Create the first commit
```bash 
git commit -m "Initial commit"
``` 

6. Add the remote repository 
```bash
git remote add origin https://github.com/<user>/<repo>
```
To verify that your remote repository has been set up type
```bash
git remote -v
```
If it was successful, this command returns the URL of the previously configured remote repository that Git is using to up- or download changes.

7. Finally, push your changes to the main branch of your remote repository
```bash
git push origin main
```

Alternatively, you can also directly clone the remote repository onto your local machine and add files to the existing directory.
```bash
git config --global user.name "John Doe"
git config --global user.email john.doe@example.com
git clone https://github.com/<user>/<repo> 
git add switch.cfg
git commit -m "Add new switch configuration file"
git push origin main
```

To work with several people on the same project you need to give the access to the participants on GitHub. To do this, go to "Settings" > "Manage access" and click "Invite a collaborator".

## Basic Git operations
We have just introduced how you can add a file to your remote Git repository. Here, we will go through them again and explain the most important and basic Git operations. 

### Clone
To copy a remote repository into a new directory on your local machine use the `git clone` command with the URL of your remote repository.
```bash
git clone https://github.com/<user>/<repo> 
```


### Add 
With `git add` the specified files are put into the staging area.
```bash
git add /path/to/file
```
To view which files have already been added, you can use
```bash
git status
```
which gives you an overview over all staged and unstaged files. It further indicates whether a file was modified, newly added, or deleted. By default, all files in the repository will be included into Git and marked as untracked as long as they are not added. To intentionally ignore untracked files that should never be checked in with GitHub their file names can be included in the `.gitignore` file. 

### Commit 
Commits staged files to a local branch
```bash
git commit -m "Commit Message"
```
The command `git log` is useful to view the history of your commits. To limit the output to one line per commit including the git hash and the commit message use
```bash
git log --oneline
```

### Pull
The command `git pull <remote> <branch>` fetches changes on the remote repository and merges them into your local branch. Most of the time, the remote repository name is specified as `origin`. For example, to pull changes onto your local main branch you can run
```bash
git pull origin main
```

### Push
To upload local changes to the remote repository use `git push <remote> <branch>`. It transfers all committed changes to the remote repository.
```bash
git push origin main
```
Before you push your own changes to the remote repository you should always pull remote changes to ensure that your local copy stays in sync with the remote repository.

### Branch
In order to create a new branch and directly navigate to it, use the `checkout` command with the `-b` flag. 
```bash
git checkout -b new_branch
```
Alternatively, you can also first create the branch and then navigate to it
```bash
git branch new_branch
git checkout new_branch
```
To list all branches that exist locally run
```bash
git branch
```
The branch marked with an * is the branch you are currently using, i.e., the branch you are checked out to. 

### Merge
To merge two branches, use the `merge` command. Before doing the merge, verify that you are checked out in the right branch you want to merge to. For example, to merge the my_branch onto your main branch you will need to check out on the main branch and merge then with my_branch.
```bash
git checkout main 
git merge my_branch
```
To handle situations where both branches being merged contain changes Git has a **conflict resolution algorithm** to resolve potential conflicts. A typical conflict situation occurs when two developers make changes to the same file. If the changes are not done on the same lines, the conflict resolution can be performed automatically by Git. However, if the changes were made on the same line, the conflict has to be resolved manually. In such a case you will receive a notification about the conflict with both versions of the file, separated by a `=====`-line. Use a text editor to apply the right changes manually by removing everthing expect the relevant line that you want to keep. 

