# Git Basics: GitHub Collaboration

Git handles the code. GitHub adds the collaboration layer on top: forks, pull requests, reviews, and issues. This topic covers how people work together on shared projects, and how you contribute to projects you don't own.

## Forking and cloning

A **fork** is your own copy of someone else's repository, hosted under your GitHub account. You can change it freely without affecting the original.

The usual contribution workflow for a project you don't have write access to:

1. Click **Fork** on the project's GitHub page.
2. Clone your fork to your machine:

```bash
git clone https://github.com/your-username/project.git
cd project
```

3. Add the original project as a second remote so you can get its latest changes. By convention it is called `upstream`:

```bash
git remote add upstream https://github.com/original-owner/project.git
git fetch upstream
```

Now `origin` points to your fork and `upstream` points to the original.

## Keeping your fork up to date

Before starting new work, bring your local `main` in line with the original:

```bash
git switch main
git pull upstream main
git push origin main
```

## Working on a contribution

Always work on a branch, never directly on `main`:

```bash
git switch -c fix-typo-in-readme
# make changes
git add .
git commit -m "Fix typo in installation steps"
git push -u origin fix-typo-in-readme
```

## Pull requests

A **pull request** (PR) asks the owner of a repository to review your branch and merge it. You open it on GitHub after pushing your branch.

A good pull request has:

- **A clear title** that says what the change does, such as "Fix typo in installation steps."
- **A description** that explains why the change is needed and how you tested it.
- **Small scope.** One PR should do one thing. Small PRs get reviewed faster and merge more easily.
- **Linked issues.** Writing "Closes #12" in the description closes the related issue automatically when the PR is merged.

### Reviewing and updating

Reviewers can comment on specific lines, request changes, or approve. To address feedback, push new commits to the same branch. The pull request updates automatically:

```bash
# make the requested changes
git add .
git commit -m "Address review feedback on error message"
git push
```

### Merging

Once approved, the maintainer merges the PR. GitHub offers three merge styles:

| Style | What it does |
|---|---|
| **Create a merge commit** | Keeps every commit from the branch and adds a merge commit |
| **Squash and merge** | Combines all the branch's commits into one commit on main |
| **Rebase and merge** | Replays the commits onto main without a merge commit |

Squash and merge is a common choice for small contributions, because it keeps the main history tidy.

## Issues

An **issue** is a place to track bugs, feature requests, and questions. Good issues include:

- A short, specific title
- Steps to reproduce the problem, or the expected behavior for a feature
- Screenshots, error messages, or logs when relevant
- Labels such as `bug`, `enhancement`, or `good first issue`

Issues connect to code through references. Typing `#12` in a commit message or PR links to issue 12 automatically.

## Project boards

A **project board** shows issues and pull requests as cards in columns, such as To do, In progress, and Done. It is useful for planning a team's work at a glance. You can create one from the Projects tab of a repository or your account.

## Things to know early

- **Never commit directly to someone else's `main`.** Use a fork and a branch.
- **Keep PRs small.** A large PR is harder to review and more likely to sit unmerged.
- **Write the PR description for a reader who has no context.** Explain what changed and why.
- **Respond to review comments promptly**, and thank reviewers. Review is a conversation, not a judgment.
