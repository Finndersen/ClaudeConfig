# Implement task from Jira Issue/ticket

## Gather task/feature context
- Read the task description for Jira issue @$ARGUMENTS (using Jira MCP server tool)
- Set Jira task status to "Developing" if not already
- Investigate relevant context and ask any clarifying questions as required
- Check whether the currently active git branch is appropriate for the feature. If not, The first step of the plan should be to create a new appropriately named git branch, based off origin/main by default

## Think and Plan
- Think step by step to come up with a detailed implementation plan to provide the user for review and approval 
- Consider and indicate which steps can be executed in parallel using subagents / task
- **DO NOT MAKE ANY CHANGES UNTIL THE PLAN IS APPROVED AND USER CONFIRMS THAT IT SHOULD BE EXECUTED.**

## Implementation
- Once the plan is revised and approved by the user, Execute it step by step, keeping track of progress and making any changes as necessary
- Launch sub-agents to parallelize steps where possible, making sure to provide detailed relevant context to avoid redundant duplicate investigation
- Do not commit changes until reviewed and approved by the user
