# AI-Workflow
Mein Demo-Project zum Thema Agent und AGentic-Workflows


## AI Einsatzmöglichkeiten

- als Googleersatz (/)
- als Googleersatz mit Zugriff auf den Code (/)
- als Coding-Assistant, schreibt Code in Projekt (/)
- als Coding-Assistant mit Skills, plant - schreibt Code - testet Code - commitet - ... (/)
- als Agent, fester Bestandteil des Workflows - erledigt eigenständig Aufgaben einer definierte Rolle (!)

## Mögliche Umsetzungen

### Einfacher Ansatz
Workflow wird durch Issues gesteuert

Issue -> Triggert Agent 1 -> Triggert Agent 2 ...

### Agent Workflow Tools
Workflow wird durch externe Tools definiert
n8n https://n8n.io/
langGraph https://www.langchain.com/langgraph

## Mögliche Agents:

- Entwickler-Agent
    -Sub-Agents:
      - Frontend-Angular-Agent
      - Backend-Agent-Agent
      - Libary-Agent
      - Planer-Agent
      - Infrastruktur-Agent
- Ticket-Verbesserungs-Agent
- Ticket-Vorschlag-Agent
- Architektur-Agent
- Tester-Agent
- Doku und Wissens-Agent
- Update-Agent
- Refactoring-Agent

## Codex-Entwickler-Agent

Der Entwickler-Agent kann GitHub-Issues mit der offiziellen OpenAI Codex Action umsetzen. Die Ausführung erfolgt geschützt in GitHub Actions; das Ergebnis ist ein Pull Request zur manuellen Prüfung.

➡️ **[Codex-Agent einrichten](CODEX-AGENT.md)**

