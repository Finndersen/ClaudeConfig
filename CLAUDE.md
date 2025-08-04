# IMPORTANT GLOBAL RULES & GUIDELINES

## General
- If installing pip or npm dependencies fails with a 401 Unauthorised error, run the `tklogin` command to authenticate
- If you require more context, documentation or answers about a business, domain or product-specific concept or process, create a Sub-agent (Task) to use the unblocked_context_engine tool and return a summarised result. It can retrieve information from company Notion documentation, Slack discussions, Jira issues and Github repositories.
- Use Context7 to retrieve up-to-date documentation for libraries or frameworks when required (`resolve-library-id` tool then `get-library-docs`)
- Use the Slack MCP server tool (NOT Unblocked) to read specific messages or conversation threads (when link or ID is provided)
- Try to be efficient with tool usage to minimize number of tool calls, such as reading more lines of a file at once

## Sub-Agent Strategy
- **PRIORITIZE parallel sub-agents** for research, analysis, and context gathering tasks to maximize efficiency and minimize context window usage
- **Decompose complex tasks** into independent, limited-scope investigation steps that can run simultaneously as tasks
- **LIMIT THE SCOPE** of each task to a single responsibility for efficiency
- **Define specific information requirements** for each sub-agent before launching them
- **Use parallel sub-agents for**:
  - File searches and code analysis across different modules/directories
  - Documentation research and API investigation
  - Using the unblocked_context_engine tool to search for domain/business-specific context and return summarised results
  - Test writing and validation
  - Dependency analysis and compatibility checks
  - Error investigation and debugging in separate components
  - Implementing feature changes and tests in parallel
- **DO NOT use sub-agents** for trivial changes when all required context is already known
- **Provide clear and detailed context** to sub-agents:
  - Specific files, functions, or patterns to investigate
  - Expected output format and level of detail
  - Relevant background information needed for the task
  - Implementation details and any other context required to implement a change or test without doing further investigation
- **Aggregate results** from sub-agents efficiently before proceeding with implementation

### Sub-Agent Examples
- **Task Research & Context Gathering**: Launch agents for (1) analysing code to learn implementation details or usage of classes/modules/functions of interest (multiple tasks is required), (2) Query Unblocked for company/domain/product-specific documentation/context/code etc from outside this repository, (3) Analyse existing test cases & patterns
- **Task/Feature Implementation**: Launch agents for (1) Implementing feature changes (multiple tasks if required), (2) Adding or updating tests

## Shell (Bash) tool usage
- For finding FILES: Use `fd` instead of `find`  (use `-H` flag when searching Python dependencies/libraries as they will probably be within `.venv/` hidden directory)
- For searching TEXT/STRINGS in files: Use `rg` (ripgrep) instead of `grep` (Use `--no-ignore` flag when searching Python dependencies/libraries as they will probably be within `.venv/` ignored directory)
  - ALWAYS use `rg` with `--no-ignore` via Bash instead of the built-in Grep tool when searching Python dependencies/libraries in `.venv/`
- For searching CODE STRUCTURE: Use `ast-grep` with FLEXIBLE PATTERNS for more reliable matching (do not include parameter details unless necessary)

## Coding Style
- Following software engineering best practices for security, testing, performance, and maintainability
- Write complete, high quality, production-ready code. Do not cut corners or make excessive changes beyond what is in scope of the requested task
- Follow existing code styles and patterns unless specified otherwise
- Where appropriate, encapsulate logic in appropriately named helper/utility functions, to reduce complexity of implementation and improve readability
- Do not write unnecessary comments, instead prefer self-documenting code that is easy to understand
- Do not add comments that only describe a change that has just been made. Comments should add context to the code as-is when read at any point in time without awareness of the previous state of the code
- Do not include any whitespace in completely blank lines
- Imports should always be at the top of the file (not within functions or tests)

## Python-Specific Guidance
- Project dependencies will usually be installed in a virtual environment at `.venv/lib/` within the project directory. Search here when needing to find library implementation details (using `fd` with `-H` flag)

## Tests
- **Launch sub-agents in parallel** to add new or update existing tests for any change in functionality. Have one sub-agent focus on implementation while another handles test coverage.
- When writing tests, ONLY mock functions or methods which perform external requests or API calls, unless specified otherwise
- Before attempting to run tests, check @README.md if present for details of how to do so

## Git / Github
- When creating a new git branch for a feature, always create it based on origin/main unless specified otherwise
- ALWAYS ask for user review and approval BEFORE commiting any changes.
- Break changes up into logical, atomic commits where possible. Group changes and their associated tests together in the same commit.
- Do not add existing untracked files to git unless they are relevant to the task at hand
- Linting and formatting pre-commit hooks may cause commit to fail, so will need to be re-attempted after issues are resolved (either automatically or manually)
- When asked to publish a Pull Request (PR) or otherwise interact with Github, ALWAYS use appropriate tool(s) from the Github MCP server
- When creating a Github PR, follow the template in @.github/PULL_REQUEST_TEMPLATE.md if present, and include the JIRA task id in the title

## Jira
- When asked to read a Jira issue, use the appropriate tool(s) from the Jira MCP server
- When using the `getJiraIssue` tool to get task details, only read these fields by default: [summary, parent, status, assignee, subtasks, description, comment, attachment]
- After publishing a Github PR, set the status of the associated Jira task/issue to "Testing/Review"
- Github PRs will automatically be linked to the associated Jira task/issue when referencing the issue, so no need to do this manually

