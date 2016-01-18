# Git: Commands

## Contents

- [git add](#git-add)
- [git branch](#git-branch)
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
