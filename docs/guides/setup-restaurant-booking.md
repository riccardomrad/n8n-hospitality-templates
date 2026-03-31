# Setup Guide: Restaurant Booking Automation

Complete setup guide for the 4-workflow restaurant booking system.

---

## What you'll get

1. **Automatic booking confirmation** via WhatsApp when a customer books
2. **24h reminder** to reduce no-shows
3. **Reply handling** -- customer confirms, cancels, or modifies via WhatsApp buttons
4. **Error monitoring** -- alerts if something goes wrong

---

## Step 1: WhatsApp Business API setup

1. Go to [Meta Business Suite](https://business.facebook.com)
2. Create or access your WhatsApp Business account
3. Get your **Phone Number ID** and **Access Token**
4. Create two message templates (Utility category, Italian language):

### Template 1: `booking_confirmation`
```
Ciao {{1}}, la tua prenotazione da {{2}} persone e confermata per il {{3}} alle {{4}} presso {{5}}. Se vuoi modificare o cancellare, rispondi a questo messaggio.
```
Sample values: Mario Rossi, 4, 2026-04-15, 20:30, Ristorante Da Gino

### Template 2: `booking_reminder`
```
Ciao {{1}}, ti ricordiamo la tua prenotazione per oggi alle {{2}} per {{3}} persone presso {{4}}. Ti aspettiamo!
```
Sample values: Mario Rossi, 20:30, 4, Ristorante Da Gino

Wait for Meta to approve both templates (usually 1-24 hours).

---

## Step 2: Google Sheets setup

1. Create a new Google Sheet
2. Name the first tab **Reservations**
3. Add these column headers in row 1:

```
reservation_id | created_at | updated_at | customer_name | phone_e164 | reservation_date | reservation_time | reservation_datetime | covers | notes | source_channel | language | status | confirmation_message_id | reminder_sent | reminder_sent_at | last_inbound_message_at | error_code | error_message
```

4. Create a second tab called **Errors** with these columns:
```
workflow_name | workflow_id | execution_id | error_message | error_node | error_timestamp | execution_url
```

5. Copy the **Spreadsheet ID** from the URL (the long string between /d/ and /edit)

---

## Step 3: n8n credentials

In n8n, create two credentials:

### WhatsApp Business Cloud
- Go to **Credentials > New > WhatsApp Business Cloud**
- Enter your **Access Token** and **Business Account ID** from Meta

### Google Sheets
- Go to **Credentials > New > Google Sheets**
- Follow the OAuth2 flow to authorize access to your Google account

---

## Step 4: Import workflows

Import all 4 workflows in this order:

1. `wf-rest-booking-error-handler.v1.json` (import first)
2. `wf-rest-booking-create.v1.json`
3. `wf-rest-booking-reminder.v1.json`
4. `wf-rest-booking-inbound.v1.json`

In n8n: **three dots menu (top right) > Import from File**

---

## Step 5: Configure each workflow

### For all workflows:
- Open the **CFG - Settings** node
- Fill in your restaurant name, phone number ID, template names, Sheet ID
- Select your Google Sheets credential in all Google Sheets nodes
- Select your WhatsApp credential in all WhatsApp nodes

### For Booking Create and Reminder:
- In Google Sheets nodes, select your document and "Reservations" sheet

### For Error Handler:
- In the Google Sheets node, select your document and "Errors" sheet
- Set all other workflows' **Error Workflow** to this one (in each workflow's Settings)

### For Inbound Reply Handler:
- Configure the Meta webhook URL in your Meta App Dashboard to point to:
  `https://your-n8n-url/webhook/whatsapp-inbound`

---

## Step 6: Test

1. **Activate** all 4 workflows
2. Send a test booking to the webhook:

```bash
curl -X POST https://your-n8n-url/webhook/restaurant-booking \
  -H "Content-Type: application/json" \
  -d '{
    "customer_name": "Test User",
    "phone": "+393401234567",
    "date": "2026-04-15",
    "time": "20:30",
    "covers": 2,
    "notes": "Test booking"
  }'
```

3. Check:
   - [ ] Reservation appears in Google Sheets
   - [ ] WhatsApp confirmation received on the test phone
   - [ ] Reply to the WhatsApp message and check status updates in the sheet
   - [ ] Wait for the reminder (or temporarily change the time window to test)

---

## Troubleshooting

| Problem | Solution |
|---------|----------|
| WhatsApp template rejected | Check that template category is "Utility" and content matches exactly |
| Reminder not sent | Verify timezone is "Europe/Rome" in workflow settings |
| Webhook returns 404 | Make sure the workflow is **active** (toggle on) |
| Google Sheets error | Re-authorize the Google Sheets credential |
| Wrong phone format | Phone must include country code (e.g., +393401234567) |

---

**Need help?** [Open an issue](https://github.com/radlabischia/n8n-local-business-pack/issues) or contact [RAD LAB](https://radlab.it).
