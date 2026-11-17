# Git Basics: Branches

A **branch** is an independent line of commits. Branches let you work on a feature, a fix, or an experiment without touching the main line of code. When the work is ready, you merge it back.

Think of the main branch as the trunk of a tree and each branch as a separate limb you can grow, test, and either attach back or leave behind.

## What a branch really is

A branch is just a movable pointer to a commit. Git keeps a special pointer called `HEAD` that tells you which branch, and therefore which commit, you are currently on. Creating a branch is cheap because Git only creates a new pointer, not a copy of your files.

## Creating, switching, and listing branches

| Command | What it does |
|---|---|
| `git branch` | Lists local branches; the current one has a `*` |
| `git branch <name>` | Creates a new branch but stays on the current one |
| `git switch <name>` | Switches to an existing branch |
| `git switch -c <name>` | Creates a new branch and switches to it in one step |
| `git branch -d <name>` | Deletes a branch that has already been merged |

A typical workflow:

Older tutorials use `git checkout` for the same jobs. `git switch` and `git restore` are the newer, clearer commands, and you should learn them first.

## Merging a branch

Once your feature branch is finished, bring its commits into the branch you are on:

```bash
git switch main
git merge add-login-form
```

Two outcomes are possible:

- **Fast-forward merge**: main hasn't changed since you branched, so Git just moves the pointer forward.
- **Merge commit**: both branches have new commits, so Git creates a new commit that joins them.

After a successful merge, you can delete the feature branch with `git branch -d add-login-form`.

## Resolving merge conflicts

A **conflict** happens when two branches change the same lines of the same file. Git stops and marks the conflicting area in the file like this:

```text
<<<<<<< HEAD
const title = "Welcome back";
=======
const title = "Welcome!";
>>>>>>> add-login-form
```

To resolve it:

1. Open the file and decide which version to keep, or write a combination of both.
2. Delete the `<<<<<<<`, `=======`, and `>>>>>>>` marker lines.
3. Stage the file with `git add <file>`.
4. Finish the merge with `git commit`.

Use `git status` to see which files still have conflicts. If you get stuck and want to start over, `git merge --abort` returns you to the state before the merge began.

## Things to know early

- **Keep branches small and short-lived.** A branch that lives for weeks tends to produce large, painful conflicts.
- **Name branches for what they do**, like `fix-date-parsing` or `add-login-form`, not `test` or `new-stuff`.
- **Pull the latest main before you start.** Run `git switch main` and then update it so your branch starts from current code.
- **Merged branches are safe to delete.** Git refuses `git branch -d` on unmerged work, which protects you from losing changes by accident.

