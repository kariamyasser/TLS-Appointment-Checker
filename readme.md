# TLS Contact Appointment Checker

This GitHub Action automatically checks the TLS Contact website for available visa appointment slots every 30 minutes and sends email notifications when appointments become available.

## How It Works

1. The workflow runs every 30 minutes or can be triggered manually
2. It uses Puppeteer to access the TLS Contact website
3. Logs in with your provided credentials (if needed)
4. Checks multiple API endpoints for different appointment types
5. Sends detailed email reports after each run, including:
   - Status of all API checks
   - Discovery of any new appointment-related APIs
   - Complete run status with timestamps
   - Available appointment notifications (when found)

## Setup Instructions

### 1. Fork or Clone This Repository

Create your own copy of this repository by forking it or creating a new repository with these files.

### 2. Configure GitHub Secrets

Add the following secrets to your GitHub repository:

- `EMAIL_USERNAME`: Your Gmail address that will be used to send notifications
- `EMAIL_PASSWORD`: Your Gmail app password ([how to create an app password](https://support.google.com/accounts/answer/185833))
- `NOTIFICATION_EMAIL`: The email address where you want to receive notifications
- `TLS_EMAIL`: Your TLS Contact account email (optional, defaults to "admin")
- `TLS_PASSWORD`: Your TLS Contact account password (optional, defaults to "admin")

To add these secrets:
1. Go to your repository on GitHub
2. Click "Settings" > "Secrets and variables" > "Actions"
3. Click "New repository secret" and add each secret

### 3. Enable GitHub Actions

Make sure GitHub Actions are enabled for your repository:
1. Go to "Settings" > "Actions" > "General"
2. Select "Allow all actions and reusable workflows"
3. Click "Save"

## Customization

### Check Frequency

To change how often the script runs, modify the cron schedule in `.github/workflows/check-appointments.yml`:

```yaml
schedule:
  - cron: '*/15 * * * *'  # Runs every 15 minutes
```

For example, to run every hour, use `0 * * * *` instead.

### Notification Method

The current setup uses email notifications. If you want to add other notification methods like WhatsApp, you'll need to integrate with an appropriate service (like Twilio) and modify the `sendNotification` function in the script.

## Troubleshooting

If the script doesn't work as expected:

1. Check the GitHub Actions logs to see detailed output
2. Verify that your credentials are correct
3. The website structure might have changed; you may need to update selectors in the script

## Security Considerations

- This repository uses GitHub Secrets to store sensitive information
- Never commit credentials directly in your code
- The Gmail account used for sending emails should have "Less secure app access" or an app password configured

## Limitations

- The script may need updates if the TLS Contact website changes its structure
- GitHub Actions has usage limits - check GitHub's documentation if you're running many workflows
