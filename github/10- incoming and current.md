# Current vs Incoming Changes: Merge and Rebase

When Git stops with a conflict, it labels the two sides. The labels depend on the operation you ran, and they swap between merge and rebase. Most confusion about conflicts comes from this swap.

- **Current** (also called **ours**): the branch you are on, shown as `HEAD`.
- **Incoming** (also called **theirs**): the changes being brought in.

## Merge

Run this from `feature`:

```bash
git switch feature
git merge main
```

| Side | Meaning | In conflict markers |
|---|---|---|
| Current | Your branch, `feature` | Between `<<<<<<< HEAD` and `=======` |
| Incoming | The branch you merged in, `main` | Between `=======` and `>>>>>>> main` |

Merge keeps both sides' history. Your `feature` commits stay where they are, and the conflict is resolved in a new merge commit.

## Rebase

Run this from `feature`:

```bash
git switch feature
git rebase main
```

| Side | Meaning | In conflict markers |
|---|---|---|
| Current | The base, `main`, which `feature` is being replayed onto | Between `<<<<<<< HEAD` and `=======` |
| Incoming | Your `feature` commit being replayed right now | Between `=======` and `>>>>>>> <commit>` |

Rebase sets your commits aside, moves the branch to `main`, and replays each commit one at a time. So during a rebase, **current** means the upstream code, and **incoming** means your change. This is the reverse of how it feels during a merge.

## Side-by-side

| Operation | Current (`HEAD`, ours) | Incoming (theirs) |
|---|---|---|
| `git merge main` (on `feature`) | Your `feature` changes | `main`'s changes |
| `git rebase main` (on `feature`) | `main`'s code (the new base) | Your `feature` commit being replayed |

## Choosing a side with `--ours` and `--theirs`

These flags follow the same labels, so they flip too:

```bash
git checkout --ours <file>     # keep the current side
git checkout --theirs <file>   # keep the incoming side
git add <file>
```

During a merge, `--ours` keeps your branch's version. During a rebase, `--ours` keeps the base's version. If you pick the wrong side, your change can be dropped without any warning, so check which operation is running first with `git status`.

`git status` says "All conflicts fixed but you are still merging" for a merge, and "You are currently rebasing" for a rebase. Read that line before you choose a side.

## Quick check

Ask one question: **which branch is checked out, and what was it told to do?**

- **Merge**: current is the branch you are on, and incoming is the one you merged.
- **Rebase**: current is the branch you are rebasing onto, and incoming is your commit.

## Things to know early

- **Read the markers, not the habit.** Look at the text under `<<<<<<<` and `>>>>>>>` to see which side is which, instead of assuming.
- **Run `git status` before resolving.** It tells you whether you are merging or rebasing.
- **If you get it wrong, abort.** `git merge --abort` or `git rebase --abort` returns you to the state before the operation started.