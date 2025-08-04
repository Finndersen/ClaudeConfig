# Create Github PR for change
## Gather task/feature context
- If you are aware of the task context and authored the changes, then you may not need to do any further investigation
- Otherwise, launch subagents to gather context and details of the changes made in the current git feature branch by inspecting the git commit status & history, and the description for associated Jira task: @$ARGUMENTS using the Jira MCP server tools

## Review changes
- Review the code changes made in the current git feature branch to ensure they:
  - Align with the task requirements
  - Have appropriate test coverage
  - Have no potential issues or bugs
  - Follow software engineering best practices and no code smells (large functions, deep nesting, duplicate code)
- Stop and suggest any changes where appropriate

## Create commits
- Commit and uncommited changes. Large or complex changes should be broken up into logically independent sequential atomic commits where possible. 
- Structure the commit message with a short subject line, followed by a concise description of the changes made and why

## Create Github Pull Request (PR) for this feature branch
- Use the Github MCP server tool to create a Github Pull Request (PR) for the changes made in the current branch, referencing the associated Jira task @$ARGUMENTS with a hyperlink  (task URL is in format https://travelperk.atlassian.net/browse/<JIRA_ISSUE_ID>)
- Follow the PR template in @.github/PULL_REQUEST_TEMPLATE.md if present
- Include task/feature Context, summary of key changes, and Impact
- Update Jira task status to "Testing/Review" after publishing the PR