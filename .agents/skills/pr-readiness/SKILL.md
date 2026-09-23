---
name: pr-readiness
description: Assess PR readiness with live GitHub MCP issue and review data.
argument-hint: "PR URL or number (optional)"
---

# PR Readiness

Evaluate a pull request against its stated goal and report what is ready,
missing, or blocked. Gather live GitHub facts through the GitHub MCP server; do
not substitute `gh` commands or unauthenticated web requests when the MCP tools
are available.

## Workflow

### 1. Identify the pull request

If the user supplied a pull request URL or number, use it. Otherwise:

1. Use the GitHub MCP server to identify the current user.
2. Search the current repository for that user's open pull requests.
3. Continue if exactly one matches.
4. If several match, ask the user to choose. Never guess.

State the base repository, base branch, head repository, head branch, and pull
request URL before continuing.

### 2. Gather live evidence

Use GitHub MCP pull request and issue tools to collect:

- title, body, state, author, draft status, and mergeability
- changed files and patch details
- commits
- status checks
- reviews, review threads, and conversation comments
- linked issue details and acceptance criteria

Follow explicit closing references such as `Fixes #123`, `Closes #123`, or a
full issue URL. If no issue is linked, say so; do not infer one only from
similar wording.

Treat unavailable or absent data as `Not available` or `Not configured`, not as
a failure. A new pull request may legitimately have no checks, reviews, or
comments.

### 3. Validate the change

Build an evidence table that compares each issue requirement or pull request
claim with the relevant changed file, test, check, or review evidence.

When a local checkout is available:

1. Inspect the repository's documented test and lint commands.
2. Run the narrowest relevant tests and lint checks.
3. Record exact commands and outcomes.

When no local checkout or command execution is available, rely on GitHub-hosted
evidence and label local validation as `Not run in this environment`. Do not
claim that a check passed unless evidence shows it.

### 4. Assess readiness

Assign exactly one result:

- **Ready**: the change matches the linked requirements, available validation
  passes, and no unresolved blocking feedback remains.
- **Needs work**: a concrete requirement, validation step, description detail,
  or review response is missing or failing.
- **Blocked**: readiness cannot be determined because required access, data, or
  an external dependency is unavailable.

Missing optional infrastructure is not automatically blocking. For example, a
repository with no configured CI can still be `Ready` when focused local
validation passes.

Report:

1. **Verdict** and one-sentence rationale
2. **Requirement coverage** table
3. **Validation** with checks and local commands
4. **Review status** including unresolved feedback, or
   `No review feedback yet`
5. **Next actions** containing only concrete remaining work

Use links to the pull request and issue. Keep the report concise and distinguish
observed facts from recommendations.

### 5. Offer, but do not perform, writes

After presenting the report, offer at most one useful GitHub update, such as
improving the pull request body or posting the readiness summary as a comment.

Before any GitHub write:

1. Show the exact repository, pull request, and operation.
2. Show the complete proposed text.
3. Ask for explicit user approval.
4. Use a GitHub MCP write tool only after approval.

Never approve, merge, close, or mark a pull request ready for review on the
user's behalf.

## Tool Rules

- Prefer GitHub MCP tools for all GitHub reads and writes.
- Use local file and terminal tools only for workspace inspection and validation.
- Do not use `gh` as a fallback unless the user explicitly requests it.
- Do not expose tokens, authorization headers, or other credentials.
- If a required GitHub MCP tool is unavailable, identify the missing capability
  and continue with the evidence that is available.
