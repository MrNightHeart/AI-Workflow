# Recherche: Codex Action in GitHub Actions

## Ergebnis

Es gibt eine offizielle OpenAI GitHub Action: [`openai/codex-action`](https://github.com/openai/codex-action).

Sie installiert die Codex CLI, startet bei Verwendung eines API-Keys den Responses-API-Proxy und führt `codex exec` mit kontrollierten Berechtigungen aus. Sie läuft als GitHub-Action-Schritt auf einem GitHub-hosted Runner.

Für diesen Workflow ist damit keine eigene Runner- oder Installationslogik erforderlich.

## Aktuelle Architektur

1. GitHub Issue wird erstellt oder erhält das Label `ai:implement`.
2. Der Workflow akzeptiert ausschließlich Issues von `MrNightHeart`.
3. `openai/codex-action` läuft mit `permission-profile: ":workspace"` und `safety-strategy: drop-sudo`.
4. Codex bearbeitet die Aufgabe und führt relevante Tests aus.
5. GitHub Actions pusht die Änderungen in einen Branch und eröffnet einen Pull Request nach `main`.
6. Der Pull Request wird nicht automatisch gemergt.

## Sicherheit

- `OPENAI_API_KEY` wird als GitHub Actions Repository-Secret gespeichert.
- Die Action ist im Workflow auf einen vollständigen Commit-SHA gepinnt; der lesbare Versionshinweis ist nur Dokumentation.
- Der Key wird nur an den Codex-Schritt übergeben.
- `drop-sudo` und das Workspace-Berechtigungsprofil reduzieren den Zugriff des Agenten.
- Issue-Texte bleiben eine Prompt-Injection-Grenze; sie dürfen keine Workflow-Sicherheitsregeln überschreiben.
- Pull Requests werden nicht automatisch gemergt.
- Für produktive Nutzung sollten `main`-Branch-Schutz, erforderliche Checks und eine manuelle Review aktiviert sein.
