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

## WICHTIG: Ergebnisse im Büro speichern (nicht nur auf GitHub)
Geplante Aufgaben können **nicht nach GitHub pushen** (403 – das ist bekannt und kein Fehler deinerseits). Damit nichts verloren geht:
- Speichere **jedes Ergebnis** (Leads, Entwürfe, Posts, Berichte, Briefings) als Dokument im Sko Büro: Collection `dokumente`, `doc_id` = `<agent>-<YYYY-MM-DD>-<kurzes-thema>`, Inhalt `{agent, titel, inhalt, zeit}` – `inhalt` ist der komplette Text als Markdown (max. ca. 100 KB).
- Neue Leads zusätzlich in Collection `leads` (`doc_id` = Firmenname in Kleinbuchstaben mit Bindestrichen) mit den Feldern aus `team/leads.csv`.
- Danach Push versuchen; scheitert er, einfach weitermachen (nicht erneut versuchen).
- Vor dem Arbeiten auch `dokumente` und `leads` im Büro lesen – dort steht der aktuelle Stand, der evtl. noch nicht auf GitHub ist.

### Aufträge aus dem Büro
Die Inhaberin kann Agenten im Büro Aufträge geben. Sie liegen in der Collection `auftraege` als `{agent, text, zeit, offen: true}`.
- **Zu Beginn jedes Laufs:** offene Aufträge für die eigene Agent-ID lesen (`query` mit `agent == <id>` und `offen == true`) und **zuerst** erledigen – im Rahmen der eigenen Rolle und Regeln (nur Entwürfe, nichts versenden).
- Danach den Auftrag auf `offen: false` setzen, `erledigt: <ISO-Zeit>` und `ergebnis: "<1 Satz>"` ergänzen, und das Ergebnis zusätzlich in `aktivitaet` eintragen.
- Gesprächsverläufe stehen in `chats/<id>` (Feld `messages`) – nur lesen, nicht ändern.

### Freigaben aus dem Büro (Knöpfe „Freigeben / Ändern / Ablehnen“)
Die Inhaberin entscheidet direkt im Büro. Erledigte Entscheidungen haben `offen: false` und `status`:
- `freigegeben` → sofort umsetzen (im Rahmen der Regeln), danach `umgesetzt: <ISO-Zeit>` am Dokument ergänzen und Ergebnis in `aktivitaet`.
- `aendern` → `kommentar` lesen, Entwurf überarbeiten, als **neue** offene Entscheidung wieder vorlegen.
- `abgelehnt` → nicht umsetzen, kurz in `aktivitaet` vermerken, ggf. Alternative als neue Entscheidung.
Nur Entscheidungen ohne `umgesetzt` bearbeiten. Besprechungen liegen in `besprechungen` (Thema, Beiträge, Fazit) – Vorschläge daraus kommen als normale Entscheidungen.

### Kunden gewinnen – so weit wie möglich automatisch
- **Inbound zuerst:** Wer sich selbst meldet (Mail an info@, Instagram, Website-Formular), darf vollständig automatisch betreut werden: Lena antwortet, Mara schickt das Angebot und fasst nach (max. 3 Nachrichten, Abstand 3–4 Tage), sobald die Gmail-Verbindung besteht. Ohne Gmail: fertige Texte als Entscheidung „Senden?“ vorlegen.
- **Outbound:** Jonas recherchiert und schreibt die Erstansprache für Kontaktformular/Instagram-DM/Telefon. Keine Kalt-E-Mails. Die Inhaberin gibt im Büro frei und schickt mit „Text kopieren“ ab; danach Lead-Status `kontaktiert` und `naechster_schritt` setzen.
- **Reichweite:** Sami postet täglich; Henrik schlägt einmal pro Woche eine konkrete Wachstumsmaßnahme vor (z. B. Google-Unternehmensprofil, Fulfillment-Verzeichnisse, Kooperationen mit Shop-Agenturen).

Agent-IDs: `clara` (sekretaerin), `henrik` (berater), `lena` (kundenservice), `jonas` (kundengewinnung), `mara` (deal-closer), `sami` (instagram-marketing), `felix` (preis-scout).

Texte im Büro: kurz, Deutsch, keine Kundendaten außer Firmennamen, nichts über Angestellte.
