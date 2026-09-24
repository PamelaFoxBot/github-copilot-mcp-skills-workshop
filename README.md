# Exploring MCP Servers with GitHub Copilot

Model Context Protocol (MCP) is an open standard that lets AI agents like GitHub Copilot tap into external tools, services, and your own account data. In this hands-on workshop, you'll connect GitHub Copilot to both public and authenticated MCP servers, explore the tools they expose, and put them to work researching topics, troubleshooting issues, and making a real contribution to a codebase. You'll also discover how combining MCP servers with agent skills unlocks more powerful, personalized developer workflows.

## Slides

https://pamelafox.github.io/github-copilot-mcp-skills-workshop/

## Prerequisites

- A [GitHub account](https://github.com/signup) with access to [GitHub Copilot](https://docs.github.com/en/copilot/get-started/plans). _If your Copilot Business or Copilot Enterprise subscription is managed by an organization or enterprise, an administrator must enable the [MCP servers in Copilot policy](https://docs.github.com/en/copilot/how-tos/provide-context/use-mcp-in-your-ide/extend-copilot-chat-with-mcp#prerequisites)._
- GitHub Copilot client: [GitHub Copilot in VS Code](https://code.visualstudio.com/docs/copilot/overview), [GitHub Copilot CLI](https://docs.github.com/en/copilot/concepts/agents/about-copilot-cli), GitHub Copilot app](https://github.com/github/app)
- For a local checkout: [Git](https://git-scm.com/), Python 3.12 or later, and [uv](https://docs.astral.sh/uv/getting-started/installation/). GitHub Codespaces is also an option.

## Exercises

| Exercise | Description |
| --- | --- |
| [Exercise 1](exercise1.md) | Fork the repository, set up the development environment, and verify GitHub Copilot. |
| [Exercise 2](exercise2.md) | Understand MCP and connect GitHub Copilot to the public Microsoft Learn MCP server. |
| [Exercise 3](exercise3.md) | Authenticate to GitHub, find a quiz issue, repair it, and open a pull request. |
| [Exercise 4](exercise4.md) | Use a project skill, then install and try a popular third-party skill. |

## Additional resources

- [Model Context Protocol](https://modelcontextprotocol.io/)
- [MCP servers in VS Code](https://code.visualstudio.com/docs/copilot/chat/mcp-servers)
- [MCP servers in GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers)
- [Microsoft Learn MCP server](https://learn.microsoft.com/training/support/mcp)
- [GitHub MCP server](https://github.com/github/github-mcp-server)
- [Agent Skills in VS Code](https://code.visualstudio.com/docs/copilot/customization/agent-skills)
