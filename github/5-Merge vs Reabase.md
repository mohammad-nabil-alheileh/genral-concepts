# Git: Rebase vs Merge

Both commands bring changes from one branch into another. The difference is how they record the result in history.

- **Merge** keeps history exactly as it happened, including the branch and the point where it joined.
- **Rebase** rewrites your commits so they appear to start from the latest base, producing a straight line of history.

## The starting point

Imagine this situation. You branched `feature` from `main`, then both branches gained new commits:

```text
        A---B---C   feature
       /
D---E---F---G       main
```

Your goal is to bring `main`'s new commits (F, G) into `feature`, or the reverse. There are two ways to do it.

## Merge

Run this from the branch you want to update:

```bash
git switch feature
git merge main
```

Result:

```text
        A---B---C-------M   feature
       /                /
D---E---F---G-----------     main
```

- Git creates a new **merge commit** (M) with two parents.
- Your original commits (A, B, C) keep their exact hashes.
- The history shows that the branches existed separately and were joined.

If `main` had not moved since you branched, Git would do a **fast-forward** merge instead. It just moves the pointer forward and creates no merge commit.

## Rebase

Run the same goal as a rebase:

```bash
git switch feature
git rebase main
```

Result:

```text
D---E---F---G---A'---B'---C'   feature
                                main
```

- Git sets your commits aside, moves `feature` to the tip of `main`, and replays A, B, C one by one.
- The replayed commits (A', B', C') have **new hashes**, because their parent changed.
- The history looks linear, as if you started your work from the latest `main`.

If a replayed commit conflicts, Git pauses so you can fix it:

```bash
git add <file>
git rebase --continue
```

Use `git rebase --abort` to cancel and return to the original state.

## Side-by-side comparison

| Question | Merge | Rebase |
|---|---|---|
| Creates a merge commit? | Yes, unless fast-forward | No |
| Changes commit hashes? | No | Yes, for the replayed commits |
| History shape | Branched and joined, can look tangled | Linear and clean |
| Preserves when work happened? | Yes | Rewrites it to look sequential |
| Conflict handling | Resolve once, then commit | May resolve conflicts commit by commit |
| Safe on shared branches? | Yes | Risky if others have the commits |
| Undo method | `git reset --hard ORIG_HEAD` right after | `git reset --hard ORIG_HEAD` right after, or reflog |

## The golden rule

**Never rebase commits that other people have already pulled.** Rebase gives them new hashes, so their copy and yours diverge. Everyone then has to reconcile two versions of the same work.

Safe rule of thumb:

- **Rebase** your own local branch to stay current with `main`, before sharing it.
- **Merge** shared branches, such as `main` or any branch others have pulled.

## Interactive rebase

Interactive rebase lets you clean up your own commits before opening a pull request:

```bash
git rebase -i HEAD~3
```

Git opens a list of the last three commits. You can change the command for each one:

| Command | Effect |
|---|---|
| `pick` | Keep the commit as it is |
| `reword` | Keep the change, edit the message |
| `squash` | Merge the commit into the one above it |
| `fixup` | Like squash, but discard its message |
| `drop` | Remove the commit |

Use this to turn messy work-in-progress commits into a few clear ones before you push.

## Pull with rebase

You can make `git pull` rebase your local commits on top of the remote ones, instead of merging:

```bash
git pull --rebase
```

Or make it the default:

```bash
git config --global pull.rebase true
```

This keeps your history linear when you are syncing a branch you own.

## Which should you use?

| Situation | Choice |
|---|---|
| Updating a shared branch like `main` | Merge |
| Updating your own feature branch from `main` | Either, rebase keeps it tidy |
| Cleaning up your commits before a pull request | Interactive rebase |
| Your branch was already pushed and others use it | Merge |
| You want a linear history for the project | Rebase, then merge with `--ff-only` |
| Unsure | Merge. It is safer and cannot rewrite history |

## Quick recap

- **Merge** joins histories and records the join. Safe, honest, slightly messier.
- **Rebase** replays your work on a new base. Clean, linear, but it rewrites hashes.
- Rewrite only what is yours and unshared.