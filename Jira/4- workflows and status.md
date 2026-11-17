# Jira: Workflows and Statuses

A **workflow** is the path an issue follows from creation to completion. It is made of **statuses**, which say where the issue is now, and **transitions**, which are the allowed moves between statuses. Workflows make the state of work visible and keep everyone following the same process.

## Statuses

A status describes the current stage of an issue, such as To Do, In Progress, In Review, or Done. Each status belongs to a **status category**, which Jira uses for reporting. The three categories are:

- **To Do:** work that has not started.
- **In Progress:** work that is being done.
- **Done:** work that is finished.

Boards and reports use these categories, so a custom status should always belong to the correct category. A status such as "Waiting for QA" would usually sit in In Progress.

## Transitions

A transition is a move from one status to another, such as moving an issue from In Progress to In Review. Transitions can carry rules:

- **Conditions** decide who may perform a transition, such as only the assignee.
- **Validators** check that something is true before the transition completes, such as a required field being filled in.
- **Post-functions** run automatically after a transition, such as clearing the assignee or setting a resolution.

## Designing a Workflow

Start from how the team actually works, then describe that process as statuses and transitions. Keep the number of statuses small, because every extra status adds clicks and confusion. Make sure every status has a clear meaning, so anyone can tell what belongs there.

Workflows are shared through **workflow schemes**, which connect a workflow to an issue type in a project. This lets different issue types, such as bugs and stories, follow different paths when needed.

## Key Idea

A workflow is the team's agreed process written down in Jira. When it matches real work, the board shows the truth. When it does not, people stop updating statuses and the data becomes useless.