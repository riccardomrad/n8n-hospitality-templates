# n8n Local Business Automation Kit

Ready-to-use n8n workflows to automate **restaurants, hotels, salons and medical practices**: bookings, WhatsApp reminders, review follow-ups, marketing campaigns and more.

[![Made with n8n](https://img.shields.io/badge/made%20with-n8n-EA4B71)](https://n8n.io)
[![License: Apache 2.0](https://img.shields.io/badge/license-Apache%202.0-blue)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen)](CONTRIBUTING.md)

> **Read this in:** [Italiano](README.IT.md)

---

## How it works

<!-- TODO: Add GIF demo of a workflow in action -->

Each workflow solves a real business problem for local businesses:

1. **Customer writes on WhatsApp** (or books online)
2. **n8n processes the request** (creates booking, updates calendar, logs data)
3. **Automatic follow-up** (confirmation, reminder 24h before, review request after visit)

No coding required. Import the JSON, set up your credentials, and you're live.

---

## Try it in 5 minutes

1. Install [n8n](https://docs.n8n.io/hosting/) (cloud or self-hosted)
2. Download a workflow `.json` from the [`workflows/`](workflows/) folder
3. In n8n, go to **Workflows > Import from File** and upload it
4. Set up the required credentials (WhatsApp, Google Calendar, etc.)
5. Click **Execute Workflow** and test with sample data

> Want a ready-to-go demo instance? [Open an issue](../../issues/new) and we'll help you get started.

---

## Use cases

- [Restaurants](#-restaurants)
- [Hotels & B\&Bs](#-hotels--bbs)
- [Salons & Beauty](#-salons--beauty)
- [Medical Practices](#-medical-practices)

---

### Restaurants

| Workflow | Description | Folder |
|----------|-------------|--------|
| WhatsApp Booking Confirmation | Auto-confirm reservations via WhatsApp | `workflows/restaurants/reservations/` |
| No-Show Recovery | Tag no-show clients and send a recovery message | `workflows/restaurants/reservations/` |
| Google Review Request | Ask for a review 2h after the dinner service | `workflows/restaurants/marketing/` |
| Weekly Report | Summary of bookings, no-shows and reviews | `workflows/restaurants/operations/` |

**Typical results:** fewer missed calls, fewer no-shows, more Google reviews.

---

### Hotels & B&Bs

| Workflow | Description | Folder |
|----------|-------------|--------|
| Pre-Stay Welcome | WhatsApp message with check-in info, parking, upsell | `workflows/hotels/booking/` |
| Booking Reminder | Confirmation + reminder 24h before arrival | `workflows/hotels/booking/` |
| Post-Stay Review | Ask for a Google/Booking review after checkout | `workflows/hotels/marketing/` |
| Win-Back Campaign | Message past guests after 30/180 days | `workflows/hotels/marketing/` |

**Typical results:** better guest experience, more direct bookings, higher review scores.

---

### Salons & Beauty

| Workflow | Description | Folder |
|----------|-------------|--------|
| Appointment Reminder | WhatsApp reminder 24h before, with confirm/cancel buttons | `workflows/salons/appointments/` |
| No-Show Follow-Up | Automatic re-engagement after a missed appointment | `workflows/salons/appointments/` |
| Rebooking Nudge | "Time for a new haircut?" after X weeks | `workflows/salons/marketing/` |

**Typical results:** fewer no-shows, higher rebooking rate.

---

### Medical Practices

| Workflow | Description | Folder |
|----------|-------------|--------|
| Appointment Reminder | Multi-channel reminder (WhatsApp + SMS fallback) | `workflows/clinics/appointments/` |
| Annual Check-Up Recall | Yearly reminder for check-ups and screenings | `workflows/clinics/appointments/` |
| Post-Visit Feedback | Quick satisfaction survey after the visit | `workflows/clinics/marketing/` |

**Typical results:** fewer missed appointments, better patient retention.

---

## Repository structure

```
workflows/           # n8n workflow JSON files, organized by industry
  restaurants/       #   reservations, marketing, operations
  hotels/            #   booking, marketing, operations
  salons/            #   appointments, marketing
  clinics/           #   appointments, marketing
  _shared-snippets/  #   reusable sub-flows (phone normalization, etc.)
docs/                # Documentation for each workflow + setup guides
  workflows/         #   one .md per workflow (mirrors workflows/ structure)
  guides/            #   general guides (self-hosted setup, credentials, etc.)
  images/            #   screenshots and diagrams
demo/                # Docker Compose for local testing
.github/             # CI, issue templates, PR template
```

---

## Compatibility

- **n8n version:** >= 1.50.0 (tested up to latest)
- **Channels:** WhatsApp Business API, Telegram, Email, SMS
- **Integrations:** Google Calendar, Google Sheets, CRM webhooks
- **Hosting:** Works on n8n Cloud and self-hosted (Docker)

---

## For Italian businesses

These workflows were born from real automation projects for restaurants, hotels, salons and medical practices in **Campania, Italy** (Ischia, Procida, Naples).

All WhatsApp message templates are available in **Italian** inside the workflow JSON files. The documentation includes Italian guides in the [`docs/`](docs/) folder.

If you run a local business in Italy and want these workflows customized for you:

- **Setup** on n8n (cloud or your own server)
- **Integration** with your existing tools (PMS, booking systems, CRM)
- **Custom workflows** tailored to your specific needs

Get in touch: [RAD LAB](https://radlab.it) -- we automate local businesses so you can focus on your customers.

---

## Contributing

We welcome contributions! Whether it's a new workflow, a bug fix, or better documentation.

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## License

This project is licensed under the [Apache License 2.0](LICENSE).

You are free to use these workflows commercially, as long as you:
- Keep clear attribution to **RAD LAB** as the original author
- Don't resell them as-is as a closed proprietary product without substantial modifications

For commercial licensing questions: [hello@radlab.it](mailto:hello@radlab.it)

---

Made with dedication by [RAD LAB](https://radlab.it) -- Digital automation for local businesses.
