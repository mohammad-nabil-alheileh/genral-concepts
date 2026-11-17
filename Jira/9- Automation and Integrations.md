# Jira: Automation and Integrations

**Automation** is Jira doing routine work for you based on rules. **Integrations** connect Jira to other tools, such as source control, chat, and documentation, so information flows between them without manual copying. Together, they reduce repetitive work and keep Jira in step with the rest of the team's tools.

## Automation Rules

An automation rule has three parts:

- **Trigger:** the event that starts the rule, such as an issue being created, a status changing, or a comment being added.
- **Conditions (optional):** checks that must pass before the rule continues, such as the issue being a bug with high priority.
- **Actions:** what happens next, such as assigning the issue, changing its status, sending a notification, or creating a sub-task.

A simple example: when an issue moves to Done, notify the reporter. Another: when a bug is created with the highest priority, assign it to the on-call person.

Automation saves time, but rules should be kept few and easy to understand. A rule that nobody remembers can cause surprises, such as an issue being reassigned without anyone knowing why.

## Integrations

Integrations link Jira to other systems. Common examples include:

- **Source control:** linking commits, branches, and pull requests to the issue they relate to, so the issue shows its development progress.
- **Chat:** posting notifications about issue updates to a team channel.
- **Documentation:** linking an issue to the design document or specification that explains it.
- **CI/CD:** showing whether a build or deployment for an issue passed or failed.

Integrations are usually installed from the Atlassian Marketplace or set up through built-in connections. Each integration should have a clear owner, because a broken connection can quietly stop information from flowing.

## Permissions and Safety

Automation and integrations can change data and send information outside Jira, so access matters. Only trusted people should create rules that affect many issues, and integrations should be given only the access they need.

## Key Idea

Automation handles routine decisions inside Jira, and integrations keep Jira connected to the tools where work actually happens. Start with a few rules that solve real, repeated problems, and add more only when the team needs them.