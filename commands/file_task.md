# Implement task from file definition

## Gather task/feature context
- Read the task definition at $ARGUMENTS
- Investigate relevant context and ask any clarifying questions as required
- Check whether the currently active git branch is appropriate for the feature. If not, The first step of the plan should be to create a new appropriately named git branch, based off origin/main by default

## Think and Plan
- Think step by step to come up with a detailed implementation plan to provide the user for review and approval 
- Consider and indicate which steps can be executed in parallel using subagents / task
- Present the plan to the user, and ask whether they would like to proceed with it, and whether to add the plan to the $ARGUMENTS file
- **DO NOT MAKE ANY CHANGES UNTIL THE PLAN IS APPROVED AND USER CONFIRMS THAT IT SHOULD BE EXECUTED.**

## Implementation
- Once the plan is revised and approved by the user, execute the plan step by step
- If the user requested to have the plan added to the task file, keep track of progress and important considerations under a "# TASK PROGRESS AND NOTES" section. 
- Launch sub-agents to parallelize steps where possible.
- - Do not commit changes until reviewed and approved by the user