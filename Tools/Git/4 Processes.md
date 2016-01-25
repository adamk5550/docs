# Git: Processes

## Contents

- [Cloning a Remote Repository](#cloning-a-remote-repository)
- [Creating a Feature Branch](#creating-a-feature-branch)
- [Resolving Merge Conflicts](#resolving-merge-conflicts)
- [Pushing an Initial Patchset to Gerrit](#pushing-an-initial-patchset-to-gerrit)
- [Pushing a New Patchset to Gerrit](#pushing-a-new-patchset-to-gerrit)

### Cloning a Remote Repository

#### Commands

- [git clone](./3%20Commands.md#git-clone)

#### Explanation

When beginning work on a new project it is necessary to create a local copy of the remote repository
on your computer. This is done using the [git clone](./3%20Commands.md#git-clone) command.

Using command line Git (*Terminal* or *Git Bash*) navigate to your `Repositories/` directory. You
will need to find the repository URL from relevant enterprise sources such as Confluence.

Run [git clone](./3%20Commands.md#git-clone) using these details. Once downloaded your local
repository subdirectory is ready to go.

### Creating a Feature Branch

#### Summary

- [git branch](./3%20Commands.md#git-branch) / [git checkout](./3%20Commands.md#git-checkout)

#### Explanation

When picking up a new Agile story for development, a new local feature branch should be created.
This gives you space to create your changes separately from other stories and most importantly,
the `master` and `development` branches; these branches should never be developed in.

Ensure there are no uncommitted changes in your local repository before beginning. Run
[git branch](./3%20Commands.md#git-branch) with a branch name, or
[git checkout](./3%20Commands.md#git-checkout) with the `-b` argument to create a new branch.

Feature branch names should be the full JIRA story ID, for example `ID-1234`. This makes it easier
for you to identify which story the branch is tracking changes for.

Finally, ensure your feature branch is **never** pushed to the remote repository if using Gerrit.
Gerrit does not allow code reviews to be pushed if they already exist anywhere in the remote
repository,
