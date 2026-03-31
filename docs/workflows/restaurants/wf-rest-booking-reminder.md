# Workflow: Restaurant Booking - Reminder 24h

## Business objective

**Problem:** Restaurants lose revenue from no-shows. A simple reminder the day before significantly reduces missed reservations.

**Solution:** This workflow runs every 15 minutes, checks for confirmed reservations happening in the next 24 hours, and sends a WhatsApp reminder to each customer.

**Who it's for:** Any restaurant using the Booking Create workflow that wants to reduce no-shows.

---

## Flow overview

```
Schedule Trigger (every 15 min)
  |
  v
CFG - Settings
  |
  v
DB - Read all reservations from Google Sheets
  |
  v
FILTER - Find reservations due in 23.5h - 24.5h with reminder_sent = "no"
  |
  v
IF - Any reminders to send?
  |
  YES --> WA - Send Reminder template --> DB - Mark reminder_sent = "yes"
  |
  NO --> End (nothing to do)
```

---

## Prerequisites

- **n8n** >= 1.50.0
- **Booking Create workflow** already saving reservations to Google Sheets
- **WhatsApp Business API** with approved reminder template

### WhatsApp template

Create a **Utility** template named `booking_reminder` (language: Italian):

> Ciao {{1}}, ti ricordiamo la tua prenotazione per oggi alle {{2}} per {{3}} persone presso {{4}}. Ti aspettiamo!

Parameters: customer_name, time, covers, restaurant_name.

---

## Configuration

Edit the **CFG - Settings** node:

| Variable | Description | Example |
|----------|-------------|---------|
| `RESTAURANT_NAME` | Your restaurant name | `Ristorante Da Gino` |
| `WHATSAPP_PHONE_NUMBER_ID` | From Meta Business Suite | `100234567890` |
| `WABA_TEMPLATE_REMINDER` | Template name | `booking_reminder` |
| `GOOGLE_SHEET_ID` | Same sheet as Booking Create | `1abc...xyz` |
| `SHEET_NAME` | Sheet tab name | `Reservations` |
| `REMINDER_HOURS_BEFORE` | Hours before reservation | `24` |

---

## How it works

1. Runs automatically every 15 minutes
2. Reads all reservations from Google Sheets
3. Filters for: `status = confirmed` AND `reminder_sent = no` AND reservation is 23.5-24.5 hours away
4. Sends WhatsApp reminder template to matching customers
5. Marks `reminder_sent = yes` to prevent duplicate reminders

The 1-hour window (23.5h to 24.5h) ensures no reservation is missed even if n8n has a brief delay.

---

## Limitations

- Reads the entire sheet each run -- for very high-volume restaurants, consider a database
- If n8n is down for more than 1 hour, some reminders may be skipped
- The timezone must be set correctly in both n8n and the workflow settings

---

## Related workflows

- [Booking Create](wf-rest-booking-create.md) -- creates reservations (required)
- [Inbound Reply Handler](wf-rest-booking-inbound.md) -- handles customer responses
- [Error Handler](wf-rest-booking-error-handler.md) -- centralized error logging

---

**Author:** RAD LAB | **Version:** 1.0 | **License:** Apache 2.0
