# Jira: Filters and JQL

A **filter** is a saved search that returns a set of issues matching certain conditions. **JQL** (Jira Query Language) is the language used to write those conditions. Filters let you find the work that matters right now, and they power boards, dashboards, and reports.

## Basic Filters

The simplest way to filter is with the search interface, which lets you pick fields such as project, assignee, status, or priority. Jira converts those choices into a JQL query behind the scenes. Once a search returns the right results, you can save it as a filter and reuse it.

Saved filters can be private or shared with a team, depending on who needs them.

## How JQL Works

A JQL query is made of **clauses** that compare a field to a value, joined by operators. The general shape is:

- A **field**, such as `project`, `assignee`, `status`, or `priority`.
- An **operator**, such as `=`, `!=`, `in`, `~` (contains text), or `is`.
- A **value**, such as a name, a status, or a date.

Clauses are combined with **AND** and **OR**, and parentheses control the order in which conditions are evaluated. Functions such as `currentUser()` and relative dates such as `-7d` let a filter stay useful over time without being rewritten.

## Useful Patterns

- Find your open work: the issues assigned to you that are not yet done.
- Find what is stuck: issues that have been in the same status for a long time.
- Find what is due soon: issues with a due date in the next few days.
- Find bugs in a release: bugs linked to a particular release version.

Each pattern is a question the team asks often. Writing these as saved filters saves time and keeps everyone looking at the same data.

## Ordering and Sorting

JQL can also sort results with `ORDER BY`, such as ordering by priority first and then by due date. Sorting makes the most urgent items appear at the top of a list.

## Key Idea

Filters and JQL turn Jira's data into answers. A well-written filter answers one clear question, and a good team keeps a small set of trusted filters rather than rebuilding searches each time.