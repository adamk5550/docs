# Git: Commands

## Contents

- [git add](#git-add)
- [git branch](#git-branch)
- [git checkout](#git-checkout)
- [git commit](#git-commit)
- [git fetch](#git-fetch)
- [git log](#git-log)
- [git pull/push](#git-pull-push)
- [git remote](#git-remote)
- [git reset](#git-reset)
- [git status](#git-status)

## git add

Add a selection of changed files to the staging area. Files in the staging area will be part of the next commit, meaning commits don't have to include all changed files.

See [git commit](#git-commit) for more info about commits.

### Options

#### -A, --all

Adds all changed files in the workspace, regardless of the current directory.

### Pathspecs

When the `--all` option is not used, `git add` requires a *pathspec* option to specify which files to add:

|Example      |Type     |What is Added                                       |
|-------------|---------|----------------------------------------------------|
|`file.txt`   |file     |The specific file.                                  |
|`a.txt b.txt`|files    |The specific files.                                 |
|`Images/`    |directory|All files in the directory and below subdirectories.|
|`*`          |wildcard |All files in or below the current directory.        |
|`*.js`       |wildcard |All files ending in `.js` (JavaScript files).       |

## git branch

Primarily used for listing all of the branches present in the repository. Can also create and delete branches.

Running `git branch` without arguments lists all local repo branches, one line each, with the currently checked out branch preceded with an asterisk `*`:

```
$ git branch
  feature/ID-1234
  feature/ID-1235
* development
  master
```

Running `git branch` proceeded with a unused branch name will branch from the HEAD (latest commit in the current branch) and create it, but not check it out. See [git checkout](#git-checkout) for more info about checking out branches.

### Options

#### -d, -D, --delete

Deletes the branch specified after the option flag. `-D` is a forceful version of `-d` which can be used to delete branches not up to date with the remote repo.

#### -v, -vv, --verbose

Displays more information about the branches listed. `-v` shows the last commit message and SHA, `-vv` additionally shows upstream (linked remote) branches when present:

```
  feature/ID-1234 ba3c79b ID-1234: Corrected off-by-1 error in calculator
  feature/ID-1235 2d68a63 ID-1235: Sass boilerplate
* development     17b9f25 [origin/development] ID-1230: Added login screen
  master          f4bdc1d [origin/master] Initial commit
```

## git checkout

Checks out another branch in the local repository. This means changing the contents of the workspace to reflect the commits present in the targeted branch.

```
$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
```

### Options

#### -b

Running `git branch -b` proceeded with an unused branch name will branch from the HEAD (latest commit in the current branch), create it and check it out immediately. See [git checkout](#git-checkout) for more info about checking out branches.

## git commit

Creates a new commit from the staged changes. See [git add](#git-add) for more info about the staging area and adding changes to it.

`git commit` requires your name and email to be pre-configured - this is covered in [First Time Setup](../2%20First%20Time%20etup.md). Additionally Git will use your system's default command line text editor, which can be changed by running `git config --global core.editor vi`, replacing `vi` with your desired editor.

When your text editor opens, several pre-populated, commented out (`#`) lines of configuration and [git status](#git-status) will be present. Write your commit message on one or more un-commented lines before save and exiting your editor. This will finalise the new commit.

### Options

#### -m, --message

Enter the commit message as part of the `git commit` command instead of opening a command line text editor. Ensure that the string proceeding `-m` is surrounded with double-quotes `"` if spaces are present.

#### --amend

Amends the staged changes to the latest commit instead of creating a new commit. This will open your command line text editor to provide an opportunity to modify the commit message; as a result `-m` can be combined with `--amend`.

`--amend` without any staged changes can be used to simply re-enter the latest commit's message.

## git reset

Removes a selection of changed files from the staging area. See [git add](#git-add) for more info about staging.

### Pathspecs

`git reset` requires a *pathspec* option to specify which files to remove. This works in the same way as [git add](#git-add), see its pathspec section for examples.

## git status

Shows the files that have changed in the repository's working directory since the last commit. This includes new files, deleted files and files that have been changed.

Files listed are grouped by change type and are colour coded based on whether they are in the staging area or not - green for staged and red for unstaged. For more info about staging, see [git add](#git-add).

*Colour omitted from examples due to Markdown limitations*

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

Each change outputs one line only. Shorthand status and staging characters are placed on the start of each line. This view is useful for reducing visual clutter or when there are many changes to view.

The position of the shorthand character determines its staging status - first column for staged, second column for unstaged. Common letters are A (added), D (deleted), M (modified) and ?? (untracked).

```
$ git status --short
 D "Deleted File.txt"
 M "Edited File.txt"
A  "Staged New File.txt"
?? New Directory/
?? New File.txt
```
