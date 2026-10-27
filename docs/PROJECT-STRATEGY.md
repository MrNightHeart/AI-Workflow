# Projektstrategie: AgentTeam, Server und Verein

## 1. Projektportfolio

Das Vorhaben besteht aus eigenständigen, miteinander verbundenen Projekten. Jedes Projekt besitzt einen eigenen Zweck, ein eigenes Backlog, eigene Ergebnisse und eigene Sicherheitsgrenzen.

### AgentTeam-Projekt

Das AgentTeam-Projekt entwickelt die organisatorischen und technischen Fähigkeiten des Agenten-Teams:

- Rollen und Verantwortlichkeiten
- Ticket- und Übergabeverträge
- Workflows und Freigabegates
- Orchestrierung und Agentenausführung
- Sicherheits- und Berechtigungsmodell
- Auditierung, Qualität und Betriebsfähigkeit

Das Agent-Team wird damit selbst wie ein Produkt behandelt. Änderungen erfolgen über Tickets, werden getestet und dokumentiert und durchlaufen dieselben kontrollierten Freigaben, die das Projekt für andere Vorhaben bereitstellen soll.

### Serverprojekt

Das Serverprojekt entwickelt das digitale Büro und die eigene Serverplattform:

- Dienste und Automatisierungen
- Infrastruktur und Konfiguration
- Deployment und Migration
- Monitoring, Wartung und Wiederherstellung
- technische Dokumentation und Runbooks

Es ist der erste produktive Anwendungsfall für das AgentTeam-Projekt.

### Vereinsprojekt

Das Vereinsprojekt verfolgt langfristig die Digitalisierung von Vereinsprozessen. Es ist fachlich eigenständig und hat erhöhte Anforderungen an Privatsphäre, Datenschutz, Zugriffskontrolle und selbstgehostete Verarbeitung.

Das Projekt wird zunächst bewusst zurückgestellt. Es startet operativ erst, wenn geeignete selbstgehostete Lösungen, sichere Datenräume und hinreichend erprobte Agenten- und Freigabeprozesse verfügbar sind.

## 2. Gemeinsame iterative Entwicklung

AgentTeam und Serverprojekt werden in einer kontrollierten Rückkopplungsschleife aufgebaut:

```text
1. Im Serverprojekt entsteht eine konkrete Anforderung.
2. Das vorhandene AgentTeam unterstützt Planung oder Umsetzung.
3. Grenzen, Risiken und fehlende Fähigkeiten werden sichtbar.
4. Daraus entstehen verknüpfte Tickets im AgentTeam-Projekt.
5. Die AgentTeam-Fähigkeit wird entwickelt, getestet und freigegeben.
6. Das Serverprojekt nutzt die verbesserte Fähigkeit.
7. Betriebserfahrungen fließen in beide Backlogs zurück.
```

Diese Vorgehensweise verhindert, dass das Agent-Team losgelöst von realen Anforderungen überdimensioniert wird. Gleichzeitig verhindert die Trennung der Projekte, dass Experimente am Agent-Team unkontrolliert zu Änderungen am Server führen.

## 3. Verhältnis der Projekte

```text
┌────────────────────────┐
│ AgentTeam-Projekt      │
│ entwickelt Fähigkeiten │
└───────────┬────────────┘
            │ stellt kontrollierte Fähigkeiten bereit
            ▼
┌────────────────────────┐
│ Serverprojekt          │
│ erster realer Use Case │
└───────────┬────────────┘
            │ liefert Anforderungen und Erfahrungen
            └──────────────────────────► AgentTeam-Backlog

┌────────────────────────┐
│ Vereinsprojekt         │
│ vorerst zurückgestellt │
└────────────────────────┘
            ▲
            │ startet nach Privacy-/Self-Hosting-Reife
            └── spätere Nutzung freigegebener Fähigkeiten
```

## 4. Ticket- und Dokumentationsgrenzen

Tickets werden in dem Projekt geführt, dessen Ergebnis verändert wird:

- Neue Agentenrolle oder Workflow-Fähigkeit → **AgentTeam-Ticket**
- Serverdienst, Konfiguration oder Deployment → **Server-Ticket**
- Vereinsprozess oder Vereinsunterlage → später **Vereins-Ticket**

Betrifft eine Initiative mehrere Projekte, wird sie in getrennte, verknüpfte Tickets zerlegt. Jedes Ticket hat eigene Akzeptanzkriterien und Freigaben. Abhängigkeiten werden gegenseitig verlinkt; Inhalte und insbesondere sensible Daten werden nicht unnötig dupliziert.

Beispiel:

```text
Server-Ticket: Dienst automatisiert aktualisieren
    ├─ benötigt AgentTeam-Ticket: Deployment-Gate unterstützen
    └─ benötigt Server-Ticket: Backup- und Rollbackverfahren definieren
```

## 5. Lernschleife und Reifegrade

Neue AgentTeam-Fähigkeiten durchlaufen schrittweise Reifegrade:

1. **Manuell beschrieben:** Prozess und Verantwortlichkeiten sind dokumentiert.
2. **Assistiert:** Agent erstellt Vorschläge, der Mensch führt aus.
3. **Sandbox:** Agent führt in einer isolierten Testumgebung aus.
4. **Kontrolliert:** Agent darf nach expliziter Freigabe begrenzte Aktionen ausführen.
5. **Betriebsreif:** Monitoring, Auditierung, Fehlerbehandlung und Rollback sind nachgewiesen.

Eine Fähigkeit darf im Serverprojekt nur bis zu dem Reifegrad verwendet werden, für den sie freigegeben wurde. Erkenntnisse aus realer Nutzung können den Reifegrad erhöhen oder bei Problemen wieder herabsetzen.

## 6. Priorisierung

Für die erste Phase gilt folgende Reihenfolge:

1. Ticketmodell, PM-, Umsetzungs- und Review-Prozess des AgentTeam-Projekts stabilisieren.
2. Kleine, reversible Anforderungen des Serverprojekts damit bearbeiten.
3. Aus den Erfahrungen konkrete AgentTeam-Verbesserungen ableiten.
4. Deployment, Wartungsfenster, Monitoring und Rollback schrittweise ergänzen.
5. Datenschutz- und Self-Hosting-Basis für das spätere Vereinsprojekt aufbauen.
6. Vereinsprojekt erst nach bewusster Reife- und Sicherheitsentscheidung aktivieren.

## 7. Schutz des Serverprojekts

Das Serverprojekt ist Lernumgebung, aber kein ungeschütztes Experimentierfeld:

- neue Fähigkeiten zuerst in Simulation oder Testumgebung erproben
- produktive Zugriffe standardmäßig verweigern
- Änderungen klein, reversibel und versioniert halten
- Backups und Rollback vor Deployment festlegen
- menschliche Freigabe für Merge und produktive Ausführung beibehalten
- AgentTeam-Fehler als eigene Tickets dokumentieren, statt sie im Server-Ticket zu verbergen

## 8. Voraussetzungen für das Vereinsprojekt

Vor der operativen Aufnahme des Vereinsprojekts sollen mindestens folgende Voraussetzungen erfüllt sein:

- geeignete selbstgehostete oder anderweitig datenschutzgerecht bewertete Dienste
- getrennte Identitäten, Rollen und Datenräume
- Klassifikation und Minimierung personenbezogener Daten
- kontrollierte Wissens- und Dokumentenablage
- nachvollziehbare Einwilligungs-, Aufbewahrungs- und Löschregeln
- Auditierung von Zugriffen und Ausführungen
- bewährte Freigabegates für externe Kommunikation und Datenänderungen
- getestete Backup- und Wiederherstellungsverfahren

Bis dahin bleibt die Vereinsdomäne ein geplanter späterer Anwendungsfall. Reale Vereinsunterlagen oder personenbezogene Inhalte werden nicht zu Testzwecken in das AgentTeam- oder Serverprojekt übernommen.

## 9. Strategische Konsequenz

Das AgentTeam-Projekt ist nicht nur Mittel zum Zweck, sondern ein dauerhaftes Plattform- und Organisationsprojekt. Das Serverprojekt liefert den ersten realen Bedarf und profitiert gleichzeitig von jeder gereiften AgentTeam-Fähigkeit. Beide Projekte entwickeln sich gemeinsam, behalten jedoch getrennte Verantwortlichkeiten, Tickets, Ergebnisse und Sicherheitsgrenzen.
