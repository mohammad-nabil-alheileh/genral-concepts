# Git Basics: Remote Repositories

So far everything has lived on your machine. A **remote** is a copy of your repository hosted somewhere else, such as GitHub. Remotes let you back up your work, share it with others, and collaborate across computers.

## Remotes, origin, and the big picture

A remote is a named link to another copy of your repository. By convention, the main remote is called `origin`.

Your local repository and the remote each keep their own commits. You sync them with four commands:

| Command | What it does |
|---|---|
| `git clone <url>` | Copies a remote repository to your machine and sets up `origin` automatically |
| `git fetch` | Downloads new commits from the remote, but does not change your files |
| `git pull` | Runs `fetch` and then merges the remote changes into your current branch |
| `git push` | Uploads your local commits to the remote |

`fetch` is the safer choice. It lets you look at what changed before deciding how to combine it with your work.

## Creating a repository on GitHub

If you already have a local project and want to put it on GitHub:

1. Go to GitHub and create a new repository. Leave the option to add a README or `.gitignore` unchecked, because your project already has content.
2. Copy the repository URL that GitHub shows you.
3. In your project folder, run:

```bash
git remote add origin https://github.com/your-username/my-project.git
git push -u origin main
```

The `-u` flag sets `origin/main` as the default upstream for your local `main` branch. After that, a plain `git push` or `git pull` is enough.

If your local branch is named `master`, use that name in the push command, or rename it first with `git branch -M main`.

## Checking your remotes

```bash
git remote -v                 # list remotes and their URLs
git remote set-url origin <url>   # change the URL if it moved
```

## Authenticating with GitHub

GitHub no longer accepts your account password for Git operations. Use one of these two options:

**SSH keys (recommended for regular use):**

```bash
ssh-keygen -t ed25519 -C "you@example.com"
cat ~/.ssh/id_ed25519.pub     # copy this output
```

Paste the public key into GitHub under Settings, then SSH and GPG keys. Then use the SSH form of the URL:

```text
git@github.com:your-username/my-project.git
```

**Personal access token (HTTPS):** create a token in GitHub's developer settings, then use it in place of a password when Git asks for one. Choose a token with only the permissions you need and an expiry date.

Never commit keys or tokens to a repository.

If `git push` is rejected with a message about the remote having changes you don't have, someone else pushed first. Run `git pull`, resolve any conflicts the way you learned in the branches topic, and push again.

## Things to know early

- **Pull before you push.** It prevents most rejected pushes and surprise conflicts.
- **Use `fetch` when you want to look first**, and `pull` when you are ready to merge.
- **Set up SSH once** and you won't be asked for credentials again.
- **Check `git remote -v`** if a push goes to the wrong place or fails unexpectedly.
