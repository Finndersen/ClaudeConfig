# My Claude Code Setup

Here's my current Claude Code setup of [CLAUDE.md](CLAUDE.md), custom slash commands and MCP server configurations.
Some of it is somewhat specific to my work environment, but most of it should be quite generic & transferable. 

I'm constantly learning and iterating and keen to hear from anyone who has suggestions for improvements! 

## Alternative commands/tools
The [CLAUDE.md](CLAUDE.md) prompt assumes that the following tools/commands are installed:
- `fd` as an alternative to `find` for better performance and respecting .gitignore
- `ripgrep` (`rg`) as an alternative to `grep` for better performance and respecting .gitignore
- `ast-grep` for searching code structure with flexible patterns

## Custom Slash Commands
- `file_task`: Implement a task from a structured file-based definition (with plan-think-implement steps)
- `jira_task`: Implement a task from a Jira issue/ticket (with plan-think-implement steps)
- `create_pr`: Create a Github Pull Request (PR) for changes made in the current git feature branch, linked to a Jira task

## MCP server configuration

- [Jira (Atlassian)](https://support.atlassian.com/rovo/docs/getting-started-with-the-atlassian-remote-mcp-server/) - Allows agent to interact with Jira tasks, for autonomous end-to-end task completion if the task description is detailed enough. The official linked MCP server is a remote SSE one, which works with Claude Code but not Gemini CLI. For Gemini, there is another local STDIO option [here](https://github.com/sooperset/mcp-atlassian?tab=readme-ov-file#-configuration-examples).
- [Github](https://github.com/github/github-mcp-server) - Allows agent to interact with Github, such as create PRs or read comments on PRs etc.
- [Unblocked](https://docs.getunblocked.com/unblocked-mcp#unblocked-mcp) - Allows agent to access company-specific resources from Notion, Slack, Github etc. Helpful for gathering context, however one of the tools description says to always use it before doing anything else, so it may cause agent to waste time and context when it doesn’t need to. Worth experimenting with
- [Context7](https://github.com/upstash/context7) - Provides up-to-date code & library documentation
- [Slack](https://github.com/korotovsky/slack-mcp-server/tree/master) - Allows access to Slack messages/threads (read-only by default)

Example config in `~/.claude.json`:

```json
{
  "mcpServers": {
    "Jira": {
      "type": "sse",
      "url": "https://mcp.atlassian.com/v1/sse"
    },
    "Github": {
      "type": "stdio",
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e",
        "GITHUB_PERSONAL_ACCESS_TOKEN",
        "ghcr.io/github/github-mcp-server"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<YOUR_ACCESS_TOKEN>"
      }
    },
    "Unblocked": {
      "command": "/Users/finn.andersen/.unblocked/agent/node/bin/node",
      "args": [
        "/Applications/Unblocked.app/Contents/Resources/mcp/server.js",
        "--client",
        "mcpClaudeCode"
      ]
    },
    "Context7": {
      "type": "sse",
      "url": "https://mcp.context7.com/sse"
    },
    "Slack": {
      "command": "npx",
      "args": [
        "-y",
        "slack-mcp-server@latest",
        "--transport",
        "stdio"
      ],
      "env": {
        "SLACK_MCP_XOXC_TOKEN": "xoxc-...",
        "SLACK_MCP_XOXD_TOKEN": "xoxd-..."
      }
    },
    ...
}
```