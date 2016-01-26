# Git: Commands

*Please note that command output color is not present in this document due to limitations with the
Markdown file format.*

## Contents

- Commands
  - [git add](#git-add)
  - [git branch](#git-branch)
  - [git checkout](#git-checkout)
  - [git clone](#git-clone)
  - [git commit](#git-commit)
  - [git fetch](#git-fetch)
  - [git log](#git-log)
  - [git pull/push](#git-pullpush)
  - [git remote](#git-remote)
  - [git reset](#git-reset)
  - [git status](#git-status)
- Patterns
  - [pathspec](#pathspec)
  - [refspec](#refspec)

## git add

`git add [options] [pathspec]`

Add a selection of changed files to the staging area. Files in the staging area will be part of the
next [commit](#git-commit) - this allows commits that don't include all changes to be made.

A *[pathspec](#pathspec)* is only required when `--all` is not present.

### Options

#### -A, --all

Add all changed files in the workspace, regardless of the current directory.

## git branch

`git branch [options] [branch]`

List all branches that exist in the local repository. Further options can be used to create and
delete branches.

By default and without providing a *branch* each line displays the branch name. The currently
checked out branch is coloured green and preceded with an asterisk `*`:

```
$ git branch
  feature/ID-1234
  feature/ID-1235
* development
  master
```

Providing a *branch* creates a new branch providing the branch name is unique and unused. The branch
is created from the HEAD (latest commit in the current branch), but is not automatically
[checked out](#git-checkout).

### Options

#### -a, --all

List both local and remote branches, coloured green and red respectively. Useful for showing remote
branches not yet tracked locally.

#### -d, -D, --delete

Delete the provided *branch*. `-d` will refuse to delete branches not up to date with the remote
repository, use `-D` to force delete.

#### -v, -vv, --verbose

Display more information when listing branches. `-v` adds the last commit message and shortened SHA,
`-vv` additionally adds upstream (linked remote) branches when present:

```
  feature/ID-1234 ba3c79b ID-1234: Corrected off-by-1 error in calculator
  feature/ID-1235 2d68a63 ID-1235: Sass boilerplate
* development     17b9f25 [origin/development] ID-1230: Added login screen
  master          f4bdc1d [origin/master] Initial commit
```

## git checkout

`git checkout [options] [branch]`

Check out another *[branch](#git-branch)* in the local repository. This effectively changes the
contents of the workspace to reflect the commits present in the targeted branch:

```
$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
```

### Options

#### -b

Create a new *[branch](#git-branch)* providing the branch name is unique and unused. The branch is
created from the HEAD (latest commit in the current branch) and is automatically
[checked out](#git-checkout).

## git clone

`git clone [URL] [name]`

Create a new local repository by cloning the contents of a remote repository accessible by the
provided *URL*. The new local repository is stored in a new relative subdirectory.

By default the subdirectory name is the name of the remote repository, or a *name* can be provided
instead. Either way, the subdirectory can be freely renamed without affecting its contents.

## git commit

`git commit [options]`

Package changed files in the [staging area](#git-add) as a new commit.

As a commit contains your name and email address, these variables must be pre-configured in Git -
this is covered in [First Time Setup](./2%20First%20Time%20Setup.md#configuration). Git also uses
your system's default command line text editor for commit message entry - this can be changed by
running `git config --global core.editor vi`, replacing `vi` with your desired editor.

When this command opens your command line text editor, review the staged changes and enter a commit
message on a new line (commented out lines begin with `#`). Multiple lines can be entered though it
is advised that single-line commit messages are used for brevity. Once done, save and close your
editor to finalise the new commit.

### Options

#### -m, --message

Enter the commit message directly on the command line instead of via your command line text editor.
Follow `-m` with a text string surrounded by double-quotes `"` to use as the commit message.

#### --amend

Amend the staged changes to the HEAD (latest commit in the current branch) instead of creating a new
commit. This will open the existing commit message with your command line text editor for editing,
or `-m` can be used to replace the existing message.

## git fetch

`git fetch [options]`

Fetch objects from the remote repository that are currently being tracked by the local repository.
This effectively downloads the latest [commits](#git-commit) for [branches](#git-branch) the local
repository is tracking, without applying new commits to branches immediately.

### Options

#### --all

Fetch all objects regardless of whether they are being tracked. This is useful for fetching branches
that are new to the remote repository and do not exist in the local repository.

## git log

`git log [options]`

List all [commits](#git-commit) in the current branch, sorted from most to least recent.

Without options all commits are listed, displaying 4 lines of information: SHA, author name and
email, date, and message. If the commit log does not fit vertically on the screen it is opened in a
command line pager program such as `less`, which allows navigation up and down the log. `less` can
be closed by pressing `q`:

```
$ git log
commit 1ecc1f1688d23aae9feaa7d8cf4cf054cb3446c0
Author: joe.bloggs <joe.bloggs@company.com>
Date:   Wed Jan 20 09:56:10 2016 +0000

    ID-1230: Added login screen

commit 2f78a38e571a4382cc2689f4dfecf731669e505c
Author: joe.bloggs <joe.bloggs@company.com>
Date:   Tue Jan 19 16:27:53 2016 +0000

    ID-1230: Configured user authentication controller

commit 5de443519a20ef260368cda1bfbf28d0e4d84dbf
Author: joe.bloggs <joe.bloggs@company.com>
Date:   Tue Jan 19 15:46:39 2016 +0000

    ID-1230: Angular.js boilerplate
```

### Options

#### -n

Limit the amount of recent commits shown to a specific number. This can be represented as `-n 5` or
shortened to `-5`.

#### --oneline

Output one line per commit and only show the shortened commit SHA and message. Useful for checking
large quantities of commits quickly when only the commit message is needed:

```
1ecc1f1 ID-1230: Added login screen
2f78a38 ID-1230: Configured user authentication controller
5de4435 ID-1230: Angular.js boilerplate
```

## git pull/push

`git [pull/push] [remote] [refspec]`

Pull/push commits from/to the remote repository. These commands are used to keep local and remote
branches up to date with each other, allowing changes to be shared between users via the remote
repository.

The *remote* to interact with must be provided; when cloning a repository this is stored as `origin`
and will typically be the remote name unless other remotes are added later. The
*[refspec](#refspec)* defines the branch or reference to pull/push from/to.

Pull/pushing may fail if there are merge conflicts, permission issues (Gerrit) or the remote
*[refspec](#refspec)* is invalid.

## git remote

`git remote [options]`

Show information about remote repositories being tracked by the local repositories. By default shows
a simple list of the remotes.

Without options and no additional remotes, this will unhelpfully show very little:

```
$ git remote
origin
```

### Options

#### -v, --verbose

Display remote URLs as well as separating remotes into `fetch` and `push` remotes:

```
$ git remote -v
origin https://git.company.com/repos/example.git (fetch)
origin https://git.company.com/repos/example.git (push)
```

## git reset

`git reset [options] [pathspec]`

Remove a selection of changed files from the staging area. This is effectively the opposite of
[git add](#git-add).

A *[pathspec](#pathspec)* is only required when options are not present.

### Options

#### --soft

Reset the current [branch](#git-branch) to the *refspec* supplied after `--soft`, potentially
changing the [commits](#git-commit) present. The contents of the working directory however are
preserved - any previously committed differences are kept in the staging area.

#### --hard

Similar to `--soft` but permanently deletes any tracked changes in the working directory. Do not use
lightly.

## git status

List file changes in the working directory since the last [commit](#git-commit). This includes
additions, deletions, and modifications.

Changes listed are grouped by change type and coloured based on whether they are in the
[staging area](#git-add) (green) or not (red).

```
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   Staged New File.txt

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	deleted:    Deleted File.txt
	modified:   Edited File.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	New Directory/
	New File.txt
```

### Options

#### -s, --short

Output one line per change. Lines start with coloured single characters representing the change type
and staging area status. In case coloured output is not supported, the staging area status is also
represented by the column the character is in: first column for staged, second column for unstaged.

Common characters are: `A` (addition), `D` (deletion), `M` (modification), and `??` (untracked).

```
$ git status --short
 D "Deleted File.txt"
 M "Edited File.txt"
A  "Staged New File.txt"
?? New Directory/
?? New File.txt
```

## pathspec

An expression that selects one or more files from the relative directory structure. Used by
[git add](#git-add) and [git reset](#git-reset).

|Example      |Explanation                                                         |
|-------------|--------------------------------------------------------------------|
|`file.txt`   |A specific file.                                                    |
|`a.css b.css`|Multiple space-separated specific files.                            |
|`Images/`    |All non-hidden non-ignored files in and below a directory.          |
|`*`          |All non-hidden non-ignored files in and below the current directory.|
|`*.js`       |All files ending in `.js` in and below the current directory.       |

### refspec

A branch or other storage area in a repository. Used by [git pull/push](#git-pullpush).

|Example                    |Explanation                                                   |
|---------------------------|--------------------------------------------------------------|
|`master`                   |Current local branch to `master` remote branch.               |
|`development:master`       |`development` local branch to `master` remote branch.         |
|`:development`             |Push nothing to `development` remote branch, deleting it.     |
|`HEAD:refs/for/development`|Push to `development` remote branch Git code review area.     |
|`origin/master`            |Reset to the local repository's stored `master` remote branch.|
