# Contributing to n8n Local Business Automation Kit

Thanks for your interest in contributing! This repository collects **ready-to-use n8n workflows for local businesses** (restaurants, hotels, salons, medical practices).

Our goal is to keep workflows: simple to understand, well documented, and immediately reusable in real scenarios.

> You can also write in Italian -- we will answer in both languages.

## How can I contribute?

- **New workflows** for real business use cases
- **Improvements** to existing workflows
- **Bug fixes** and corrections
- **Better documentation** (README, workflow docs, examples)

Before starting, **open a Discussion or Issue** to propose your idea so we avoid duplicates.

## Requirements for new workflows

Your workflow should:

1. Be exported from n8n as a `.json` file
2. Have a clear, descriptive name, e.g.: `wf-rest-reservations-whatsapp-confirmation.v1.json`
3. Include a `README.md` in the same docs folder with:
   - Business use case description
   - Requirements (APIs, credentials, external accounts)
   - Step-by-step setup instructions
   - Optional screenshots

### Folder structure

```
workflows/restaurants/reservations/
  wf-rest-reservations-whatsapp-confirmation.v1.json

docs/workflows/restaurants/
  wf-rest-reservations-whatsapp-confirmation.md
```

### Naming convention

- Prefix: `wf-` for workflows, `sn-` for shared snippets
- Pattern: `wf-<industry>-<domain>-<action>.v<version>.json`
- Examples:
  - `wf-rest-marketing-review-request.v1.json`
  - `wf-hotel-booking-whatsapp-reminder.v1.json`
  - `sn-shared-normalize-phone.v1.json`

## Opening an Issue

Use the available templates:

- **Bug report**: something doesn't work in an existing workflow
- **Workflow request**: request a new workflow or improvement

Always include: clear title, business context, n8n version, steps to reproduce (if bug).

## Opening a Pull Request

1. Fork the repository
2. Create a descriptive branch: `feature/new-restaurant-review-workflow`
3. Add or modify the relevant files
4. Make sure the workflow imports correctly in n8n
5. Open a PR to `main` with:
   - Type of contribution (new workflow / fix / docs)
   - Use case it solves
   - How to test it

## Style guidelines

- Keep workflows **configurable** (use credentials, env variables)
- **No hardcoded sensitive data** (API keys, tokens, URLs)
- Use **clear node names** (e.g., "Check booking status", not "Function1")
- Add comments to complex nodes directly in n8n
- Keep Italian content for WhatsApp message templates; use English for technical comments

## Acceptance criteria

For a PR to be accepted:

1. Solves a **real business use case** for local businesses
2. **Importable and functional** in n8n without errors
3. **Documented** with a dedicated README
4. **Generic and reusable** (no hardcoded brand-specific data)
5. **Follows project style** (naming, folder structure, node names)

Maintainers may request changes, reject duplicates, or decline workflows that are too niche to maintain.

Not sure if your idea fits? Open a **Discussion** first.

## Code of Conduct

By participating, you agree to our [Code of Conduct](CODE_OF_CONDUCT.md).
