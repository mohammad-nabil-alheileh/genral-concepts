# Git and GitHub Command Reference

## Setup and configuration

```bash
git --version                                   # check installed version
git config --global user.name "Your Name"       # set author name
git config --global user.email "you@example.com" # set author email
git config --global init.defaultBranch main     # new repos start on main
git config --global core.editor "code --wait"   # editor for commit messages
git config --list                               # show all settings
git config --global --list                      # show global settings only
```

## Creating and cloning repositories

```bash
git init                          # turn current folder into a repository
git clone <url>                   # copy a remote repository locally
git clone <url> <folder>          # clone into a named folder
git clone --depth 1 <url>         # shallow clone with only the latest commit
```

## Checking status and history

```bash
git status                        # modified, staged, and untracked files
git status -s                     # short status
git log                           # full commit history
git log --oneline                 # one line per commit
git log --oneline --graph --all   # visual history of all branches
git log -n 5                      # last 5 commits
git log --author="Mohammad"       # commits by one author
git log -- <file>                 # history of one file
git show <commit>                 # changes in one commit
git blame <file>                  # who last changed each line
```

## Viewing differences

```bash
git diff                          # unstaged changes
git diff --staged                 # staged changes (--cached also works)
git diff <branch1> <branch2>      # differences between two branches
git diff HEAD~1                   # changes since the previous commit
```

## Staging and committing

```bash
git add <file>                    # stage one file
git add <folder>                  # stage a folder
git add .                         # stage everything in the current folder
git add -p                        # stage parts of files interactively
git commit -m "Message"           # commit staged changes
git commit -am "Message"          # stage tracked files and commit
git commit --amend                # edit the last commit
git commit --amend --no-edit      # add staged changes to the last commit
```

## Unstaging and discarding

```bash
git restore --staged <file>       # unstage a file, keep changes
git restore <file>                # discard unstaged changes in a file
git restore .                     # discard all unstaged changes
git clean -n                      # preview untracked files to remove
git clean -fd                     # delete untracked files and folders
```

## Ignoring files

```bash
# Add patterns to a .gitignore file in the project root
git rm --cached <file>            # stop tracking a file, keep it on disk
git check-ignore -v <file>        # find which rule ignores a file
```

## Branches

```bash
git branch                        # list local branches
git branch -a                     # list local and remote branches
git branch <name>                 # create a branch
git switch <name>                 # switch to a branch
git switch -c <name>              # create and switch to a branch
git switch -c <name> <start>      # create from a specific commit or branch
git branch -m <new-name>          # rename current branch
git branch -d <name>              # delete a merged branch
git branch -D <name>              # force delete an unmerged branch
```

## Merging and rebasing

```bash
git merge <branch>                # merge a branch into the current one
git merge --no-ff <branch>        # always create a merge commit
git merge --abort                 # cancel a merge with conflicts
git rebase <branch>               # replay current branch on top of another
git rebase --continue             # continue after fixing a conflict
git rebase --abort                # cancel a rebase
git rebase -i HEAD~3              # interactively edit the last 3 commits
```

## Resolving conflicts

```bash
git status                        # list files with conflicts
# Edit the file, remove <<<<<<<, =======, >>>>>>> markers
git add <file>                    # mark a conflict as resolved
git commit                        # finish a merge
git checkout --ours <file>        # keep your version
git checkout --theirs <file>      # keep the incoming version
```

## Undoing changes

```bash
git reset --soft HEAD~1           # undo last commit, keep changes staged
git reset --mixed HEAD~1          # undo last commit, keep changes unstaged
git reset --hard HEAD~1           # undo last commit and delete its changes
git revert <commit>               # create a commit that reverses another
git revert --no-commit <commit>   # reverse changes without committing yet
git cherry-pick <commit>          # copy one commit onto the current branch
git stash                         # save unfinished work temporarily
git stash push -m "message"       # stash with a description
git stash list                    # list stashes
git stash pop                     # restore latest stash and remove it
git stash apply                   # restore latest stash and keep it
git stash drop                    # delete latest stash
git reflog                        # history of where HEAD has pointed
git reset --hard <hash>           # return to a commit found in reflog
```

## Tags

```bash
git tag                           # list tags
git tag v1.0.0                    # create a lightweight tag
git tag -a v1.0.0 -m "Message"    # create an annotated tag
git show v1.0.0                   # show tag details
git push origin v1.0.0            # push one tag
git push origin --tags            # push all tags
git tag -d v1.0.0                 # delete a local tag
git push origin --delete v1.0.0   # delete a remote tag
```

## Remotes

```bash
git remote -v                     # list remotes and URLs
git remote add origin <url>       # add a remote named origin
git remote add upstream <url>     # add another remote, e.g. original project
git remote set-url origin <url>   # change a remote's URL
git remote rename origin new-name # rename a remote
git remote remove <name>          # remove a remote
git remote show origin            # details about a remote
```

## Syncing with remotes

```bash
git fetch                         # download changes without merging
git fetch --all                   # fetch from every remote
git pull                          # fetch and merge into current branch
git pull --rebase                 # fetch and rebase instead of merging
git push                          # push current branch to its upstream
git push -u origin <branch>       # push and set upstream
git push --force-with-lease       # safer force push after rewriting history
git push origin --delete <branch> # delete a remote branch
```

## Searching

```bash
git grep "text"                   # search tracked files
git grep -n "text"                # search with line numbers
git log -S "text"                 # find commits that add or remove text
git log --grep="fix"              # find commits by message
git bisect start                  # begin searching for the commit that broke something
git bisect bad                    # mark current commit as broken
git bisect good <commit>          # mark a known good commit
git bisect reset                  # finish bisecting
```

## Maintenance

```bash
git gc                            # clean up and compress the repository
git fsck                          # check repository integrity
git count-objects -vH             # show repository size
```