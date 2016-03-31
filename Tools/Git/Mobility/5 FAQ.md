# Git: Frequently Asked Questions

*Part of a series of articles on Git by
[Newcastle Mobility](https://github.com/newcastle-mobility).*  
:arrow_backward: [Processes](4 Processes.md) | [Miscellaneous](6 Misc.md) :arrow_forward:

Answers to questions that are not covered on [other](1 Introduction.md)
[Git](2 First Time Setup.md) [documentation](3 Commands.md) [pages](4 Processes.md).

## Contents

- [What do I do with my local feature branch once finished?](#what-do-i-do-with-my-local-feature-branch-once-finished)
- [How do I push to Gerrit if I have multiple commits?](#how-do-i-push-to-gerrit-if-i-have-multiple-commits)
- [How do I revert a commit?](#how-do-i-revert-a-commit)
- [How do I change branch if I have unstaged changes?](#how-do-i-change-branch-if-i-have-unstaged-changes)

### What do I do with my local feature branch once finished?

As covered by [Creating a Feature Branch](4 Processes.md#creating-a-feature-branch), a local
feature branch is created for each story developed by the user. This is never pushed to the remote
repository due to how Gerrit works.

As a result the local feature branch can be left in place without consequences, or deleted after
checking out any other branch:

`git branch -D` followed by the feature branch name.

### How do I push to Gerrit if I have multiple commits?

For each [commit pushed to Gerrit](4 Processes.md#pushing-an-initial-patchset-to-gerrit), a new
review is created. This means that if multiple commits are pushed at once, multiple reviews are
created that are dependent on each other; this is a massive headache to deal with and should be
avoided entirely. This is why
[pushing another patchset to Gerrit](4 Processes.md](#pushing-another-patchset-to-gerrit) involves
amending the same commit.

Multiple commits can be squashed into a single commit using [git rebase](3 Commands.md#git-rebase)
and the `-i` or `--interactive` option. Follow the below instructions after committing all of your
changes and checking out the correct feature branch:

- `git rebase -i HEAD~4`
  - Replace `4` with the amount of commits being squashed into one.

A list of the selected commits will be displayed in your command line text editor, arranged least
to most recent (backwards compared to [git log](3 Commands.md#git-log)):

```
pick dbccb83 ID-1230: Configured user authentication controller
pick 7623f23 ID-1230: Added login screen
pick 28e5880 ID-1230: Added styling for login screen
```

Modify all but the top line, changing `pick` to `squash`. This tells Git to squash the commits into
the top (least recent) commit:

```
pick dbccb83 ID-1230: Configured user authentication controller
squash 7623f23 ID-1230: Added login screen
squash 28e5880 ID-1230: Added styling for login screen
```

Saving and exiting the command line text editor will open it once again, this time to enter the
squashed commit's message. All squashed commit messages will be shown:

```
# This is a combination of 3 commits.
# The first commit's message is:
ID-1230: Configured user authentication controller

# This is the 2nd commit message:

ID-1230: Added login screen

# This is the 3rd commit message:

ID-1230: Added styling for login screen
```

All lines not commented out (beginning with `#`) will be kept once you save and exit. Either keep
an existing commit message or write a new one, and then delete all non-commented out lines:

```
ID-1230: Configured user auth controller and added login screen
```
Saving and exiting the command line text editor will begin the squashing process. During each
individual squash it is possible for a [merge conflict](4 Processes.md#resolving-merge-conflicts) to
occur which will need resolving manually before the squash completes.

### How do I revert a commit?

It is possible to quickly revert a commit providing it:

- Has not been pushed to the remote repository yet.
- Is at the HEAD (latest commit) of its branch.
- Does not exist in any other branch yet.

If that's the case, check out the branch it is in and run the following command to
[reset](3 Commands.md#git-reset) to before the commit and lose all of its changes in the process:

`git reset --hard HEAD~1`

If you would like to revert the commit but instead keep the changes in the staging area, replace
`--hard` with `--soft`.

### How do I change branch if I have unstaged changes?

#### Untracked Only

If the changes are untracked (use [git status](3 Commands.md#git-status) to find out), changing
branches will not disturb the files in question.

#### Discard Changes

If you do not wish to keep the unstaged changes, [git reset](3 Commands.md#git-reset) can be used to
revert to the last commit by following the `--hard` option with `HEAD`. Untracked changes will need
deleting manually.

#### Keep Changes Using stash

Untracked changes can temporarily be stashed by running the `git stash` command. This stores the
changes within the local repository for later use and will allow another branch to be checked out.

Once complete, return to the **same** branch and run `git stash pop` to un-stash the unstaged
changes.

#### Keep Changes by Creating a Commit

Another method involves creating a temporary commit and soft [resetting](3 Commands.md#git-reset) it
once complete. This method is not suitable if you are planning on interacting with the current
branch from another branch ([merge](3 Commands.md#git-merge), [rebase](3 Commands.md#git-rebase)).

Use [git add](3 Commands.md#git-add) and [git commit](3 Commands.md#git-commit) as normal to create
it.

Once complete, [checkout](3 Commands.md#git-checkout) the same branch and use
`git reset --soft HEAD~1` to unpack your temporary commit into the staging area. Changes can be
unstaged if required with [git reset](3 Commands.md#git-reset).
