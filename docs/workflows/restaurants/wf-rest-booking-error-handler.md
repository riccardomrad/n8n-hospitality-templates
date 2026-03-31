# Workflow: Restaurant Booking - Error Handler

## Business objective

**Problem:** When an automation fails silently, nobody notices until a customer complains. Errors in booking confirmation or reminders can mean lost reservations.

**Solution:** This workflow catches errors from all other booking workflows, logs them to a Google Sheet, and optionally sends a WhatsApp alert to the restaurant admin.

**Who it's for:** Anyone running the booking automation workflows in production.

---

## Flow overview

```
Error Trigger (catches errors from other workflows)
  |
  v
MAP - Extract error details (workflow name, node, message, URL)
  |
  v
DB - Log to "Errors" sheet in Google Sheets
  |
  v
WA - Alert Admin (optional WhatsApp notification)
```

---

## Prerequisites

- **n8n** >= 1.50.0
- **Google Sheets** with an "Errors" sheet tab

### Google Sheet "Errors" tab columns

Create a new tab called "Errors" in the same Google Sheet with these columns:

| workflow_name | workflow_id | execution_id | error_message | error_node | error_timestamp | execution_url |

### Link to other workflows

In each booking workflow (Create, Reminder, Inbound), go to **Settings** and set the **Error Workflow** to this workflow.

---

## Configuration

1. Configure the Google Sheets node with your document and the "Errors" sheet tab
2. **(Optional)** Edit the **WA - Alert Admin** node with your admin phone number and a WhatsApp template for error alerts
3. If you don't want WhatsApp alerts, you can delete or disable the WA node -- errors will still be logged

### Alternative alert channels

Instead of WhatsApp, you can replace the last node with:
- **Email** node for email alerts
- **Telegram** node for Telegram notifications
- **Slack** node for team channels

---

## Limitations

- Only catches errors if the other workflows have this workflow set as their Error Workflow
- WhatsApp alert template must be approved by Meta (or replace with email/Telegram)
- Does not retry failed operations -- it only logs and alerts

---

## Related workflows

- [Booking Create](wf-rest-booking-create.md)
- [Booking Reminder](wf-rest-booking-reminder.md)
- [Inbound Reply Handler](wf-rest-booking-inbound.md)

---

**Author:** RAD LAB | **Version:** 1.0 | **License:** Apache 2.0
