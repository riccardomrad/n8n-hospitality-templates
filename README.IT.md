<p align="center">
  <img src="docs/images/booking-flow.png" width="900"
       alt="Il flusso: il cliente scrive su WhatsApp, n8n controlla e salva la prenotazione, parte la conferma, il promemoria esce 24 ore prima, la risposta del cliente aggiorna la tabella, e ogni errore avvisa il titolare">
</p>

<h1 align="center">n8n Local Business Automation Kit</h1>

<p align="center">
  Workflow n8n pronti da importare che fanno rispondere WhatsApp al posto del ristorante:<br>
  prenotazioni, conferme, promemoria, e un gestore di errori che non fallisce mai in silenzio.
</p>

<p align="center">
  <a href="https://n8n.io"><img src="https://img.shields.io/badge/-n8n%20%E2%89%A5%201.50-1B3A5C?style=flat&colorA=1B3A5C" alt="n8n 1.50 o superiore"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/-Apache%202.0-1B3A5C?style=flat&colorA=1B3A5C" alt="Licenza Apache 2.0"></a>
  <a href="CONTRIBUTING.md"><img src="https://img.shields.io/badge/-PRs%20welcome-1B3A5C?style=flat&colorA=1B3A5C" alt="PR benvenute"></a>
  <a href="https://radlab.it"><img src="https://img.shields.io/badge/-Made%20in%20Italy%20%F0%9F%87%AE%F0%9F%87%B9-1B3A5C?style=flat&colorA=1B3A5C" alt="Made in Italy"></a>
</p>

<p align="center">
  <a href="#provalo-in-5-minuti">Come partire</a> |
  <a href="docs/guides/setup-restaurant-booking.md">Guida di installazione</a> |
  <a href="#disponibili-adesso-prenotazioni-ristorante">Workflow</a> |
  <a href="README.md">English 🇬🇧</a>
</p>

---

## Come funziona

<!-- TODO: Aggiungere GIF demo di un workflow in azione -->

Ogni workflow risolve un problema reale per le attivita locali:

1. **Il cliente scrive su WhatsApp** (o prenota online)
2. **n8n elabora la richiesta** (crea prenotazione, aggiorna calendario, salva i dati)
3. **Follow-up automatico** (conferma, promemoria 24h prima, richiesta recensione dopo la visita)

Nessun codice richiesto. Importa il JSON, configura le credenziali e sei operativo.

---

## Provalo in 5 minuti

1. Installa [n8n](https://docs.n8n.io/hosting/) (cloud o self-hosted)
2. Scarica un file `.json` dalla cartella [`workflows/`](workflows/)
3. In n8n vai su **Workflows > Import from File** e carica il file
4. Configura le credenziali necessarie (WhatsApp, Google Calendar, ecc.)
5. Clicca **Execute Workflow** e testa con dati di esempio

> Vuoi un'istanza demo gia pronta? [Apri una issue](../../issues/new) e ti aiutiamo a partire.

---

## Disponibili adesso: prenotazioni ristorante

Quattro workflow che lavorano insieme come un unico sistema di prenotazione. Ognuno ha la sua pagina in [`docs/workflows/restaurants/`](docs/workflows/restaurants/).

| Workflow | File | Cosa fa |
|----------|------|---------|
| Create & Confirm | [`wf-rest-booking-create.v1.json`](workflows/restaurants/reservations/wf-rest-booking-create.v1.json) | Riceve la richiesta da un webhook, la valida, salva la prenotazione e manda la conferma su WhatsApp |
| Inbound Reply Handler | [`wf-rest-booking-inbound.v1.json`](workflows/restaurants/reservations/wf-rest-booking-inbound.v1.json) | Legge la risposta del cliente, segna la prenotazione come confermata o annullata, e mette da parte per un umano quello che non riesce a interpretare |
| Reminder 24h | [`wf-rest-booking-reminder.v1.json`](workflows/restaurants/reservations/wf-rest-booking-reminder.v1.json) | Gira ogni 15 minuti, manda il promemoria alle prenotazioni di domani e le segna come avvisate |
| Error Handler | [`wf-rest-booking-error-handler.v1.json`](workflows/restaurants/reservations/wf-rest-booking-error-handler.v1.json) | Intercetta gli errori degli altri tre, li registra e avvisa il titolare invece di fallire in silenzio |

**Risultati tipici:** meno telefonate perse, meno no-show.

---

## Cosa arriva dopo

Non ancora pubblicati. Girano in produzione per i clienti e vengono rilasciati qui quando diventano abbastanza generici da servire anche a qualcun altro.

- **Ristoranti:** recupero no-show, richiesta recensione Google, report settimanale
- **Hotel e B&B:** welcome pre-soggiorno, promemoria prenotazione, recensione post-soggiorno, campagna win-back
- **Saloni e centri estetici:** promemoria appuntamento, follow-up no-show, nudge riprenotazione
- **Studi medici:** promemoria appuntamento, richiamo check-up annuale, feedback post-visita

Te ne serve uno prima degli altri? [Apri una issue](../../issues/new) e dimmi quale, mi aiuta a scegliere l'ordine.

---

## Struttura del repository

```
workflows/
  restaurants/
    reservations/    # i 4 workflow di prenotazione qui sopra
docs/
  workflows/
    restaurants/     # un .md per workflow
  guides/            # guide generali (setup self-hosted, credenziali)
demo/                # Docker Compose per test in locale
.github/             # CI, template issue, template PR
```

---

## Compatibilita

- **Versione n8n:** >= 1.50.0 (testato fino all'ultima versione)
- **Canali:** WhatsApp Business API, Telegram, Email, SMS
- **Integrazioni:** Google Calendar, Google Sheets, webhook CRM
- **Hosting:** Funziona su n8n Cloud e self-hosted (Docker)

---

## Per le attivita italiane

Questi workflow nascono da progetti di automazione reali per ristoranti, hotel, saloni e studi medici in **Campania** (Ischia, Procida, Napoli).

Tutti i template dei messaggi WhatsApp sono disponibili in **italiano** nei file JSON dei workflow. La documentazione include guide in italiano nella cartella [`docs/`](docs/).

Se hai un'attivita locale in Italia e vuoi questi workflow personalizzati per te:

- **Setup** su n8n (cloud o server dedicato)
- **Integrazione** con i tuoi strumenti esistenti (PMS, gestionali, CRM)
- **Workflow personalizzati** su misura per le tue esigenze

Contattaci: [RAD LAB](https://radlab.it) -- automatizziamo le attivita locali per farti concentrare sui tuoi clienti.

---

## Contribuire

Le contribuzioni sono benvenute! Che sia un nuovo workflow, un bugfix o documentazione migliore.

Leggi [CONTRIBUTING.md](CONTRIBUTING.md) per le linee guida.

---

## Licenza

Questo progetto e rilasciato sotto [Apache License 2.0](LICENSE).

Puoi usare liberamente questi workflow anche in contesti commerciali, a condizione di:
- Mantenere chiaro riferimento a **RAD LAB** come autore originario
- Non rivenderli cosi come sono come prodotto proprietario chiuso senza modifiche sostanziali

Per domande su licenze commerciali: [riccardo@radlab.it](mailto:riccardo@radlab.it)

---

Fatto con dedizione da [RAD LAB](https://radlab.it) -- Automazione digitale per attivita locali.
