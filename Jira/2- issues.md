# Jira: Creating and Managing Issues

An **issue** is the basic unit of work in Jira. It can be a task, a bug, a story, or an epic. Each issue belongs to one project and gets a unique key made of the project key and a number, such as `WEB-42`. That key is how people refer to the issue in conversations, commits, and searches.

## Core Fields of an Issue

- **Summary:** a short title that states the work clearly. It is the most important field, because it appears on boards and in lists.
- **Description:** the full detail. It should explain the goal, the context, and what "done" means.
- **Issue type:** what kind of work this is, such as bug, task, or story.
- **Assignee:** the person currently responsible for doing the work.
- **Reporter:** the person who created the issue. Jira sets this automatically.
- **Priority:** how urgent the issue is relative to other work.
- **Status:** where the issue sits in the workflow, such as To Do, In Progress, or Done.
- **Labels and components:** tags for grouping and filtering related issues.
- **Due date:** when the work should be finished, if the deadline matters.

## Creating an Issue

Most issues are created with the **Create** button. Jira asks for the project, the issue type, and the summary at minimum, and everything else is optional. Good practice is to fill in the description early, since it saves questions later.

## Sub-tasks and Links

- **Sub-tasks** break a larger issue into smaller pieces that belong to a parent. They are useful when one person or a small group handles a clearly separate part of the work.
- **Issue links** connect issues that relate to each other, such as "blocks", "is blocked by", or "relates to". Links make dependencies visible, so the team knows what must finish first.

## Working on an Issue

- **Comments** hold discussion, questions, and decisions. Keep decisions in comments or the description so they are not lost.
- **Attachments** hold files such as screenshots, logs, or documents that support the issue.
- **Watchers** receive notifications about changes to an issue, even if they are not assigned to it.
- **History** records every change, which makes it possible to see who changed what and when.
