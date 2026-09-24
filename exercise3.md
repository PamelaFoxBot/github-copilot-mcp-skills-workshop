# Exercise 3: Connect GitHub Copilot to GitHub MCP server

In this exercise, you will connect to the [GitHub MCP server](https://github.com/github/github-mcp-server), which gives Copilot access to GitHub repositories, issues, pull requests, and more. Unlike the Microsoft Learn server from Exercise 2, this server requires authentication.

## Contents

- [Step 1: Connect GitHub Copilot to GitHub MCP](#step-1-connect-github-copilot-to-github-mcp)
- [Step 2: Use GitHub MCP](#step-2-use-github-mcp)
- [Bonus](#bonus)

## Step 1: Connect GitHub Copilot to GitHub MCP

### GitHub Copilot in VS Code or Codespaces

1. Add the GitHub MCP server alongside Microsoft Learn in `.mcp.json`:

 ```json
 {
   "mcpServers": {
    "microsoft-learn": {
      "type": "http",
      "url": "https://learn.microsoft.com/api/mcp"
    },
    "github": {
      "type": "http",
      "url": "https://api.githubcopilot.com/mcp/"
    }
   }
 }
 ```

1. Select **Start** above the GitHub server definition.
1. When prompted, allow the server to authenticate to GitHub.
1. Select **Configure Tools** in Copilot Chat and confirm that GitHub tools such as `list_issues`, `get_file_contents`, and `create_pull_request` are available.

### GitHub Copilot CLI

The GitHub MCP server is built into Copilot CLI, with a smaller set of tools enabled by default.

1. Start Copilot CLI with all GitHub MCP toolsets enabled:

 ```bash
 copilot --enable-all-github-mcp-tools
 ```

 For additional setup options, see the [Copilot CLI installation guide](https://github.com/github/github-mcp-server/blob/main/docs/installation-guides/install-copilot-cli.md).

1. Enter `/mcp show github-mcp-server` and confirm that the built-in server and its tools are available.

### GitHub Copilot app

Configure the GitHub MCP server with the toolsets needed to research an issue, update your fork, and open a pull request.

1. Open the GitHub Copilot app.
1. Select **Customize** in the sidebar, then select the **MCP** tab.
1. Open the **Add** menu in the upper-right corner and select **MCP Server**.
1. Enter `github` for the server name and select **HTTP**.
1. Enter `https://api.githubcopilot.com/mcp/` for the URL.
1. Select **Add server**.
1. Complete GitHub authorization when prompted.
1. Ask Copilot to verify the available tools:

 ```text
 Do you have access to the GitHub MCP server? Confirm that you have the list_issues, get_file_contents, and create_pull_request tools.
 ```

## Step 2: Use GitHub MCP

This repository has a small quiz script in `src/quiz.py` with known bugs and missing features tracked as GitHub issues. Complete this workflow in the Copilot environment you connected in Step 1.

1. Ask Copilot to list the workshop's open issues:

 ```text
 List the open issues in pamelafox/github-copilot-mcp-skills-workshop and summarize them.
 ```

1. Ask Copilot to choose an issue:

 ```text
 Which of these issues would be the easiest to fix? Pick one for me.
 ```

1. If you have a Python environment available, run the quiz to see the suggested issue for yourself:

 ```bash
 uv run python src/quiz.py
 ```

1. Ask Copilot to implement the issue in your fork and create a pull request:

 ```text
 Fix that issue. Follow these steps:
 1. Create a new branch in my fork for the fix.
 2. Make only the required change to src/quiz.py.
 3. Commit and push the branch.
 4. Create a PR to pamelafox/github-copilot-mcp-skills-workshop that references the issue.
 ```

 Confirm that the branch and commit target your fork, while the pull request targets `pamelafox/github-copilot-mcp-skills-workshop`.

1. Open the returned pull request URL and review the changes.

## Bonus

If you have more time:

- **Explore more GitHub MCP server tools**: For example, you can ask Copilot to examine pull requests submitted by other workshop participants:

  ```text
  List the open pull requests in pamelafox/github-copilot-mcp-skills-workshop,
  excluding my pull request.
  Inspect their changes and summarize the different problems and approaches.
  Include links to the pull requests.
  ```

  You may see it use the `list_pull_requests` and `pull_request_read` tools.
- **Try a different authenticated server**: Connect to another MCP server that uses OAuth:
  - [Notion MCP](https://developers.notion.com/docs/mcp): search, read, create, and update content in a Notion workspace
  - [Linear MCP](https://linear.app/docs/mcp): find, create, and update issues, projects, and comments in Linear
  - [Azure DevOps MCP](https://learn.microsoft.com/azure/devops/mcp-server/mcp-server-overview): query work items, repos, pipelines, and wikis in Azure DevOps
  - [Work IQ MCP](https://github.com/microsoft/work-iq): search emails, meetings, documents, and Teams messages from Microsoft 365
  - [Azure MCP](https://learn.microsoft.com/azure/developer/azure-mcp-server/get-started): manage Azure resources, storage, and AI services

  Browse the [GitHub MCP Registry](https://github.com/mcp) for more server ideas.
