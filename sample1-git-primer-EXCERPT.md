# Git Primer for the Impatient

Version control is a core skill for technical communicators working in docs-as-code environments. This primer covers Git essentials — from initial configuration to branching and syncing — written for documentation professionals adopting Git-based workflows.

# Short introduction

Git is a VCS (Version Control System). Basically, a version control system allows you to perform a number of essential tasks, including:

- creating a copy of the original project
- tracking all the changes that you have made to the project
- keeping track of previous versions of the project
- marking milestones during the development cycle

Git was initially introduced in the Linux community as a revision control system for kernel development. Unlike centralized version control systems such as Subversion and CVS, Git is a fast distributed system.

With Git, you do not need a single central repository to work on your project, since you can work locally on a full clone of the remote repository. What is beautiful about Git is that you can also use it to automate your documentation process.

# Git states

In a Git workflow, your files will basically go through 3 different states:

- Modified: This is when you make changes to the files in your working directory.
- Staged: In this intermediate state, Git saves snapshots of the modified files in the staging area.
- Committed: Once you commit your changes, Git will save the staged files in the Git directory.

The Git directory is a hidden folder `.git` at the top level of your working tree.

# Installation on Linux

To install Git on Debian based distros, run the following commands:

```
$ sudo apt-get update
$ sudo apt install git-all
```

For Red Hat based distros, use the following commands:

```
$ sudo dnf update
$ sudo dnf install git-all
```

# Initial configuration

Git ships with a tool called `git config` that allows you to set multiple configuration variables. These variables control how Git looks and behaves.

Depending on your system, the configuration variables will be stored at different locations. For further details about the topic, check Git's official documentation.

Once you have installed Git, you should set your credentials by indicating your user name and email. To do so, type the following commands:

```
$ git config --global user.name "Random User"
$ git config --global user.email randomuser@test.com
```

To check all your personal settings, type the following command:

```
$ git config --list
```

# Git essential commands

Here are the most essential commands that will get you up and running within minutes.

## Initializing a new repository

If you already have a project, you can immediately navigate to the relevant folder, then initialize an empty repository with the command:

```
$ git init
```

## Cloning an existing repository

To clone an existing repository, type the command:

```
$ git clone <URL>
```

For instance, if we want to clone the documentation repository from the collaboration platform Codeberg, then we will type the following command:

```
$ git clone https://codeberg.org/Codeberg/Documentation.git
```

## Adding files

Git will not begin tracking your files unless you add them. To add all the files that are available in your directory to Git, type the command:

```
$ git add -A
```

You can achieve the same result with the following command:

```
$ git add .
```

Either way, the files existing in your project's folder will be added recursively to Git's index.

To add a single file called 'foo', type the command:

```
$ git add foo
```

## Committing changes

To commit your changes with a message, type the command:

```
$ git commit -m "Initial commit for Git's documentation project"
```

Note: If you do not insert a commit message at the time of committing your files, i.e. if you only type `git commit`, Git will launch the default text editor that is set in your environment variables.

## Checking the status

If you want to check the status of the project's files, type the command:

```
$ git status
```

The command `git status` provides the default description. To get a verbose description, type the following command:

```
$ git status -v
```

If you prefer a shorter description, type the command:

```
$ git status -s
```