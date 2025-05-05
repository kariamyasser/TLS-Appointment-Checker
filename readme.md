# TLSContact Appointment Checker GitHub Action

This repository contains a GitHub Actions workflow that automatically checks for available appointments on the TLSContact website and sends email notifications when appointments become available.

## How It Works

The workflow runs every 30 minutes and:
1. Launches a headless browser
2. Logs into your TLSContact account 
3. Monitors API responses for appointment availability
4. Sends email notifications about the results

## Setup Instructions

### 1. Create a New Repository

Create a new GitHub repository to host this workflow.

### 2. Add the Workflow File

Create a new file at `.github/workflows/TLSContact-Appointment-Checker.yml` and copy the workflow configuration from this repository.

### 3. Configure Secrets

Add the following secrets to your GitHub repository:

1. Go to your repository → Settings → Secrets and variables → Actions
2. Click "New repository secret" and add each of these:

| Secret Name      | Description                              |
|------------------|------------------------------------------|
| `TLS_EMAIL`      | Your TLSContact login email              |
| `TLS_PASSWORD`   | Your TLSContact password                 |
| `EMAIL_USERNAME`     | Email address to send notifications from |
| `EMAIL_PASSWORD`     | Email app password or regular password   |
| `NOTIFICATION_EMAIL`| Email address to receive notifications   |

> **Note for Gmail users:** If you're using Gmail, you'll need to create an "App Password" if you have 2FA enabled on your Google account. Go to your Google Account → Security → App passwords to generate one.

### 4. Enable Actions

Make sure GitHub Actions is enabled for your repository:
1. Go to Settings → Actions → General
2. Select "Allow all actions and reusable workflows"
3. Click "Save"

### 5. Manual Trigger (Optional)

You can manually trigger the workflow:
1. Go to the "Actions" tab in your repository
2. Select the "TLSContact Appointment Checker" workflow
3. Click "Run workflow"

## Customization

### Changing Check Frequency

To change how often the checker runs, modify the cron schedule in the workflow file:

```yaml
on:
  schedule:
    # Current: Every 30 minutes
    - cron: '*/30 * * * *'
    
    # Examples:
    # Every hour: '0 * * * *'
    # Every 15 minutes: '*/15 * * * *'
    # Every 2 hours: '0 */2 * * *'
```

### Changing Target URL

If you need to check a different TLSContact appointment URL, modify the `targetUrl` variable in the script.

## Troubleshooting

### Check Workflow Logs

If you're not receiving emails or experiencing issues:
1. Go to the "Actions" tab
2. Click on the latest workflow run
3. Expand the "Run appointment checker" step to view logs

### GitHub Actions Limitations

- GitHub provides 2,000 free minutes per month for private repositories
- Workflows may have brief delays when GitHub resources are under high demand
- GitHub disables scheduled actions if a repository remains inactive for 60 days

## Security Considerations

- Your credentials are stored as encrypted GitHub secrets
- The workflow runs in an isolated environment
- No credentials are exposed in logs or commit history
