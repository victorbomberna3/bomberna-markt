# REQUIREMENTS

## Market tracker

### Captured per market day
| Field        | Required | Notes |
|--------------|----------|-------|
| Date         | yes      | Defaults to today. Weekday derived and shown (Wed vs Sat comparison). |
| Revenue (EUR)| yes      | Total takings for the day. |
| Staff count  | no       | Number of people working the stall. |
| Note         | no       | Free text: weather, "Pasen", "drukke dag", etc. |

### Outputs
- Running totals: number of market days, total revenue, average per day.
- Simple visual of revenue per day (Saturdays distinguished).
- CSV export.
- Email-the-overview stopgap (until durable storage is decided).
- **Wanted (pending Python layer):** revenue by weekday, by month, season view, Easter
  effect, year-over-year once enough data exists.

## Invoice request

### Captured per request
| Field               | Required | Notes |
|---------------------|----------|-------|
| Company name        | yes      | |
| Contact person      | no       | Name of the buyer. |
| Ondernemingsnummer  | yes      | Format hint `BE 0XXX.XXX.XXX`, no hard validation (must not block at the stall). |
| Address             | yes      | |
| Phone               | no       | |
| Email               | no       | Recommended: the invoice is usually emailed to the customer. |
| Order description   | yes      | What was sold. **Added: admin cannot invoice without this.** |
| Amount incl. btw    | yes      | **Added: admin cannot invoice without this.** |
| Remark              | no       | |

### Flow (current)
Fields are assembled into a structured Dutch email and sent to the administration office
via the device mail app (`mailto:`). Works offline: the mail queues and sends when signal
returns. Admin raises the formal invoice from this.

### Email format (current)
```
Onderwerp: Factuuraanvraag - <Bedrijfsnaam>

Nieuwe factuuraanvraag van de markt.

Bedrijfsnaam: ...
Contactpersoon: ...
Ondernemingsnummer: ...
Adres: ...
Telefoon: ...
E-mail: ...

Bestelling: ...
Bedrag incl. btw: EUR ...
Opmerking: ...
```

## Non-functional
- Offline capture for both functions.
- Mobile-first, fast entry, large tap targets.
- No em dashes in any copy.
- Dutch UI and email copy, formal `u` register.
