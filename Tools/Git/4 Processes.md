# Git: Processes

## Contents

- [Cloning a Remote Repository](#cloning-a-remote-repository)
- [Creating a Feature Branch](#creating-a-feature-branch)
- [Resolving Merge Conflicts](#resolving-merge-conflicts)
- [Pushing an Initial Patchset to Gerrit](#pushing-an-initial-patchset-to-gerrit)
- [Pushing a New Patchset to Gerrit](#pushing-a-new-patchset-to-gerrit)

## Cloning a Remote Repository

### Overview

- Get remote repository URL
- [git clone](./3%20Commands.md#git-clone)

### Explanation

When beginning work on a new project it is necessary to create a local copy of the remote repository
on your computer. This is done using the [git clone](./3%20Commands.md#git-clone) command.

Using command line Git (*Terminal* or *Git Bash*) navigate to your `Repositories/` directory. You
will need to find the repository URL from relevant enterprise sources such as Confluence.

Run [git clone](./3%20Commands.md#git-clone) using these details. Once downloaded your local
repository subdirectory is ready to go.

## Creating a Feature Branch

### Overview

- Get JIRA story ID
- [git branch](./3%20Commands.md#git-branch) / [git checkout](./3%20Commands.md#git-checkout)

### Explanation

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
repository, feature branches included.

## Resolving Merge Conflicts

### Overview

- [git merge](./3%20Commands.md#git-merge) / [git rebase](./3%20Commands.md#git-rebase)
- Manually edit conflicted files
- Continue merge/rebase

### Explanation

When running [git merge](./3%20Commands.md#git-merge) and [git rebase](./3%20Commands.md#git-rebase)
as part of other processes it is possible that a merge conflict will occur. This is when there are
new commits in both branches being combined that change code in the same place (changes can still
occur in the same file without causing a merge conflict). When this happens, Git defers to the user
to resolve the commit.

Below is a sample rebase conflict, indicating that 2 files have conflicts: `index.html` and
`products.html`:

```
$ git rebase development
First, rewinding head to replay your work on top of it...
Applying: ID-1234: Corrected off-by-1 error in calculator
Using index info to reconstruct a base tree...
M	index.html
Falling back to patching base and 3-way merge...
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Auto-merging products.html
CONFLICT (content): Merge conflict in products.html
Failed to merge in the changes.
Patch failed at 0001 ID-1234: Corrected off-by-1 error in calculator
The copy of the patch that failed is found in:
   /Users/joe.bloggs/Documents/Repositories/Example/.git/rebase-apply/patch

When you have resolved this problem, run "git rebase --continue".
If you prefer to skip this patch, run "git rebase --skip" instead.
To check out the original branch and stop rebasing, run "git rebase --abort".
```

The actual merge conflicts can be picked out of this busy log by looking for lines beginning with
`CONFLICT`:

```
CONFLICT (content): Merge conflict in index.html
CONFLICT (content): Merge conflict in products.html
```

Git allows the merge/rebase to be aborted by running the relevant command with the `--abort` option.
This reverts the current branch to its state before the merge/rebase began.

Git adds both copies of the conflicted code inline to each conflicted file. The conflict can be
resolved by removing the conflict markers from these files, staging all changes, and running the
relevant command with the `--continue` option.

Below is an example of an inline conflict:

```javascript
Action
  .aggregate()
<<<<<<< c6ee904d58e042302a8c75cb6d04d0e6597bdc28
  .match({ id: id })
=======
  .match({ _id: ObjectId(ids.action) })
>>>>>>> ID-1234: Reworked record object data structure
  .exec(function(err, actions) {
    return callback(err, actions);
  });
```

Git looks for `<<<<<<<` (start, existing commit below), `=======` (middle), and `>>>>>>>`
(end, commit being merged above) markers at the start of lines to determine if a merge conflict is
present. Removing these markers is enough to "resolve" the conflict. This allows you to keep one
version only, combine both or replace both with something new entirely.

**Please note** that merge conflicts are a collaborative process and typically include code from
multiple developers. Make sure to confirm with the developers that made these commits that it is
okay to change/remove the conflicted code.

## Pushing an Initial Patchset to Gerrit

### Overview

- [git add](./3%20Commands.md#git-add)
- [git commit](./3%20Commands.md#git-commit)
- [git fetch](./3%20Commands.md#git-fetch) all branches
- [git reset](./3%20Commands.md#git-reset) `development`
- [git rebase](./3%20Commands.md#git-rebase) `development` onto feature branch
- [git merge](./3%20Commands.md#git-merge) feature branch onto `development`

### Explanation

As part of Newcastle Mobility's development process, feature branch commits must be code reviewed
in Gerrit before being merged into the `development` branch. Once complete Gerrit automatically
merges your commit into `development`.

Begin by creating a new commit containing your story's changes:

- `git add` all relevant files to be considered during code review.
- `git commit` to create a new commit. Ensure the commit message begins with the story ID from JIRA
and a colon, for example `ID-1234:`. Commit messages should be succinct, unique, informative and
easy to understand.

In order to prepare the local `development` branch, it needs synchronising with the remote
repository's `development` branch. This prevents merge conflicts from occuring in Gerrit and forces
them to be resolved beforehand by the user. This is achieved by
[checking out](./3%20Commands.md#git-checkout) `development`,
[fetching](./3%20Commands.md#git-fetch) the latest remote `development` branch and applying it
locally with a [hard reset](./3%20Commands.md#git-reset):

- `git checkout development`
- `git fetch origin`
- `git reset --hard origin/development`

To prevent the repository's tree from getting messy with each [merge](./3%20Commands.md#git-merge), [rebase](./3%20Commands.md#git-rebase) is used in the opposite direction before merging. This
creates a two-step merge process which can feel counter-intuitive. Note that any
[merge conflicts](#resolving-merge-conflicts) will appear after rebasing and will need resolving
manually before continuing:

- `git rebase feature-branch:development`
- `git merge development:feature-branch`

Your local `development` branch is now ready to be [pushed](./3%20Commands.md#git-pullpush) to the
Gerrit review area for the remote `development` branch:

- `git push origin HEAD:refs/for/development`

If this succeeds, the commit can be found in Gerrit as a new review, ready to have code reviewers
assigned. Pushing can fail if the commit already exists in the remote repository (feature branch was
pushed) or you do not have permission to push to Gerrit.
