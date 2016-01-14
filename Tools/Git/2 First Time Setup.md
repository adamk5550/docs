# Git: First Time Setup

## Contents

- [Introduction](#introduction)
- [Installation](#installing-git)
  - [OS X](#os-x)
  - [Microsoft Windows](#microsoft-windows)
- [Using Command Line Git](#using-git)
  - [OS X](#os-x-1)
  - [Microsoft Windows](#microsoft-windows-1)
- [Configuration](#configuration)
- [SSH Key Generation](#ssh-key-generation)
  - [Checking for an Existing Key](#checking-for-an existing-key)
  - [Generating a New Key](#generating-a-new-key)
  - [Adding Your Key to Gerrit](#adding-your-key-to-gerrit)

## Introduction

This guide provides instructions on how to install and configure git ready for enterprise usage via Gerrit. Steps are provided for both Microsoft Windows and OS X users.

Git usage via a third party GUI is not supported by this guide - steps are provided for command line use only.

## Installation

Even if Git is already installed, complete this step to ensure the latest version is installed.

Before continuing, download the latest stable version of Git for your operating system from http://git-scm.com/.

### OS X

Run the Git installer file `.dmg`. A new Finder window will show its contents, including a package file `.pkg` and a readme `.txt`.

Follow the instructions in the readme, in particular *Step 2 - Remove stubs* (if present).

### Microsoft Windows

Run the Git installer file `.exe` and carefully consider each option presented on each installation screen. Ensure the following settings are configured correctly:

- **Select components**  
  Windows Explorer Integration can be unselected at the user's preference. By default this adds *Git Bash Here* to the right click context menu in folders.

- **Adjusting your PATH environment**  
  Select *Use Git from Git Bash only* (top option).

- **Choosing the SSH executable**  
  Select *Use OpenSSH* (top option).

- **Configuring the line ending conversions**  
  Select *Checkout Windows-style, commit Unix-style line endings* (top option).
