# AgentTeam

Projekt zum iterativen Aufbau eines ticketzentrierten Agent-Teams für private Projekte.

## Vision

Ziel ist ein Team spezialisierter Agents, das private Software-, Server- und später Vereinsprojekte unterstützt. Issues bilden dabei die operative Wahrheit: Sie halten Anforderungen, Freigaben, Übergaben und Arbeitsschritte fest. GitHub-Repositories enthalten die langlebigen Ergebnisse wie Quellcode, Tests, Architektur- und Betriebsdokumentation.

Agents handeln nicht als unkontrollierter Schwarm. Ein Orchestrator weist ihnen genehmigte Tickets nach festen Rollen, Zuständen und Sicherheitsregeln zu. Kritische Übergänge – insbesondere Umsetzung, Merge, Deployment, Migration und externe beziehungsweise fachlich relevante Aktionen – bleiben durch explizite menschliche Freigaben kontrolliert.

➡️ **[Architekturvision des Agent-Teams](docs/AGENT-TEAM-VISION.md)**

## AgentTeam als eigenständiges Projekt

Der Aufbau des Agent-Teams ist selbst ein Projekt und kein einmaliger Infrastrukturbaustein. Es besitzt eine eigene Vision, ein Backlog, Releases, Architekturentscheidungen und Qualitätsziele.

Das AgentTeam-Projekt und das Serverprojekt werden zunächst gemeinsam und iterativ weiterentwickelt:

```text
Serverprojekt erzeugt reale Anforderungen
                ↓
AgentTeam unterstützt deren Bearbeitung
                ↓
Erfahrungen zeigen Lücken im Agent-Team
                ↓
AgentTeam wird gezielt erweitert
                ↓
Verbessertes AgentTeam unterstützt den nächsten Serverschritt
```

Das Serverprojekt ist damit der erste reale Anwendungsfall und zugleich die Lern- und Validierungsumgebung des AgentTeam-Projekts. Anforderungen und Ergebnisse bleiben trotzdem in getrennten Projektkontexten dokumentiert und werden über verknüpfte Tickets und Pull Requests verbunden.

Das Vereinsprojekt wird bewusst zurückgestellt. Wegen der höheren Anforderungen an Privatsphäre, personenbezogene Daten und selbstgehostete Lösungen wird es erst aufgenommen, wenn die dafür notwendige sichere Infrastruktur verfügbar und der Agentenprozess ausreichend erprobt ist.

## AI-Einsatzmöglichkeiten

- Als Google-Ersatz ✅
- Als Google-Ersatz mit Zugriff auf den Code ✅
- Als Coding-Assistant, der Code im Projekt schreibt ✅
- Als Coding-Assistant mit Skills, der plant, Code schreibt, Tests ausführt, committet, … ✅
- Als Agent, der fester Bestandteil des Workflows ist und eigenständig eine definierte Rolle erfüllt 🚧

## Strategischer Workflow

```text
Vision / Anforderung
        ↓
PM-Agent schlägt Tickets vor
        ↓
Menschliche Freigabe
        ↓
Umsetzungs-Agent → Tests + Dokumentation + Pull Request
        ↓
Qualitätsprüfung und menschliche Abnahme
        ↓
Deployment-/Ausführungsfreigabe
        ↓
Kontrollierte Ausführung und Verifikation
        ↓
Inspection-Agent überwacht und erstellt bei Bedarf Bugtickets
```

## Mögliche Umsetzungen

### Einfacher Ansatz

Der Workflow wird durch Issues, Labels, Pull Requests und GitHub Projects gesteuert:

```text
Issue → Freigabe → Agent 1 → Übergabe → Agent 2 → menschliche Abnahme
```

### Agent-Workflow-Tools

Der Workflow kann später durch externe Tools persistent orchestriert werden:

- [n8n](https://n8n.io/)
- [LangGraph](https://www.langchain.com/langgraph)
- eine persistente Workflow-Engine für langlebige, pausierbare Abläufe

## Vorgesehene Agent-Rollen

- **PM-Agent:** zerlegt Visionen in prüfbare Ticketvorschläge.
- **Umsetzungs-/Entwickler-Agent:** setzt genehmigte Tickets um, testet und dokumentiert.
- **Review-/Qualitäts-Agent:** prüft Akzeptanzkriterien, Tests, Dokumentation und Risiken unabhängig.
- **Deployment-/Migrations-Agent:** rollt exakt freigegebene Artefakte in Wartungsfenstern aus.
- **Inspection-/Wartungs-Agent:** sucht nach Fehlern und erstellt nachvollziehbare, deduplizierte Bugtickets.
- **Vereins-Ausführungs-Agent:** langfristige Rolle für datenschutzgerecht betriebene Vereinsprozesse.

## Codex-Entwickler-Agent

Der Entwickler-Agent kann GitHub-Issues mit der offiziellen OpenAI-Codex-Action umsetzen. Die Ausführung erfolgt geschützt in GitHub Actions; das Ergebnis ist ein Pull Request zur manuellen Prüfung.

➡️ **[Codex-Agent einrichten](CODEX-AGENT.md)**

## Automatisierung

Die Maschine baut die Maschine,
die Maschine baut die Maschine,
die Maschine …
