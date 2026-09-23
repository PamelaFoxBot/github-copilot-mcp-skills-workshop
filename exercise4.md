# Exercise 4: Use agent skills

In Exercise 3, you used GitHub MCP tools to repair a quiz issue and open a pull
request. In this exercise, choose one or more of the following activities to
explore project, installed, client-provided, and custom skills.

## Contents

- [Use a project skill](#use-a-project-skill)
- [Install a third-party skill](#install-a-third-party-skill)
- [Explore skills provided by your Copilot client](#explore-skills-provided-by-your-copilot-client)
- [Create your own project skill](#create-your-own-project-skill)
- [What to observe](#what-to-observe)

## Prerequisites

- To use `pr-readiness`, complete Exercise 3, keep its pull request URL, and
  keep GitHub MCP connected with the `repos`, `issues`, and `pull_requests`
  toolsets.
- To install a third-party skill, use VS Code, Codespaces, or Copilot CLI with
  a workspace terminal.

If you used the Copilot app for earlier exercises, open your fork in a
Codespace to run the skill installer. The app does not provide a workspace
terminal.

## Use a project skill

The workshop includes `.agents/skills/pr-readiness/SKILL.md`. Open the file and
inspect its frontmatter and workflow. The skill provides instructions; GitHub
MCP provides the live tools and authenticated data.

Start a fresh chat and ask Copilot:

```text
Use the /pr-readiness skill to assess this pull request: <YOUR-PR-URL>

Use GitHub MCP for all GitHub data. Show me the readiness report, but do not
make any GitHub changes.
```

If slash invocation is unavailable, ask Copilot to use the repository's
`pr-readiness` skill by name. Approve the read-only GitHub calls as they appear.

Check that the report:

1. Names the correct upstream base and your fork's head branch.
2. Connects the linked issue requirements to the changed file.
3. Distinguishes missing checks or reviews from failures.
4. Claims local validation only when commands actually ran.

## Install a third-party skill

[Matt Pocock's skills repository](https://github.com/mattpocock/skills) contains
small, composable engineering workflows. Its `/grill-me` skill interviews you
to expose unresolved decisions in a plan or design.

Before installing third-party skills, inspect their source and consider what
instructions or scripts they contain. In this case, `grill-me` is a user-facing
wrapper around the companion `grilling` skill, so install both using one of the
following options.

### Option A: GitHub CLI

Skill installation in GitHub CLI is currently in preview. If your version of
`gh` includes the `gh skills` command, run:

```bash
gh skills add mattpocock/skills grill-me \
  --agent github-copilot --scope project
gh skills add mattpocock/skills grilling \
  --agent github-copilot --scope project
```

GitHub CLI installs one named skill at a time. `gh skill install` is the
canonical command; `gh skills add` is its shorter alias.

### Option B: skills.sh CLI

```bash
npx --yes skills@latest add mattpocock/skills \
  --skill grill-me grilling \
  --agent github-copilot \
  --copy \
  --yes
```

Both options copy the skills into `.agents/skills` and record their source.
Open both installed `SKILL.md` files and compare their frontmatter and roles:

- `grill-me` is invoked explicitly by the user.
- `grilling` contains the reusable interview procedure.

Start a fresh chat and try the installed flow:

```text
Use /grill-me to stress-test this idea: add a timed mode to the MCP quiz.
Ask the first round of questions, then stop so I can review them.
```

Notice how one skill can delegate to another. You do not need to implement the
idea or commit the installed files during this exercise.

## Explore skills provided by your Copilot client

Available skills vary by client, installed extensions or plugins, and version.
Choose the instructions for your current surface:

- **VS Code or Codespaces**: Type `/` to browse available skills, or type
  `/skills` to open **Configure Skills**. Inspect the source of a skill provided
  by VS Code or an extension, then invoke it on a small task. If `/create-skill`
  is available, you can use it for the next activity.
- **Copilot CLI**: Run `/skills list`, then `/skills info SKILL-NAME` to inspect
  a preinstalled skill and its location. Invoke it with
  `/SKILL-NAME your task`.
- **GitHub Copilot app**: Select **Customize**, then **Skills**, to browse the
  available set. Try a GitHub-provided skill such as `/af` to find a skill for
  a task. The app's built-in skills differ from those in VS Code and CLI.

Do not assume that a skill available in one client exists in another. Compare
its name, source, purpose, and tools before invoking it.

## Create your own project skill

Create `.agents/skills/quiz-question-reviewer/SKILL.md`. In VS Code, invoke
`/create-skill`; in another client, ask Copilot to create the file directly.
Use this request:

```text
Create a project skill named quiz-question-reviewer. It should review a
multiple-choice MCP quiz question, use Microsoft Learn MCP to verify the fact,
check that exactly one of four options is correct, assess whether the
distractors are plausible, and recommend precise revisions. It must not edit
the quiz unless I explicitly ask.
```

Inspect the generated file. Confirm that the directory matches the skill name,
the frontmatter includes a specific `name` and `description`, and the body
defines a repeatable workflow rather than one fixed answer.

Start a fresh chat so Copilot discovers the new skill. In Copilot CLI, you can
instead run `/skills reload`, followed by
`/skills info quiz-question-reviewer`. Then try it:

```text
Use /quiz-question-reviewer to review this question:

Which MCP primitive lets a server expose executable operations?
A. Tools
B. Resources
C. Prompts
D. Roots
Correct answer: A
```

Watch for a Microsoft Learn MCP call and verify that the response separates
factual evidence from editorial recommendations. Keep or delete the new skill
after the experiment; do not commit it unless you want it in your fork.

## What to observe

- Repository skills are available to everyone who opens the project.
- The installer can add selected skills for a specific Copilot host.
- Skills are files you can inspect and adapt, not trusted executable magic.
- A skill can coordinate MCP tools, local tools, or other skills.
- Installing a skill does not grant new credentials or MCP permissions.

Return to the [README](README.md) for reference links and next steps.
