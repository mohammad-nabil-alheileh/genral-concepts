# Jira: Issue Types, Fields, and Priorities

Every issue in Jira has an **issue type**, a set of **fields**, and a **priority**. Together they describe what kind of work it is, what information it carries, and how urgent it is. Choosing these well makes boards, filters, and reports useful.

## Issue Types

- **Epic:** a large body of work that spans several stories, such as "Add user login." Epics group related work and track progress across it.
- **Story:** a piece of work described from the user's point of view, such as "As a user, I can reset my password." Stories are the usual unit of planned work in Scrum.
- **Task:** a general piece of work that is not a user-facing feature, such as "Set up the staging database."
- **Bug:** something that does not work as expected. Bugs usually include steps to reproduce, the expected result, and the actual result.
- **Sub-task:** a small piece of a story or task. Sub-tasks always belong to a parent issue.

Some projects add their own types, such as "Improvement" or "Incident." Keep the list short, because too many types make it harder for people to choose the right one.

## Fields

Fields are the pieces of information stored on an issue. Jira has two kinds:

- **System fields** come built in, such as summary, description, assignee, priority, labels, and due date.
- **Custom fields** are added by admins for information the team needs, such as "Customer name," "Story points," or "Browser."

Which fields appear on the issue screen depends on the project's configuration. Adding too many fields makes issues slow to create, so add only the fields the team actually uses.

## Priorities

The default priority scale is:

1. **Highest:** blocks the team or affects many users now.
2. **High:** important and needed soon.
3. **Medium:** normal work that should be done in the planned timeframe.
4. **Low:** useful but not urgent.
5. **Lowest:** nice to have when time allows.

Teams can rename or reorder priorities to match their own language, but they should agree on what each level means. Otherwise, everything ends up marked "High," and the priority field stops helping.
