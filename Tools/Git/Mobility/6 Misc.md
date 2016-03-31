# Git: Miscellaneous

*Part of a series of articles on Git by
[Newcastle Mobility](https://github.com/newcastle-mobility).*  
<- [Frequently Asked Questions](5 FAQ.md)

Very specific, less useful documentation about Git. Essentially a scrapbook of everything else.

## Contents

- [Get Current Branch Name](#get-current-branch-name)
- [Get Tracking Branch](#get-tracking-branch)

### Get Current Branch Name

The currently checked out branch name can be displayed using
[`git branch`](3 Commands.md#git-branch). If scripting Git commands, this output is noisy and
requires extra effort to pick out the current branch.

Instead, the following command can be used to return the name of the current branch and nothing
else:

```
git rev-parse --abbrev-ref HEAD
```

*Source: [Stack Overflow](http://stackoverflow.com/a/1418022)*

### Get Tracking Branch

The tracking branch (or upstream branch) of all checked out branches can be displayed using
[`git branch -vv`](3 Commands.md#git-branch). If scripting Git commands, this output is very noisy
and requires extra effort to pick out the tracking branch from the current branch.

Instead, the following command can be used to return the current branch's tracking branch, in the
format `upstream/branch`:

```
git rev-parse --abbrev-ref --symbolic-full-name @{u}
```

If there is no tracking branch an error is displayed and the process exits with error code 128. This
can be avoided by instead running the following command which outputs an empty line instead of an
error:

```
git for-each-ref --format='%(upstream:short)' $(git symbolic-ref -q HEAD)
```

*Source: [Stack Overflow](http://stackoverflow.com/a/9753364)*
