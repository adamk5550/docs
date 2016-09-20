# Git: An Introduction

*Part of a series of articles on Git by [DigitEels](https://github.com/digiteels).*  
[First Time Setup](2 First Time Setup.md) :arrow_forward:

## Contents

- [Overview](#overview)
- [Advantages](#advantages)
- [Concepts](#concepts)
  - [Repositories](#repositories)
  - [Remote vs. Local](#remote-vs-local)
  - [Workspace](#workspace)
  - [Commits](#commits)
  - [Branches](#branches)
  - [Merging](#merging)
    - [Merge Conflicts](#merge-conflicts)

## Overview

Git is an open source version control system covered by the
[MIT license](https://github.com/git/git-scm.com/blob/master/README.md#license). It is currently the
most popular version control system in use and ubiquitous in programming.

## Advantages

The following selling points make a compelling case for using Git and are why Newcastle Mobility
uses Git on all of its projects:

- **Centrally stored code**  
The master copy of each Git project is stored in one place, typically on a server. No more disparate
code scattered between multiple developers.

- **Incremental versioning**  
Git stores updates as references to the previous update. This ensures projects don't rapidly balloon
in size and allows for rollbacks to any point in time.

- **Concurrent collaboration**  
Git allows multiple developers to modify the same code at once through branching changes and
intelligent merging.

## Concepts

This section will cover the most important concepts in Git which are key to understanding how Git
works. If you are not using Git yourself but are working with developers who are, this section will
give you an insight into the terms they use and what it means.

### Repositories

Repositories are the most fundamental concept in Git. They represent a single project or code base,
and store all information related to it. This includes all files, changes and Git-specific
structures that will be covered below. Typically each new project is given its own Git repository.

### Remote vs. Local

Although it is possible to have a Git repository that exists solely on a particular developer's
computer, it's not very useful to anyone else. As a result the repository needs hosting somewhere
that the entire development team can access. But how do they contribute to it?

When a repository is hosted on a server, it is referred to as a **remote repository**. Typically
this is set up in a way that means it cannot be edited directly on the server.

In order for a developer to contribute to the remote repository, they **clone** the remote
repository, making a copy of it on their computer; this is called a **local repository**. The
developer can then freely make changes to this code without immediately affecting the remote repo.

Because of this, each developer can have their own local repo without having to worry about code
conflicting with each other until it is time to **push** those changes to the remote repo.

### Workspace

A repository is represented locally as a directory. Within this Git stores all of its meta-data in
the hidden `.git` sub-directory. Everything else in the repository is referred to as the
**workspace**.

The files in the workspace are populated and can be changed by Git, but can also be changed by the
developer. This is how the codebase is modified, and therefore where development takes place. Git is
then able to see what has changed.

### Commits

Commits can be considered a package of changes made by a developer. They include: everything that
has changed since the last commit, an author, unique ID (SHA), timestamp and a message created by
the developer to label the changes.

Although there are no set rules on when a commit should be made, typically each is an individual
working feature. *Every change in Git is part of a commit*.

### Branches

Branches allow code in a repository to be in multiple states at once. This is a bit like having
multiple versions of the code base kept at once, but can also be used to separate out features that
are being contributed to by multiple developers. A branch is just a set of commits connected
together.

All repositories start with the `master` branch by default. Here is a scenario of branches in
action:

The `master` branch contains 3 commits creating a website homepage. From the latest commit a new
branch is created called `login`. 4 commits are then made here. At this point there are 2 branches:
`master` and `login`. Login is 4 commits ahead of the master branch.

Newcastle Mobility has a set way of using branches:

- `master`: Production code that is ready for deployment.
- `development`: Features that have passed code review and **merged** into the codebase.
- `feature/ID-1234`: Feature in development, represented by its ID.

### Merging

Once development has occurred in two or more branches, a **merge** is required to bring the code
back together. Merging adds commits not present in one branch to the other, in one direction only.

If each feature has its own branch, eventually each branch needs merging back into a single branch
(Newcastle Mobility uses `development`) so that the codebase can be consolidated.

When merging into a branch that is behind the target branch and has no new commits of its own
(such as in the example above), this is a straightforward process.

#### Merge Conflicts

Often merging is not straightforward; if both branches being merged have "new" commits that don't
yet exist in the other, there is potential for a merge conflict to occur.

Fortunately Git is competent enough to deal with scenarios where the same piece of code wasn't
changed by both files. When this is true, Git will automatically perform a merge and all is good.
This means that developers can even change different parts of the same file without issue.

If Git is not able to automatically perform a merge, the developer is shown where the
**merge conflicts** are and is asked to resolve them. Git places both copies of the code in the
files so that the developer can remove one or combine both before telling Git to continue.
