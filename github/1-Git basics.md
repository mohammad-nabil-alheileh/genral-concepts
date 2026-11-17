# Git Basics

Git tracks changes to your files over time. Each saved snapshot is called a **commit**, and Git keeps the full history so you can look back at any of them.

## Installing and configuring

Git is usually installed with:

```bash
sudo dnf install git
```

Before your first commit, tell Git who you are. Every commit records this name and email:

```bash
git config --global user.name "yourname"
git config --global user.email "you@example.com"
```

Use the same email as your GitHub account so your commits show up on your profile.

## The three areas

This is the mental model that makes everything else click. A file can sit in one of three places:

1. **Working directory**: the files you edit in your editor.
2. **Staging area** (also called the index): a holding area for the changes you want in your next commit.
3. **Repository history**: the commits Git has saved.

You move changes through them in this order: edit in the working directory, stage with `git add`, and save with `git commit`. Staging lets you choose exactly which changes go into a commit, so one commit can contain only the related work.

## Core commands

| Command | What it does |
|---|---|
| `git init` | Turns the current folder into a Git repository |
| `git status` | Shows which files are modified, staged, or untracked |
| `git add <file>` | Stages a file (`git add .` stages everything) |
| `git commit -m "message"` | Saves the staged changes as a commit |
| `git log` | Shows the commit history |
| `git diff` | Shows unstaged changes line by line |
| `git diff --staged` | Shows what is staged and about to be committed |

A typical first session looks like this:


## Things to know early

- **Run `git status` often.** It tells you where you are, and it's the command people run most.
- **Write commit messages in the imperative**, like "Add login form" or "Fix date parsing." Keep them short and say what the change does.
- **Commits are local until you push.**