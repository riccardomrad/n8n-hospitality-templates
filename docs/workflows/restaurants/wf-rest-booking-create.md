# Workflow: Restaurant Booking - Create & Confirm

## Business objective

**Problem:** Restaurants receive bookings from multiple channels (website, forms, phone) and manually confirm each one via WhatsApp or phone call. This wastes time and leads to errors, double bookings, and forgotten confirmations.

**Solution:** This workflow automatically receives a booking request, validates the data, saves it to Google Sheets, and sends a WhatsApp confirmation to the customer -- all in seconds.

**Who it's for:** Restaurants, pizzerias, trattorias, wine bars -- any food service business that takes reservations.

---

## Flow overview

```
Webhook (booking request)
  |
  v
CFG - Settings (restaurant config)
  |
  v
MAP - Normalize (standardize input format)
  |
  v
VAL - Validate (check required fields, E.164 phone, date/time)
  |
  v
IF - Valid? ---NO---> Return 400 error with details
  |
  YES
  |
  v
DB - Save Reservation (Google Sheets - append)
  |
  v
WA - Send Confirmation (WhatsApp template)
  |
  |---SUCCESS---> Update status to "confirmed" --> Return 201
  |
  |---FAIL------> Mark as "confirmation_failed" --> Return 202 (saved but WA failed)
```

---

## Prerequisites

- **n8n** >= 1.50.0 (cloud or self-hosted)
- **WhatsApp Business API** account with approved template
- **Google Sheets** with a reservations sheet
- **WhatsApp Business Cloud** credentials configured in n8n

### WhatsApp template to create in Meta Business Suite

Create a **Utility** template named `booking_confirmation` (language: Italian) with this body:

> Ciao {{1}}, la tua prenotazione da {{2}} persone e confermata per il {{3}} alle {{4}} presso {{5}}. Se vuoi modificare o cancellare, rispondi a questo messaggio.

Parameters: customer_name, covers, date, time, restaurant_name.

### Google Sheet columns

Create a sheet named "Reservations" with these columns (row 1):

| reservation_id | created_at | customer_name | phone_e164 | reservation_date | reservation_time | reservation_datetime | covers | notes | source_channel | language | status | confirmation_message_id | reminder_sent | error_code | error_message |

---

## Configuration

After importing the workflow, edit the **CFG - Settings** node:

| Variable | Description | Example |
|----------|-------------|---------|
| `RESTAURANT_NAME` | Your restaurant name | `Ristorante Da Gino` |
| `WHATSAPP_PHONE_NUMBER_ID` | From Meta Business Suite | `100234567890` |
| `WABA_TEMPLATE_CONFIRM` | Template name in Meta | `booking_confirmation` |
| `TIMEZONE` | Your timezone | `Europe/Rome` |
| `DEFAULT_LANGUAGE` | Message language | `it` |
| `GOOGLE_SHEET_ID` | Google Sheet document ID | `1abc...xyz` |
| `SHEET_NAME` | Sheet tab name | `Reservations` |
| `ADMIN_PHONE` | Admin phone for alerts | `+393401234567` |
| `MAX_COVERS` | Max guests per booking | `20` |

Also configure the Google Sheets credential and WhatsApp credential in n8n.

---

## Test payload

Send this JSON to the webhook URL:

```json
{
  "customer_name": "Mario Rossi",
  "phone": "+393401234567",
  "date": "2026-04-15",
  "time": "20:30",
  "covers": 4,
  "notes": "Tavolo all'aperto se possibile",
  "channel": "website"
}
```

Expected response (201):
```json
{
  "success": true,
  "reservation_id": "RES-ABC123",
  "status": "confirmed",
  "message": "Booking confirmed. WhatsApp confirmation sent."
}
```

---

## Input format

The workflow accepts multiple field naming conventions:

| Standard | Also accepted |
|----------|--------------|
| `customer_name` | `name`, `nome` |
| `phone` | `telefono`, `phone_number` |
| `date` | `data`, `reservation_date` |
| `time` | `ora`, `reservation_time` |
| `covers` | `coperti`, `guests`, `persone` |
| `notes` | `note` |

Phone numbers are automatically normalized to E.164 format (Italian +39 default).

---

## Limitations

- Storage is Google Sheets (not a database) -- suitable for small/medium restaurants
- No built-in duplicate detection across different phone numbers for the same person
- WhatsApp template must be pre-approved by Meta before the workflow can send messages
- The webhook has no authentication by default -- add API key validation for production use

---

## Related workflows

- [Booking Reminder 24h](wf-rest-booking-reminder.md) -- sends a reminder the day before
- [Inbound Reply Handler](wf-rest-booking-inbound.md) -- handles customer responses
- [Error Handler](wf-rest-booking-error-handler.md) -- centralized error logging

---

**Author:** RAD LAB | **Version:** 1.0 | **License:** Apache 2.0
