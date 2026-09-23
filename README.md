# AI-Workflow

Mein Demo-Projekt zum Thema Agents und agentische Workflows.

## AI-Einsatzmöglichkeiten

- Als Google-Ersatz ✅
- Als Google-Ersatz mit Zugriff auf den Code ✅
- Als Coding-Assistant, der Code im Projekt schreibt ✅
- Als Coding-Assistant mit Skills, der plant, Code schreibt, Tests ausführt, committet, … ✅
- Als Agent, der fester Bestandteil des Workflows ist und eigenständig eine definierte Rolle erfüllt 🚧

## Mögliche Umsetzungen

### Einfacher Ansatz

Der Workflow wird durch Issues gesteuert:

```text
Issue → Agent 1 → Agent 2 → …
```

### Agent-Workflow-Tools

Der Workflow wird durch externe Tools definiert:

- [n8n](https://n8n.io/)
- [LangGraph](https://www.langchain.com/langgraph)

## Mögliche Agents

- **Entwickler-Agent**
  - **Sub-Agents:**
    - Frontend-Angular-Agent
    - Backend-Agent
    - Library-Agent
    - Planer-Agent
    - Infrastruktur-Agent
- **Ticket-Verbesserungs-Agent**
- **Ticket-Vorschlag-Agent**
- **Architektur-Agent**
- **Tester-Agent**
- **Dokumentations- und Wissens-Agent**
- **Update-Agent**
- **Refactoring-Agent**

## Codex-Entwickler-Agent

Der Entwickler-Agent kann GitHub-Issues mit der offiziellen OpenAI-Codex-Action umsetzen. Die Ausführung erfolgt geschützt in GitHub Actions; das Ergebnis ist ein Pull Request zur manuellen Prüfung.

➡️ **[Codex-Agent einrichten](CODEX-AGENT.md)**

## Automatisierung

Die Maschine baut die Maschine,
die Maschine baut die Maschine,
die Maschine …
