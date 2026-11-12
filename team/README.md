# Dein KI-Team für die Logistikfirma

| Agent | Name | Rolle |
|---|---|---|
| `kundenservice` | Lena | Kundenanfragen, Sendungsstatus, Meldungen aus der Warenkontrolle, Reklamationen |
| `kundengewinnung` | Jonas | Leads recherchieren, Erstansprache, Follow-ups |
| `deal-closer` | Mara | Angebote, Verhandlung, Einwände, Abschluss |
| `instagram-marketing` | Sami | Redaktionsplan, Posts/Reels, Captions, Community |
| `sekretaerin` | Clara | Hält dich über jeden Schritt auf dem Laufenden: Briefings, Logbuch, To-dos, Wiedervorlagen |
| `berater` | Dr. Henrik Brandt | Strategischer Berater: Preise, Wachstum, Personal, Prozesse, Risiken |
| `preis-scout` | Felix | Sammelt Konkurrenzpreise mit Quelle und vergleicht sie mit unseren |

Die Agenten liegen in `.claude/agents/` und stehen in Claude Code automatisch zur Verfügung.

## 1. Einrichten (einmalig)
Fülle **`team/firmenprofil.md`** aus. Ohne diese Infos arbeiten die Agenten mit Platzhaltern.

## 2. So beauftragst du dein Team
Schreib in Claude Code einfach, was du brauchst, z. B.:

- „**Kundenservice:** Beantworte diese E-Mail: …“
- „**Kundengewinnung:** Finde 15 Onlineshops in [Stadt], die Versandlogistik brauchen, und schreib Erstnachrichten.“
- „**Deal-Closer:** Bereite mein Gespräch morgen mit Firma X vor und schreib danach ein Angebot.“
- „**Instagram-Marketing:** Erstelle einen Redaktionsplan für Dezember mit 12 Posts.“
- „**Sekretärin:** Briefing – was gibt's Neues und was muss ich entscheiden?“
- „**Berater:** Sind meine Preise profitabel? Schaffen wir 24/7 mit 5 Leuten?“

Oder direkt per `@kundenservice`, `@deal-closer` usw.

## 3. Ablauf im Team
```
Instagram-Marketing ──Anfrage──┐
Kundengewinnung ──Lead──▶ Deal-Closer ──Neukunde──▶ Kundenservice
Kundenservice ──neue Anfrage──┘
```

## Ablage
- `team/leads.csv` – Leadliste (Kundengewinnung & Deal-Closer)
- `team/kunden/` – Notizen pro Kunde
- `team/instagram/` – Redaktionsplan & Posts
- `team/status/` – Logbuch, To-dos und Entscheidungen (Sekretärin & Berater)

## Wichtig
Die Agenten erstellen **Entwürfe**. Du prüfst und gibst frei, bevor etwas an Kunden geht oder veröffentlicht wird. Preise, Rabatte, Haftungsfragen und rechtliche Themen (DSGVO, Kaltakquise) entscheidest du.
