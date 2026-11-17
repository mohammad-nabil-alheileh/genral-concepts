# Git Basics: Good Habits

The commands are only half of working well with Git. The other half is the habits that keep your history readable, your repository clean, and your teammates' work safe. Most of these take seconds to practice and save hours later.

## Writing clear commit messages

A commit message is a note to your future self and to your teammates. Good messages say what changed and why.

A simple structure works well:

```text
Short summary in the imperative, 50 characters or fewer

Optional longer explanation. Wrap lines at about 72 characters.
Describe why the change was needed, not just what the code does.
```

Examples:

| Weak message | Better message |
|---|---|
| `fix stuff` | `Fix date parsing for UTC timestamps` |
| `update` | `Add pagination to the orders endpoint` |
| `changes` | `Remove unused session cleanup job` |
| `WIP` | `Add draft validation for the signup form` |

Write the summary in the imperative mood, as if giving a command: "Add," "Fix," "Remove," "Update." This matches the messages Git itself writes, such as "Merge branch 'main'."

For a longer explanation, leave a blank line after the summary and add a paragraph:

```bash
git commit          # opens your editor so you can write a full message
```

## Using a `.gitignore` file

Some files should never be committed: dependencies, build output, secrets, and editor settings. A `.gitignore` file in the project root tells Git to skip them.

```gitignore
# Dependencies
node_modules/
venv/
__pycache__/

# Environment and secrets
.env
*.key

# Build output
dist/
build/

# Editor and OS files
.vscode/
.idea/
.DS_Store
```

Add the file before your first commit. If you already committed a file that should be ignored, remove it from tracking without deleting it from your disk:

```bash
git rm --cached .env
git commit -m "Stop tracking .env file"
```

Remove secrets from tracking right away, then rotate them. Once a secret is pushed to GitHub, deleting it in a later commit does not remove it from history.

## Keeping branches small and focused

Each branch should do one thing. A branch named `add-login-form` should contain login form changes, not an unrelated refactor, a typo fix, and a new dependency.

Focused branches:

- Are easier to review
- Merge with fewer conflicts
- Are easy to revert if something goes wrong
- Can be deleted cleanly once merged

Delete branches after they merge to keep your list tidy:

```bash
git branch -d add-login-form
git push origin --delete add-login-form
```

## Committing often, in logical pieces

Commit when you finish a logical step, not only at the end of the day. Small commits give you more checkpoints to return to.

Use `git add -p` to stage parts of a file, so one commit contains only one idea:

```bash
git add -p
```

Git will show each change and ask whether to stage it. This is useful when you fixed a bug and also reformatted unrelated code in the same file.

## Checking before you commit

Before every commit, run through a short routine:

```bash
git status          # is everything I expect staged?
git diff --staged   # does every line belong in this commit?
```

Reading the staged diff is the single best habit for catching mistakes such as leftover debug logs, stray files, and accidental edits.

## Keeping your local copy current

Pull regularly so your branch stays close to the latest code. This makes conflicts smaller and easier to fix.

```bash
git switch main
git pull
git switch my-branch
git merge main
```

## Things to know early

- **Read the diff before you commit.** Most accidental commits are caught here.
- **Never commit secrets.** Keep `.env` files and keys in `.gitignore` from day one.
- **Write messages for the next reader**, who may be you in six months.
- **Keep one idea per commit and one purpose per branch.** It makes everything else easier.
