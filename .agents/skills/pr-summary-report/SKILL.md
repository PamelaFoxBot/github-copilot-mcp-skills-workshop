---
name: pr-summary-report
description: Create a read-only summary report for multiple open pull requests, grouping related work when useful. Use only when explicitly invoked by name. Do not use while creating a pull request or reviewing a single pull request.
argument-hint: "repository URL or owner/repository (optional)"
---

# Pull Request Summary Report

Summarize the open pull requests in a repository and identify related,
overlapping, or potentially duplicate work. Gather all GitHub facts through
the GitHub MCP server. Do not substitute `gh` commands, editor-specific active
pull request tools, or unauthenticated web requests.

## Workflow

### 1. Identify the repository

Use the repository supplied by the user. If none was supplied, identify the
upstream project for the current workspace rather than assuming a personal
fork is the intended target. For this workshop, the upstream project is
`pamelafox/github-copilot-mcp-skills-workshop`.

State the owner and repository before gathering pull requests.

### 2. Gather live evidence

Use GitHub MCP pull request tools to list all open pull requests in the target
repository. For each pull request, gather:

- number, title, author, and URL
- body and explicitly linked issues
- changed files and a concise description of the patch
- base repository and branch
- head repository and branch

Use GitHub MCP issue tools to read explicitly linked issues. Follow closing
references such as `Fixes #123`, `Closes #123`, or a full issue URL. Do not
infer an issue link from similar wording.

If no open pull requests exist, report that fact and stop. If some details are
unavailable, mark them `Not available` rather than guessing.

### 3. Organize the report

When there are five or fewer open pull requests, give every pull request its
own table row.

When there are more than five, group pull requests only when evidence shows
that they address the same issue, implement the same goal, or substantially
overlap in changed files. Keep unrelated pull requests in individual rows.
Label each relationship as one of:

- **Explicit**: the pull requests link to the same issue.
- **Inferred**: their stated goals or changed files substantially overlap.
- **Standalone**: no meaningful relationship was found.

Do not force every pull request into a cluster. A group may contain one pull
request.

### 4. Present the report

Sort grouped work first, followed by standalone pull requests in ascending
number order. Produce this table:

| Group | Pull request(s) | Topic | Changed areas | Relationship |
|---|---|---|---|---|

Requirements:

- Link every pull request number to its GitHub URL.
- Link every issue number wherever it appears.
- Name individual pull requests even when they share a group.
- Keep topics and changed-area summaries concise.
- Distinguish observed GitHub facts from inferred relationships.

After the table, add brief sections only when relevant:

1. **Potential duplicates**: pull requests that appear to offer competing
   implementations of the same change.
2. **Potential conflicts**: related pull requests with overlapping changes
   that may require coordination.
3. **Report limits**: missing descriptions, unavailable patches, or other
   evidence gaps that affect the summary.

Do not assign readiness, quality, or merge recommendations. This report
organizes the open work; it does not review individual contributions.

## Tool Rules

- Use GitHub MCP for all GitHub data.
- Keep the workflow read-only.
- Do not create comments, labels, reviews, issues, branches, or pull requests.
- Do not use local Git state to decide which remote pull requests to include.
- Do not expose tokens, authorization headers, or other credentials.
- If a required GitHub MCP capability is unavailable, identify it explicitly
  and continue only with evidence returned by GitHub MCP.
