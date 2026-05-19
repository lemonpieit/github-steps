# Usage Guide

## Available Actions

### 1. NPM Audit with Slack

Runs `npm audit` and notifies Slack when vulnerabilities are detected.

#### Location
`npm-audit@v1.0.6`

#### Inputs

| Input | Required | Description |
|-------|----------|-------------|
| `webhook` | ✅ | Slack incoming webhook URL |

#### Behavior

- Runs `npm audit --audit-level=high` to check for high or higher severity vulnerabilities
- If vulnerabilities are found, sends a Slack notification with details
- Fails the workflow if vulnerabilities are detected

#### Example Usage

```yaml
- uses: lemonpieit/github-steps/npm-audit@v1.0.6
  with:
    webhook: ${{ secrets.SLACK_WEBHOOK_URL }}
```

---

### 2. Slack Notify

Sends formatted Slack notifications with repository, workflow, and commit information.

#### Location
`slack-notify@v1.0.6`

#### Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `webhook` | ✅ | - | Slack incoming webhook URL |
| `title` | ✅ | - | Notification title/header text |
| `color` | ❌ | `good` | Message color (good, warning, danger, etc.) |

#### Example Usage

```yaml
- uses: lemonpieit/github-steps/slack-notify@v1.0.6
  with:
    webhook: ${{ secrets.SLACK_WEBHOOK_URL }}
    title: "✅ Deployment successful"
    color: "good"
```