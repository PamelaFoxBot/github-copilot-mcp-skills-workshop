# Exercise 2: Understand MCP and connect a public server

In this exercise, you will connect GitHub Copilot to a public MCP server and inspect the tools it provides.

## Contents

- [Step 1: Connect Microsoft Learn MCP](#step-1-connect-microsoft-learn-mcp)
- [Step 2: Inspect the available tools](#step-2-inspect-the-available-tools)
- [Step 3: Use the tools for research](#step-3-use-the-tools-for-research)
- [Bonus](#bonus)

## Step 1: Connect Microsoft Learn MCP

Microsoft Learn MCP is a remote Streamable HTTP server at `https://learn.microsoft.com/api/mcp`. It is public, free, and requires no sign-in.

### VS Code or Codespaces

1. Open `.mcp.json` in the repository root and add the server:

   ```json
   {
     "servers": {
       "microsoft-learn": {
         "type": "http",
         "url": "https://learn.microsoft.com/api/mcp"
       }
     }
   }
   ```

2. Save the file and select **Start** above the server definition. If VS Code asks whether you trust the server, review the URL and approve it.
3. Open Copilot Chat in **Agent** mode.
4. Select **Configure Tools** in the chat input and expand `microsoft-learn`.

### GitHub Copilot CLI

1. Add the server to your user configuration:

   ```bash
   copilot mcp add --transport http microsoft-learn https://learn.microsoft.com/api/mcp
   ```

2. Start an interactive `copilot` session.
3. Enter `/mcp show microsoft-learn` to inspect its status and tools.

### GitHub Copilot app

1. Open **Settings**, select **MCP**, then select **Add server**.
2. Name it `microsoft-learn`, choose **HTTP**, and enter `https://learn.microsoft.com/api/mcp`.
3. Add the server and confirm it's shown as enabled and loaded with a green check mark.

## Step 2: Inspect the available tools

Confirm that the server currently exposes these tools:

- `microsoft_docs_search` for semantic search of official Microsoft documentation
- `microsoft_docs_fetch` for reading a selected documentation page
- `microsoft_code_sample_search` for official code examples

Ask Copilot:

```text
List the tools exposed by the Microsoft Learn MCP server. For each tool, show its purpose and required arguments.
```

## Step 3: Use the tools for research

Ask Copilot:

```text
Find the current GPU options for Azure Container Apps. Cite the relevant Microsoft Learn docs.
```

### What to observe

- Copilot should choose `microsoft_docs_search`, and may follow with `microsoft_docs_fetch`.
- You can expand tool calls to see the arguments and return value.
- A read-only documentation lookup may still require a tool approval in GitHub Copilot, depending on how you've [configured approvals](https://code.visualstudio.com/docs/agents/run/approvals).

## Bonus

If you have more time:

- Disable `microsoft_docs_fetch`, repeat the prompt, and compare the depth of the answer.
- Ask Copilot to find an official Python code sample for uploading text to Azure Blob Storage, then watch whether it chooses `microsoft_code_sample_search`.
- Connect another read-only MCP server and compare its tools:

  | Server | Endpoint | Provides |
  | --- | --- | --- |
  | [DeepWiki](https://docs.devin.ai/work-with-devin/deepwiki-mcp) | `https://mcp.deepwiki.com/mcp` | GitHub repository documentation |
  | [French government](https://github.com/datagouv/datagouv-mcp) | `https://mcp.data.gouv.fr/mcp` | French government data |
  | [Hugging Face](https://huggingface.co/mcp) | `https://huggingface.co/mcp` | Model, dataset, paper, and Space discovery |

  Find more public servers in the [GitHub MCP Registry](https://github.com/mcp).

Continue to [Exercise 3](exercise3.md).
