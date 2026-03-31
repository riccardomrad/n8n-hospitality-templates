# Workflow: Restaurant Booking - Inbound Reply Handler

## Business objective

**Problem:** After sending a confirmation or reminder, customers may reply to confirm, cancel, or request a change. Without automation, staff must manually read and process each reply.

**Solution:** This workflow receives WhatsApp replies (button clicks or text), classifies the intent, finds the matching reservation, and updates its status automatically.

**Who it's for:** Restaurants using the Booking Create and Reminder workflows.

---

## Flow overview

```
WhatsApp Webhook (incoming message from Meta)
  |
  v
MAP - Parse Reply (extract phone, action, text)
  |
  v
IF - Is it a message? (skip status updates)
  |
  v
IF - Confirm? --> SET status "confirmed_by_customer"
  |
  ELSE
  |
  v
IF - Cancel? --> SET status "cancelled_by_customer"
  |
  ELSE --> SET status "needs_manual_review"
  |
  v
DB - Find reservation by phone number
  |
  v
DB - Update reservation status
```

---

## Prerequisites

- **n8n** >= 1.50.0
- **WhatsApp Business API** webhook configured to forward messages to this n8n webhook
- **Google Sheets** with the same reservations sheet used by Booking Create

### Meta webhook configuration

In your Meta App Dashboard, set the webhook URL to your n8n webhook:
`https://your-n8n-instance.com/webhook/whatsapp-inbound`

Subscribe to the `messages` webhook field.

---

## Supported reply types

| Reply type | How it's detected | Result |
|------------|-------------------|--------|
| Quick reply button "Confermo" | Button text contains "conferm" | `confirmed_by_customer` |
| Quick reply button "Cancella" | Button text contains "cancel" or "annul" | `cancelled_by_customer` |
| Quick reply button "Modifica" | Button text contains "modif" or "cambi" | `needs_manual_review` |
| Text "si", "ok", "confermo" | Text matching | `confirmed_by_customer` |
| Text "no", "cancella", "annulla" | Text matching | `cancelled_by_customer` |
| Text "modificare", "spostare" | Text matching | `needs_manual_review` |
| Any other text | No match | `needs_manual_review` |

Replies classified as `needs_manual_review` should be handled by staff manually.

---

## Configuration

Configure the Google Sheets nodes with the same document and sheet used by the Booking Create workflow.

---

## Limitations

- Matches replies by phone number only -- if a customer has multiple reservations, it may update the wrong one
- Free-text parsing is basic (keyword matching) -- not AI-powered
- Modification requests are flagged for manual review, not processed automatically
- The Meta webhook must be verified and configured separately in the Meta App Dashboard

---

## Related workflows

- [Booking Create](wf-rest-booking-create.md) -- creates reservations (required)
- [Booking Reminder](wf-rest-booking-reminder.md) -- sends 24h reminders
- [Error Handler](wf-rest-booking-error-handler.md) -- centralized error logging

---

**Author:** RAD LAB | **Version:** 1.0 | **License:** Apache 2.0
