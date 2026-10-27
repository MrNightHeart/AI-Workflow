# Vision: Ticketzentriertes Agent-Team

## 1. Ziel

Dieses Projekt dient als Referenz und Experimentierplattform für ein Agent-Team, das private Projekte unterstützt. Die Agents sollen Aufgaben nicht nur beantworten, sondern innerhalb eines nachvollziehbaren Arbeitsprozesses planen, umsetzen, prüfen, dokumentieren und – nach Freigabe – ausführen.

Die Architektur soll zwei Arten von Vorhaben unterstützen:

1. **Digitales Büro und Homeserver:** Software, Automatisierung, Infrastruktur, Deployment und Wartung.
2. **Digitalisierung der Vereinsarbeit:** Aufbereitung von Unterlagen, Planung von Abläufen, kontrollierte Umsetzung und laufende Prüfung.

Der Mensch bleibt Auftraggeber, fachliche Entscheidungsinstanz und Freigeber risikoreicher Aktionen.

## 2. Leitprinzipien

### Ticket-first

Jede relevante Arbeit beginnt mit einem Ticket. Das Ticket enthält mindestens Ziel, Kontext, Akzeptanzkriterien, Risiken, Freigabestatus und Links zu Ergebnissen. Informelle Agent-Kommunikation darf keine nicht dokumentierte Arbeit auslösen.

### Orchestrator statt unkontrolliertem Schwarm

Agents beauftragen sich nicht beliebig gegenseitig. Ein zentraler Orchestrator reagiert auf Ereignisse und entscheidet anhand fester Regeln:

- Ist das Ticket vollständig und genehmigt?
- Welche Rolle ist zuständig?
- Welche Werkzeuge und Daten darf sie verwenden?
- Ist eine menschliche Freigabe erforderlich?
- Darf die Aktion jetzt stattfinden?
- Wie wird ein Fehler oder Abbruch behandelt?

### Human-in-the-loop

Menschliche Freigaben bilden explizite Gates. Besonders Merge, produktives Deployment, Migration, Datenänderung, externe Kommunikation und rechtlich oder fachlich relevante Vereinsaktionen dürfen nicht allein aus einem Agentenvorschlag folgen.

### Trennung von Ereignis und Ergebnis

- **Issues und Workflow-Ereignisse** dokumentieren den Weg: Vorschlag, Entscheidung, Übergabe, Test, Fehler, Ausführung und Verifikation.
- **Repository-Dokumente und Artefakte** dokumentieren das Ergebnis: Code, Tests, README, Architekturentscheidungen, Benutzeranleitungen und Runbooks.

### Least Privilege

Jede Agent-Rolle erhält nur die minimal erforderlichen Lese-, Schreib- und Ausführungsrechte. Vorschlagen, Genehmigen, Umsetzen und produktiv Ausführen sind getrennte Fähigkeiten.

## 3. Zielarchitektur

```text
Mensch / Projektverantwortlicher
              │
              ▼
 GitHub Issues + Projects + Pull Requests
              │  Webhooks / Zustandsänderungen
              ▼
       Workflow-Orchestrator
       ├─ Zustandsautomat
       ├─ Policy- und Freigabeprüfung
       ├─ Job Queue / Sperren
       ├─ Agent Registry
       └─ Audit Log
              │
     ┌────────┼─────────┬───────────┬────────────┐
     ▼        ▼         ▼           ▼            ▼
 PM-Agent  Umsetzung  Qualität  Deployment   Inspection
              │                     │            │
              ▼                     ▼            ▼
     Git/isolierte Tests      Zielsysteme     Monitoring
```

### GitHub als erste Steuerungsebene

In der ersten Ausbaustufe übernimmt GitHub mehrere Aufgaben:

- **Issues:** Anforderungen, Vorschläge, Bugs und Ereignisdokumentation
- **Projects:** Status, Priorität, Zuständigkeit und Freigabephase
- **Pull Requests:** prüfbare Änderungen und fachlich-technische Abnahme
- **Repository:** Ergebnisdokumentation und versionierte Artefakte
- **Actions:** kontrollierte Ausführung einzelner Automatisierungen

Die Architektur soll GitHub jedoch über einen Adapter anbinden. Dadurch kann für Vereinsarbeit später ein separates Ticketsystem verwendet werden, ohne Rollen und Prozessmodell neu zu entwerfen.

## 4. Rollenmodell

### PM-Agent

**Aufgaben:**

- Vision und Unterlagen analysieren
- Annahmen und offene Fragen ausweisen
- Epics, Features und Tickets vorschlagen
- Akzeptanzkriterien, Abhängigkeiten und Risiken formulieren
- erforderliche Dokumentation bestimmen

**Grenze:** Darf eigene Vorschläge nicht genehmigen.

### Umsetzungs-/Entwickler-Agent

**Aufgaben:**

- nur genehmigte Tickets bearbeiten
- isolierten Branch und Arbeitsbereich verwenden
- Implementierung beziehungsweise Umsetzung erstellen
- Tests durchführen und Ergebnisse dokumentieren
- Ergebnisdokumentation aktualisieren
- Pull Request oder prüfbaren Umsetzungsplan vorlegen

**Grenze:** Kein direkter Push auf geschützte Hauptbranches und keine eigene Endabnahme.

### Review-/Qualitäts-Agent

**Aufgaben:**

- Erfüllung der Akzeptanzkriterien prüfen
- Tests, Dokumentation, Sicherheit und Datenschutz bewerten
- Abweichungen nachvollziehbar im Ticket oder Review dokumentieren

**Grenze:** Die fachliche Endabnahme verbleibt zunächst beim Menschen.

### Deployment-/Migrations-Agent

**Aufgaben:**

- Deployment-, Backup- und Rollbackplan prüfen
- Wartungsfenster abwarten
- ausschließlich das freigegebene Artefakt ausrollen
- Migrationen und Health Checks ausführen
- Version, Zeiten, Ergebnis und Abweichungen protokollieren

**Grenze:** Keine produktive Ausführung ohne explizite Freigabe.

### Inspection-/Wartungs-Agent

**Aufgaben:**

- Monitoring, Logs, Tests und Dokumentationsstand prüfen
- Fehler reproduzieren und bewerten
- Duplikate vermeiden
- Bugtickets mit Nachweisen und Schweregrad erstellen

**Grenze:** Behebt produktive Fehler nicht eigenmächtig, sondern startet den regulären Ticketprozess.

### Vereins-Ausführungs-Agent

**Aufgaben:**

- Unterlagen strukturiert aufbereiten
- Checklisten, Vorlagen und Ausführungspläne erzeugen
- ausdrücklich freigegebene Verwaltungsschritte durchführen
- Ausführungsnachweise dokumentieren

**Grenze:** Externe Kommunikation, personenbezogene Datenänderungen und rechtlich relevante Erklärungen benötigen eigene Policies und Freigaben.

## 5. Use Case: Digitales Büro und Homeserver

```text
Vision
→ PM-Ticketvorschläge
→ fachliche Genehmigung oder Ablehnung
→ Umsetzung auf Branch
→ Tests und Dokumentation
→ unabhängiges Review
→ menschliche PR-Abnahme
→ Deploymentfreigabe
→ Warten auf Wartungsfenster
→ Deployment/Migration
→ Health Check und Abschluss
→ fortlaufende Inspection
```

Der Deployment-Agent darf nur den geprüften Commit beziehungsweise das freigegebene Release ausrollen. Vor produktiven Änderungen müssen Backup, Rollback und Erfolgskriterien feststehen.

## 6. Use Case: Digitalisierung der Vereinsarbeit

```text
Unterlagen und Ziel
→ PM-Prozess- und Ticketvorschläge
→ fachliche Genehmigung oder Ablehnung
→ Vorbereitung der Umsetzung
→ Tests/Plausibilitätsprüfung und Dokumentation
→ Abnahme des Ausführungsplans
→ separate Ausführungsfreigabe
→ kontrollierte Durchführung
→ Ergebniskontrolle
→ fortlaufende Inspection
```

Planfreigabe und Ausführungsfreigabe sind absichtlich getrennt. Sensible Originalunterlagen und personenbezogene Daten sollen nicht unkontrolliert in Issues oder Prompts kopiert werden.

## 7. Zustandsmodelle

### Software und Server

```text
Idee
→ Vorgeschlagen
→ Zur fachlichen Freigabe
→ Genehmigt
→ In Umsetzung
→ Im technischen Review
→ Zur Abnahme
→ Für Deployment freigegeben
→ Wartet auf Wartungsfenster
→ Ausgerollt
→ Verifiziert
→ Abgeschlossen
```

### Vereinsprozesse

```text
Anforderung
→ Prozessvorschlag
→ Zur Freigabe
→ Genehmigt
→ Vorbereitung
→ Zur Ausführungsfreigabe
→ Ausführung
→ Kontrolle
→ Dokumentiert
→ Abgeschlossen
```

Für beide Modelle existieren Querschnittszustände wie `Rückfrage`, `Blockiert`, `Abgelehnt`, `Fehlgeschlagen` und `Rollback erforderlich`.

## 8. Ticketvertrag

Ein Ticket soll mindestens folgende Informationen tragen:

- Problem und gewünschtes Ergebnis
- Kontext und Nicht-Ziele
- prüfbare Akzeptanzkriterien
- Projekt, Typ, Priorität und Risikostufe
- Abhängigkeiten
- verantwortliche Rolle
- benötigte Freigaben
- erwartete Dokumentation
- Links zu Branch, Pull Request, Artefakt und Folgetickets

Jede Agent-Übergabe ergänzt strukturiert:

- ausgeführte Schritte
- Ergebnis und Nachweise
- Tests beziehungsweise Kontrollen
- bekannte Einschränkungen
- Risiken und offene Fragen
- vorgeschlagenen nächsten Status

## 9. Freigabe- und Risikomodell

| Risiko | Beispiele | Regel |
|---|---|---|
| Niedrig | Analyse, Ticket- oder Dokumentationsentwurf | Agent darf Vorschlag erstellen |
| Mittel | Änderung auf isoliertem Branch | PR und Prüfung erforderlich |
| Hoch | Deployment, Migration, personenbezogene Datenänderung | explizite Ausführungsfreigabe |
| Kritisch | Datenlöschung, rechtliche Erklärung, Zahlung | mehrfach bestätigen oder manuell ausführen |

Eine Freigabe ist ein eigenes Audit-Ereignis mit freigebender Identität, Zeitpunkt, Umfang und exakt freigegebenem Artefakt. Ein Label kann in frühen Experimenten als bewusster Trigger dienen, ist langfristig aber durch eine robustere Policy-Prüfung zu ergänzen.

## 10. Sicherheits- und Datenschutzanforderungen

- getrennte Identitäten und Berechtigungen pro Rolle
- geschützte Hauptbranches und verpflichtende Pull Requests
- Secrets nur in einem Secret Manager
- isolierte Entwicklungs- und Testumgebungen
- kurzlebige produktive Berechtigungen
- Whitelist erlaubter Werkzeuge und Zielsysteme
- keine unnötigen personenbezogenen Daten in Tickets, Logs oder Prompts
- unveränderbares Audit Log für Entscheidungen und Ausführungen
- definierte Aufbewahrungs- und Löschregeln
- Backups und regelmäßig geprüfte Wiederherstellung
- Schutz vor Prompt Injection durch nicht vertrauenswürdige Issue- und Dokumentinhalte

## 11. Einführung in Stufen

### Stufe 1 – Assistiertes Arbeiten

- GitHub Issues, Projects und Pull Requests verwenden
- PM-Agent erstellt nur Vorschläge
- Umsetzungs-Agent erstellt Branch und Pull Request
- sämtliche Freigaben und Deployments bleiben manuell
- Ticket- und Dokumentationsvorlagen standardisieren

### Stufe 2 – Kontrollierte Orchestrierung

- Webhooks und persistenten Orchestrator einführen
- Agents anhand genehmigter Zustände starten
- strukturierte Übergaben und Audit Log etablieren
- Tests sowie Dokumentationsprüfungen automatisieren

### Stufe 3 – Geregelte Ausführung

- Deployment- und Vereins-Ausführungs-Agent anbinden
- Wartungsfenster, Backups und Rollbackregeln hinterlegen
- kurzlebige Berechtigungen und separate Ausführungsfreigaben nutzen

### Stufe 4 – Proaktive Qualität

- Inspection-Agent für Monitoring und regelmäßige Prüfungen aktivieren
- deduplizierte Bugticket-Erstellung einführen
- Dokumentation, Abhängigkeiten, Backups und Sicherheitsregeln regelmäßig kontrollieren

## 12. Nicht-Ziele der ersten Ausbaustufe

- vollständig autonome Produktivänderungen
- freie Agent-zu-Agent-Delegation ohne Ticket und Policy-Prüfung
- ein globales, unkontrolliertes Agentengedächtnis
- Speicherung sensibler Vereinsunterlagen direkt in öffentlichen oder ungeeigneten Repositories
- gleichzeitige Automatisierung aller Rollen

## 13. Nächster strategischer Schritt

Als erstes werden PM-, Umsetzungs- und Review-Rolle mit eindeutigen Tickettypen, Zuständen, Übergabeverträgen und menschlichen Gates modelliert. Deployment, Migration und proaktive Wartung folgen erst, wenn Freigaben, Auditierung, Fehlerbehandlung und Rollback zuverlässig funktionieren.
