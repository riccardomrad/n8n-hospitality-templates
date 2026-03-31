# n8n Local Business Automation Kit

Workflow n8n pronti all'uso per automatizzare **ristoranti, hotel, saloni e studi medici**: prenotazioni, promemoria WhatsApp, follow-up recensioni, campagne marketing e molto altro.

[![Made with n8n](https://img.shields.io/badge/made%20with-n8n-EA4B71)](https://n8n.io)
[![License: Apache 2.0](https://img.shields.io/badge/license-Apache%202.0-blue)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen)](CONTRIBUTING.md)

> **Read this in:** [English](README.md)

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

## Casi d'uso

- [Ristoranti](#-ristoranti)
- [Hotel e B\&B](#-hotel-e-bb)
- [Saloni e centri estetici](#-saloni-e-centri-estetici)
- [Studi medici](#-studi-medici)

---

### Ristoranti

| Workflow | Descrizione | Cartella |
|----------|-------------|----------|
| Conferma prenotazione WhatsApp | Conferma automatica della prenotazione via WhatsApp | `workflows/restaurants/reservations/` |
| Recupero no-show | Tagga i clienti no-show e invia messaggio di recupero | `workflows/restaurants/reservations/` |
| Richiesta recensione Google | Chiede una recensione 2h dopo il servizio cena | `workflows/restaurants/marketing/` |
| Report settimanale | Riepilogo prenotazioni, no-show e recensioni | `workflows/restaurants/operations/` |

**Risultati tipici:** meno telefonate perse, meno no-show, piu recensioni su Google.

---

### Hotel e B&B

| Workflow | Descrizione | Cartella |
|----------|-------------|----------|
| Welcome pre-soggiorno | Messaggio WhatsApp con info check-in, parcheggio, upsell | `workflows/hotels/booking/` |
| Promemoria prenotazione | Conferma + reminder 24h prima dell'arrivo | `workflows/hotels/booking/` |
| Recensione post-soggiorno | Richiesta recensione Google/Booking dopo il checkout | `workflows/hotels/marketing/` |
| Campagna win-back | Messaggio agli ex ospiti dopo 30/180 giorni | `workflows/hotels/marketing/` |

**Risultati tipici:** esperienza ospite migliore, piu prenotazioni dirette, punteggi recensioni piu alti.

---

### Saloni e centri estetici

| Workflow | Descrizione | Cartella |
|----------|-------------|----------|
| Promemoria appuntamento | Reminder WhatsApp 24h prima con pulsanti conferma/cancella | `workflows/salons/appointments/` |
| Follow-up no-show | Re-engagement automatico dopo un appuntamento mancato | `workflows/salons/appointments/` |
| Nudge riprenotazione | "E ora di un nuovo taglio?" dopo X settimane | `workflows/salons/marketing/` |

**Risultati tipici:** meno no-show, tasso di riprenotazione piu alto.

---

### Studi medici

| Workflow | Descrizione | Cartella |
|----------|-------------|----------|
| Promemoria appuntamento | Reminder multi-canale (WhatsApp + SMS fallback) | `workflows/clinics/appointments/` |
| Richiamo check-up annuale | Promemoria annuale per visite di controllo | `workflows/clinics/appointments/` |
| Feedback post-visita | Sondaggio di soddisfazione rapido dopo la visita | `workflows/clinics/marketing/` |

**Risultati tipici:** meno appuntamenti saltati, migliore fidelizzazione pazienti.

---

## Struttura del repository

```
workflows/           # File JSON dei workflow n8n, organizzati per settore
  restaurants/       #   prenotazioni, marketing, operazioni
  hotels/            #   booking, marketing, operazioni
  salons/            #   appuntamenti, marketing
  clinics/           #   appuntamenti, marketing
  _shared-snippets/  #   sub-flow riutilizzabili (normalizzazione telefono, ecc.)
docs/                # Documentazione per ogni workflow + guide setup
  workflows/         #   un .md per workflow (specchia la struttura workflows/)
  guides/            #   guide generali (setup self-hosted, credenziali, ecc.)
  images/            #   screenshot e diagrammi
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

Per domande su licenze commerciali: [hello@radlab.it](mailto:hello@radlab.it)

---

Fatto con dedizione da [RAD LAB](https://radlab.it) -- Automazione digitale per attivita locali.
