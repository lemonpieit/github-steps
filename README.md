# Usage Guide

## Available Actions

### 1. NPM Audit with Slack

Runs `npm audit` and notifies Slack when vulnerabilities are detected.

#### Location
`npm-audit@v1.0.8`

#### Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `webhook` | ❌ | - | Slack incoming webhook URL. Omit to skip Slack notification. |
| `include-results` | ❌ | `true` | Include the npm audit summary as a subtitle in the Slack notification. |

#### Behavior

- Runs `npm audit --audit-level=high` to check for high or higher severity vulnerabilities
- If vulnerabilities are found and `webhook` is provided, sends a Slack notification with details
- Fails the workflow if vulnerabilities are detected

#### Example Usage

```yaml
# With Slack notification and audit summary
- uses: lemonpieit/github-steps/npm-audit@v1.0.8
  with:
    webhook: ${{ secrets.SLACK_WEBHOOK_URL }}

# With Slack notification but without audit summary
- uses: lemonpieit/github-steps/npm-audit@v1.0.8
  with:
    webhook: ${{ secrets.SLACK_WEBHOOK_URL }}
    include-results: 'false'

# Without Slack notification
- uses: lemonpieit/github-steps/npm-audit@v1.0.8
```

---

### 2. Slack Notify

Sends formatted Slack notifications with repository, workflow, and commit information.

#### Location
`slack-notify@v1.0.8`

#### Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `webhook` | ❌ | - | Slack incoming webhook URL. Omit to skip sending the notification. |
| `title` | ✅ | - | Notification title/header text |
| `subtitle` | ❌ | - | Optional subtitle rendered below the title |
| `color` | ❌ | `good` | Message color (good, warning, danger, etc.) |

#### Example Usage

```yaml
- uses: lemonpieit/github-steps/slack-notify@v1.0.8
  with:
    webhook: ${{ secrets.SLACK_WEBHOOK_URL }}
    title: "✅ Deployment successful"
    subtitle: "Deployed to production by ${{ github.actor }}"
    color: "good"
```

---

## Releasing a New Version

To create a new release from the terminal using the GitHub CLI:

```bash
gh release create v1.0.0 --title "v1.0.0"
```

Replace `v1.0.0` with the desired version tag. Actions in this repo are referenced by these version tags (e.g. `npm-audit@v1.0.0`).