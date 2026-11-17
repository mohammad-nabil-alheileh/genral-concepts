# Connecting GitHub to Jira

Connecting the two lets Jira show your branches, commits, and pull requests next to the issues they belong to. It also lets you move issues through your workflow automatically when code is merged.

The steps below cover Jira Cloud. Menu names change from time to time, so if something looks different, check Atlassian's current documentation for the GitHub integration.

## Before you start

You need:

- **A Jira Cloud site** and permission to install apps. This is usually a Jira site administrator.
- **A GitHub organization or account** where you can install apps. For an organization, you usually need to be an owner.
- **Repositories you want to link.** You can choose specific repositories, so you don't need to share everything.

## Part 1: Install the GitHub app

1. Go to the GitHub Marketplace and search for **Jira Cloud** (published by Atlassian), or find the GitHub integration from inside Jira.
2. Choose **Set up** or **Install**, then select your GitHub organization or account.
3. Under repository access, choose **Only select repositories** and pick the ones your team works in. Choosing only what you need is the safer option.
4. Complete the installation.

## Part 2: Link the app to your Jira site

1. In Jira, open **Settings** and find the **Apps** section.
2. Choose the option to connect or set up **GitHub**. You may find it under **Apps**, **Find new apps**, or **Development tools**.
3. Sign in to GitHub when prompted and authorize the connection.
4. Confirm that the repositories you selected appear in the list.

If the connection fails, check that you are signed in as someone who has permission to install apps on both sides.

## Part 3: Use issue keys in your work

Jira links work through **issue keys**, such as `PROJ-123`. Include the key anywhere Jira can read it:

| Where | Example |
|---|---|
| Branch name | `PROJ-123-add-login-form` |
| Commit message | `PROJ-123: Add validation to login form` |
| Pull request title | `PROJ-123 Add login form` |
| Pull request description | `Resolves PROJ-123` |

After you push or open a pull request, the issue's **Development** panel in Jira shows the branch, commits, and PR. Its status updates as the PR is reviewed and merged.

## Part 4: Smart commits

With the integration in place, you can also update the issue directly from a commit message:

```text
PROJ-123 #comment Fixed the validation edge case #time 2h
PROJ-123 #done
```

Common commands include:

| Command | Effect |
|---|---|
| `#comment` | Adds your text as a comment on the issue |
| `#time 2h` | Logs time on the issue |
| `#done` or `#resolve` | Moves the issue to a done status |

Smart commits depend on your Jira workflow, so the status names may need to match your project's setup.

## Part 5: Automate status changes

To move issues automatically when code moves, create an automation rule in Jira:

1. Open your project and go to **Project settings**, then **Automation**.
2. Create a rule with a GitHub trigger, such as **Pull request merged**.
3. Add an action that transitions the linked issue, such as **Transition issue to Done**.

This means that when a PR merges, the issue moves to Done without anyone touching it in Jira.

## Troubleshooting

| Problem | Likely cause and fix |
|---|---|
| Commits don't appear in Jira | The issue key is missing or misspelled. Check the branch name and commit message. |
| A repository is missing from the list | It wasn't selected during GitHub installation. Update the repository access in GitHub. |
| "Not authorized" or expired connection | Re-authorize the app from the Jira Apps settings. |
| Smart commits do nothing | The command syntax or status name is wrong. Check your project's workflow names. |
| Automation doesn't fire | The rule's trigger doesn't match the event, or the connection is not active for that project. |

## Good practices

- **Put the issue key in every branch name.** It is the easiest way to keep work linked.
- **Limit repository access** to the projects that need Jira.
- **Review automation rules** periodically, so a status change doesn't surprise the team.
- **Use the Development panel** to find a PR quickly from an issue during review.