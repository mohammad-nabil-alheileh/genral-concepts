# Git Basics: Undoing and Fixing Things

Mistakes are normal in Git, and most of them are easy to fix. The key idea is that commits are saved snapshots, so you can usually step back to an earlier state without losing work.

## Restoring files

If you changed a file and want to throw those changes away, restore it from the last commit:

```bash
git restore <file>            # discard unstaged changes in a file
git restore --staged <file>   # unstage a file, but keep its changes
```

Be careful with `git restore <file>`. It permanently discards the unstaged changes in that file, and Git cannot bring them back.

## Amending the last commit

If you forgot a file or made a typo in the last commit message, you can rewrite that commit:

```bash
git add forgotten-file.js
git commit --amend -m "Add login form with validation"
```

Amending replaces the last commit rather than adding a new one. Only do this for commits you have not pushed yet. Rewriting pushed history causes problems for anyone else who has the old commit.

## Unstaging changes

If you staged something by accident, `git restore --staged` moves it back out of the staging area and leaves your edits in place.

```bash
git add .                     # oops, staged too much
git restore --staged config.js
```

## `reset` vs `revert`

Both commands move you back to an earlier state, but they work very differently.

| Command | What it does | When to use it |
|---|---|---|
| `git reset --soft HEAD~1` | Undoes the last commit but keeps its changes staged | Re-do a commit with different contents |
| `git reset --mixed HEAD~1` | Undoes the last commit and unstages its changes (the default) | Re-select which changes to commit |
| `git reset --hard HEAD~1` | Undoes the last commit and deletes its changes from your files | Throw away a commit completely; cannot be undone easily |
| `git revert <commit>` | Creates a new commit that reverses the old one | Undo a change that has already been pushed |

The rule of thumb: use `reset` on commits that only exist on your machine, and use `revert` on commits that others may already have. `revert` is safe for shared history because it adds a new commit instead of rewriting the old one.

`git reset --hard` is the most dangerous command in this list. Check `git status` and make sure you really want to lose those changes before running it.

## Looking at history

These commands help you find the commit you want to undo or inspect:

| Command | What it does |
|---|---|
| `git log` | Shows the commit history |
| `git log --oneline` | Shows one short line per commit |
| `git show <commit>` | Shows the changes in one commit |
| `git reflog` | Shows where HEAD has pointed recently, including commits you "lost" |

`git reflog` is your safety net. If you reset too far or deleted a branch by mistake, the commit is usually still in the reflog for a while:

```bash
git reflog                    # find the commit hash from before the mistake
git reset --hard <hash>       # return to that state
```

## Things to know early

- **Check before you destroy.** Run `git status` and `git log --oneline` before any reset or restore.
- **Use `revert` for shared work** and `reset` only for your own local commits.
- **Commits are rarely truly lost.** If you panic, look in `git reflog` first.
- **Undo small and often.** Fixing a mistake right after it happens is far easier than untangling it later.
