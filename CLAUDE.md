# Sko Logistik – KI-Team

Firmenwissen: `team/firmenprofil.md`. Agenten: `.claude/agents/`. Anleitung: `team/README.md`.

## Sko Büro (Live-Ansicht) – immer aktuell halten
Die Inhaberin verfolgt die Arbeit des Teams live im **Sko Büro**: https://claude.ai/artifact/4NWv3Ur1VSFp8RMChXZbeV
Schreibe dafür mit dem `ArtifactData`-Tool (url = obige Adresse) in die Datenbank:

- **Wenn ein Agent startet:** `agents/<id>` → `{status: "arbeitet", aufgabe: "<kurz, was er tut>", aktualisiert: <ISO-Zeit>}`
- **Wenn er fertig ist:** `agents/<id>` → `status: "frei"` (oder `"wartet"`, wenn eine Freigabe der Inhaberin nötig ist), und ein neues Dokument in `aktivitaet` → `{agent: "<id>", text: "<1 Satz Ergebnis>", zeit: <ISO-Zeit>}`
- **Braucht es eine Entscheidung:** neues Dokument in `entscheidungen` → `{agent, text, zeit, offen: true}`; erledigt → `offen: false`.
- Vor jedem Überschreiben das Dokument lesen und `if_version` mitgeben. Mehrere Writes als `batch`.
- `aktivitaet` klein halten: ältere Einträge als die neuesten 100 löschen.

Agent-IDs: `clara` (sekretaerin), `henrik` (berater), `lena` (kundenservice), `jonas` (kundengewinnung), `mara` (deal-closer), `sami` (instagram-marketing), `felix` (preis-scout).

Texte im Büro: kurz, Deutsch, keine Kundendaten außer Firmennamen, nichts über Angestellte.
