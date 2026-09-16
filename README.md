# xAI Code Review

AI-powered GitHub Pull Request code review using xAI Grok models. Automatic PR comments, bug detection, and improvement suggestions via GitHub Actions.

## Features

- 🚀 Detect bugs
- 🔍 Suggest improvements
- 🧠 AI-driven PR feedback
- ⚡ Works with GitHub Actions

## Quickstart

Add this to your `.github/workflows/code-review.yml`:

```yaml
name: AI Code Review with xAI

on:
  pull_request:
    types: [opened, synchronize]

permissions:
  pull-requests: write

jobs:
  review:
    name: Review
    runs-on: ubuntu-latest
    steps:
      - name: Code Review
        uses: tarmojussila/xai-code-review@v0.1.1
        with:
          XAI_API_KEY: ${{ secrets.XAI_API_KEY }}
```

## Inputs

| Input | Required | Default | Description |
|---|---|---|---|
| `XAI_API_KEY` | Yes | — | Your xAI API key |
| `XAI_MODEL` | No | `grok-3` | xAI Grok model to use for review |
| `XAI_SYSTEM_PROMPT` | No | See below | Custom system prompt for the AI reviewer |
| `XAI_REVIEWER_NAME` | No | `xAI Code Review` | Name shown in the review comment header |
| `EXCLUDE_PATTERNS` | No | `*.lock,package-lock.json,yarn.lock,pnpm-lock.yaml` | Comma-separated file patterns to exclude from review |
| `MAX_DIFF_CHARS` | No | `0` (unlimited) | Maximum total characters for the diff sent to the API |

The default system prompt is:

> You are an expert code reviewer. Review the provided code changes and give clear, actionable feedback.

You can override it to focus on specific concerns, enforce coding standards, or adjust the review tone, e.g.:

> You are a security-focused code reviewer. Identify vulnerabilities, unsafe patterns, and authentication issues. Skip style comments.

## Configuration

To use this action, you must add your xAI API key as a GitHub secret.

### 1️⃣ Get your xAI API key

Generate an API key from the [xAI console](https://console.x.ai/).

### 2️⃣ Add the API key to your repository

1. Go to your GitHub repository
2. Click **Settings**
3. Navigate to **Secrets and variables → Actions**
4. Click **New repository secret** and add:

   - **Name:** `XAI_API_KEY` — **Value:** your xAI API key

## Advanced configuration

Instead of using default values for `XAI_MODEL`, `XAI_SYSTEM_PROMPT`, and `XAI_REVIEWER_NAME`, you can override them, and manage them as GitHub Actions variables. This lets you update the model, review prompt, or reviewer name without touching the workflow file.

### 1️⃣ Add the variables to your repository

1. Go to your GitHub repository
2. Click **Settings**
3. Navigate to **Secrets and variables → Actions**
4. Click the **Variables** tab
5. Click **New repository variable** and add:

   - **Name:** `XAI_MODEL` — **Value:** e.g. `grok-3`
   - **Name:** `XAI_SYSTEM_PROMPT` — **Value:** your custom system prompt
   - **Name:** `XAI_REVIEWER_NAME` — **Value:** e.g. `AI Code Review`

### 2️⃣ Reference them in your workflow

```yaml
      - name: Code Review
        uses: tarmojussila/xai-code-review@v0.1.1
        with:
          XAI_API_KEY: ${{ secrets.XAI_API_KEY }}
          XAI_MODEL: ${{ vars.XAI_MODEL }}
          XAI_SYSTEM_PROMPT: ${{ vars.XAI_SYSTEM_PROMPT }}
          XAI_REVIEWER_NAME: ${{ vars.XAI_REVIEWER_NAME }}
```

## Contributing

Contributions are welcome. See the [CONTRIBUTING](CONTRIBUTING.md) file for more information.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more information.
