# Exercise 0: Set up your development environment and GitHub Copilot

In this exercise, you will fork the workshop repository, open your fork in a development environment, verify its Python environment, and confirm that GitHub Copilot can work with the project.

## Contents

- [Step 1: Fork the workshop repository](#step-1-fork-the-workshop-repository)
- [Step 2: Set up your development environment](#step-2-set-up-your-development-environment)
- [Step 3: Set up GitHub Copilot](#step-3-set-up-github-copilot)

## Step 1: Fork the workshop repository

1. Sign in to your GitHub account and open the [workshop repository](https://github.com/pamelafox/github-copilot-mcp-skills-workshop).
1. Select **Fork**, choose your personal account as the owner, and keep the repository name `github-copilot-mcp-skills-workshop`.
1. Select **Create fork** and wait for GitHub to open the new repository under your account.
1. Confirm that the page identifies it as forked from `pamelafox/github-copilot-mcp-skills-workshop`.

Use your fork for every setup option below. This ensures your Codespace or local
checkout already has a writable Git repository when you create the pull request
in Exercise 2.

## Step 2: Set up your development environment

Choose one option. GitHub Codespaces is recommended because the repository's development container installs Python, uv, dependencies, and the required VS Code extensions.

### Option A: GitHub Codespaces (recommended)

1. Open `https://github.com/YOUR-GITHUB-USERNAME/github-copilot-mcp-skills-workshop`.
1. Select **Code**, then **Codespaces**, then **Create codespace on main**.

   ![Create a codespace from the repository](docs/screenshot_codespaces_open.png)

1. Wait for the browser-based VS Code editor to load and the `postCreateCommand` to finish.

### Option B: VS Code with Dev Containers

Install [VS Code](https://code.visualstudio.com/), [Docker Desktop](https://www.docker.com/products/docker-desktop/), and the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers). Then run:

```bash
git clone https://github.com/YOUR-GITHUB-USERNAME/github-copilot-mcp-skills-workshop.git
code github-copilot-mcp-skills-workshop
```

When VS Code opens, select **Reopen in Container**. If the prompt does not appear, run **Dev Containers: Reopen in Container** from the Command Palette. Wait for the container setup to finish.

### Option C: Local environment

Install [Git](https://git-scm.com/), Python 3.12 or later, [uv](https://docs.astral.sh/uv/getting-started/installation/), and an environment from the [supported Copilot environments](README.md#supported-copilot-environments). Then run:

```bash
git clone https://github.com/YOUR-GITHUB-USERNAME/github-copilot-mcp-skills-workshop.git
cd github-copilot-mcp-skills-workshop
uv sync
```

### Verify the environment

From the repository root, run:

```bash
uv run python --version
uv run python -c "from src.quiz import QUESTIONS; print(len(QUESTIONS))"
```

Confirm that Python is version 3.12 or later and the second command reports the
number of quiz questions.

## Step 3: Set up GitHub Copilot

Choose the Copilot environment you will use for the workshop.

### GitHub Copilot in VS Code or Codespaces

1. Open Copilot Chat using the chat icon in the VS Code title bar.

   ![Open Copilot Chat in VS Code](docs/screenshot_copilot_togglechat.png)

1. Sign in and accept the usage terms if prompted.
1. Select **Agent** mode in the chat input.

   ![Copilot Chat with Agent mode selected](docs/screenshot_copilot_agent.png)

1. Send `Which workspace folder is currently open?` and confirm the response names this repository.
1. Ask `What is the upstream repository for this fork?` and confirm the response identifies `pamelafox/github-copilot-mcp-skills-workshop`.

### GitHub Copilot CLI

1. Install Copilot CLI by following the [installation guide](https://docs.github.com/en/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli).
1. From the repository root, run `copilot` and sign in if prompted.
1. Ask `Which repository am I currently working in?` and confirm the response.
1. Ask `What is the upstream repository for this fork?` and confirm the response identifies `pamelafox/github-copilot-mcp-skills-workshop`.

### GitHub Copilot app

1. Install and open the [GitHub Copilot app](https://github.com/github/app).
1. From **Sessions**, select **+**, then **Add project from GitHub repository**.
1. Add `https://github.com/YOUR-GITHUB-USERNAME/github-copilot-mcp-skills-workshop`.
1. Ask `Which repository is attached to this session?` and confirm the response.
1. Ask `What is the upstream repository for this fork?` and confirm the response identifies `pamelafox/github-copilot-mcp-skills-workshop`.

Continue to [Exercise 1](exercise1.md).
