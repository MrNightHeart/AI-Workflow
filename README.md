# AI-Workflow
My visualisation how to use ai-agents in software-developer workflows of small teams.

## Codex-Entwickler-Agent

Der Entwickler-Agent kann GitHub-Issues mit der offiziellen OpenAI Codex Action umsetzen. Die Ausführung erfolgt geschützt in GitHub Actions; das Ergebnis ist ein Pull Request zur manuellen Prüfung.

➡️ **[Codex-Agent einrichten](CODEX-AGENT.md)**

## Abgrenzung Begriff
- Skills
- Tools
- Wissensbasis
- Agent

## AI Einsatzmöglichkeiten

- als Googleersatz (/)
- als Googleersatz mit Zugriff auf den Code (/)
- als Coding-Assistant, schreibt Code in Projekt (/)
- als Coding-Assistant mit Skills, plant - schreibt Code - testet Code - commitet - ... (/)
- als Agent, fester Bestandteil des Workflows - erledigt eigenständig Aufgaben einer definierte Rolle

## Mögliche Umsetzungen

### Einfacher Ansatz

## Mögliche Agents:

- Ticket-Refinement-Agent
- Architektur-/Impact-Agent
- PR-/Merge-Request-Agent
- Wissens-Agent

### Ticket-Refinement-Agent
Vor dem IMP läuft ein Agent über neue Jira-Tickets.

Er prüft beispielsweise:
Sind Akzeptanzkriterien vorhanden?
Gibt es widersprüchliche Anforderungen?
Welche Services/Repos sind vermutlich betroffen?
Fehlen technische Details?
Gibt es ähnliche frühere Tickets?

Ausgabe als Jira-Kommentar

### Architektur-/Impact-Agent

Beim Erstellen eines Tickets:

"Welche Komponenten wären vermutlich betroffen?"

Der Agent analysiert das Repository und erstellt z.B.:

Frontend
User-Service
Notification-Service
Datenbankmigration notwendig

Nutzen: bessere Aufwandsschätzungen.

### PR-/Merge-Request-Agent

Sobald ein MR erstellt wird:

Agent analysiert:

Diff
Ticketbeschreibung
betroffene Tests
Sonarqube-Ergebnisse

Er erzeugt:

Zusammenfassung des MRs
potenzielle Bugs
fehlende Tests
Security-Probleme
Breaking Changes

Beispiel:

Ticket fordert Validierung von E-Mail-Adressen.

Implementierung prüft nur beim Anlegen, nicht beim Update.

Möglicherweise fehlt Testfall.

Damit konzentrieren sich menschliche Reviewer auf die wichtigen Stellen.

### Wissens-Agent

Über Jira, GitHub, Confluence und Codebase.

Entwickler können fragen:

"Wie funktioniert die Berechtigungsprüfung?"

oder

"Wo wurde OAuth zuletzt angepasst?"

Der Agent durchsucht:

Code
Pull Requests
Jira
Dokumentation

und liefert eine Antwort mit Quellen.

Gerade bei 6 Entwicklern kann das viel Kontextverlust verhindern.

### Entwickler-Agent
Ablauf:

Ticket lesen
Implementierung erzeugen
Tests erzeugen
Branch anlegen
Commit erstellen
Pull Request erstellen

Der Entwickler wird dann eher zum Reviewer.

Das funktioniert heute erstaunlich gut bei:

CRUD-Funktionen
API-Endpunkten
Standardformularen
Datenbankmigrationen

Aber deutlich schlechter bei:

komplexer Geschäftslogik
Architekturentscheidungen
Legacy-Code

Eher für ausgewählte Tickettypen einsetzen.

