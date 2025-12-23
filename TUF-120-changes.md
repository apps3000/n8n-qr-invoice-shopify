# TUF-120: Optimierung des Mailversand-Nodes

## Änderungen

### TUF-121: Mail-Inhalt basierend auf Customer Locale
- Locale-Erkennung über `order.customer.locale` oder `order.customer_locale`
- Wenn Locale mit "de" beginnt → Deutsche Texte
- Sonst → Englische Texte

### TUF-122: Deutsche Mail in "Du"-Form
- "Guten Tag" → "Hallo [Vorname]"
- "Ihre Bestellung" → "deine Bestellung"
- "vielen Dank für Ihre" → "Vielen Dank für deine"
- "Sie uns" → "du uns"
- "Liebe Grüsse, Jenni und das Tuftinglove-Team"

### TUF-123: Hinweis auf Fälligkeit nur bei Rechnungskauf
- `showDueDate` Flag basierend auf `_isInvoiceOrder`
- Fälligkeitsdatum und Zahlungshinweis werden nur angezeigt wenn `isInvoiceOrder === true`

### TUF-124: Formatierung der Mailvorlage
- Logo: `https://www.tuftinglove.com/cdn/shop/files/logo_schrift.png?v=1677444262&width=200`
- Haupthintergrund: #FFFFFF
- Content-Bereich: #FFF0E5 mit border-radius: 16px
- Buttons: #7E97FF mit weisser Schrift und border-radius: 9999px
- Button-Styling: padding: 0 1.25rem, min-height: 2.25rem, font-weight: 700

## Geänderte Nodes

### Prepare Email Data (id: 20fdce6c-695d-4ede-acc9-649b271eba7d)
- Locale-Erkennung hinzugefügt
- Sprachspezifische Email-Inhalte (DE/EN) mit `emailContent` Objekt
- `showDueDate` Flag für bedingte Fälligkeit
- Alle Texte in Du-Form für Deutsche Version

### Send Invoice Email (id: 9b260bee-865a-48a5-9d9c-f368f00cdf08)
- Neues HTML-Template mit responsivem Table-Layout
- Tuftinglove Logo im Header
- Neue Farbpalette (#FFF0E5, #7E97FF)
- Dynamischer Inhalt aus `_email.content`
- Bedingter Fälligkeitshinweis über `{{ $json._email.showDueDate ? ... : '' }}`

## Workflow
- ID: EtqPDBEYAI6Lh90a
- Name: QR-Rechnung
- URL: https://n8n.apps3k.com/workflow/EtqPDBEYAI6Lh90a
