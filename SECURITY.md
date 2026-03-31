# Security Policy

## Reporting a Vulnerability

If you discover a security vulnerability in this repository, please report it responsibly.

**Email:** hello@radlab.it

Please include:
- Description of the vulnerability
- Steps to reproduce
- Potential impact

We will respond within 48 hours and work with you to resolve the issue.

## Credential Safety

This repository contains n8n workflow JSON files. These files **must never** contain:

- API keys or tokens
- Passwords or secrets
- Webhook URLs pointing to production systems
- Personal data (names, phone numbers, emails)
- OAuth tokens or session data

### Before committing a workflow

1. Export the workflow from a **development instance** with dummy credentials
2. Review the JSON and remove any `credentials` values that reference real accounts
3. Replace production URLs with placeholders (e.g., `https://your-n8n-instance.com`)
4. Check for hardcoded phone numbers, email addresses, or API endpoints

### If you find exposed credentials

If you notice any real credentials in a committed workflow, please:
1. **Do not use them**
2. Report it immediately via email (above)
3. We will rotate the credentials and clean the git history

## Supported Versions

We apply security fixes to the latest version on the `main` branch only.
