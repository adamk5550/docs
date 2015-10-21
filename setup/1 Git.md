# Setup 1: Git

[git]: http://git-scm.com/

## Contents

- [Overview](#overview)
- [Installing Git](#installing-git)
  - [Apple OSX](#apple-osx)
    - [With Xcode](#with-xcode)
    - [Without Xcode](#without-xcode)
  - [Microsoft Windows](#microsoft-windows)
- [Accessing Command Line Git](#accessing-command-line-git)
  - [Apple OSX](#apple-osx-1)
  - [Microsoft Windows](#microsoft-windows-1)
- [Git Configuration](#git-configuration)

## Overview

Git is a distributed version control system used by the Newcastle Mobility team to manage code, during and after development. It provides the following benefits:

* Allows for a centralised code store on a server.
* Acts as a backup solution, allowing rollbacks.
* Facilitates multiple developers working on the same code at once.

This page will guide you through installing Git, using SSH keys to authenticate with Gerrit for code review purposes, and cloning your first project repository.

## Installing Git

Git is a piece of software that needs installing on your computer to be used. First use the command line to check if Git is already installed.

- **Apple OSX:** *Terminal*
- **Microsoft Windows:** *Command Prompt*

```bash
git --version
```

If a version number is returned, Git is installed and ready to use and you may [skip](#accessing-command-line-git) to the next step.

### Apple OSX

#### With Xcode

Git is installed automatically as part of the Xcode installation, which is not covered in this guide.

#### Without Xcode

Git can be downloaded from the [Git website][git]. Ensure that the latest source release for Mac is downloaded.

Open the `.dmg` file downloaded. This should show its contents in a new Finder window.

Follow the instructions in `README.txt` to install the `.pkg` file and configure for use; the latter step is important, don't miss it out!

### Microsoft Windows

Git can be downloaded from the [Git website][git]. Ensure that the latest source release for Windows is downloaded.

Run the installer `.exe` file and make sure that the options detailed below are selected. Do not click next until you are certain that the options are correct.

- **Select Components:**
  - *Windows Explorer Integration* can be unselected if you do not wish to add a *Git Bash here* right-click context menu option to Explorer.
- **Adjusting your PATH environment:**
  - Select *Use Git from Git Bash only*.
- **Choosing the SSH executable:**
  - Select *Use OpenSSH*.
- **Configuring the line ending conversions:**
  - Select *Checkout Windows-style, commit Unix-style line endings*.

## Accessing Command Line Git

### Apple OSX

Open a new *Terminal* window. If need be *Terminal* can be found via Spotlight, the magnifying glass icon in the top right corner of the screen.

### Microsoft Windows

If the Git installation instructions above were followed correctly, Git can now be accessed via the *Git Bash* application.

This is built on *Command Prompt* and allows access to the UNIX Bash shell, allowing you to use basic UNIX commands on your computer.

## Git Configuration

Before using Git for the first time, some additional configuration is needed to tell Git who you are. This is needed for our enterprise-level authentication that is part of Gerrit; if this step is not completed correctly you will be unable to push commits to Gerrit for code review.

Regardless of platform, run the following commands, substituting the angle brackets as needed.

```bash
git config --global user.name <enterprise id>
git config --global user.email <work email>
```

Additionally **only** Microsoft Windows users need to run the following command to provide automatic line break conversion in their working directory:

```bash
git config --global core.autocrlf true
```

All of these configuration values are stored in the `.gitconfig` file located in your home directory. In *Terminal* *or Git Bash* running the following command will show you the stored values:

```bash
cat ~/.gitconfig
```
