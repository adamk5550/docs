# Git: Miscellaneous

*Very specific, less useful documentation about Git. Essentially a scrapbook of everything else.*

## Contents

- [Get Current Branch Name](#get-current-branch-name)

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
